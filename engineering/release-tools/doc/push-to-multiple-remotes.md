# Pushing to multiple remotes

GitLab's code is available at [gitlab.com], [dev.gitlab.org], and [github.com].
This guide provides simple methods for pushing changes to all three locations at
once.

## Using `hub`

[hub] is a wrapper around the `git` command that adds a few niceties, one of
which is the ability to push to multiple remotes in a single command by
separating them with a comma.

See the [installation instructions](https://github.com/github/hub#installation)
to get started.

For the example below, it's assumed that `hub` is installed and that you have
remotes called `origin`, `dev`, and `github`, pointing to the appropriate
repository at [gitlab.com], [dev.gitlab.org], and [github.com], respectively.

You can push the `master` branch to all three at once like this:

```sh
hub push origin,dev,github master
```

## Using a Bash script (advanced)

Add this script to your `~/.bashrc`, `~/.zshrc`, etc.:

```sh
gpa ()
{
  git push origin ${1:-master} && git push dev ${1:-master} && git push github ${1:-master}
}
```

Again, this assumes that you have remotes called `origin`, `dev`, and `github`,
pointing to the appropriate repository at [gitlab.com], [dev.gitlab.org], and
[github.com], respectively.

Then you can push to all three at once like this:

```sh
# Defaults to `master`
gpa

# Push to `feature-1`
gpa feature-1
```

[gitlab.com]:     https://gitlab.com/gitlab-org/
[dev.gitlab.org]: https://dev.gitlab.org/gitlab/
[github.com]:     https://github.com/gitlabhq/
[hub]:            https://github.com/github/hub

---

[Return to Guides](../README.md#guides)
