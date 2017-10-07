# Monthly Release

GitLab releases a new minor version (`X.Y`) every month on the 22nd. The history
and reasoning behind this schedule can be found [on the blog].

The [release manager] should begin the monthly release process *no earlier than* the 8th (Pacific time, midnight is the start of the workday in Europe).
The last day to reliably get your code in the release is the 7th (Pacific time).

For an idea of the release process please see the [monthly template](https://gitlab.com/gitlab-org/release-tools/blob/master/templates/monthly.md.erb).

The release manager should make sure there's a work in progress blog post
available for the next release the moment the previous release has been
published. This allows other developers to leave comments about the release,
instead of having to note them down elsewhere.

[on the blog]: https://about.gitlab.com/2015/12/07/why-we-shift-objectives-and-not-release-dates-at-gitlab/
[release manager]: release-manager.md

## Process

### 1. Create an issue to track the release

In order to keep track of the various tasks that need to happen each day leading
up to the final release, we create an issue on the [GitLab CE issue tracker] and
update it as we progress.

1. Set up [API access for rake tasks](rake-tasks.md#setup)

1. Create the issue using the
   [`monthly_issue`](rake-tasks.md#monthly_issueversion) Rake task:

    ```sh
    # NOTE: This command is an example! Update it to reflect new version numbers.
    bundle exec rake "monthly_issue[8.2.0]"
    ```

1. You may want to **bookmark** the issue until it's closed at the end of the
   release cycle.

[GitLab CE issue tracker]: https://gitlab.com/gitlab-org/gitlab-ce/issues

### 2. Complete the daily release tasks

Once the release schedule begins, each work day has something that needs to be
done. Perform the tasks and mark them as complete in the issue as you progress.

If you're not sure what to do for any task, [check the guides](../README.md#guides).

## Getting Help

Completing release tasks on time is very important. If you experience problems with any of
release tasks and you don't know who to ask then you should contact someone from this list:

* Build Lead [@marin](https://gitlab.com/marin)
* VP of Engineering [@stanhu](https://gitlab.com/stanhu)
* CTO [@dzaporozhets](https://gitlab.com/dzaporozhets)

The earlier we determine problem or delay in release - the easier it is to fix it.

## Priorities

Keep up with the release schedule. It's better to ship less but on time.
Revert code that delays the release.

---

[Return to Guides](../README.md#guides)
