Also see [the GitLab Handbook on the Critical Release Process](https://about.gitlab.com/handbook/engineering/critical-release-process/)
for the timeline of handling a critical security release.
Only a subset of the security releases are critical.

# Security Releases

Security vulnerabilities in GitLab and its dependencies are to be addressed with
the highest priority.

Security releases are naturally very similar to [patch releases](patch.md), but
on a much shorter timeline. The goal is to make a security release available as
soon as possible, while ensuring that the security issue is properly addressed
and that the fix does not introduce regressions.

Depending on the severity and the attack surface of the vulnerability, an
immediate patch release consisting of just the security fix may be warranted.
For less severe issues, it may be acceptable to include the fix in a future
patch. This is one case where the release manager _does not_ have final say
concerning a release, and he or she should consult with the GitLab development
team as well as any applicable security experts, such as the person disclosing
the issue.

As noted in the [checklist](https://about.gitlab.com/handbook/engineering/critical-release-process/),
a specific "security release manager" is designated to act as the release
manager for security releases. By default, the security release manager is the
RM from the _previous_ release. Having one RM for the security release - even
though a security release will typically span multiple prior versions - is more
efficient and less likely to lead to confusion or unintended "leaking" of the
vulnerability. By designating the RM from the _previous_ release, the RM for the
_current_ release is not hindered in their work to get out the next release.

## What to include

A security release, even one for the latest monthly release, should _only_
include the changes necessary to resolve the security vulnerabilities. Including
fixes for regressions in a security patch increases the chances of breaking
something, both for users and for our packaging and release process.

The only exception to this policy is [release
candidates](release-candidates.md). If the monthly release process is in
progress as we're preparing for a security release, it's acceptable for a new RC
to include both security fixes and regression fixes. Care should be taken to
coordinate the publishing of an RC package with the other security patches so as
to not disclose the security vulnerabilities publicly before we're ready to
disclose them.

Be sure NOT to pre-announce which GitLab versions are affected, since that may
allow malicious users to narrow the search space.

## Process

### Before the release

When preparing a security release, the most important thing is to **always work
with the `dev` remote**:

- Merge requests that fix CE security issues should be submitted on
  https://dev.gitlab.org/gitlab/gitlabhq against the
  [`security-X-Y` branch](https://dev.gitlab.org/gitlab/gitlabhq/branches)

- Merge requests that fix EE security issues should be submitted on
  https://dev.gitlab.org/gitlab/gitlab-ee against the
  [`security-X-Y` branch](https://dev.gitlab.org/gitlab/gitlab-ee/branches)

If the latest GitLab release is 9.2, first create a merge request against the
`security-9-2` branch. If that branch does not yet exist, create it by branching
off of the latest stable release. In this case that would be `9-2-stable`.

### 1. Create an issue to track the security patch release

In order to keep track of the various tasks that need to happen before a security
patch release is considered "complete", we create an issue on the [GitLab CE issue
tracker] and update it as we progress.

1. Set up [API access for rake tasks](rake-tasks.md#setup)

1. Create the issue using the [`security_patch_issue`](rake-tasks.md#security_patch_issueversion)
   Rake task:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    bundle exec rake "security_patch_issue[version]"
    ```

### 2. Complete the security patch release tasks

Use the security patch issue created above to keep track of the process and
mark off tasks as you complete them.

### About the security branches

The `security` branches are "parallel" to the latest stable branches for each
release and ensure no one inadvertently exposes security fixes on GitLab.com,
since the `security-X-Y` -> `X-Y-stable` merge is a manual and conscious operation.

`X-Y-stable` can and should be merged frequently to `security-X-Y`, but `security-X-Y` can
only be merged once all the security fixes it contains are released as part of
official releases (and possibly backports).

### Backporting

Backports should be provided for at least the previous two monthly releases. Using
the example above that means that `9-1-security` and `9-0-security` should also
have merge requests. Each security release consists of at least three merge
requests.

For very serious security issues, there is
[precedent](https://about.gitlab.com/2016/05/02/cve-2016-4340-patches/)
to backport security fixes to even more monthly releases of GitLab. This will be
decided on a case-by-case basis.

If a security fix warrants backporting to previous releases, doing a single blog
post that mentions all of the patches at once is acceptable.

### Merging CE stable into EE stable

To merge CE into EE stable, you can either add
https://dev.gitlab.org/gitlab/gitlabhq.git as a new remote or fetch the remote
and reference it in the merge with `FETCH_HEAD`, and remember to **push to `dev`
only**:

```shell
$ git fetch git@dev.gitlab.org:gitlab/gitlabhq.git X-Y-stable
$ git merge --no-ff FETCH_HEAD X-Y-stable-ee
$ git push dev X-Y-stable-ee
```

**Note:** Please change `FETCH_HEAD` to `dev/X-Y-stable` in the commit message so it's
obvious what was the merge remotes & branches when viewing the history.

### About the blog post

Create the blog post merge request **only once all the EE and CE packages are built and
available on https://packages.gitlab.com/gitlab**.

Before that, you can share the draft either in a private snippet, a confidential
issue or by any other secure and private means.

The title of the blog post should be of the format "GitLab Security Release: x.y.z".

### Other communications about the Security Release

Per the [checklist](https://about.gitlab.com/handbook/engineering/critical-release-process/),
security releases need to be communicated about widely and loudly, using 
- Twitter: consider adopting guidelines from how frequently we tweet, and with what timing
from the [guidelines on Twitter use for deployments](https://gitlab.com/gitlab-org/takeoff/blob/master/doc/announce-a-deployment.md#twitter)
- Security Newsletter: this is only sent out after the blog post is published, 
and the marketing team needs to be involved in sending the newsletter.

### After the release

After the packages are built and announced on our blog, you **should not** merge
the `security-X-Y` branches to their `stable` counterparts but only cherry-pick the
security merge commits that are already part of a tagged (and announced) release
to `X-Y-stable` and sync `X-Y-stable` to all the remotes.

This is because new security fixes can be merged to `security-X-Y` between the time
you prepare a security release and the time you're done with it.

---

[Return to Guides](../README.md#guides)
