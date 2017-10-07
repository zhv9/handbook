# Production Readiness Guide

For any new or existing system or a large feature set the questions in this guide help make the existing service more robust, and for new systems it helps prepare them and speed up the process of becoming fully production-ready.

Initially, this guide is likely to be used by Production Engineers who are embedded with other teams working on existing services and features. However, anyone working on a new service or feature set is encouraged to use this guide as well.

The goal of this guide is to help others understand how the new service or feature set may impact the rest of the (production) system; what steps need to be taken (besides deploying this new system) to ensure that it can be properly managed; and to understand what it will take to manage the reliability of the new system / feature / service beyond its' initial deployment.


## Summary

- [ ] Provide a high level summary of this new product feature. Explain how this change will benefit GitLab customers. Enumerate the customer use-cases.
- [ ] What metrics, including business metrics, should be monitored to ensure will this feature launch will be a success?

## Architecture

- [ ] Add architecture diagrams to this issue of feature components and how they interact with existing GitLab components. Include internal dependencies, ports, security policies, etc.
- [ ] Describe each component of the new feature and enumerate what it does to support customer use cases.
- [ ] For each component and dependency, what is the blast radius of failures? Is there anything in the feature design that will reduce this risk?
- [ ] If applicable, explain how this new feature will scale and any potential single points of failure in the design.

## Operational Risk Assessment

- [ ] What are the potential scalability or performance issues that may result with this change?
- [ ] List the external and internal dependencies to the application (ex: redis, postgres, etc) for this feature and how the it will be impacted by a failure of that dependency.
- [ ] Were there any features cut or compromises made to make the feature launch?
- [ ] List the top three operational risks when this feature goes live.
- [ ] What are a few operational concerns that will not be present at launch, but may be a concern later?
- [ ] Can the new product feature be safely rolled back once it is live, can it be disabled using a feature flag?
- [ ] Document every way the customer will interact with this new feature and how customers will be impacted by a failure of each interaction.
- [ ] As a thought experiment, think of worst-case failure scenarios for this product feature, how can the blast-radius of the failure be isolated?

## Database

- [ ] If we use a database, is the data structure verified and vetted by the database team?
- [ ] Do we have an approximate growth rate of the stored data (for capacity planning)?
- [ ] Can we age data and delete data of a certain age?

## Security

- [ ] Were the [gitlab security development guidelines](https://about.gitlab.com/security/#gitlab-development-guidelines) followed for this feature?
- [ ] If this feature requires new infrastructure, will it be updated regularly with OS updates?
- [ ] Has effort been made to obscure or elide sensitive customer data in logging?
- [ ] Is any potentially sensitive user-provided data persisted? If so is this data encrypted at rest?

## Performance

- [ ] Explain what validation was done following GitLab's [performance guidlines](https://docs.gitlab.com/ce/development/performance.html) please explain or link to the results below
    * [Query Performer](https://docs.gitlab.com/ce/development/query_recorder.html)
    * [Sherlock](https://docs.gitlab.com/ce/development/profiling.html#sherlock)
    * [Request Profiling](https://docs.gitlab.com/ce/administration/monitoring/performance/request_profiling.html)
- [ ] Are there any potential performance impacts on the database when this feature is enabled at GitLab.com scale?
- [ ] Are there any throttling limits imposed by this feature? If so how are they managed?
- [ ] If there are throttling limits, what is the customer experience of hitting a limit?
- [ ] For all dependencies external and internal to the application, are there retry and back-off strategies for them?
- [ ] Does the feature account for brief spikes in traffic, at least 2x above the expected TPS?

## Backup and Restore

- [ ] Outside of existing backups, are there any other customer data that needs to be backed up for this product feature?
- [ ] Are backups monitored?
- [ ] Was a restore from backup tested?

## Monitoring and Alerts

- [ ] Is the service logging in JSON format and are logs forwarded to logstash?
- [ ] Is the service reporting metrics to Prometheus?
- [ ] How is the end-to-end customer experience measured?
- [ ] Do we have a target SLA in place for this service?
- [ ] Do we know what the indicators (SLI) are that map to the target SLA?
- [ ] Do we have alerts that are triggered when the SLI's (and thus the SLA) are not met?
- [ ] Do we have troubleshooting runbooks linked to these alerts?
- [ ] What are the thresholds for tweeting or issuing an official customer notification for an outage related to this feature?

## Responsibility

- [ ] Which individuals are the subject matter experts and know the most about this feature?
- [ ] Which team or set of individuals will take responsibility for the reliability of the feature once it is in production?
- [ ] Is someone from the team who built the feature on call for the launch? If not, why not?

## Testing

- [ ] Describe the load test plan used for this feature. What breaking points were validated?
- [ ] For the component failures that were theorized for this feature, were they tested? If so include the results of these failure tests.
- [ ] Give a brief overview of what tests are run automatically in GitLab's CI/CD pipeline for this feature?
