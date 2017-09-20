---
layout: markdown_page
title: "Set up your own demo GitLab CE or EE instance on Google Container Engine"
---

## Video
{:.no_toc}

The video below has three parts: creating a Kubernetes cluster, installing GitLab on it, and going through the software development lifecycle. It's outdated as of GitLab 9.0, but is included here since it's the most recent video that includes the setup steps. For the software development lifecycle, please refer to the [sales demo](../demo).

<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/3A8mdJl_icM" frameborder="0" allowfullscreen="true"> </iframe>
 </iframe>
</figure>

## Table of Contents
{:.no_toc}

- TOC
{:toc}

## Preparation

*TODO: Preconfigure `GITLAB_GKE_IP`, etc. before starting demo. Maybe even pre-generate the configuration and just point to the repo for instructions.*

> * You need a Google Cloud Platform account, GitLab employees will have this. Ensure you are logged in with your GitLab account.
> * Login to [Google Cloud Platform](https://console.cloud.google.com/kubernetes).
> * GitLab employees should use the `gitlab-demos` project. Others should select or create a project to work in.
>   * URL: [https://console.cloud.google.com/kubernetes/list?project=gitlab-demos](https://console.cloud.google.com/kubernetes/list?project=gitlab-demos)
> * Clone the [kubernetes-gitlab-demo](https://gitlab.com/gitlab-org/kubernetes-gitlab-demo) for use.
> * If you've run through the demo before but didn't clean up your [demo cluster(s)](https://console.cloud.google.com/kubernetes/list), [do so now](#cleanup).
> * This script assumes the `make-sid-dance.com` domain, but you should either:
>   * Pick the least-recently used domain from the [Google Doc](https://docs.google.com/spreadsheets/d/1HZ-7XhDNzdCBxfjzDFIQi7EjliptkpY4CB3LbiLa9MY/edit#gid=0). (Let's Encrypt limits SSL cert creation on a weekly basis, so rotating usage helps reduce hitting the limits), or
>   * Buy a new domain for your demo and substitute throughout the script.
>     * [Google Domains](https://domains.google.com) is $12 for `.com` domains, which isn't the cheapest, but comes with privacy protection. You still have to configure DNS to use custom name servers, even though Google Domain name servers is the default since GCP cycles through many different name servers.
>     * [Create DNS Zone](https://console.cloud.google.com/networking/dns/zones/~new?project=gitlab-demos) to let Google manage DNS for you.
>     * Click `Registrar Setup` to see what name servers to use.
> * Disable desktop notifications (on a Mac, top-right corner, option click).
> * Open up new browser window so the audience doesn’t see all your other open tabs.
> * Consider just sharing web browser window so the audience isn’t distracted by notes or other windows.
> * Go to 'Displays' settings, Resolution: Scaled, Larger text.
> * Open this page on an iPad that has screen lock disabled.
> * Have a Terminal window ready, open to the `kubernetes-gitlab-demo` directory you have just cloned.
>
> **Alternative CLI instructions**
> * You need to have the [Google Cloud SDK](https://cloud.google.com/sdk/downloads) installed. e.g.
> * On OSX, install brew for all the things
> * `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
> * Install Brew Caskroom
> * `brew install caskroom/cask/brew-cask`
> * Install Google Cloud SDK
> * `brew cask install google-cloud-sdk`
> * Run `gcloud components install kubectl`
> * Before each demo, run `sudo gcloud components update; gcloud auth application-default login`, saving you time from doing this in the middle of the demo.

## Set up a container scheduler cluster

We’re going to install everything from scratch and we’ll start by creating a new container cluster. Today I'm going to use Google Cloud Platform, which includes Container Engine, a Kubernetes platform hosted by Google.

> * [Create cluster](https://console.cloud.google.com/kubernetes/add?project=gitlab-demos) (or open [GCP](https://console.cloud.google.com/kubernetes), pick [`gitlab-demos` project](https://console.cloud.google.com/kubernetes/list?project=gitlab-demos) and click Create cluster).

We'll name this cluster `make-sid-dance` and have it created in the us-central zone. I’ll leave it at 3 nodes, but bump of the machine type to have 2 virtual CPUs for performance reasons.

> * Name the cluster after your domain name (e.g. `make-sid-dance`).
> * Make note of the `Zone` field should read `us-central1-*`, and will have a letter on the end. This letter does not matter.
> * Change the number of vCPU in Machine type to `2 vCPU`.
> * *Note: The demo will run fine on a single node, if desired*
> * Click the `Create` button at the bottom of the page.

Now we need to get an external IP address for the demo so that we can use a domain name and Let's Encrypt for SSL.

> * Navigate to [Networking](https://console.cloud.google.com/networking/addresses/list).
> * Select `External IP addresses` from the menu on the left.
> * Click [`Reserve static address`](https://console.cloud.google.com/networking/addresses/add?project=gitlab-demos) at the top of the page.
> * Set the name to match the name used for the cluster (e.g. `make-sid-dance`).
> * Set the Region to `us-central1` to match the Zone where you made the cluster.
> * **Warning:** The external IP **must not** be assigned to a cluster. It will be automatically assigned when creating the Application in a later step.
> * Click the `Reserve` button at the bottom of the page.

We'll now create a wildcard DNS entry for our demonstration domain, pointing to the IP we just created.

> * Copy the External Address from the list, from the line containing the name you used.
> * Click `Cloud DNS` from the menu on the left.
> * Click on the Zone that has the name of the domain to be used for the demo. (e.g. `make-sid-dance-com`)
> * Click on the `Add Record Set` button at the top of the page.
> * Set the DNS Name to `*`.
> * Set the IPv4 Address to the clipboard contents (the External Address you just copied).
> * Click the `Create` button at the bottom of the page.

Now that we have created the cluster and configured a domain, we can go back and check on our cluster.

> * Navigate to [Container Engine](https://console.cloud.google.com/kubernetes/list).
> * Confirm a green checkmark. This tells us the cluster is ready to be used.

Good, our cluster is ready for us to use. Let's connect to it.

> * Click on the pencil edit button for your cluster.
> * Copy the Endpoint IP address.
> * Open up another tab with `https://<insert IP>/ui`. You'll get a security warning. On Chrome, click `Advanced` and then `Proceed to <IP> (unsafe)`. You'll be prompted for authentication.
> * Go back to cluster info, click on `Show credentials` next to the Endpoint.
> * Copy the admin password and close the popup.
> * Switch back to the tab, type in `admin` and paste the password you just copied.
>
> **Alternative CLI instructions:**
> * Click on the `Connect` button for your cluster.
> * Click the `copy` icon to the right of the `gcloud container ...` entry. It looks like two overlapping white boxes.
>   * `gcloud container clusters get-credentials makesiddance-com \
    --zone us-central1-a --project gitlab-demos`
> * Switch to the Terminal window, paste this command in, run it.

## Set up GitLab itself

Now that we have our cluster configured, we're ready to generate our configuration. To do this, we'll need the External IP Address we just configured, a domain name, and an email address to use with Let's Encrypt. Then we can use this bash script to generate a YML file that describes everything we need. *And then we use `kubectl` to create all the resources from the YML file.*

> * Stay in the Terminal window
> * Compose the following, filling in your values from the previous steps: (use your email address and the ip you set in Network -> External IP Addresses)
>   * `GITLAB_GKE_IP=104.198.192.151 GITLAB_GKE_DOMAIN=make-sid-dance.com GITLAB_LEGO_EMAIL=user@gitlab.com bash generate.bash`
> * You will see the output similar to
>   * `Using gitlab-make-sid-dance-com.yml`
> * Click on `+ Create` in the top-right corner of the Kubernetes dashboard.
> * Select `Upload a YAML or JSON file`.
> * Click on `...`.
> * Select `gitlab-make-sid-dance-com.yml` (or your newly generated configuration).
> * Click on `Upload`. (It can take a while to upload, and then it just displays "There is nothing to display here".)
>
> **Alternative GitLab EE instructions:**
> * Edit `gitlab-make-sid-dance-com.yml`
> * Find `gitlab/gitlab-ce:9.0.0-rc5.ce.0` and replace with `gitlab/gitlab-ee:9.0.0-rc5.ee.0` (note `ce` appears twice)
>
> **Alternative CLI instructions:**
> * From the Terminal window, run the following, changing the yml file name to match the name of the one that was just created for you
>   * `kubectl create -f gitlab-make-sid-dance-com.yml`
>   * `kubectl proxy`
> * Go the the Kubernetes Dashboard at [http://localhost:8001/ui](http://localhost:8001/ui)

GitLab is now deploying, and we can watch the status from the Workloads page in the Kubernetes dashboard.

> * Change the `Namespace` drop-down on the left. Change it from `default` to `All Namespaces`
> * Click on `Workloads` on the left.

We'll watch here for all items to have a green checkmark showing that they have completed. This process can take a few minutes as GKE allocates resources and starts up the various containers. You can see here there are several containers. The main GitLab container has the Rails app, but also Mattermost for Chat, the integrated Docker Registry, and Prometheus for monitoring. Then there's separate containers for Postgres and Redis and the autoscaling GitLab Runner for CI and CD. This is everything you need for the application development lifecycle on Kubernetes.

While this is spinning up, we'll go ahead and open a new tab to the URL that GitLab CE will be accessible on.

> * Open a new Chrome tab and go to [https://gitlab.make-sid-dance.com](https://gitlab.make-sid-dance.com), adjusting the URL to the domain you used for this demo.

While the system is deploying, it is expected that we will see a 503 message from the load balancer until GitLab has been fully started.

> *Note:* You can expect that you will see a 503 message for a short period as everything comes online. Feel free to refresh the page and / or switch between the Kubernetes dashboard and the gitlab page.

While we're waiting: In the rest of the demo, I’ll take you through everything you need to take ideas to production, including chat with Mattermost, issues and issue tracking, planning with issue boards, coding with terminal access, committing with git version control, merge requests for code review, testing with continuous integration, getting peer reviews with live review apps, continuous delivery to staging, deploying to production directly from chat, cycle analytics to measure how fast you’re going from idea to production, and lastly, Prometheus monitoring of your GitLab instance. With GitLab, everything is integrated out of the box.

What takes 10 minutes in this demo will take days if you're not using GitLab and have to integrate different tools. Not only is GitLab faster to set up, but it is also more convenient to have everything in one interface. Developers want to work on creating a great product, not on learning and maintaining the integrations between theirs tools.

*If there is more time talk about what a review app is and what cycle analytics are.*

> * Wait for gitlab pod to go to green

Looks like our deployment and all pods are green. Let's check our GitLab deployment...

> * Go to `gitlab.make-sid-dance.com`, adjusting the URL to the domain you used for this demo.

Boom, we’ve got a shiny new GitLab installation!

### Log in as root, add a license, and configure Kubernetes

First things first, we need to secure the root account with a new password.

> * Set password for root user
> * Log in as `root` with password you just created

### [OPTIONAL] GitLab EE License

Now let's add a trial license.
> * Go to [https://about.gitlab.com/free-trial/](https://about.gitlab.com/free-trial/) and enter in your info to request a trial license for GitLab EE
> * Wait for email
> * Copy license from email
> * Click on Update License, and paste in the license

### Add Kubernetes credentials to CI

*TODO: [Automatically configure Kubernetes for project when GitLab is installed in cluster](https://gitlab.com/gitlab-org/gitlab-ce/issues/28888)*

Now let's set up the Kubernetes integration for all of our projects.

> * Go to Admin wrench, Settings > Service templates
> * Select Kubernetes

First I need to activate it, and get the IP address for the cluster from GKE.

> * Select `Active`
> * Go to GCP, [Container Engine tab](https://console.cloud.google.com/kubernetes/list)
> * Click on cluster
> * Copy Endpoint to  `API URL` in GitLab, making it an HTTPS URL (such as `https://104.154.177.137`)

Then I grab an Access Token and Cert from the Kubernetes Dashboard.

> * Go to [Kubernetes Dashboard](http://localhost:8001/ui) that is proxied on your localhost.
> * Navigate to Secrets > Config on the left.
> * Click on `default-token-xxx` for the `default` namespace
> * Click the eyeball next to `token` (last item) and copy to `Service token` in GitLab
> * Click the eyeball next to `ca.crt` (first item) and copy (including `BEGIN` and `END` lines) to `Custom CA bundle` in GitLab
> * Click Save Settings

We're done with the administrator, so let's log out.

> * Click Gravatar > Sign out

## Cleanup

> * *TODO: [Document how to clean up a GKE cluster after demo](https://gitlab.com/gitlab-org/gitlab-ce/issues/28502)*
> * Before you delete the cluster, delete all of the underlying services/pods/etc. using the CLI.
> * If you accidentally delete the cluster using the web UI, make sure you:
>   * Look for [persistent disks](https://console.cloud.google.com/compute/disks?project=gitlab-demos&organizationId=769164969568) that need to be deleted manually.
>   * Look up the [external IP](https://console.cloud.google.com/networking/addresses/list?project=gitlab-demos&organizationId=769164969568) you used, find the ID of the load balancer it is forwarding to, then find that ID in the list of [load balancers](https://console.cloud.google.com/networking/loadbalancing/list?project=gitlab-demos&organizationId=769164969568). Delete the load balancer.
> * Release the [static IP](https://console.cloud.google.com/networking/addresses/list?project=gitlab-demos&organizationId=769164969568).

## Troubleshooting

### Various failures block Let's Encrypt, and thus GitLab
There are several scenarios which can cause deployment failures due to issues surrounding the `kube-lego-nginx` and the Let's Encrypt (LE) ACME process. The easiest way to find these errors is checking the logs of the `kube-lego-nginx` service in the `kube-lego` namespace of the dashboard for your Kubernetes cluster.

1.  **Let's Encrypt top-level domain request rate limit exceeded**

     The failure mode here is the most vague from the logs, however it occurs when you have exceeded the number of certificate or renewal requests allowed for a single TLD. [Please see their documentation regarding this](https://letsencrypt.org/docs/rate-limits/).

1.  **Unresolvable DNS**

     If your DNS records are not correctly configured, the Let's Encrypt servers may not be able to resolve your domain when the ACME requests are filed against it. Let's Encrypt performs a reachability test that depends on valid, resolvable Fully-Qualified Domain Names. You must confirm that your entry DNS is functional, and has propagated. You can do this by using an external host (anywhere not directly querying your primary DNS where this record is present) to ping `test.my.tld` where `my.tld` is the domain name you are using. Because you should have configured a wildcard record (`*.my.tld`), `test.my.tld` should resolve to that address.

1.  **Host not responding (reachability)**

    This has been observed as a failure of the LoadBalancer to be properly connected to the reserved statis external IP address. There are a few methods of failure here, but the primary cases are:
    *  Unable to assign due to prior assignment.

        Either an existing use, or a failure to fully remove the prior deployment. This has been seen in both scenarios by GitLab personnel.  If you are re-creating a previous deployment, you need to wait a short period and/or confirm that the previously used GCP Networking LoadBalancer has been removed. You can manually remove these if you do not wish to wait for GCP to catch up with the de-provisioning.
    *  Unable to assign due to incorrect region.

        If you inadvertently create a GKE Kubernetes cluster in a region that is not the same as the static IP address you are attempting to use, your deployment will fail to attach to that IP address, and result in the inability to listen and respond to requests.

### Other errors

* **You upload the yaml configuration FILE and see** `SchedulerPredicates failed due to persistentvolumeclaims "gitlab-rails-storage" not found, which is unexpected` **on the Kubernetes Dashboard (in Workspaces)**
  * Try to reupload the configuration again using CLI `kubectl apply -f gitlab-make-sid-dance-com.yml`

* **You upload the yml configuration file, everything's green but GitLab still doesn't work**
  * Open the yml file
  * Check if you set the IP correctly (search for `loadBalancerIP`)
  * Check if you set the domain correctly (search for `host`)
  * Update file if needed (or generate a new one)
  * Apply the configuration file again `kubectl apply -f gitlab-make-sid-dance-com.yml`

### General notes

#### Creating connection to your cluster from kubectl

* Navigate to [Container Engine](https://console.cloud.google.com/kubernetes/list).
* Click on the `Connect` button for your cluster.
* Click the `copy` icon to the right of the `gcloud container ...` entry. It looks like two overlapping white boxes.
  * `gcloud container clusters get-credentials makesiddance-com \
    --zone us-central1-a --project gitlab-demos`
* Switch to the Terminal window, paste this command in, run it.
* run `kubectl proxy`

#### Logs

* You can find logs for each pod in the Kubernetes Dashboard
  * Select `Namespace` you want to see logs for
  * Navigate to `Pods`
  * Select `Pod` you want to see logs for
  * Click on `View logs`

* You can check logs from CLI using `kubectl` as well
 ```
  kubectl get namespaces
  kubectl get pods --namespace=<NAMESPACE>
  kubectl logs <POD> --namespace=<NAMESPACE>
 ```
