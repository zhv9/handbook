# Release Manager

The release manager oversees the [monthly release] of GitLab as well as any
[patch releases] for that version.

## Onboarding
### Master checklist for onboarding of new release managers

The following checklist can be copied and pasted into a [new issue in the Organization project](https://gitlab.com/gitlab-com/organization/issues/new?issue[title]=Onboarding%20Release%20Manager%20[your%20name%20here])
to make sure the new release manager has the tools and some initial knowledge ready.
The topics are ordered by priority and should be tackled by the new release manager
before starting the appointed release.

```
### On-Boarding

- [ ] Make a note of your `dev` and `github` usernames and add them to this issue.
- [ ] Use the [release manager infrastructure permissions template](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/release-manager.md#infrastructure-permissions-template) to request chef and SSH access: [link to infrastructure issue]
- [ ] Make sure you have the [takeoff](https://gitlab.com/gitlab-org/takeoff) and [release-tools](https://gitlab.com/gitlab-org/release-tools) cloned locally, with all dependencies installed through [bundle](http://bundler.io/).
- [ ] If your ssh key has a passphrase, you will want to do `ssh-add` in your local takeoff repo
- [ ] Read through the [release guides](https://gitlab.com/gitlab-org/release-tools/blob/master/README.md#guides)
- [ ] Join #releases on Slack, and introduce yourself
- [ ] Master access on gitlab-ce  (dev and com)
- [ ] Master access on gitlab-ee (dev and com)
- [ ] Master access on gitlab-omnibus (dev and com)
- [ ] Get added to the [Release Managers team](https://github.com/orgs/gitlabhq/teams/release-managers) on GitHub.
- [ ] Make sure you have VPN access (follow instructions from [creating client certificate](https://gitlab.com/gitlab-cookbooks/gitlab_openvpn#how-to-create-a-client-certificate)
      up to and including google authenticator setup), and test by bringing VPN up and sshing into staging sidekiq node (`sidekiq-asap01.sv.stg.gitlab.com`)

### First Tasks

- [ ] Read the deploy docs: https://gitlab.com/gitlab-org/takeoff#deploying-gitlab
- [ ] Be involved in the merge/pick to stable for at least one RC/Patch
- [ ] Perform the ce-to-ee merge at least once for a RC/Patch
- [ ] Tag the release for at least one RC/patch
- [ ] Join a staging deploy call
- [ ] Join a gitlab.com deploy call
- [ ] Deploy to staging at least once
- [ ] Deploy to gitlab.com at least once

### Last task (after the release)

- [ ] Ensure the next RM trainee has an onboarding issue like this one, using [the onboarding template](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/release-manager.md#master-checklist-for-onboarding-of-new-release-managers).


### Usernames

| | Username |
|-|-------------------|
| Gitlab.com |  |
| dev |  |
| github |  |


```

### Infrastructure permissions template

Use this template when creating your [new infrastructure permissions issue](https://gitlab.com/gitlab-com/infrastructure/issues/new?issue[title]=Chef%20and%20SSH%20access%20request%20for%20YOUR%20NAME)

Make sure to set the issue to **confidential** and include your SSH username and public key

```
## What
- [ ] Master access to chef repo until end of Release Manager duties including patch releases
- [ ] Access to chef-server
- [ ] SSH access for release manager
- [ ] Added to the `release-manager` group in Cog in `#production` so you can tweet and broadcast messages.
  - A Cog admin in `#production` can run `!group-member-add release-manager <your handle>`, or you could be [manually added to Marvin](https://gitlab.com/gitlab-com/runbooks/blob/master/howto/manage-cog.md#add-a-user)

## Why

I'll be a trainee release manager in TRAINEE_RELEASE and release manager in RELEASE_YOU_WILL_MANAGE.

Onboarding task: LINK_TO_ONBOARING_ISSUE

## SSH Details

### Username

\```
YOUR_SSH_USER_NAME
\```

### Public Key

\```
YOUR_PUBLIC_KEY
\```

```


## Responsibilities

### Pre-release

The release manager's job begins with creating and tracking the [release
issue](monthly.md#1-create-an-issue-to-track-the-release).

Any task can be delegated to any member of the team who can perform it. When
delegating a task, be sure to mention a person directly rather than asking
something indirect like "Can someone help me do QA?". If someone is unavailable
to perform a task, ask someone else, or ask Job or a previous release manager to
find someone. The monthly releases are a company-wide effort, and should not
fall entirely on the release manager's shoulders.

Once the [regressions issue is created](rake-tasks.md#regression_issueversion),
the release manager is responsible for tracking and managing it. This usually
involves checking the reported issues and any available fixes for those issues,
and ensuring they are included either in the next release candidate or the final
release.

### Training

Release managers have the responsibility to deliver appropriate training to
the release manager trainees appointed to the same release.

They'll need to make sure that trainees already have an [onboarding checklist](#master-checklist-for-onboarding-of-new-release-managers)
early on the release process, as well as giving them the opportunity to tackle
most of the release tasks during the release, at least once.

### Release

After performing all of his or her pre-release tasks, and releasing the final
version of the monthly release, the release manager gets to relax, sometimes for
as long as **six hours**!

But no release is ever perfect, and the bug reports will start to come in as
users update to the latest version. That's where patch releases come in.

### Post-release

The amount and scheduling of [patch releases] is entirely at the discretion of
the release manager (with the exception of [security releases], which should be
addressed immediately).

If a bug affects a large number of users and/or a critical piece of
functionality, it's fine to release a patch with only one fix. Sometimes a patch
will include five or more minor fixes. The release manager should use his or her
best judgement to determine when a patch release is warranted. We strive to
continue releasing patches until all known regressions for that release are
addressed.

### Deployment

With the help of the infrastructure team, the release manager is also
responsible for deploying the latest version to GitLab.com. During the merge
window, the release manager needs to pay particular attention to migrations that
may block the deploy. For example, migrations that take a long time (e.g.,
adding a column with a default value to the issues table) should be reviewed
carefully.

When the release packages are ready, the release manager should begin the
[deployment procedure].

## Further Reading

- ["Release Manager - The invisible hero"](https://about.gitlab.com/2015/06/25/release-manager-the-invisible-hero/) (2015-06-25)
- ["How we managed 49 monthly releases"](https://about.gitlab.com/2015/12/17/gitlab-release-process/) (2015-12-17)

[deployment procedure]: https://gitlab.com/gitlab-org/takeoff#deploying-gitlab
[monthly release]: monthly.md
[patch releases]: patch.md
[security releases]: security.md

---

[Return to Guides](../README.md#guides)
