### First working day after 7th

Stable branch should be created after the 7th. The 7th is the last date to reliably get things in.

- [ ] In `#development`:

    ```
    @channel

    I am about to create the `<%= version.stable_branch %>` branch. Everything merged into `master`
    after this point will go into next month's release. Only regression and security fixes
    will be cherry-picked into `<%= version.stable_branch %>`.

    Please ensure that merge requests have the correct milestone (`<%= version.to_minor %>` for this release)
    and the `Pick into Stable` label.

    From now on, please follow the "After the 7th" process:
    https://gitlab.com/gitlab-org/gitlab-ce/blob/master/PROCESS.md#after-the-7th
    ```
- [ ] Create branch `<%= version.stable_branch %>` from CE `master` manually
- [ ] Create branch `<%= version.stable_branch(ee: true) %>` from EE `master` manually
- [ ] In Omnibus create both `<%= version.stable_branch %>` and `<%= version.stable_branch(ee: true) %>` from `master` manually
- [ ] Merge [GitLab CE into EE] on the stable branches
- [ ] Sync stable branches: CE, EE, and Omnibus to `dev`, CE and Omnibus to `github`
- [ ] Sync master branches to `dev` and `github`, as the CHANGELOG will be automatically updated on master during tagging
- [ ] If needed, sync tags for dependencies (`gitlab-shell`, `gitlab-workhorse`, `gitlab-pages`, `gitaly`) to `dev` and `github` (when applicable)

#### RC1

- [ ] Ensure `omnibus-gitlab` is ready to build packages by asking the Omnibus maintainers in Slack (`#build`)
- Follow the [Creating RC1] guide:
  - [ ] Create MR on CE master updating the "Installation from Source" guide, creating the "Update" guides
  - [ ] Create MR on EE master creating the "CE to EE" guides
  - [ ] Create MR on CE master updating the gitignore and license templates
  - [ ] Create MR on CE master updating the dependencies license list
  - [ ] Ensure above MRs are merged and marked `Pick into Stable` for milestone `<%= version.to_minor %>`
