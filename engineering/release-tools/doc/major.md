# Major release

GitLab occasionally releases a new major version (e.g. from 8.X to 9.X).

A major release allows us to make breaking changes, for instance removing or
changing (deprecating) existing APIs and functionalities.

## Handling deprecations

Deprecations should be announced and if necessary replaced one or more releases
in advance of the major release.

For instance, when going from API v4 to v5, v5 will have to be active for at
least a single release before deprecating v4. In practice, it's very unfriendly
to deprecate an API over a single month and a longer time period might be chosen
(such as one major release for a new API version, or a span of a number of
releases).

## New functionalities and APIs

New functionalities and APIs can freely be added at any time and should not be
ported back.

For instance, GitLab 8.16 introduced an API for time tracking. This adds to the
API and will not break any integrations, so could be introduced in a minor
update.

## Frequency

At this time, there is no particular frequency to the occurrence of major
releases.

## Creating awareness

People need to be aware of changes and deprecations. For each major or breaking
change, consider:

- updating all documentation
- making customers aware in blog and release posts
- training the service engineers in the change, but also in how to help
  customers transition
- optionally: reaching out to customers and/or external applications

---

[Return to Guides](../README.md#guides)
