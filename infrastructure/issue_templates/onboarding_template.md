Title: Production Engineer Onboarding  - [Fill in name and start date]

New team member = N
Onboarder = O

1. [ ] Getting Started:
  1. [ ] O: create this issue and mark it confidential
  1. [ ] O: cross-link general onboarding issue in the peopleops issue tracker
  1. [ ] N: read the [infrastructure handbook](https://about.gitlab.com/handbook/infrastructure/) and pages linked from there. Find something to improve? Make a merge request!
1. [ ] Accounts:
  1. [ ] N: comment in this issue with your desired Unix username and your SSH public key. Tip: use the same username you use on your laptop.
  1. [ ] N: [create Microsoft account](https://signup.live.com) for yourname@gitlab.com
  1. [ ] N: create your GitLab `admin` account. [Register](https://gitlab.com/users/sign_in#register-pane) using yourname+admin@gitlab.com. After that, make sure you create an issue in the [infrastructure project](https://gitlab.com/gitlab-com/infrastructure/issues) so you are granted the appropriate privileges (please label the issue as `access request`)
  1. [ ] O: invite new production engineer to [Digital Ocean](https://cloud.digitalocean.com/settings/team) (new production engineer: make sure you are not signed in to DO when accepting the invite!)
1. [ ] Permissions:
  1. [ ] O: add new production engineer as 'developer' to the [gitlab-com](https://gitlab.com/groups/gitlab-com/group_members) group.
  1. [ ] O: add new production engineer as 'developer' to the [gitlab-org](https://gitlab.com/groups/gitlab-org/group_members) group.
  1. [ ] O: add new production engineer as 'master' to the [cookbooks](https://gitlab.com/groups/gitlab-cookbooks/group_members) group.
  1. [ ] O: add new production engineer as 'master' to the [gl-infra](https://gitlab.com/groups/gl-infra/group_members) group.
  1. [ ] O: add new production engineer as 'master' to the [gitlab-cog](https://gitlab.com/groups/gitlab-cog/group_members) group.
  1. [ ] O: create a cog user and add the new production engineer to the right groups (gitlab-admin, for a start)
  1. [ ] O: invite the new production engineer to [Azure Active Directory](https://portal.azure.com/?reAuth=true#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
    1. Azure AD -> Users and Groups -> All Users -> New Guest User -> Enter email and invite.
  1. [ ] N: create your account with the invitation.
  1. [ ] O: grant owner permission to the new production engineer in [Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)
    1. Subscriptions -> Microsoft Azure Sponsorship -> Access control -> Add -> (Role Owner - Pick the User) -> Save
  1. [ ] O: add new production engineer to the Azure subscription
  1. [ ] O: make new production engineer 'co-admin' (Click on the user -> Directory Role -> Global Administrator -> Save)
  1. [ ] O: make new production engineer 'admin' on [AWS](https://console.aws.amazon.com/iam/home#home)
1. [ ] Tools:
  1. [ ] N: install the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
  1. [ ] N: investigate installing and enabling the [toolbelt](https://gitlab.com/gl-infra/toolbelt)
1. Monitoring:
  1. [ ] O: make new production engineer 'admin' on [private monitoring infrastructure](https://performance.gitlab.net)
  1. [ ] N: get familiar with the dashboards in the [private monitoring infrastructure](https://performance.gitlab.net)
  1. [ ] N: get familiar with the dashboards in the [public monitoring infrastructure](http://monitor.gitlab.net)
  1. [ ] N: get familiar with [prometheus](https://prometheus.gitlab.com/graph), investigate how to [query](https://prometheus.io/docs/querying/basics/) to get information out of it.
  1. [ ] N: get familiar with [targets](https://prometheus.gitlab.com/targets) and [alerts](https://prometheus.gitlab.com/alerts) within prometheus.
  1. [ ] N: get familiar with [prometheus alert manager](https://alerts.gitlab.com), look for the documentation of this in the [runbooks](https://gitlab.com/gitlab-com/runbooks).
1. [ ] Runbooks and Alerts:
  1. [ ] O: add new production engineer as 'master' to [runbooks](https://gitlab.com/gitlab-com/runbooks/project_members).
  1. [ ] N: clone and get familiar with the [runbooks](https://gitlab.com/gitlab-com/runbooks)
  1. [ ] N: submit a fix of documentation to the runbooks.
  1. [ ] N: submit a fix to an alert in the runbooks (or submit a new one).
  1. [ ] N: after having the MR merged, run `chef-client` in prometheus to enable the new alert.
1. [ ] Chef:
  1. [ ] N: clone the [chef-repo](https://dev.gitlab.org/cookbooks/chef-repo) and run `bundle install` to install all the dependencies
  1. [ ] N: [create a SSH user](https://dev.gitlab.org/cookbooks/chef-repo/blob/master/README.md#add-a-new-sysadmin) and send an MR to [chef-repo](https://dev.gitlab.org/cookbooks/chef-repo)
  1. [ ] O: run `sudo chef-client` on `chef.gitlab.com` to ensure the new production engineer has SSH access there
  1. [ ] N: create Chef user and Chef key via `ssh chef.gitlab.com` and [chef-server-ctl user-create](https://dev.gitlab.org/cookbooks/chef-repo/blob/master/doc/set-up-chef-server.md#creating-users)
  1. [ ] N: add your Chef user to the 'gitlab' and 'staging' groups with `chef-server-ctl org-user-add`
  1. [ ] O: make the new chef user admin with [knife acl](https://dev.gitlab.org/cookbooks/chef-repo/blob/master/doc/set-up-chef-server.md#add-users-to-the-admins-group-of-the-gitlab-organization)
  1. [ ] N: create chef-repo/.chef/knife.rb from [knife.rb.example](https://dev.gitlab.org/cookbooks/chef-repo/blob/master/knife.rb.example)
  1. [ ] N: test your chef setup with `knife status`
  1. [ ] O: add new Chef user to VAULT_ADMINS in Rakefile and run `rake update_vault_admins`
1. [ ] VPN Access:
  1. [ ] N: Make sure you have VPN by following the instructions from [creating client certificate](https://gitlab.com/gitlab-cookbooks/gitlab_openvpn#how-to-create-a-client-certificate).
  1. [ ] N: Test VPN access by bringing the VPN up and ssh'ing into a staging sidekiq host (`sidekiq-asap01.sv.stg.gitlab.com`)
1. [ ] Communications:
  1. [ ] O: mention the new production engineer in the `production` channel.
  1. [ ] O: mention the new production engineer in the `prometheus-alerts` channel.
  1. [ ] N: learn who your teammates are and ping them in your onboarding issue - We do mention the people we address to in issues, get used to doing it.
1. [ ] Context & Comfort with GitLab's code base:
  1. [ ] N: review issues labeled as `outage` in the infrastructure issue tracker.
  1. [ ] O: point the new production engineer to the ongoing meta issues that define the team strategy.
  1. [ ] N: read about the [application architecture](https://docs.gitlab.com/ce/development/architecture.html)
  1. [ ] N: contribute a merge request to one of the following repos: gitlab-ce, gitlab-ee, gitaly, workhorse, gitlab-runner (or take a look at the [engineering projects](https://about.gitlab.com/handbook/engineering/projects) for more inspiration). The idea here is to get comfortable with the application architecture and codebase, but not to spend more than 0.5 - 1 day on coding for this task.
