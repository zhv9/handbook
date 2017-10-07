---
layout: markdown_page
title: "Engineering"
---

## 沟通<a name="reach-engineering"></a>

- [**Issue Tracker**](https://gitee.com/zhv/handbook/issues); 
- [**聊天室**](https://gitlab.slack.com/archives/development); 请使用 `#development` , `#frontend`, `#infrastructure`, `#ci-cd`, 和 `#support` 在聊天室中可以问那些不适合写在issue tracker上或发邮件的问题。

## On this page
{:.no_toc}

- TOC
{:toc}

## 其他相关页面

- [开发人员入职培训](../developer-onboarding)
- [开发流程](../engineering/workflow)
- [常用项目](../engineering/projects)
- [Issue甄别策略](../engineering/issues/issue-triage-policies)
- [关键安全发布过程](../engineering/critical-release-process)
- [产品性能](/handbook/engineering/performance)
- [产品监控](/handbook/infrastructure/monitoring)
- [产品准备指南](../infrastructure/issue_templates/production_readiness.md)

## 公司代码库

公司产品由很多子项目构成，他们的代码库地址可以在这个页面查看：[公司开发的项目](../engineering/projects)。

添加一个代码库时请按照如下步骤操作:
1. 确保项目在公司的命名空间下。
1. [添加项目到项目目录中](https://gitee.com/zhv/note/blob/master/project.md)
1. 给代码仓库添加MIT许可证。 请见 [MIT许可证示例](../legal/license-agreement/LICENSE)。
1. 添加开发者指南。 参见 [Contribution Example](../engineering/development/CONTRIBUTING.md), 确保所有的开发者签署了 [个人](../legal/license-agreement/individual_contributor_license_agreement.md) 和 [公司](../legal/license-agreement/corporate_contributor_license_agreement.md) 的贡献许可协议。
1. 在 `README.md` 文件中添加 `CONTRIBUTING.md` 文件的链接。

## 工程组

- [运维](../support)
- [后端](../backend)
- [Edge](../edge)
- [前端](../frontend)
- [构建](../build)
- [用户体验](../ux)
- [安全](../engineering/security)
- [基础架构](../infrastructure)
  - [产品](../infrastructure/production)
  - [数据库](../infrastructure/database)
  - [Gitaly](../infrastructure/gitaly)

## 协作

为了每月可以保持高速的发布节奏，我们必须降低各种障碍来完成各个事项。自从团队分布到各地，并且工作时间也不一样，所以必须更加并行和异步工作。

这意味着如果你实现了一个新功能，就应该把这个功能尽快推送到服务器。

## 代码质量和标准

为了保证代码质量和标准化，熟悉 [开发指南] 是最基本要求，并且根据所在工作组不同需要参考以下各类指南：

- [用户体验指南](../engineering/development/ux_guide/index.md)
- [后端指南](../engineering/development/README.md#backend-howtos)
- [前端指南](../engineering/development/fe_guide/index.md)
- [数据库指南](../engineering/development/README.md#databases)

[开发指南]: ../engineering/development/README.md

## 代码评审

代码评审是做每次合并请求时的强制要求，所以必须熟悉并遵守我们的[代码评审准则](../engineering/development/code_review.md)。

## 开发人员到运维团队轮换制

参见 [the fix4all description](../engineering/fix4all/)。

## 发布管理员

在 [发布工具库](../engineering/release-tools/readme.md) 中，包含很多对于 [发布管理员](../engineering/release-tools/doc/release-manager.md) 的职责和任务执行很有用的相关信息。

由于工作量巨大，所以有两个主要的发布管理员：

1. 一个在本地
2. 一个在外地

经过培训的发布管理员，任命后对发布候选版本的建立和部署承担最终责任。

* 此发布管理员在需要帮助和对任何影响发布候选版本的问题都要直言不讳的提出。

* 实习的发布管理员需要做大部分的手工工作(例如：挑选候选版、构建候选版本、发布和其他工作)。

* 培训者应该允许实习生干活，就像飞机主驾驶在关键的时候能够把工作接管下来。

这是 [即将上任和已在任的发布管理员列表](/release-managers/)。
