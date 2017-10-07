# Remove packages from [packages.gitlab.com](https://packages.gitlab.com/gitlab/)

In the event that something goes wrong with a release, you can remove packages
from [packages.gitlab.com] by following the [packagecloud documentation].

## Requirements

1. Install the `package_cloud` Ruby gem:

    ```sh
    sudo gem install package_cloud
    ```

1. Get the API token for the for [packages.gitlab.com]. Credentials are
   available in the **Release** 1Password vault. Login and click on
   "API Token" on the upper right. Alternatively, you can find the
   `PACKAGECLOUD_TOKEN` value in the [secret variables of omnibus-gitlab on dev].

1. Export `PACKAGECLOUD_TOKEN` to your environment:

    ```sh
    export PACKAGECLOUD_TOKEN=<api token>
    ```

## Example

Be sure to provide the `--url` argument to override the default of
`packagecloud.io`:

```sh
package_cloud yank --url https://packages.gitlab.com gitlab/gitlab-ce/el/6 gitlab-ce-7.10.2~omnibus-1.x86_64.rpm
```

A first-time run of this command should look similar to this:

```sh
Looking for repository at gitlab/gitlab-ce... Using https://packages.gitlab.com with token:**********
success!
Attempting to yank package at gitlab/gitlab-ce/el/6/gitlab-ce-7.10.2~omnibus-1.x86_64.rpm...done!
```

NOTE: PackageCloud does not handle periods in the request nicely. You must use encode periods as `%2E`. For example,
yanking a package from the opensuse 42.1 repository would look like:

```
```sh
package_cloud yank --url https://packages.gitlab.com gitlab/gitlab-ce/opensuse/42%2E1 gitlab-ce-7.10.2~omnibus-1.x86_64.rpm
```

[packages.gitlab.com]: https://packages.gitlab.com/
[packagecloud documentation]: https://packagecloud.io/docs#yank_pkg
[secret variables of omnibus-gitlab on dev]: https://dev.gitlab.org/gitlab/omnibus-gitlab/variables

---

[Return to Guides](../README.md#guides)
