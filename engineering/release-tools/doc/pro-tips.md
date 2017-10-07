# Pro tips

This is a collection of tips that previous [Release Managers](release-manager.md)
have found to be helpful during their reign. They are _suggestions_, not
requirements. Feel free to contribute your own!

## Use Git aliases

### Add a `git stab` and a `git stabee` aliases

As a release manager, you will have to checkout the latest stable branches quite
often. As you'll be doing this a lot, it's helpful to have
[Git aliases][git-alias] to cut down on typing.

```ini
# ~/.gitconfig
[alias]
  plff = pull --ff-only
  # Check out the latest `X-Y-stable` branch
  stab   = "!f() { br=`git branch --list [0-9]*-[0-9]*-stable | tail -1 | tr -d ' ' | sed 's/*//'`; git checkout $br && git plff; }; f"
  # Check out the latest `X-Y-stable-ee` branch
  stabee = "!f() { br=`git branch --list [0-9]*-[0-9]*-stable-ee | tail -1 | tr -d ' ' | sed 's/*//'`; git checkout $br && git plff; }; f"
```

```sh
$ git stabee
Switched to branch '8-6-stable-ee'
```

### Add a `git pdo` and a `git pdog` aliases

As a release manager, you will have to push to multiple remotes quite often. As
you'll be doing this a lot, it's helpful to have [Git aliases][git-alias] to cut
down on typing. In the following aliases we are using `hub` as explained in the
[Push to multiple remotes](push-to-multiple-remotes.md) doc and we assume that:

- the dev.gitlab.org is called `dev`
- the GitLab.com remote is called `origin`
- the GitHub.com origin is called `github`

```ini
# ~/.gitconfig
[alias]
  pdo  = push dev,origin
  pdog = push dev,origin,github
```

```sh
$ git pdog
Total 0 (delta 0), reused 0 (delta 0)
To git@dev.gitlab.org:gitlab/gitlabhq.git
   c87adc4..63c8a05  8-6-stable -> 8-6-stable
Everything up-to-date
To git@github.com:gitlabhq/gitlabhq.git
   c87adc4..63c8a05  8-6-stable -> 8-6-stable
```

### Add `git cherry-pick` aliases

As merge requests get accepted into master, you're responsible for making sure
they make it into the appropriate `stable` branch. Currently the preferred way
of doing this is via [Git cherry picks] of the merge commit. As you'll be doing
this a lot, it's helpful to have a [Git alias][git-alias] to cut down on typing.

```ini
# ~/.gitconfig
[alias]
  cp  = cherry-pick
  cpm = cherry-pick -m 1
```

```sh
$ git cp <COMMIT SHA>
$ git cpm <MERGE COMMIT SHA>
```

[git-alias]: https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases
[Git cherry picks]: https://git-scm.com/docs/git-cherry-pick

## Leave notes to yourself

As the 22nd nears, it can be stressful trying to make sure that everything that
needs to be included in a release is _actually_ included. It can be helpful to,
for example, [leave a note] to yourself (and anyone else interested) in a merge
request after it's been picked into the `stable` branch. Here's a template that
allows you to remove the relevant label using slash commands:

 ```
Picked into `8-14-stable`, will go into `8.14.1`

/unlabel ~"Pick into Stable" 
```

When picking into a merge request instead of directly to stable, the following may be useful:
```
Picked into https://gitlab.com/gitlab-org/gitlab-EE_OR_CE/merge_requests/MERGE_REQUEST_ID, will merge into `9.3-stable-ee` ready for `9.3.5`

/unlabel ~"Pick into Stable"
```

Unfortunately, this isn't [100% fool-proof].

[leave a note]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2530#note_3332148
[100% fool-proof]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2530#note_3347972

## Update the Regression Issue

The [regressions issue](rake-tasks.md#regression_issueversion) is your overview
of the regressions issues that are still not addressed in the current version.
After each new version (RC, stable or patches), you should delete the notes for
regressions that are fixed and released.

## Use a clipboard history or text expander app

So now that you're constantly [adding notes to yourself] and [updating regression notes],
you might find yourself typing the same things over and over. Unacceptable!

> I use the [Clipboard History and Snippets](https://www.alfredapp.com/help/features/clipboard/)
> feature from Alfred on OS X so that adding something like "Picked into
> `8-4-stable`" is as simple as hitting <kbd>⌥⌘C</kbd>, typing "picked", and
> hitting <kbd>Enter</kbd>.
>
> -- @rspeicher

> I use [TextExpander](https://smilesoftware.com/TextExpander) on OS X so that
> adding something like "Picked into `8-4-stable`" is as simple as typing `pi`
> (or `piee` for "Picked into `8-4-stable-ee`"), and hitting <kbd>Tab</kbd>.
>
> -- @rymai

[adding notes to yourself]: #leave-notes-to-yourself
[updating regression notes]: #update-the-regression-issue

## Keep `#releases` in Slack updated

Check previous messages to see how other release managers are communcating the release status.

If something looks useful, copy it!
One example is the following Slack snippet for build status:

```
Current Status 9.3.3
Gitlab.com
CE :green: - `https://gitlab.com/gitlab-org/gitlab-ce/commits/9-3-stable`
EE :running: - `https://gitlab.com/gitlab-org/gitlab-ee/commits/9-3-stable-ee`
Omnibus CE :green: - `https://gitlab.com/gitlab-org/omnibus-gitlab/commits/9-3-stable`
Omnibus EE :red: :repeat: - `https://gitlab.com/gitlab-org/omnibus-gitlab/commits/9-3-stable-ee`

Dev
CE :hourglass: - Awaiting MRs to merge before sync
EE :hourglass: - Awaiting MRs to merge before sync
Omnibus CE :running: - `https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/9-3-stable`
Omnibus EE :running: - `https://dev.gitlab.org/gitlab/omnibus-gitlab/commits/9-3-stable-ee`
```

---

[Return to Guides](../README.md#guides)
