## Pick specific changes into the `stable` branches

The latest RCs, and all patch releases are made up of one or more merge requests
that have been merged into the `master` branch of GitLab CE or EE, and which
then need to be [cherry-picked] into the respective `stable` branches.

We merge into master first instead of merging in a stable branch first because
master moves faster than stable branches. Getting there first prevents the most
merge conflicts by more quickly having all developers fetch the changed code.

We cherry pick the single **merge commit** that results from accepting a merge
request and which may have been made up of more than one commit. This means we
only have to perform one pick per merge request and reduces the chances of
missing commits.

1. Make sure you have the latest changes to `master`:

    ```sh
    git checkout master
    git pull origin master
    ```

1. Check out the `stable` branch:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    git checkout 8-3-stable
    ```
    **Note:** For CE/EE these instructions have been superseded/extended by [picking-into-merge-requests.md](picking-into-merge-requests.md). The branch you'll use in this step might instead look like `X-Y-stable-patch-Z`.

1. Cherry-pick the **merge commit** from `master`. You should almost always be
   picking merge commits because there may be a series of commits in a merge
   request that must go together.

    ```sh
    # NOTE: This command is an example! Update it to reflect the actual SHA.
    git cherry-pick [merge commit sha] -m 1
    ```

    To learn why it's safe to use `-m 1`, please read [this StackOverflow
    answer](https://stackoverflow.com/a/12628579/223897).

   If you do not see the merge commit in the GitLab system note, it's likely
   this a Sidekiq job failed to post it. The merge commit likely exists in the
   repository. Check to see if you can find it by searching for the
   title of the merge request in `git log`.

1. Push the updated `stable` branch:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    git push origin 8-3-stable
    ```

    > **Note:** You'll probably want to push the stable branch to all of our
    remotes. See [Pushing to multiple remotes](push-to-multiple-remotes.md).

1. As merges are picked and stable branches updated, it can be helpful to
   [post a note](pro-tips.md#leave-notes-to-yourself) in the merge request's
   discussion.

1. [Update any notes](pro-tips.md#update-the-regression-issue) from the
   regression issue to reflect their latest status.

[cherry-picked]: pro-tips.md#add-a-git-cherry-pick-alias

---

[Return to Guides](../README.md#guides)
