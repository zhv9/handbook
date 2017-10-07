# Creating Release Candidates

Release Candidates (RCs) are pre-release versions of the next major version of
GitLab CE and EE. The first RC, appropriately called RC1, is typically created
on the 8th. This is because we have a feature freeze, and new features can only
be merged into the release up through the 7th.

Every release will have several RCs, and there is no limit on the final number.
Usually, at least four RCs are made before the official release. This ensures
new changes are tried in production, at scale, and new bugs can be fixed before
the official release.

Usually RC1 has the most number of migrations that should be deployed into
production as soon as possible. Release managers should prioritize getting RC1
deployed. If there are showstopping issues with RC1 (e.g. failed migrations,
critical bugs that prevent logins, etc.), a new RC2 should be created
that contains the **minimal set of changes** needed to deploy the
package. Avoid picking more patches that may slow down the release, especially
those that contain new migrations.

## About the "Release Candidate" naming

We call them "Release Candidates" even though the early RCs are closer to Beta
than real RC. This simplifies our releasing/packaging tools and scripts. This
approach is coherent with packages.gitlab.com since our RC packages are
available under [`gitlab/unstable`].

## Guides

- [Creating RC1](#creating-rc1)
- [Creating subsequent RCs](#creating-subsequent-rcs)

### Creating RC1

#### Step 1: Update the "Installation from Source" guide

> **Note:** This only needs to be done for the GitLab CE repository. Changes
will be merged into GitLab EE.

1. Update the name of the `stable` branch in **Clone the Source**.
   There are two occurrences.
1. Depending on changes in the upcoming release, you may need to add or remove
   sections. For example, in GitLab 8.0 we had to add the section about
   installing `gitlab-workhorse` (called `gitlab-git-http-server` at the time).

#### Step 2: Create the "Update" guides

Each major release of GitLab needs a corresponding [update guide](https://gitlab.com/gitlab-org/gitlab-ce/tree/master/doc/update)
with instructions on how to manually upgrade from the previous major release.

> **Note:** GitLab CE and EE each have specific guides that need to be created.
Make sure to do both!

> **Note:** For the examples below, we're going to be using GitLab 8.2 as an
example of the upcoming release, and 8.1 as an example of the previous release.

##### GitLab CE

1. Copy the previous update guide to use as a template:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    cp doc/update/8.0-to-8.1.md doc/update/8.1-to-8.2.md
    ```

1. Update the versions in the top-level header.
1. Update the name of the latest `X-Y-stable[-ee]` branch **Get latest code**.
   There are two occurrences.
1. Update the names of the `X-Y-stable` branches in **Update configuration
   files**.
1. Update references to the "previous version" in **Things went south?** and the
   link to the previous guide.
1. Add any special instructions specific to this version. For example, maybe
   this version adds a new external dependency not in the previous version.
1. Read through the entire guide to make sure it makes sense. For example, maybe
   the previous version required special steps that no longer apply this
   version.

##### GitLab EE

GitLab EE releases include guides to migrate from the CE version of a major
release to the EE version of the same release.

1. Copy the previous update guide to use as a template:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    cp doc/update/8.1-ce-to-ee.md doc/update/8.2-ce-to-ee.md
    ```

1. Update the version numbers in the top-level header and introduction. There
   are three occurrences.
1. Update the name of the `stable` branch in **Get the EE code**.
1. Update the version number in **Things went south?** and the name of the
   `stable` branch in **Revert the code to the previous version**.

#### Step 3: Update the gitignore and license templates

Run `bin/rake gitlab:update_templates` and open a merge request to `master`.

#### Step 4: Update the dependencies license list

Run `bin/bundle exec license_finder report --format=csv --save=vendor/licenses.csv` and
open a merge request to `master`.

#### Step 5: Merge CE `master` into EE `master`

Ensure that CE's `master` branch is merged into EE's. See the [Merge GitLab CE
into EE](merge-ce-into-ee.md#merging-ce-master-into-ee-master) guide.

#### Step 6: Tag the RC1 version

Use the [`release`](rake-tasks.md#releaseversion) Rake task:

```sh
# NOTE: This command is an example! Update it to reflect new version numbers.
bundle exec rake "release[8.2.0-rc1]"
```

#### Step 7: Integrating changes from `master` into `X-Y-stable`

Once the `X-Y-stable` branch is created, it is the sole source of future
releases for that version. From the 8th, merge requests will either
be [cherry-picked] into `X-Y-stable` by the release manager, or a second merge
request targeting `X-Y-stable` (instead of `master`) should be opened.

Developers are responsible for notifying the release manager that a merge
request is ready to be moved into `X-Y-stable` by following the ["Change for
stable release" process].

---

### Creating subsequent RCs

#### Step 1: Bring changes to the `stable` branches

[Cherry-pick][cherry-picked] CE and EE merge requests into their respective `stable` branch.
Keep in mind that after RC1 only regressions and security fixes should be
cherry-picked into `stable` branch.

#### Step 2: Merge CE `stable` into EE `stable`

Ensure that CE's `X-Y-stable` branch is merged into EE's `X-Y-stable-ee`. See
the [Merge GitLab CE into EE](merge-ce-into-ee.md#merging-a-ce-stable-branch-into-its-ee-counterpart)
guide.

#### Step 3: Tag the RC version

Use the [`release`](rake-tasks.md#releaseversion) Rake task:

```sh
# NOTE: This command is an example! Update it to reflect new version numbers.
bundle exec rake "release[8.2.0-rc2]"
```

[`gitlab/unstable`]: https://packages.gitlab.com/gitlab/unstable
["Change for stable release" process]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#changes-for-stable-releases
[cherry-picked]: pick-changes-into-stable.md

---

[Return to Guides](../README.md#guides)
