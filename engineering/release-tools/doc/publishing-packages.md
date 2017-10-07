# Package build

## Overview

Packages are built and released in the following steps:

1. Packages builds automatically run when a new [release is tagged](rake-tasks.md#releaseversion)
1. Once the [build pipelines](https://dev.gitlab.org/gitlab/omnibus-gitlab/pipelines?scope=tags) complete these are privately available for internal deploys
1. Builds are manually published using [the instructions below](#publishing-packages)

Running the release task (eg. `bundle exec rake "release[9.4.1]"`), will
create a [pipeline for a tag on dev.gitlab.org](https://dev.gitlab.org/gitlab/omnibus-gitlab/pipelines?scope=tags)
on the omnibus-gitlab repository.

Pipelines for tags in this repository create the final packages.
Every package will be automatically built and pushed to a *private* package
repository. This repository will then be used for deploys to staging, canary
and production environments of GitLab.com.

Once we are confident that the GitLab release is working in GitLab.com environments,
we can publish the packages to public repositories. Public repositories are
being used by our users and customers, so make sure that you only publish
after successful deploy.

Package build is divided roughly with following stages:

* Package build (Automatic)
* Package upload to private repository (Automatic)
* Package upload to public repositories (Manual)
* Docker image build (Automatic)
* Docker image release (Manual)
* Raspberry Pi package build (Automatic)
* Raspberry Pi package release (Manual)

## Publishing packages

When the release is ready to be published to the public, release manager needs
to start the manual job for:

* Package upload to public repositories
* Docker image release
* Raspberry Pi package release

*Note*: Raspberry Pi package builds can take a very long time to complete.
The release can be completed without the finished Raspberry Pi package build.

In order to push the package to public repositories, click on each manual job in
the pipeline:

![Package build pipeline](doc/images/release.png)

### FAQ

#### Why is the upload to the private repository a separate job?

To avoid having to rebuild the package if the only failure is during package push.

#### What happens if one of the package builds failed?

In this case, retry the failed job. If the issue persists, escalate to the
Build team. This is a release blocker.

#### What happens if one of the uploads to the *private* repository failed?

In this case, finalizing release is not possible. Retry the job and if the
upload fails again, escalate to the Build team.

#### What happens if one of the uploads to the *public* repositories failed?

In this case, retry the failed job. If the upload fails again, escalate to the
Build team.