- [ ] Follow steps to create a release candidate
  - [ ] Create preperation MRs by following the [instructions in release-tools](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/picking-into-merge-requests.md).
  - [ ] Cherry-pick changes into preparation MRs following their instructions
  - [ ] Cherry-pick remaining merge requests labeled `Pick into Stable` for the current
  milestone using the
  [`Pick into Stable` <%= version.to_minor %> merged merge requests] page
  - [ ] Check the following list of critical issues/MRs which are to be included in `<%= version.to_patch %>`. Ensure each has made both CE and EE
    - [ ] REFERENCE_TO_MR_TO_PICK
  - [ ] Merge CE `<%= version.stable_branch %>` into EE `<%= version.stable_branch(ee: true) %>` following the [Merging a CE stable branch into its EE counterpart] guide
  - [ ] Sync stable branches: CE, EE, and Omnibus to `dev`, CE and Omnibus to `github`
  - [ ] Sync master branches to `dev` and `github`, as the CHANGELOG will be automatically updated on master during tagging
  - [ ] If needed, sync tags for dependencies (`gitlab-shell`, `gitlab-workhorse`, `gitlab-pages`, `gitaly`) to `dev` and `github` (when applicable)
  - [ ] Check for any problematic migrations in EE (EE migrations include CE ones), and paste the diff in a snippet: `git diff v<%= version.to_rc %>-ee..<%= version.stable_branch(ee: true) %> -- db/migrate db/post_migrate` =>
  - [ ] Ensure builds are green on [CE stable branch] and [EE stable branch]
  - [ ] Ensure builds are green on [Omnibus CE stable branch] and [Omnibus EE stable branch]
  - [ ] Make sure to [announce the deployment] on Twitter and GitLab.com
      * With downtime: 1 hour before
      * Without downtime: 15 minutes before
  - [ ] In `#releases`: I'm going to tag `<%= version.to_rc %>`
  - [ ] Tag the `<%= version.to_rc %>` version using the [`release` task]:

        ```sh
        # In the release-tools project:
        bundle exec rake "release[<%= version.to_rc %>]"
        ```
  - [ ] Check progress of [EE packages build] and [CE packages build]
  - [ ] In `#production`: I'm going to deploy `<%= version.to_rc %>` to staging
  - [ ] Do the [deploy] of [`<%= version.to_rc %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc %>.ee.0_amd64.deb) to [staging.gitlab.com]
        ```sh
        # In the takeoff project:
        bundle exec rake "deploy[staging, <%= version.to_rc %>.ee.0]"
        ```
  - [ ] If needed, in `#production`: I'm going to deploy `<%= version.to_rc %>` to canary
  - [ ] If needed, do the [deploy] of [`<%= version.to_rc %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc %>.ee.0_amd64.deb) to [canary.gitlab.com]
        ```sh
        # In the takeoff project:
        bundle exec rake "deploy[canary, <%= version.to_rc %>.ee.0]"
        ```
  - [ ] In `#production`: I'm going to deploy `<%= version.to_rc %>` to production
  - [ ] Publicly [announce the deploy on Twitter], at this point the deploy alert banner on GitLab.com should already be up.
  - [ ] Do the [deploy] of [`<%= version.to_rc %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc %>.ee.0_amd64.deb) to GitLab.com
        ```sh
        # In the takeoff project:
        bundle exec rake "deploy[production, <%= version.to_rc %>.ee.0]"
        ```
  - [ ] Take notes of the time it took for the migrations to complete on the deployment to production.
      ```
      # On the takeoff repo
      bundle exec rake "follow_migrations[production]"
      ```
  - [ ] From the [build pipeline], [manually publish public packages]
  - [ ] Verify that packages appear on `packages.gitlab.com`: [EE & CE](https://packages.gitlab.com/app/gitlab/unstable/search?q=<%= version.to_rc %>)
  - [ ] Verify that Docker images appear on `hub.docker.com`: [EE](https://hub.docker.com/r/gitlab/gitlab-ee/tags) / [CE](https://hub.docker.com/r/gitlab/gitlab-ce/tags)
  - [ ] Post a [tweet about] the `<%= version.to_rc %>` release:

        ```
        GitLab <%= version.to_rc %> is available: https://packages.gitlab.com/gitlab/unstable
        Use at your own risk. Please link regressions issues from
        LINK_TO_REGRESSION_ISSUE
        ```
- [ ] Create the [regression issue] in the CE issue tracker using the [`regression_issue` task] and bookmark it:

      ```sh
      # In the release-tools project:
      bundle exec rake "regression_issue[<%= version.to_patch %>]"
      ```

#### QA

- [ ] Determine QA person and notify this person: MENTION_THIS_PERSON_HERE
- [ ] Do QA and fix anything coming out of it: LINK_TO_QA_ISSUE

### Anytime after RC1 but before 22nd

- [ ] Update the [blog post] `barometer section` with the migration types for this release, including the time they took to complete.
- [ ] Create another RC as needed.

Keep in mind that:

1. After feature freeze only regression and security fixes can be
cherry-picked into `<%= version.stable_branch %>`.
2. Last RC should point to the same commit as the final release.

**Copy-paste the tasks below for any other RCs (be sure to update the RC number).**

```
#### RC2

- [ ] Create preperation MRs by following the [instructions in release-tools](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/picking-into-merge-requests.md).
- [ ] Cherry-pick changes into preparation MRs following their instructions
- [ ] Cherry-pick remaining merge requests labeled `Pick into Stable` for the current
milestone using the
[`Pick into Stable` <%= version.to_minor %> merged merge requests] page
- [ ] Check the following list of critical issues/MRs which are to be included in `<%= version.to_patch %>`. Ensure each has made both CE and EE
  - [ ] REFERENCE_TO_MR_TO_PICK
- Follow the [Creating subsequent RCs] guide for `<%= version.to_rc(2) %>`:
  - [ ] Merge CE `<%= version.stable_branch %>` into EE `<%= version.stable_branch(ee: true) %>` following the [Merging a CE stable branch into its EE counterpart] guide
  - [ ] Sync stable branches: CE, EE, and Omnibus to `dev`, CE and Omnibus to `github`
  - [ ] Sync master branches to `dev` and `github`, as the CHANGELOG will be automatically updated on master during tagging
  - [ ] If needed, sync tags for dependencies (`gitlab-shell`, `gitlab-workhorse`, `gitlab-pages`, `gitaly`) to `dev` and `github` (when applicable)
  - [ ] Check for any problematic migrations in EE (EE migrations include CE ones), and paste the diff in a snippet: `git diff v<%= version.to_rc %>-ee..<%= version.stable_branch(ee: true) %> -- db/migrate db/post_migrate` =>
  - [ ] Ensure builds are green on [CE stable branch] and [EE stable branch]
  - [ ] Ensure builds are green on [Omnibus CE stable branch] and [Omnibus EE stable branch]
  - [ ] Make sure to [announce the deployment] on Twitter and GitLab.com
      * With downtime: 1 hour before
      * Without downtime: 15 minutes before
  - [ ] In `#releases`: I'm going to tag `<%= version.to_rc(2) %>`
  - [ ] Tag the `<%= version.to_rc(2) %>` version using the [`release` task]:

        ```sh
        # In the release-tools project:
        bundle exec rake "release[<%= version.to_rc(2) %>]"
        ```
- [ ] Check progress of [EE packages build] and [CE packages build]
- [ ] In `#production`: I'm going to deploy `<%= version.to_rc(2) %>` to staging
- [ ] On video call, [deploy] release [`<%= version.to_rc(2) %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc(2) %>.ee.0_amd64.deb) to [staging.gitlab.com]
      ```sh
      # In the takeoff project:
      bundle exec rake "deploy[staging, <%= version.to_rc(2) %>.ee.0]"
      ```
- [ ] If needed, in `#production`: I'm going to deploy `<%= version.to_rc(2) %>` to canary
- [ ] If needed, [deploy] release [`<%= version.to_rc(2) %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc(2) %>.ee.0_amd64.deb) to [canary.gitlab.com]
      ```sh
      # In the takeoff project:
      bundle exec rake "deploy[canary, <%= version.to_rc(2) %>.ee.0]"
      ```
- [ ] In `#production`: I'm going to deploy `<%= version.to_rc(2) %>` to production
- [ ] On video call, [deploy] release [`<%= version.to_rc(2) %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc(2) %>.ee.0_amd64.deb) to GitLab.com
      ```sh
      # In the takeoff project:
      bundle exec rake "deploy[production, <%= version.to_rc(2) %>.ee.0]"
      ```
- [ ] Take notes of the time it took for the migrations to complete on the deployment to production.
      ```
      # On the takeoff repo
      bundle exec rake "follow_migrations[production]"
      ```
- [ ] Publicly [announce the deploy on Twitter], at this point the deploy alert banner on GitLab.com should already be up.
- [ ] From the [build pipeline], [manually publish public packages]
- [ ] Verify that packages appear on `packages.gitlab.com`: [EE & CE](https://packages.gitlab.com/app/gitlab/unstable/search?q=<%= version.to_rc(2) %>)
- [ ] Verify that Docker images appear on `hub.docker.com`: [EE](https://hub.docker.com/r/gitlab/gitlab-ee/tags) / [CE](https://hub.docker.com/r/gitlab/gitlab-ce/tags)
- [ ] Post a [tweet about] the `<%= version.to_rc(2) %>` release:

      ```
      GitLab <%= version.to_rc(2) %> is available: https://packages.gitlab.com/gitlab/unstable
      Use at your own risk. Please link regressions issues from
      LINK_TO_REGRESSION_ISSUE
      ```
```

### 21st final RC

- Before 13:00 UTC:
  - Final RC is ready for tagging. Including changes at this stage requires signoff from VP of Eng.
    - [ ] Ensure tests are green on [CE stable branch]
    - [ ] Ensure tests are green on [EE stable branch]
    - [ ] Ensure tests are green on [Omnibus CE stable branch]
    - [ ] Ensure tests are green on [Omnibus EE stable branch]
    - [ ] In `#releases`: I'm going to tag final RC release
    - [ ] Replace XX in the tasks below with the RC version number:
    - [ ] Tag the final RC version using the [`release` task],

          ```sh
          # In the release-tools project:
          bundle exec rake "release[<%= version.to_rc(21) %>]"
          ```
    - [ ] Check progress of [EE packages build] and [CE packages build]
    - [ ] In `#production`: I'm going to deploy `<%= version.to_rc(21) %>` to staging
    - [ ] On video call, [deploy] release [`<%= version.to_rc(21) %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc(21) %>.ee.0_amd64.deb) to [staging.gitlab.com]
        ```sh
        # In the takeoff project:
        bundle exec rake "deploy[staging, <%= version.to_rc(21) %>.ee.0]"
        ```
    - [ ] If needed, in `#production`: I'm going to deploy `<%= version.to_rc(21) %>` to canary
    - [ ] If needed, [deploy] release [`<%= version.to_rc(21) %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc(21) %>.ee.0_amd64.deb) to [canary.gitlab.com]
        ```sh
        # In the takeoff project:
        bundle exec rake "deploy[canary, <%= version.to_rc(21) %>.ee.0]"
        ```
    - [ ] In `#production`: I'm going to deploy `<%= version.to_rc(21) %>` to production
    - [ ] On video call, [deploy] release [`<%= version.to_rc(21) %>`](https://packages.gitlab.com/gitlab/unstable/packages/ubuntu/xenial/gitlab-ee_<%= version.to_rc(21) %>.ee.0_amd64.deb) to GitLab.com
        ```sh
        # In the takeoff project:
        bundle exec rake "deploy[production, <%= version.to_rc(21) %>.ee.0]"
        ```
    - [ ] Publicly [announce the deploy on Twitter], at this point the deploy alert banner on GitLab.com should already be up.
    - [ ] From the [build pipeline], [manually publish public packages]
    - [ ] Verify that packages appear on `packages.gitlab.com`: [EE & CE](https://packages.gitlab.com/app/gitlab/unstable/search?q=<%= version.to_rc(21) %>)
    - [ ] Verify that Docker images appear on `hub.docker.com`: [EE](https://hub.docker.com/r/gitlab/gitlab-ee/tags) / [CE](https://hub.docker.com/r/gitlab/gitlab-ce/tags)
    - [ ] Post a [tweet about] the `<%= version.to_rc(21) %>` release:

        ```
        GitLab <%= version.to_rc(21) %> is available: https://packages.gitlab.com/gitlab/unstable
        Use at your own risk. Please link regressions issues from
        LINK_TO_REGRESSION_ISSUE
        ```

- At 15:00 UTC:
  - [ ] If the final RC is not tagged and deployed by this time, notify the [Build Lead](doc/monthly.md#getting-help)

- At 20:00 UTC:
  - [ ] If the final RC is not tagged and deployed by this time, notify the [VP of Engineering](doc/monthly.md#getting-help)

### 22nd, the release day:

No new code is added to release that was not included in the last RC.
This way we ensure the release does not introduce new regressions.

- At 8:00 UTC, final release is ready for tagging (Including changes at this stage requires signoff from VP of Eng.):
  - [ ] Sync stable branches: CE, EE, and Omnibus to `dev`, CE and Omnibus to `github`
  - [ ] Sync master branches to `dev` and `github`, as the CHANGELOG will be automatically updated on master during tagging
  - [ ] If needed, sync tags for dependencies (`gitlab-shell`, `gitlab-workhorse`, `gitlab-pages`, `gitaly`) to `dev` and `github` (when applicable)
  - [ ] Ensure tests are green on [CE stable branch]
  - [ ] Ensure tests are green on [EE stable branch]
  - [ ] Ensure tests are green on [Omnibus CE stable branch]
  - [ ] Ensure tests are green on [Omnibus EE stable branch]
  - [ ] If at this time final release is not ready for tagging, notify the [CTO](doc/monthly.md#getting-help)

- Before 10:00 UTC:
  - [ ] In `#releases`: I'm going to tag `<%= version.to_patch %>`
  - [ ] Tag the `<%= version.to_patch %>` version using the [`release` task]:

        ```sh
        # In the release-tools project:
        bundle exec rake "release[<%= version.to_patch %>]"
        ```
  - [ ] Check progress of [EE packages build] and [CE packages build]

- Before 12:00 UTC:
  - [ ] In `#production`: I'm going to deploy `<%= version.to_patch %>` to staging
  - [ ] Do the [deploy] of [`<%= version.to_patch %>`](https://packages.gitlab.com/gitlab/gitlab-ee/packages/ubuntu/xenial/gitlab-ee_<%= version.to_patch %>-ee.0_amd64.deb) to [staging.gitlab.com]
  - [ ] In `#production`: I'm going to deploy `<%= version.to_patch %>` to production
  - [ ] Publicly [announce the deploy on Twitter], at this point the deploy alert banner on GitLab.com should already be up.
  - [ ] Do the [deploy] of [`<%= version.to_patch %>`](https://packages.gitlab.com/gitlab/gitlab-ee/packages/ubuntu/xenial/gitlab-ee_<%= version.to_patch %>-ee.0_amd64.deb) to GitLab.com
  - [ ] Create the first patch issue using the [`patch_issue` task]:

      ```sh
      # In the release-tools project:
      bundle exec rake "patch_issue[<%= version.next_patch %>]"
      ```
  - [ ] If at this point final release is not ready for public, notify the [CEO](https://about.gitlab.com/team/#sytses)

- At 15:00 UTC:
  - [ ] From the [build pipeline], [manually publish public packages]
  - [ ] Verify that packages appear on `packages.gitlab.com`: [EE](https://packages.gitlab.com/app/gitlab/gitlab-ee/search?q=<%= version.to_patch %>) / [CE](https://packages.gitlab.com/app/gitlab/gitlab-ce/search?q=<%= version.to_patch %>)
  - [ ] Verify that Docker images appear on `hub.docker.com`: [EE](https://hub.docker.com/r/gitlab/gitlab-ee/tags) / [CE](https://hub.docker.com/r/gitlab/gitlab-ce/tags)
  - [ ] Create the `<%= version.to_patch %>` version on https://version.gitlab.com
  - [ ] Ensure someone tweets about the `<%= version.to_patch %>` release

[regression issue]: LINK_TO_REGRESSION_ISSUE

[Creating RC1]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/release-candidates.md#creating-rc1
[CE stable branch]: https://dev.gitlab.org/gitlab/gitlabhq/commits/<%= version.stable_branch %>
[EE stable branch]: https://dev.gitlab.org/gitlab/gitlab-ee/commits/<%= version.stable_branch(ee: true) %>
[Omnibus CE stable branch]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch %>
[Omnibus EE stable branch]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch(ee: true) %>
[announce the deployment]: https://gitlab.com/gitlab-org/takeoff/blob/master/doc/announce-a-deployment.md
[CE packages build]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch %>
[EE packages build]: https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/<%= version.stable_branch(ee: true) %>
[tweet about]: https://gitlab.com/gitlab-org/takeoff#announce-that-the-deploy-is-done
[announce the deploy on Twitter]: https://gitlab.com/gitlab-org/takeoff#announce-the-deployment
[`gitlab/unstable`]: https://packages.gitlab.com/gitlab/unstable
[`gitlab/gitlab-ee`]: https://packages.gitlab.com/gitlab/gitlab-ee
[`gitlab/gitlab-ce`]: https://packages.gitlab.com/gitlab/gitlab-ce
[Sync CE, EE, and Omnibus to `dev`]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/pro-tips.md#add-a-git-pdo-and-a-git-pdog-aliases
[Creating subsequent RCs]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/release-candidates.md#creating-subsequent-rcs
[GitLab CE into EE]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/merge-ce-into-ee.md#merging-ce-master-into-ee-master
[Merging a CE stable branch into its EE counterpart]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/merge-ce-into-ee.md#merging-a-ce-stable-branch-into-its-ee-counterpart
[`Pick into Stable`]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#changes-for-stable-releases
[`release` task]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc%2Frake-tasks.md#releaseversion
[`patch_issue` task]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc%2Frake-tasks.md#patch_issueversion
[`regression_issue` task]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc%2Frake-tasks.md#regression_issueversion
[`Pick into Stable` <%= version.to_minor %> merged merge requests]: https://gitlab.com/groups/gitlab-org/merge_requests?label_name%5B%5D=Pick+into+Stable&milestone_title=<%= version.milestone_name %>&scope=all&sort=id_desc&state=merged
[deploy]: https://gitlab.com/gitlab-org/takeoff#deploying-gitlab
[staging.gitlab.com]: https://staging.gitlab.com/
[canary.gitlab.com]: https://canary.gitlab.com/
[manually publish public packages]: https://gitlab.com/gitlab-org/release-tools/blob/master/doc/publishing-packages.md
[build pipeline]: https://dev.gitlab.org/gitlab/omnibus-gitlab/pipelines?scope=tags
