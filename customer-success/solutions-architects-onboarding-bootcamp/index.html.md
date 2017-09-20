---
layout: markdown_page
title: "Solutions Architect Onboarding"
---

**SOLUTIONS ARCHITECTS Onboarding Bootcamp**



**Week 1**

**Regular Onboarding Duties** 
 https://about.gitlab.com/handbook/general-onboarding/
 
  
**Week 2 Technical Onboarding**
 
Download Git https://docs.gitlab.com/ce/gitlab-basics/start-using-git.html
Stage 1: Become familiar with git and GitLab basics

Cover the Beginner and Intermediate sections (and a few Advanced) in the GitLab University (https://university.gitlab.com/):
Under the topic of Git
*  About Version Control (https://docs.google.com/presentation/d/16sX7hUrCZyOFbpvnrAFrg6tVO5_yT98IgdAqOmXwBho/edit#slide=id.gd69537a19_0_14) 
*  Try Git (https://www.codeschool.com/account/courses/try-git)
*  Under the topic of GitLab Basics
*  All the GitLab Basics (http://docs.gitlab.com/ce/gitlab-basics/README.html) that you don't feel comfortable with. If you get stuck, see the linked videos under GLB in GitLab University 
*  GitLab Flow (https://www.youtube.com/watch?v=UGotqAUACZA)
*  Take a look at how the different GitLab versions compare (https://about.gitlab.com/features/#compare)
*  Any of these that you don't feel comfortable with in the user training (https://gitlab.com/gitlab-org/University/tree/master/training) we use for our customers.
  - `env_setup.md`
  -`feature_branching.md`
  - `explore_gitlab.md`
  -`stash.md`
  - `git_log.md`
* For the rest of the topics in `user training`, just do a quick read over the file names so you start remembering where to find them.
*  Get familiar with the services GitLab offers
  - The differences between [CE and EE](https://about.gitlab.com/pricing/)
  - GitHost (https://about.gitlab.com/gitlab-hosted/)
  - Read through the GitHost documentation (https://dev.gitlab.org/gitlab/GitHost/blob/master/doc/README.md)

Perform each of the following Installation Methods (https://about.gitlab.com/installation/) on your preferred test environment you chose above:
*  Install via [Omnibus](https://gitlab.com/gitlab-org/omnibus-gitlab/)
*  Populate with some test data: User account, Project, Issue
*  Backup using our Backup rake task
(http://docs.gitlab.com/ce/raketasks/backup_restore.html#create-a-backup-of-the-gitlab-system)
*  Install via [Docker](https://gitlab.com/gitlab-org/gitlab-ce/tree/master/docker)
*  Restore backup to your Docker VM using our Restore rake task (http://docs.gitlab.com/ce/raketasks/backup_restore.html#restore-a-previously-created-backup)

Getting to know GitLab Support
*  Pair with a support team member 
      - Identify support engineer (appropriate to timezone)
      - Pair on 3-5 calls 
     
Complete Zendesk Agent training (allow 40 minutes for completion)
*  Navigate to [Zendesk university](https://university.zendesk.com/#/purchase/category/34942) and order the **"Agents: Zendesk Fundamentals Online"** course
*  Add the **"Agents: Zendesk Fundamentals Online"** course to your cart and click "Proceed to Checkout"
      - Follow the prompts and finalize your order.
      - You'll receive an email with information on accessing the Zendesk course
      - Proceed to complete the **"Agents: Zendesk Fundamentals Online"** course
      - Review additional Zendesk resources
      - UI Overview (https://support.zendesk.com/hc/en-us/articles/203661806-Introduction-to-the-Zendesk-agent-
 interface)
      - Updating Tickets (https://support.zendesk.com/hc/en-us/articles/212530318-Updating-and-solving-tickets)
      - Working w/ Tickets (https://support.zendesk.com/hc/en-us/articles/203690856-Working-with-tickets) *Read: avoiding agent collision.*
*  Dive into our ZenDesk support process by reading how to handle tickets (https://about.gitlab.com/handbook/support/onboarding/#handling-tickets)
*  Learn about the tiered support system (https://about.gitlab.com/handbook/support/#tiered-support)
*  Read about Escalation (https://about.gitlab.com/handbook/support/onboarding/#create-issues)
*  Take a look at the GitLab.com Team page (https://about.gitlab.com/team/) to find the resident experts in their fields
*  Understand what's in the pipeline and proposed features at GitLab: Direction Page (https://about.gitlab.com/direction/)
*  Practice searching issues and filtering using labels (https://gitlab.com/gitlab-org/gitlab-ce/labels) to find existing feature proposals and bugs
*  If raising a new issue always provide a relevant label and a link to the relevant ticket in Zendesk
*  Take a look at the existing issue templates (https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#issue-tracker) to see what is expected
*  Environment Information and maintenance checks (http://docs.gitlab.com/ce/raketasks/maintenance.html)
*  GitLab check (http://docs.gitlab.com/ce/raketasks/check.html)
*  Omnibus commands
*  Status (https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/maintenance/README.md#get-service-status)
*  Starting and stopping services (https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/maintenance/README.md#starting-and-stopping)


*  Starting a rails console (https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/maintenance/README.md#invoking-rake-tasks)
*  Get to know the GitLab API (https://docs.gitlab.com/ee/api/README.html), its capabilities and shortcomings
*  Learn how to migrate from SVN to Git (https://docs.gitlab.com/ee/workflow/importing/migrating_from_svn.html)
*  Set up  GitLab CI (https://docs.gitlab.com/ee/ci/quick_start/README.html)

**Self assessments**
*  [General SCM/Git knowledge and DevOps](https://goo.gl/forms/BjNezQx487d7uFpz2)
*  [Installing/configuring GitLab and Gitlab best practices](https://goo.gl/forms/zN5OwQIrulR8g6G32)
*  [Gitlab CI/CD](https://goo.gl/forms/KMj3U6xfLfo4sBnp1)

**Week 3-4**

*  GitLab Workflow (https://about.gitlab.com/2016/10/25/gitlab-workflow-an-overview/) 
*  Latest Version released features (https://about.gitlab.com/2017/06/07/gitlab-9-dot-2-dot-5-security-release/#)
*  GitLab Products (https://about.gitlab.com/products/)
*  Future Releases (https://about.gitlab.com/direction/#future-releases)
*  Know EE features for upgrade from CE (https://about.gitlab.com/comparison/gitlab-ce-vs-gitlab-ee.html#dropdown)
*  EE Starter to EE Premium (https://about.gitlab.com/comparison/gitlab-ees-vs-gitlab-eep.html)  
*  Who's who in Product (https://about.gitlab.com/handbook/product/)
 
*  Study the [Sales Handbook](https://about.gitlab.com/handbook/sales/) 
 
*  Familiarize yourself with our [Lead Qualification Process](https://about.gitlab.com/handbook/marketing/lead-generation/content/#leadQual) 
 
*  [Idea to Production Demo](https://about.gitlab.com/handbook/product/i2p-demo/)

*  [GitLab EE product qualification questions](https://about.gitlab.com/handbook/EE-Product-Qualification-Questions/)
*  [Understanding of Gitlab HA and Gitlab GEO] (https://about.gitlab.com/high-availability/)
 
 
In the Sales Folder, familiarize yourself with:
Our [Sales Agenda](https://docs.google.com/document/d/1l1ecVjKAJY67Zk28CYFiepHAFzvMNu9yDUYVSQmlTmU/edit)
[Competition](https://about.gitlab.com/comparison/)

**Self assessments**
*  [Gitlab HA and Gitlab GEO](https://goo.gl/forms/qkVaOMLGKF9k9jcf1)

**Week 5-6**

**Understanding the Competition**
(Competition (https://about.gitlab.com/comparison/))
*  Github
*  Bitbucket
*  Other

**Understand Integrations**
*  Jira (https://docs.gitlab.com/ee/user/project/integrations/jira.html)
*  Jenkins (https://docs.gitlab.com/ee/integration/jenkins.html)

**Migrations from other Version Control Systems**
*  SVN (https://git-scm.com/book/en/v1/Git-and-Other-Systems-Git-and-Subversion)

**Integrating with GitLab**

**Ways to Integrate**

If you want to integrate with GitLab there are three possible paths you can take:

*  Utilizing webhooks - If you want to reflect information from GitLab or initiate an action based on a specific activity that occurred on GitLab you can utilize the existing infrastructure of our webhooks. To read about setting up webhooks on GitLab visit this page.

*  API integration - If you're seeking a richer integration with GitLab, the next best option is to utilize our ever expanding API. The API contains pretty much anything you'll need, however if there's an API call that is missing we'd be happy to explore it and develop it.

*  Project Services - Project services give you the option to build your product into GitLab itself. This is the most advanced and complex method of integration but is by far the richest. It requires you to add your integration to GitLab's code base as a standard contribution. You can see the list of project services available, and look into this example. If you're thinking of creating a project service, the steps to follow are similar to any contribution to the GitLab codebase.

*  Authentication via LDAP/OAuth (https://docs.gitlab.com/ee/integration/oauth_provider.html)

**Self assessments**
*  [Data migration & integrations](https://goo.gl/forms/Ld2mg6LjmcGgGqkj1)

**Solutions Architect Pre sales activities**
*  RFI
*  PoC planning & execution 


**Solutions Architect Post sales activities**
*  Implementation
*  [Health Checks](https://docs.google.com/document/d/1aHA3W2FsHUApnz2XVtJoyhpcGYy6bgOHoRi4ArXnF0o/edit)

**Demo Scenarios**
You will be required to demo to team all demo scenarios specific to customer/prospect requirements in mock style showing business value (https://docs.google.com/document/d/1kSVUNM4u6KI8M9FxoyiUbHEHAHIi34iiY25NhMxLucc/edit) 

Final certification

*  Sales role play (demo scenarios)

*  Comparison of Gitlab editions (key differentiators and business drivers)

*  Ecosystem and how Gitlab interacts/compete with other tools

*  Presentation on Idea to Production

*  Interactive demo paired with another SA

