---
layout: markdown_page
title: "Production Architecture"
---


Our core infrastructure is currently hosted on several cloud providers,
all with different functions. This document does not cover servers that
are not integral to the public facing operations of GitLab.com.

## On this page
{:.no_toc}

- TOC
{:toc}

## Other Related Pages

- [Application Architecture documentation](https://docs.gitlab.com/ce/development/architecture.html)
- [GitLab.com Settings](https://about.gitlab.com/gitlab-com/settings/)
- [Monitoring Performance of GitLab.com](monitoring)
- [GitLab performance monitoring documentation](https://docs.gitlab.com/ce/administration/monitoring/performance/introduction.html)
- [Performance of the Application](/handbook/engineering/performance)

## Diagram of the Architecture
{: #infra-archi-diagram}

<img src="https://docs.google.com/drawings/d/1zXRSMSe1eI55jI6BbLkhGzCwkVYQMJNnTzMv8qdscYw/pub?w=1279&amp;h=1021">

[Source](https://docs.google.com/drawings/d/1zXRSMSe1eI55jI6BbLkhGzCwkVYQMJNnTzMv8qdscYw/edit), GitLab internal use only

## Infrastructure "Services" and Their SLx's
{: #infra-services}

In order for us to reach the goals around availability and latency for GitLab.com,
we started by setting a target [internal SLA](/handbook/infrastructure/#internal-sla) for the service as a whole from the user's
perspective. From those targets, we can work backwards through the architecture
to determine what the Service Level objectives should be for the infrastructure
"services" that support GitLab.com.

Since we are relying on hardware that itself only offers an [SLA of 99.9%
availability](https://azure.microsoft.com/en-us/support/legal/sla/virtual-machines/v1_6/),
we face an "SLA inversion" (read more about this
[here](http://screamingtiger.blogspot.com.es/2010/04/release-it-chapter-410-sla-inversion.html)
or [here](http://assets.en.oreilly.com/1/event/79/Stability%20Patterns%20Presentation.pdf)).
For example, in the _current_  situation, each time an NFS server goes down, this
results in an outage of GitLab.com. Since we are only guaranteed 99.9% uptime per
NFS server, the maximum SLA for GitLab.com as a whole will be <= (99.9%)<sup>_N_</sup>, where
_N_ is the number of NFS servers. To overcome this, the service that is offered
by the NFS servers either needs to be redesigned in some way (e.g. through using
  [Gitaly](https://gitlab.com/gitlab-org/gitaly/)), or the application that
  depends on it needs to have a way to not go down when the NFS service is
  unavailable (i.e. graceful degradation). Similar considerations apply to things
  such as the cache, background jobs processing, availability of the database,
  and so on.

To tackle this challenge, we consider the following
elements of the infrastructure to be "services" that should be able to meet their
own internal SLAs:
- Git Files (i.e. NFS, and Gitaly)
   - SLOs:
      - Uptime
      - Latency
      - Recovery time after failure
   - Defenses for service degradation
      - Timeout - fail fast
      - Circuit breakers
   - Performance opportunity
      - Amortized queries using caching
      - Cached unique objects
    - Cost reduction opportunity
      - Detach performance from capacity using slower disks with caching, replication and load balancing.
      - Consider using cold and warm storage for frequently accessed repos.
- Non-git Files (i.e. some NFS, some object based storage)
   - SLOs:
      - Uptime
      - Reply latency
      - Recovery time after failure
   - Defenses for service degradation:
      - Timeouts
      - Circuit breaker
      - SCRAM for operational support
  - Cost reduction opportunity:
      - Stop using NFS and switch to a service like S3 eliminating the operational cost.
      - Storage policies for cold and warm objects
      - Locality caching with LRU
      - Applying CDNs
- Database (i.e. PostgreSQL)
   - SLOs:
      - Service Uptime
      - Dropped queries due to timeouts (degradation)
      - Query latency for alerting when the system is degrading
      - Bulkheads by Query Priority (user facing queries have lower timeouts)
   - Defenses for service degradation
      - Connection timeout
      - Query timeout
      - Exponential backoff on recovery
      - Circuit breaker on failover
      - Redundancy for failover
      - Load balancing with read replicas
      - Read only mode
   - Cost opportunity
      - Multiple downsized read only replicas while keeping only 2 primary capable hosts
- Cache (i.e. Redis)
   - SLOs:
      - Service uptime
      - Replication.
      - Reply Latency.
   - Defenses for service degradation
      - Aggressive query timeouts.
      - Read only mode.
      - Exponential backoff on connection timeout.
      - Limit object size
      - Bulkheads separating different key spaces in different instances.
      - Secondary file system level caching for large objects
      - Scram button to remove the cache in a O(1) operation - just restart the process.
   - Cost opportunity
      - Tiny instances that are focused on a single thing with different behaviors and persistence settings.
      - LRU to naturally reduce the dataset alive.
      - Zero downtime by removing failover for volatile data.
      - Cold and hot data policies.
      - Reuse hosts with multiple cores for multiple instances because redis is single threaded.
- Background Processing (i.e., Sidekiq)
   - SLOs
      - Job start latency segregated by priority.
      - Job execution timeout.
      - Queue team troubleshooting contract.
   - Defenses for service degradation
      - Job execution timeout
      - Bulkheads by job priorities
      - Replication - easy because they are stateless
      - Exponential backoffs
      - Decouple with a message bus
   - Cost opportunity
      - Auto scaling based on latency
- CI Runners
   - SLOs
   - Defenses for service degradation
- Search (i.e. Elasticsearch)
   - SLOs
      - Query latency
      - Service uptime
   - Defenses for service degradation
      - Timeouts
      - Circuit breaker
      - Recording of outliers for posterior analysis
- Real-time notifications (i.e. long-polling)
   - SLAs
      - Use tracer bullets to measure the latency of the system.
      - Uptime of the service.
   - Defenses for service degradation
      - Timeout for event registration.
      - Exponential backoff with retries when registering a message.
      - Buffering with middleware for when the registering system fails.
      - Dead letter to be replayed in case of failure.
   - Cost opportunity
      - This service inverts the need of massively scaling systems that support polling.
- Unicorn
   - SLOs
   - Defenses for service degradation
- API
   - SLOs
   - Defenses for service degradation
- Git processes (i.e. gitlab-shell, workhorse)
   - SLOs
   - Defenses for service degradation


## Host Naming Standards

### Hostnames

A hostname shall be constructed by using the service offered by that node, followed
by a dash, and a two digit incrementing number.

i.e.: `sidekiq-NN`, `git-NN`, `web-NN`

Service specific identifiers, when it connotes a difference in build or function,
will be identified as `-specific` and precede the two digit numeric

i.e.: `sidekiq-realtime-01`

When services have both an internal and an external facing function, the usage of
`-int-` or `-ext-` shall be used.

i.e.: `api-int-01`, `api-ext-01`

### Service Tiers

Following the hostname shall be the service tier that the node belongs in:
- `sv` for Service
- `lb` for Load Balancer
- `db` for Database Nodes
- `inf` for Infrastructure Nodes

### Environments

Following the service tier shall be the environment:
- `prd` for Production
- `cny` for Canary
- `stg` for Staging
- `dev` for Development

### Locations

Following the environment is the location where the host resides, for example:
- `eus2` for East US 2 DC

### TLD Zones

When it comes to DNS names all services providing `GitLab.com` as a service shall
be in the `GitLab.com` domain, ancillary services in the support of GitLab (i.e.
Chef, ChatOps, VPN, Logging, Monitoring) shall be in the `gitlab.net` domain.

### Examples

- An internal API Server:
  - `api-int-01.sv.prd.eus2.gitlab.com`

- A DNS server:
    - `dns-01.inf.prd.eus2.gitlab.net`


## Internal Networking Scheme

A visualization of the whole address space can be found [here](https://docs.google.com/spreadsheets/d/1l-Oxx8dqHqGnrQ23iVP9XGYariFGPFDuZkqFj4KOe5A/) (GitLab internal use only).

### Production

Virtual Network Name: `GitLabProd`

Resource Group: `GitLabProd`

IP space: `10.64.0.0/11`

| Subnet Name       | Subnet Range  | Tier             | Domain                |
|:------------------|:--------------|:-----------------|:----------------------|
| ExternalLBProd    | 10.65.1.0/24  | Load balancers   | `lb.prd.gitlab.com`   |
| InternalLBProd    | 10.65.2.0/24  | Load balancers   | `lb.prd.gitlab.com`   |
| DBProd            | 10.66.1.0/24  | Databases        | `db.prd.gitlab.com`   |
| RedisProd         | 10.66.2.0/24  | Databases        | `db.prd.gitlab.com`   |
| ElasticSearchProd | 10.66.3.0/24  | Databases        | `db.prd.gitlab.com`   |
| ConsulProd        | 10.67.1.0/24  | Support Services | `inf.prd.gitlab.net`  |
| VaultProd         | 10.67.2.0/24  | Support Services | `inf.prd.gitlab.net`  |
| DeployProd        | 10.67.3.0/24  | Support Services | `inf.prd.gitlab.net`  |
| DNSProd           | 10.67.4.0/24  | Support Services | `inf.prd.gitlab.net`  |
| MonitoringProd    | 10.68.1.0/24  | Logging          | `log.prd.gitlab.net`  |
| LogProd           | 10.68.2.0/24  | Logging          | `log.prd.gitlab.net`  |
| LogStorageProd    | 10.68.50.0/24 | Logging          | `log.prd.gitlab.net`  |
| APIProd           | 10.69.2.0/23  | Services         | `sv.prd.gitlab.com`   |
| GitProd           | 10.69.4.0/23  | Services         | `sv.prd.gitlab.com`   |
| SidekiqProd       | 10.69.6.0/23  | Services         | `sv.prd.gitlab.com`   |
| WebProd           | 10.69.8.0/23  | Services         | `sv.prd.gitlab.com`   |
| RegistryProd      | 10.69.10.0/23 | Services         | `sv.prd.gitlab.com`   |
| StorageProd       | 10.70.2.0/23  | Storage          | `stor.prd.gitlab.com` |

### Canary

Virtual Network Name: `GitLabCanary`

Resource Group: `GitLabCanary`

IP space: `10.192.0.0/13`

| Subnet Name      | Subnet Range   | Tier           | Domain              |
|:-----------------|:---------------|:---------------|:--------------------|
| ExternalLBCanary | 10.192.1.0/24  | Load balancers | `lb.cny.gitlab.com` |
| InternalLBCanary | 10.192.2.0/24  | Load balancers | `lb.cny.gitlab.com` |
| APICanary        | 10.196.2.0/23  | Services       | `sv.cny.gitlab.com` |
| GitCanary        | 10.196.4.0/23  | Services       | `sv.cny.gitlab.com` |
| SidekiqCanary    | 10.196.6.0/23  | Services       | `sv.cny.gitlab.com` |
| WebCanary        | 10.196.8.0/23  | Services       | `sv.cny.gitlab.com` |
| RegistryCanary   | 10.196.10.0/23 | Services       | `sv.cny.gitlab.com` |

### Staging

Virtual Network Name: `GitLabStaging`

Resource Group: `GitLabStaging`

IP space: `10.128.0.0/12`

| Subnet Name          | Subnet Range   | Tier             | Domain                |
|:---------------------|:---------------|:-----------------|:----------------------|
| ExternalLBStaging    | 10.128.1.0/24  | Load balancers   | `lb.stg.gitlab.com`   |
| InternalLBStaging    | 10.128.2.0/24  | Load balancers   | `lb.stg.gitlab.com`   |
| DBStaging            | 10.129.1.0/24  | Databases        | `db.stg.gitlab.com`   |
| RedisStaging         | 10.129.2.0/24  | Databases        | `db.stg.gitlab.com`   |
| ElasticSearchStaging | 10.129.3.0/24  | Databases        | `db.stg.gitlab.com`   |
| ConsulStaging        | 10.130.1.0/24  | Support Services | `inf.stg.gitlab.net`  |
| VaultStaging         | 10.130.2.0/24  | Support Services | `inf.stg.gitlab.net`  |
| DeployStaging        | 10.130.3.0/24  | Support Services | `inf.stg.gitlab.net`  |
| DNSStaging           | 10.130.4.0/24  | Support Services | `inf.stg.gitlab.net`  |
| LogStaging           | 10.131.2.0/24  | Logging          | `log.stg.gitlab.net`  |
| APIStaging           | 10.132.2.0/23  | Services         | `sv.stg.gitlab.com`   |
| GitStaging           | 10.132.4.0/23  | Services         | `sv.stg.gitlab.com`   |
| SidekiqStaging       | 10.132.6.0/23  | Services         | `sv.stg.gitlab.com`   |
| WebStaging           | 10.132.8.0/23  | Services         | `sv.stg.gitlab.com`   |
| RegistryStaging      | 10.132.10.0/23 | Services         | `sv.stg.gitlab.com`   |
| StorageStaging       | 10.133.2.0/23  | Storage          | `stor.stg.gitlab.com` |

### Remote Access

Virtual Network Name: Mirrors `Subnet Name`

Resource Group: Mirrors `Subnet Name`

IP Space: `10.254.0.0/16`

| Subnet Name   | Subnet Range  | Tier          | Domain           |
|:--------------|:--------------|:--------------|:-----------------|
| VPN-East-US-2 | 10.254.4.0/23 | Remote Access | `sec.gitlab.net` |


## Azure

The main portion of GitLab.com is hosted on Microsoft Azure. We have
the following servers there.

* 6 HAProxy load balancers for GitLab.com
* 2 HAProxy load balancers for GitLab Pages
* 2 HAProxy nodes for altssh.GitLab.com
* 22 front-end nodes of which:
  * 7 are Web nodes
  * 8 are API nodes
  * 12 are Git nodes
* 20 Sidekiq nodes
* 3 PostgreSQL servers
* 3 Redis servers
* 3 Prometheus servers
* 17 NFS servers

Note that these numbers can fluctuate to adapt to the platform needs.

We also use availability sets to ensure that a minimum number of servers in each
group are available at any given time. This ensures that Azure will not reboot
all instances in the same availability set at the same time for anything that
is planned.

All our servers run the latest Ubuntu LTS unless there is a specific need to do
otherwise. Every server is configured with a fully fledged set of firewall rules
for increased security.

### Load Balancers

We utilize Azure load balancers in front of our HAProxy nodes. This allows us to
leverage on the Azure infrastructure for HA as well as [taking advantage of the
power of HAProxy](https://gitlab.com/gitlab-cookbooks/gitlab-haproxy).

Additionally, we utilize an Azure load balancer to manage PostgreSQL failovers.

* The GitLab.com load balancer pool serves git over ssh, git over https, http
and https traffic.
* The GitLab Pages load balancer serves http and https.
* The AltSSH load balancer serves [git on port 443](https://about.gitlab.com/2016/02/18/gitlab-dot-com-now-supports-an-alternate-git-plus-ssh-port/)
and translates it to port 22 on the back-end.

### Service nodes

Different services have different resource utilization patterns so we use a
variety of instance types across our service nodes that are consistent for each
group. We have recently isolated traffic by type on dedicated pools of nodes. We
hope you noticed the performance improvement.

## Digital Ocean

Digital Ocean houses several servers that do not need to directly interact
with our main infrastructure. There are many of these that do a variety of
things, however not all will be listed here.

The primary things on Digital Ocean at this time are:

* Chef Configuration Management Servers
* Blackbox monitoring servers
* Shared runner managers
* Runner cache servers
* ELK servers

## AWS

We host our DNS with route53 and we have several EC2 instances for various
purposes. The servers you will interact with most are listed Below

* Version
* Mattermost
* License

## Google Cloud

We are currently investigating Google Cloud.

## Monitoring

See how it's doing, for more information on that, visit the [monitoring
handbook](/handbook/engineering/monitoring/).

## Technology at GitLab

We use a lot of cool ([but boring](https://about.gitlab.com/handbook/#values))
technologies here at GitLab. Below is a non-exhaustive list of tech we use here.

* [Ruby](https://www.ruby-lang.org/) (probably goes without saying)
* [Chef](https://www.chef.io/chef/)
* [Prometheus](https://prometheus.io/)
* [PostgreSQL](https://www.postgresql.org/)
* [Redis](https://redis.io/)
* [ELK Stack](https://www.elastic.co/products)
* [Terraform](https://www.terraform.io)
* [Consul](https://www.consul.io)
