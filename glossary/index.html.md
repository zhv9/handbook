---
layout: markdown_page
title: "GitLab Glossary"
---

The following terms are often used in documentation, blog posts, and everyday
life at GitLab. This list is always a work in progress and additions are very
welcome. When adding or editing an entry, please do _not_ have the headers be
clickable hyperlinks as this seems to break the TOC functionality (i.e. clicking
  on the item in the TOC will go to the external hyperlink instead of the deep
  link).

---

### On this page
{:.no_toc}

- TOC
{:toc}

----

---
### A

#### Amazon RDS

External reference:<http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html>

#### Application lifecycle management (ALM)

The oversight, development, and maintenance of computer programs. Gitlab has [advantages](https://docs.google.com/presentation/d/1vCU-NbZWz8NTNK8Vu3y4zGMAHb5DpC8PE5mHtw1PWfI/edit#slide=id.g72f2e4906_2_288) over both legacy and modern ALM tools.

#### Audit Logs

---
### B

#### Branch

Independent line of development. New commits are recorded in the history of the branch you are working in.

#### Build triggers

Related [documentation](https://docs.gitlab.com/ce/ci/triggers/README.html)

---
### C

#### Canonical source

#### ChatOps

The ability to initiate an action from chat.

#### ChatBots

Bots that run in your chat application and give you the ability to do "anything" from chat.


#### Clone

a local copy of the project you want to work on.


#### Commit



#### ConvDev or Conversational Development

Introduction to ConvDev: <https://about.gitlab.com/2016/09/14/gitlab-live-event-recap/>

A natural evolution of software development that carries a conversation across
functional groups throughout the development process, enabling developers to
track the full path of development in a cohesive and intuitive way. ConvDev
accelerates the development lifecycle by fostering collaboration and knowledge
sharing from idea to production.

---

#### CI / CD

##### Continuous Integration

Related blog post: <https://about.gitlab.com/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/>

A process that involves adding new code commits to source code with the combined
code being run on an automated test to ensure that the changes do not break the
software. [Thoughtworks discusses continuous integration.](https://www.thoughtworks.com/continuous-integration)

##### Continuous Deployment

Continuous deployment is the next step of continuous delivery: Every change that
passes the automated tests is deployed to production automatically. [The difference
between Continuous Delivery and Continuous Integration.](https://www.youtube.com/watch?v=igwFj8PPSnw)

##### Continuous Delivery

Continuous delivery is a series of practices designed to ensure that code can be
rapidly and safely deployed to production by delivering every change to a
production-like environment and ensuring business applications and services
function as expected through rigorous automated testing.[Amazon moves toward
continuous delivery](https://www.youtube.com/watch?v=esEFaY0FDKc)

---

#### Cycle Time

The time it takes to move from [idea to production.](https://about.gitlab.com/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/#from-idea-to-production-with-gitlab)

#### Cycle Analytics

See <https://gitlab.com/gitlab-org/gitlab-ce/issues/22458>

---
### D

#### Dependencies

As in "specify [dependencies](https://gitlab.com/gitlab-org/gitlab-ce/issues/14728) between stages"

#### DevOps

The epicenter of software engineering, quality assurance, and technology operations. [DevOps glossary by XebiaLabs](https://xebialabs.com/glossary/).

#### Diff

A commit that shows the changes before and after.

#### Directory

A folder used for storing multiple files.

#### Dynamic environments (review apps)

#### Docker container registry

Related blog post: <https://about.gitlab.com/2016/05/23/gitlab-container-registry/>

---
### E

#### EC2 Instance

#### Emacs

External reference: <https://www.masteringemacs.org/article/mastering-key-bindings-emacs>

---
### F

#### Fork

A copy of an original repository that you can put somewhere else or where you
can experiment and apply changes that you can later decide if publishing or not,
without affecting your original project.

#### Funnel, or: TOFU, MOFU, BOFU
{: #funnel}

External reference: [Blog post](https://www.weidert.com/whole_brain_marketing_blog/bid/113688/ToFu-MoFu-BoFu-Serving-Up-The-Right-Content-for-Lead-Nurturing)


TOFU: top of funnel
MOFU: middle of funnel
BOFU:  bottom of funnel

---

---
### G

#### Git commands and concepts

Also see the main [Git project](https://git-scm.com/about).

##### Git Hook

External reference: <https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks>

From the page that is linked in the title: "Git has a way to fire off custom
scripts when certain important actions occur. There are two groups of these
hooks: client-side and server-side. Client-side hooks are triggered by operations
such as committing and merging, while server-side hooks run on network operations
such as receiving pushed commits."

Difference between a [webhook](#webhooks) and a git hook: a git hook is local to its repo
(usually) while a webhook is not (it can make API or http calls). So for example
if you want your linter to fire before you commit, you can set that up with a git hook. If
the linter fails, the commit does not go through. A git hook _can_ be configured
to go beyond its repo, e.g. by having it make an API call.

##### GUI/Git GUI

External reference: <https://git-scm.com/docs/git-gui>

##### pull

Git command to synchronize the local repository with the remote repository, by fetching all remote changes and merging them into the local repository. ("git pull origin [branch name]")

##### push

Git command to send commits from the local repository to the remote repository.

##### Rebase (v)

##### Staging area

Modified files that have been marked to go into the next commit.

##### Untracked files

New files that Git has not been told to track previously. Add them by using the
command "git add [file path]"

##### Working area

Files that have been modified but are not committed. Check them by using the
command "git status"

---

#### GitLab Geo

See GitLab Geo [documentation](https://docs.gitlab.com/ee/gitlab-geo/README.html)

#### GitLab High Availability

#### GitLab Master Plan

Related blog post: <https://about.gitlab.com/2016/09/13/gitlab-master-plan/>.

#### GitLab Pages

See GitLab Pages [description](https://about.gitlab.com/features/pages/).

#### GitLab Runner

Related project: <https://gitlab.com/gitlab-org/gitlab-ci-multi-runner>

#### Gogs

External reference: <https://gogs.io/>

#### golang

---
### I

#### Inner-sourcing

Related [blog post](https://about.gitlab.com/2014/09/05/innersourcing-using-the-open-source-workflow-to-improve-collaboration-within-an-organization/)

The use of open source development techniques within the corporation.


---

#### Integrations

##### JIRA integration

Related [documentation](https://docs.gitlab.com/ee/project_services/jira.html)

##### Jenkins Integration

Related [documentation](https://docs.gitlab.com/ee/integration/jenkins.html)

##### Slack Integration

Related [documentation](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/project_services/slack.md)

---

#### Internet Relay Chat (IRC)

External reference: <http://www.irchelp.org/>

---
### J

#### JUnit

---
### L

#### LDAP group sync


#### Lint

Static code analysis for our various file types. For example, we use [scss-lint](https://github.com/brigade/scss-lint)
to ensure that a consistent code styling is respected. Similar tools: rubocop / eslint.

#### Load Balancer

---
### M

#### Mattermost

#### Merge conflict resolution

Related blog post: <https://about.gitlab.com/2016/09/06/resolving-merge-conflicts-from-the-gitlab-ui/>

#### Merge Request

Documentation: <https://docs.gitlab.com/ce/gitlab-basics/add-merge-request.html>

Takes changes from one branch, and applies them into another branch.


#### Mount

External reference: <https://en.wikipedia.org/wiki/Mount_(Unix)>

As stated on the wikipedia page, "Mounting makes file systems, files, directories,
devices and special files available for use and available to the user."

For example, we have NFS servers where the _git files_  reside. In order for a
worker node to "see" or "use" the git files, the NFS server needs to be _mounted_
on the worker; that is, the worker needs to know that the NFS server exists and
how to connect to it. Think of it as getting a shared drive to show up in your
Finder (on Mac) or Explorer (on Windows).

---
### N

#### NGINX

Related [documentation](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/nginx.md)

---
### O

#### OAuth

#### On premise

On your own server. The fact that GitLab is on premise is a strong point for
large corporate clients concerned with security.

#### Open Core

External reference: <https://en.wikipedia.org/wiki/Open_core>

GitLab's business model. Coined by Andrew Lampitt in 2008, the open core model
primarily involves offering a "core" or feature-limited version of a software
product as free and open-source software, while offering "commercial" versions
or add-ons as proprietary software.

#### Open Source

External reference: <https://opensource.org/docs/osd>

Including to providing access to the source code, open source software must
comply with a number of criteria, among them free distribution and no
discrimination against persons,  groups, or fields of endeavor.

#### Open Source Stewardship

Related blog post: <https://about.gitlab.com/2016/01/11/being-a-good-open-source-steward/>

---
### P

#### PostgreSQL / MySQL DBMS

Related [documentation](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/database.md)

---
### R

#### Raketasks

#### Regression

A regression is something that used to work one way in the last release and
then we made a **breaking change** and it no longer works the same way.

_or_

A regression is defined as a change that results in a negative impact on the
functionality of an existing feature due to recent changes, i.e. the latest release.

#### Repository

A directory where Git has been initialized to start version controlling your
files. The history of your work is stored here.

#### Remote mirroring

##### Remote repository

Related blog post: <https://about.gitlab.com/2015/05/18/simple-words-for-a-gitlab-newbie/>

A repository that is not-on-your-machine, so it's anything that is not your
computer. Usually, it is online, GitLab.com for instance. The main remote
repository is usually called “Origin”.

#### Route Table

---
### S

#### Shell

Related documentation: <https://docs.gitlab.com/ce/gitlab-basics/start-using-git.html>

Terminal on Mac OSX, GitBash on Windows, or Linux Terminal on Linux

#### Shell command runner

#### Slash commands

#### SSH Key

Documentation on [creating your own SSH key](https://docs.gitlab.com/ce/gitlab-basics/create-your-ssh-keys.html)
A unique identifier of a computer. It is used to identify computers without the need for a password. e.g. On GitLab I have added the ssh key of all my work machines so that the GitLab instance knows that it can accept code pushes and pulls from this trusted machines whose keys I have added.

#### Static Site Generators (SSGs)

External definition: <https://wiki.python.org/moin/StaticSiteGenerator>

#### Subnet

---
---
### T

#### Tenancy

##### Multi-tenant

External definition: <http://whatis.techtarget.com/definition/multi-tenancy>

A multi-tenant GitLab instance can have any number of customers - such as companies or
groups of users using it. GitLab.com is an example of a multi-tenant GitLab instance.

##### Single-tenant

External definition: <http://searchcloudapplications.techtarget.com/definition/single-tenancy>

A single-tenant GitLab instance has only one customer - such as a company - using it.
On premise GitLab instances are almost exclusively single-tenant.

---

#### True-Up licensing model

#### Ubuntu

#### Upstream repository vs. GitLab repository

External conversation: <https://news.ycombinator.com/item?id=12487112>

---

---
### V

#### Version control (systems)

Version control is a system that records changes to a file or set of files over
time so that you can recall specific versions later.

##### Local version control systems

Related [presentation](https://docs.google.com/presentation/d/16sX7hUrCZyOFbpvnrAFrg6tVO5_yT98IgdAqOmXwBho/edit#slide=id.gd69537a19_0_32)

Copying files into another directory on your local computer. This is a common
and early form of version control, but it is error-prone.

##### Centralized version control systems

These systems, such as [CVS](#CVS), Subversion, and Perforce, have a single
server that contains all the versioned files, and a number of clients that
check out files from that central place. For many years, this has been the
standard for version control.

##### Distributed version control systems

External reference: <https://en.wikipedia.org/wiki/Distributed_version_control>

Distributed version control, also known as distributed revision control or
decentralized version control, allows many software developers to work on a
given project without requiring them to share a common network.

DVCSs fully mirror the repository. Git, Mercurial, Bazaar, and Darcs are DVCSs.
If any server dies, and these systems were collaborating via it, any of the
client repositories can be copied back up to the server to restore it.

#### CVS (Concurrent Versioning System)
{: #CVS}

---

#### VM Instance

External reference: <https://cloud.google.com/compute/docs/instances/>

#### VPC - Virtual Private Cloud

Related definition: <https://docs.gitlab.com/ce/university/glossary/README.html#virtual-private-cloud-vpc>

#### Virtual private server (VPS)

---
### W

#### Webhooks

A way for for an app to provide other applications with real-time information
e.g. send a message to a slack channel when a commit is pushed

---
### Y

#### yaml configuration
