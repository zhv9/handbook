# GitLab Release Tools

This repository contains instructions and tools for releasing new versions of
GitLab Community Edition (CE) and Enterprise Edition (EE).

The goal is to provide clear instructions and procedures for our entire release
process, along with automated tools, to help anyone perform the role of [Release
Manager](doc/release-manager.md).

## Guides

- [什么是发布管理员？](doc/release-manager.md)
- [如何每月发布一个新的小版本](doc/monthly.md)
- [如何发布软件的补丁版本](doc/patch.md)
- [如何发布一个软件安全修复版本](doc/security.md)
- [如何选择特定的变更到 `稳定` 分支](doc/pick-changes-into-stable.md)
- [如何合并社区版到企业版中](doc/merge-ce-into-ee.md)
- [如何给月度发布版本建立发布候选版](doc/release-candidates.md)
- [如何执行QA的手工测试](doc/qa-checklist.md)
- [如何同一时间给多个远程库推送](doc/push-to-multiple-remotes.md)
- [如何从包管网站移除包(packages)](doc/remove-packages.md)
- [如何推送一个新tag版本](doc/omnibus-tag.md)
- [获取建立tag和发布许可](doc/permissions.md)
- [主要版本发布准则](doc/major.md)
- [Rake tasks](doc/rake-tasks.md)
- [专业建议](doc/pro-tips.md)
- [发布模板文件](./templates)

## Development

[![build status](https://gitlab.com/gitlab-org/release-tools/badges/master/build.svg)](https://gitlab.com/gitlab-org/release-tools/commits/master)
[![coverage report](https://gitlab.com/gitlab-org/release-tools/badges/master/coverage.svg)](http://gitlab-org.gitlab.io/release-tools/coverage/)

## Contributing

See [CONTRIBUTING.md](../../engineering/development/CONTRIBUTING.md).

## License

See [LICENSE](../../legal/license-agreement/LICENSE).
