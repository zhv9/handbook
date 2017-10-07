# Merge GitLab CE into EE

This guide details the process for merging any GitLab CE branch (`master`, `8-0-stable`,
etc.) into the corresponding GitLab EE branch (`master`, `8-0-stable-ee`, etc.).

NOTE: Be careful about squashing commits when merging between CE and EE. When
in doubt, do NOT squash. See the [explanation for more
details](#why-squashing-is-bad-for-merge-commits).

## Setup

1. We're going to pull CE into EE, so we first need a working copy of EE:

    ```sh
    git clone git@gitlab.com:gitlab-org/gitlab-ee.git
    cd gitlab-ee
    ```

1. Now add a remote inside the EE repository pointing to the CE repository:

    ```sh
    git remote add ce git@gitlab.com:gitlab-org/gitlab-ce.git
    ```

## Tasks

### Merging CE `master` into EE `master`

Before [releasing a new Release Candidate](release-candidates.md) of GitLab, we
need to merge the latest changes from CE into EE. Make sure that there is not a
merge request where this work is already in progress. All merge requests that
are related to merging CE into EE have the ["CE upstream" label][upstream label].

1. Make sure your EE repository has all the latest changes:

    ```sh
    git fetch origin master
    ```

1. Then make sure your `ce` remote has the latest branch information:

    ```sh
    git fetch ce master
    ```

1. Create a new branch off of `master` onto which we'll perform the merge:

    ```sh
    git checkout -b ce-to-ee origin/master
    ```

1. Now perform the merge:

    ```sh
    git merge --no-ff ce/master ce-to-ee
    ```

1. At this point it's common to encounter conflicts. Display the list of
  conflicting files and save it somewhere:

    ```sh
    git status
    ```

1. Manually add all the conflicting files as-is:

    ```sh
    git add file1 file2
    ```

1. Commit (this is to have a snapshot of the conflicts):

    ```sh
    git commit
    ```

1. Push the updated branch to `origin`:

    ```sh
    git push origin ce-to-ee
    ```

1. Submit a new [merge request in the GitLab EE project], selecting `ce-to-ee`
   as the **source** branch and `master` as the **target**:
   - Set the title as `CE upstream` and the `~"CE upstream"` label
   - Paste the list of conflicting files in the description: you can make it a
     checklist and check conflicts that you've already resolved
   - Set the due date as **today**

1. Resolve the conflicts that you feel confident to resolve. 
   Ping relevant people for help in resolving the remaining conflicts.
   

From this point on, it is your responsibility to get this merge request merged
before the end of your workday, so don't hesitate to ping people and kindly
remind them that they forgot to create
[a EE-specific merge request in the first place] etc.

[merge request in the GitLab EE project]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests
[upstream label]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests?label_name%5B%5D=CE+upstream&scope=all&sort=id_desc&state=opened
[a EE-specific merge request in the first place]: https://docs.gitlab.com/ce/development/limit_ee_conflicts.html

### Merging a CE stable branch into its EE counterpart

Before releasing a new stable version of GitLab, we need to merge any changes
from CE's stable branch for that version into EE's.

In this example, we'll be releasing the first patch version of 7.14, 7.14.1.
Both CE and EE should already have branches called `7-14-stable` and
`7-14-stable-ee`, respectively, which were created during the
[RC1 release](release-candidates.md#4-tag-the-rc1-version).

1. Checkout a local branch, tracking the remote one:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    git checkout --track origin/7-14-stable-ee

    # The command above will fail if you've already checked out the stable
    # branch during a previous release. Switch to your local branch instead:
    git checkout 7-14-stable-ee
    ```

1. Make sure your local branch has all the latest changes:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    git pull origin 7-14-stable-ee
    ```

1. Create a new temporary branch for the merge:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version and date
    git checkout -b 7-14-stable-ee-with-ce-2017-12-31
    ```

1. Then make sure your `ce` remote has the latest branch information:

    ```sh
    git fetch ce
    ```

1. Now perform the merge:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers and date.
    git merge --no-ff ce/7-14-stable 7-14-stable-ee-with-ce-2017-12-31
    ```

1. At this point there will be a merge conflict, but likely only on the
   `VERSION` file. Resolve it and commit the merge.

1. Push the new branch to `origin` ready to create a merge request:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    git push origin 7-14-stable-ee-with-ce-2017-12-31
    ```
    
1. Submit a new [merge request in the GitLab EE project], selecting the new branch (e.g. `7-14-stable-ee-with-ce-2017-12-31`)
   as the **source** branch and the stable branch (e.g. `7-14-stable-ee`) as the **target**

---

## Why Squashing is Bad for Merge Commits

If the tip of the branch is a merge commit, squashing will convert a merge
commit into a regular commit, causing ancestor history to be lost. This will
likely cause unnecessary merge conflicts down the road. For example, consider
the following scenario:

1. Developer adds file `foo.rb` to `9-0-stable`.
2. Release manager creates a merge commit `XYZ` for `9-0-stable` and `9-0-stable-ee`.
3. Squashing `XYZ` will make it look like `XYZ` introduced `foo.rb`.
4. Developer updates file `foo.rb` in `9-0-stable`.
5. When the release manager attempts to resync `9-0-stable-ee` with
   `9-0-stable`, step 4 will look like a conflict because Git will think both
   branches modified the file, when only one did. For example, the
   `git log --graph foo.rb` output may look like:

    ```
    *   0b6e1dd5b2 Merge commit '12345678' into 9-0-stable-ee
    |\
    | * 5819ca1a24 Modified foo.rb
    | * cd74c1434e Added foo.rb
    * 621cbd0414 Squashed merge for `9-0-stable` to `9-0-stable-ee`
    ```

    Because `621cbd0414` is a squashed commit and no longer a merge commit, it has
    no link back to `cd74c1434e`. When Git attempts to merge `621cbd0414` with
    `9-0-stable-ee`, Git will flag a conflict.

    Instead, if everything is done properly, the graph should look more like this:

    ```
    * 5819ca1a24 Modified foo.rb
    * cd74c1434e Added foo.rb
    ```

---

[Return to Guides](../README.md#guides)
