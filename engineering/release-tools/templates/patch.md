- [ ] Create preparation MRs by following the [instructions in release-tools](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/picking-into-merge-requests.md).
- [ ] Cherry-pick changes into preparation MRs following their instructions
- [ ] Cherry-pick remaining merge requests labeled `Pick into Stable` for the current
  milestone using the
  [`Pick into Stable` <%= version.to_minor %> merged merge requests] page
- [ ] Check for merge requests marked [`Pick into Backports`] and cherry-pick those which should go into this release.
- [ ] Check the following list of critical issues/MRs which are to be included in `<%= version.to_patch %>`. Where appropriate, ensure each has made it into both CE and EE
  - [ ] REFERENCE_TO_MR_TO_PICK
- [ ] Merge CE `<%= version.stable_branch %>` into EE `<%= version.stable_branch(ee: true) %>` following the [Merging a CE stable branch into its EE counterpart] guide
- [ ] Sync stable branches: CE, EE, and Omnibus to `dev`, CE and Omnibus to `github`
- [ ] Sync master branches to `dev` and `github`, as the CHANGELOG will be automatically updated on master during tagging
- [ ] If needed, sync tags for dependencies (`gitlab-shell`, `gitlab-workhorse`, `gitlab-pages`, `gitaly`) to `dev` and `github` (when applicable)
- [ ] Check for any problematic migrations in EE (EE migrations include CE ones), and paste the diff in a snippet: `git diff <%= version.previous_tag(ee: true) %>..<%= version.stable_branch(ee: true) %> -- db/migrate db/post_migrate` =>
- [ ] Check [`omnibus-gitlab/<%= version.stable_branch %>` CHANGELOG.md][omnibus-stable-changelog]
- [ ] Check [`omnibus-gitlab/<%= version.stable_branch(ee: true) %>` CHANGELOG.md][omnibus-stable-ee-changelog]
- [ ] While waiting for tests to be green, now is a good time to start on the blog post: BLOG_POST_MR
- [ ] Ensure builds are green on [CE stable branch] and [EE stable branch]
- [ ] Ensure builds are green on [Omnibus CE stable branch] and [Omnibus EE stable branch]
- [ ] In `#releases`: I'm going to tag `<%= version.to_patch %>`
- [ ] Tag the `<%= version.to_patch %>` version using the [`release` task]:

      ```sh
      # In the release-tools project:
      bundle exec rake "release[<%= version.to_patch %>]"
      ```
