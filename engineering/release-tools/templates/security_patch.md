**Be sure to follow the [Security Releases guide](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/security.md).**

- Picked into respective `stable` branches from the `dev/security` branch. [`Pick into Stable` <%= version.to_minor %> merged merge requests]:
  - [ ] REFERENCE_TO_MR_TO_PICK
- [ ] **Push `ce/<%= version.stable_branch %>` to `dev` only: `git push dev <%= version.stable_branch %>`**
- [ ] **Push `ee/<%= version.stable_branch(ee: true) %>` to `dev` only: `git push dev <%= version.stable_branch(ee: true) %>`**
- [ ] Merge `ce/<%= version.stable_branch %>` into `ee/<%= version.stable_branch(ee: true) %>` following [the security process]
- [ ] Check [`omnibus-gitlab/<%= version.stable_branch %>` CHANGELOG.md][omnibus-stable-changelog]
- [ ] Check [`omnibus-gitlab/<%= version.stable_branch(ee: true) %>` CHANGELOG.md][omnibus-stable-ee-changelog]
- [ ] **Push `omnibus-gitlab/<%= version.stable_branch %>` to `dev` only: `git push dev <%= version.stable_branch %>`**
- [ ] **Push `omnibus-gitlab/<%= version.stable_branch(ee: true) %>` to `dev` only: `git push dev <%= version.stable_branch(ee: true) %>`**
- [ ] While waiting for tests to be green, now is a good time to start on [the blog post], **in a private snippet**: BLOG_POST_SNIPPET
  - [ ] Ensure the blog post discloses as much information about the vulnerability as is responsibly possible. We aim for clarity and transparency, and try to avoid secrecy and ambiguity.
  - [ ] If the vulnerability was responsibly disclosed to us by a security researcher, ensure they're [publicly acknowledged] and thank them again privately as well.
- [ ] Ensure [tests are green on CE]
- [ ] Ensure [tests are green on EE]
- [ ] Check for any problematic migrations in EE (EE migrations include CE ones), and paste the diff in a snippet: `git diff <%= version.previous_tag(ee: true) %>..<%= version.stable_branch(ee: true) %> -- db/migrate` =>
- [ ] Tag the `<%= version.to_patch %>` version using the [`release` task]:

      ```sh
      SECURITY=true bundle exec rake "release[<%= version.to_patch %>]"
      ```
- [ ] Check that [EE packages are built], [CE packages are built] and appears on `packages.gitlab.com`: [EE](https://packages.gitlab.com/app/gitlab/gitlab-ee/search?q=<%= version.to_patch %>) / [CE](https://packages.gitlab.com/app/gitlab/gitlab-ce/search?q=<%= version.to_patch %>)
- [ ] In `#production`:

      ```
      I'm going to deploy `<%= version %>` to staging
      ```
- [ ] Deploy [`<%= version %>`](https://packages.gitlab.com/gitlab/gitlab-ee/packages/ubuntu/xenial/gitlab-ee_<%= version %>-ee.0_amd64.deb) to [staging.gitlab.com]
- [ ] In `#production`:

      ```
      I'm going to deploy `<%= version %>` to production
      ```
- [ ] Deploy [`<%= version %>`](https://packages.gitlab.com/gitlab/gitlab-ee/packages/ubuntu/xenial/gitlab-ee_<%= version %>-ee.0_amd64.deb) to [GitLab.com]
- [ ] Manually [publish the packages], one tag at a time to prevent 504 errors on our packages server.
- [ ] Create the `<%= version %>` version on https://version.gitlab.com
- [ ] Mark any applicable previous releases as vulnerable on https://version.gitlab.com.
- [ ] Check any sensitive information from the confidential security issues, and redact them if needed
- [ ] Create the blog post merge request
- [ ] Deploy the blog post
- [ ] Push `ce/<%= version.stable_branch %>` to all remotes
- [ ] Push `ee/<%= version.stable_branch(ee: true) %>` to all remotes
- [ ] Push tags to all remotes
- [ ] Make the confidential security issues public
- [ ] Tweet (prepare the Tweet text below or paste the tweet URL instead):

      ```
      GitLab <%= version %> is released! BLOG_POST_URL DESCRIPTION OF THE CHANGES
      ```
- [ ] Coordinate with the Marketing team to send out a security newsletter
- In the [<%= regression_issue.title %>](<%= regression_issue.url %>) issue:
  - [ ] Add the following notice:

      ```
      `<%= version %>` has been tagged, further fixes will go into `<%= version.next_patch %>` as necessary.
      ```
  - [ ] Remove notes for the regressions fixed by version `<%= version %>`
- [ ] Cherry-pick the merges from the `security` branch into `master` and push to all remotes.
- [ ] Add [`omnibus-gitlab/<%= omnibus_version.tag %>` CHANGELOG.md][omnibus-tag-changelog] items to [`omnibus-gitlab/master` CHANGELOG.md][omnibus-master-changelog]

---

For references:
- https://dev.gitlab.org/gitlab/gitlab-ee/commits/<%= version.stable_branch(ee: true) %>
- https://dev.gitlab.org/gitlab/gitlabhq/commits/<%= version.stable_branch %>
- https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch(ee: true) %>
- https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch %>

[`Pick into Stable` <%= version.to_minor %> merged merge requests]: https://gitlab.com/groups/gitlab-org/merge_requests?label_name%5B%5D=Pick+into+Stable&milestone_title=<%= version.milestone_name %>&scope=all&sort=id_desc&state=merged

[omnibus-stable-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/<%= version.stable_branch %>/CHANGELOG.md
[omnibus-stable-ee-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/<%= version.stable_branch(ee: true) %>/CHANGELOG.md

[tests are green on CE]: https://dev.gitlab.org/gitlab/gitlabhq/commits/<%= version.stable_branch %>
[tests are green on EE]: https://dev.gitlab.org/gitlab/gitlab-ee/commits/<%= version.stable_branch(ee: true) %>
[EE packages are built]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/8-10-stable-ee
[CE packages are built]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/8-10-stable

[omnibus-tag-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/<%= omnibus_version.tag %>/CHANGELOG.md
[omnibus-master-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/CHANGELOG.md

[EE packages are built]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch(ee: true) %>
[CE packages are built]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch %>

[`gitlab/gitlab-ee`]: https://packages.gitlab.com/gitlab/gitlab-ee
[`gitlab/gitlab-ce`]: https://packages.gitlab.com/gitlab/gitlab-ce

[`release` task]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc%2Frake-tasks.md#releaseversion
[`patch_issue` task]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc%2Frake-tasks.md#patch_issueversion

[staging.gitlab.com]: https://gitlab.com/gitlab-org/takeoff#deploying-gitlab
[GitLab.com]: https://gitlab.com/gitlab-org/takeoff#deploying-gitlab

[publicly acknowledged]: https://about.gitlab.com/vulnerability-acknowledgements/
[the blog post]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/security.md#about-the-blog-post
[the security process]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/security.md#merging-ce-stable-into-ee-stable

[publish the packages]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/publishing-packages.md
