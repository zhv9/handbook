---
layout: markdown_page
title: "Engineering"
---

## Communication<a name="reach-engineering"></a>

- [**Public Issue Tracker (for GitLab CE)**](https://gitlab.com/gitlab-org/gitlab-ce); please use confidential issues for topics that should only be visible to team members at GitLab.
- [**Chat channel**](https://gitlab.slack.com/archives/development); please use the `#development` , `#frontend`, `#infrastructure`, `#ci-cd`, and `#support` chat channels for questions that don't seem appropriate to use the issue tracker or the internal email address for.

## On this page
{:.no_toc}

- TOC
{:toc}

## Other Related Pages

- [Developer onboarding](/handbook/developer-onboarding)
- [Engineering Workflow](/handbook/engineering/workflow)
- [Frequently Used Projects](/handbook/engineering/projects)
- [Issue Triage Policies](/handbook/engineering/issues/issue-triage-policies)
- [Critical Security Release Process](/handbook/engineering/critical-release-process)
- [Performance of GitLab](/handbook/engineering/performance)
- [Monitoring of GitLab.com](/handbook/infrastructure/monitoring)
- [Production Readiness Guide](https://gitlab.com/gitlab-com/infrastructure/blob/master/.gitlab/issue_templates/production_readiness.md)

## GitLab Repositories

GitLab consists of many subprojects. A curated list of GitLab Repositories
can be found at the [GitLab Engineering Projects](/handbook/engineering/projects) page.

When adding a repository please follow these steps:
1. Ensure the project is under the gitlab-org namespace for anything related to the application or gitlab-com for anything strictly company related.
1. [Add the project to the list of GitLab Repositories](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/doc/projects.md)
1. Add MIT license to the repository. See [MIT License Example](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/LICENSE).
1. Add Contribution Guide. See [Contribution Example](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md),
and be sure to refer to the Contributor License Agreements for
[individuals](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/doc/legal/individual_contributor_license_agreement.md)
and [corporations](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/doc/legal/corporate_contributor_license_agreement.md).
1. Add link to `CONTRIBUTING.md` from the project's `README.md`

## Engineering Groups

- [Support](/handbook/support)
- [Backend](/handbook/backend)
- [Edge](/handbook/edge)
- [Frontend](/handbook/frontend)
- [Build](/handbook/build)
- [UX](/handbook/ux)
- [Security](/handbook/engineering/security)
- [Infrastructure](/handbook/infrastructure)
  - [Production](/handbook/infrastructure/production)
  - [Database](/handbook/infrastructure/database)
  - [Gitaly](/handbook/infrastructure/gitaly)

## Collaboration

To maintain our rapid cadence of shipping a new release every month, we must
keep the barrier low to getting things done. Since our team is distributed
around the world and therefore working at different times, we need to work
in parallel and asynchronously as much as possible.

That also means that if you are implementing a new feature, you should feel
empowered to work on the entire stack if it is most efficient for you to do so.

## Code quality and standards

We need to maintain code quality and standards. It's very important
that you are familiar with the [Development Guides] in general, and the ones that
relates to your group in particular:

- [UX Guides](https://docs.gitlab.com/ee/development/ux_guide/index.html)
- [Backend Guides](https://docs.gitlab.com/ee/development/README.html#backend-howtos)
- [Frontend Guides](https://docs.gitlab.com/ee/development/fe_guide/index.html)
- [Database Guides](https://docs.gitlab.com/ee/development/README.html#databases)

[Development Guides]: https://docs.gitlab.com/ee/development/README.html

## Code Reviews

Code reviews are mandatory for every merge request, you should get familiar and
follow our [Code Review Guidelines](https://docs.gitlab.com/ce/development/code_review.html).

## Developers on Support Team Rotation

See [the fix4all description](/handbook/engineering/fix4all/).

## Release Managers

The [release-tools repository](https://gitlab.com/gitlab-org/release-tools/tree/master)
contains useful information about the responsibilities and tasks performed
by a [release manager](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/release-manager.md).

Because of the volume of work required to get a release out the door, there
will be two primary release managers:

1. One in the America time zones
2. One in Europe/Middle East/Africa (EMEA) or Asia Pacific (APAC)

Trained release managers, one in Americas and one on EMEA/APAC, will
ultimately be in charge of making sure the release candidates (RCs) get created and deployed.

* These release managers need to be very vocal if they need help or something
is blocking the release candidate (RC)

* Trainee release managers will do most of the hands-on work
(e.g. cherry-picking, creating RCs, deploying, etc.).

* Trainers should allow trainees to do the work, but like a pilot of an
airplane they can take over when time becomes critical.

Here is the [upcoming and current list of release managers](/release-managers/).