- [ ] Check progress of [EE packages build] and [CE packages build]
- [ ] In `#production`: I'm going to deploy `<%= version.to_patch %>` to staging
- [ ] On video call, [deploy] release [`<%= version %>`](https://packages.gitlab.com/gitlab/gitlab-ee/packages/ubuntu/xenial/gitlab-ee_<%= version %>-ee.0_amd64.deb) to [staging.gitlab.com]
      ```sh
      # In the takeoff project:
      bundle exec rake "deploy[staging, <%= version.to_patch %>-ee.0]"
      ```
- [ ] In `#production`: I'm going to deploy `<%= version.to_patch %>` to canary
- [ ] On video call, [deploy] release [`<%= version %>`](https://packages.gitlab.com/gitlab/gitlab-ee/packages/ubuntu/xenial/gitlab-ee_<%= version %>-ee.0_amd64.deb) to [canary.gitlab.com]
      ```sh
      # In the takeoff project:
      bundle exec rake "deploy[canary, <%= version.to_patch %>-ee.0]"
      ```
- [ ] In `#production`: I'm going to deploy `<%= version.to_patch %>` to production
- [ ] Make sure to [announce the deploy] on Twitter and GitLab.com
  * With downtime: 1 hour before
  * Without downtime: 15 minutes before
- [ ] On video call, [deploy] release [`<%= version %>`](https://packages.gitlab.com/gitlab/gitlab-ee/packages/ubuntu/xenial/gitlab-ee_<%= version %>-ee.0_amd64.deb) to GitLab.com
      ```sh
      # In the takeoff project:
      bundle exec rake "deploy[production, <%= version.to_patch %>-ee.0]"
      ```
- [ ] From the [build pipeline], [manually publish public packages]
- [ ] Verify that packages appear on `packages.gitlab.com`: [EE](https://packages.gitlab.com/app/gitlab/gitlab-ee/search?q=<%= version.to_patch %>) / [CE](https://packages.gitlab.com/app/gitlab/gitlab-ce/search?q=<%= version.to_patch %>)
- [ ] Verify that Docker images appear on `hub.docker.com`: [EE](https://hub.docker.com/r/gitlab/gitlab-ee/tags) / [CE](https://hub.docker.com/r/gitlab/gitlab-ce/tags)
- [ ] Create the `<%= version %>` version on https://version.gitlab.com
- [ ] Deploy the blog post
- [ ] Tweet (prepare the Tweet text below or paste the tweet URL instead):

      ```
      GitLab <%= version %> is released! BLOG_POST_URL DESCRIPTION OF THE CHANGES
      ```
- In the [<%= regression_issue.title %>](<%= regression_issue.url %>) issue:
  - [ ] Add the following notice:

      ```
      `<%= version %>` has been tagged, further fixes will go into `<%= version.next_patch %>` as necessary.
      ```
  - [ ] Remove notes for the regressions fixed by version `<%= version %>`
- [ ] Add [`omnibus-gitlab/<%= omnibus_version.tag %>` CHANGELOG.md][omnibus-tag-changelog] items to [`omnibus-gitlab/master` CHANGELOG.md][omnibus-master-changelog]

---

For references:
- https://dev.gitlab.org/gitlab/gitlab-ee/commits/<%= version.stable_branch(ee: true) %>
- https://dev.gitlab.org/gitlab/gitlabhq/commits/<%= version.stable_branch %>
- https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch(ee: true) %>
- https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch %>

[`Pick into Stable` <%= version.to_minor %> merged merge requests]: https://gitlab.com/groups/gitlab-org/merge_requests?label_name%5B%5D=Pick+into+Stable&milestone_title=<%= version.milestone_name %>&scope=all&sort=id_desc&state=merged
[`Pick into Backports`]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests?label_name%5B%5D=Pick+into+Backports&scope=all&sort=updated_asc&state=merged
[Merging a CE stable branch into its EE counterpart]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/merge-ce-into-ee.md#merging-a-ce-stable-branch-into-its-ee-counterpart

[omnibus-stable-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/<%= version.stable_branch %>/CHANGELOG.md
[omnibus-stable-ee-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/<%= version.stable_branch(ee: true) %>/CHANGELOG.md

[CE stable branch]: https://dev.gitlab.org/gitlab/gitlabhq/commits/<%= version.stable_branch %>
[EE stable branch]: https://dev.gitlab.org/gitlab/gitlab-ee/commits/<%= version.stable_branch(ee: true) %>
[Omnibus CE stable branch]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch %>
[Omnibus EE stable branch]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch(ee: true) %>
[CE packages build]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch %>
[EE packages build]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch(ee: true) %>

[omnibus-tag-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/<%= omnibus_version.tag %>/CHANGELOG.md
[omnibus-master-changelog]: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/CHANGELOG.md

[`release` task]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc%2Frake-tasks.md#releaseversion

[deploy]: https://gitlab.com/gitlab-org/takeoff#deploying-gitlab
[staging.gitlab.com]: https://staging.gitlab.com/
[canary.gitlab.com]: https://canary.gitlab.com/

[announce the deploy]: https://gitlab.com/gitlab-org/takeoff#announce-the-deployment

[manually publish public packages]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/publishing-packages.md
[build pipeline]: https://dev.gitlab.org/gitlab/omnibus-gitlab/pipelines?scope=tags
