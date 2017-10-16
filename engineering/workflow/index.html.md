---
layout: markdown_page
title: "Engineering Workflow"
---

这个文档解释了在公司中每个人在对项目issues工作时所遵循的工作流。
对于适用于每个人的工作流，请参见 [PROCESS.md](../../engineering/development/PROCESS.md).

## On this page
{:.no_toc}

- TOC
{:toc}


## GitLab Flow

公司使用 [GitLab Flow](./workflow/gitlab_flow.md) 来构建产品。

## 损坏的 master

如果发现 `master` 库的自动化测试失败(红色)或被破坏(绿色带有负号)，解决这个问题比其他任何开发事项都重要。 只要我们做了任何导致自动化测试失败，都意味着已有功能被破坏了，或者引入新的bug和安全问题。

建立一个issue，把它发布到 `#development` 频道，以便其他开发人员就可以意识到这个问题并且可以提供帮助。 如果你无法在数个小时内修复问题，在这个issue和中协作群(Slack)中 `@mention` 相关的工程师主管和CTO。 这样就可以最快速度分配其他资源来修复这个issue。

## 安全 issues

如果发现了安全issue警报，无论大还是小，修复这个是所有开发中最高优先级的事项。

建立一个 **confidential issue** 提醒安全团队和相关工程主管，包括工程副总，并且将它发布到 `#security` 频道。

## Basics

1. 开始处理你被分配的issue。 如果你没有分配任何issue，根据相关的标签，找一个你可以做的最高优先级的issue。 [你可以使用这个查询，根据优先级排序已开始的里程碑中的issue][priority-issues]，同时通过标签筛选属于你团队的issue。
1. 如果你需要将某些事情列入日程或做区分，给它添加适当的标签。(参见 [Scheduling issues](#scheduling-issues)).
1. 如果你在处理某些issue时碰到了超出你经验的事项，请一定要在开始这项工作时告知其他组的同事。 这样其他人员就可以尽早给你反馈，从长远来看，这可以节省你的时间。
1. 你需要对分配给你的issue负责。 这意味着它必须与它所关联的里程碑一起提交。 如果你没有办法完成这事，你应该尽早和你的经理沟通。 在团队中，整个团队对这个 (参见 [在团队中工作](#working-in-teams)) 负责。
1. 你(和你的团队，如果适用)为以下事项负责：
  - 确保你的变更 [可以干净的应用于GitLab Enterprise Edition][ce-ee-docs] (减少相似项目合并时的冲突)。
  - 对新功能修正进行测试，特别是在合并和打包后。
1. 一旦发布候选版已部署到模拟环境中，请验证您的更改是否按预期工作。 因为出现过开发中没有出现但在生产中出现错误的问题。(例如 由于 CE-EE 合并导致的issues)。

关于issues和合并请求的一般准则，请参考 [公司工作流][公司工作流].

[priority-issues]: https://gitlab.com/groups/gitlab-org/issues?scope=all&sort=priority&state=opened&milestone_title=%23started&assignee_id=0
[ce-ee-docs]: https://docs.gitlab.com/ee/development/limit_ee_conflicts.html
[公司工作流]: ../../communication/index.html.md#公司工作流

## Working in Teams

对于工作或包括很多不同组件的工作，是需要一个团队进行工作的。 一般的团队由以下几个方面组成。
[后端开发](https://about.gitlab.com/jobs/developer/)，
[前端开发](https://about.gitlab.com/jobs/frontend-engineer/)，
[用户体验设计](https://about.gitlab.com/jobs/ux-designer/)，
[产品经理](https://about.gitlab.com/jobs/product-manager/)。

1. 团队每个人在解决计划的发布版中issue有着共同的责任。
    1. 如果团队发现有可能无法按时完成某些事项，团队应该尽快向上一级/告知其他团队。 最佳的方法是告知你的领导。
    1. 一般来说，发行一个较小的迭代，比稍后发布一个版本要好。
1. 考虑一下给新团队开一个协助频道(Slack)，但是请记住要在相关issues中写下所有相关信息。 相对于单信息通道，你不会想去两个信息通道找信息的。 协助频道(Slack)不能开放给公司以外的人员。

## Choosing something to work on

从目前里程碑中最高优先级的事情开始工作。 每个项目的优先级是通过库中的标签来定义的，同时你也可以通过优先级进行排序。

在通过优先级排序后，选择那些属于你职责并且可以处理事项。 这意味着对于前端开发，你应该处理有 `前端` 标签的事项。

为了准确筛选，你可以对issues通过以下几个事项进行筛选：

- 里程碑: 已开始
- 分配情况: 未分配
- 标签: 你选择的标签。 例如 `持续集成(CI)/持续交付(CD)`, `讨论`, `Edge`, `前端`, or `平台`
- 通过优先级排序

[使用这个链接来快速的设置上面所有参数][priority-issues]。 你还需要按照你所在的组负责的标签进行筛选。

如果对你要做哪些事有疑问，请问下你的领导。 他们会告诉你的。

## Triaging and reviewing code from the rest of the community

It's every [developers' responsibilities] to triage and review code contributed
by the rest of the community, and work with them to get it ready for production.

Merge requests from the rest of the community should be labeled with the
`Community Contribution` label.

This should be to be part of your daily routine. For instance, every morning you
could triage new merge requests from the rest of the community that are not yet
labeled `Community Contribution` and either review them or ask a relevant person
to review it.

Make sure to follow our
[Code Review Guidelines](https://docs.gitlab.com/ce/development/code_review.html).

[developers' responsibilities]: /positions/developer/#responsibilities

## Workflow labels

Labels are described in our [Contribution guide][contrib-labels-guide].

[contrib-labels-guide]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#workflow-labels

## Working with GitLab.com

GitLab.com is a very large instance of GitLab Enterprise Edition.
It runs release candidates for new releases, and sees a lot of issues because of the amount of traffic it gets.
There are several internal tools available for developers at GitLab to get data about what's happening in the production system:

### Performance data

There is extensive [monitoring](https://monitor.gitlab.net/) publicly available
for GitLab.com. For more on this and related tools, see the [monitoring
 handbook](/handbook/engineering/monitoring).

More details on [GitLab Profiler](http://redash.gitlab.com/dashboard/gitlab-profiler-statistics)
are also found in the [monitoring performance handbook](/handbook/engineering/monitoring).

### Error reporting

- [Sentry](https://sentry.gitlap.com/) is our error reporting tool
- [log.gitlap.com](https://log.gitlap.com/) has production logs
- [prometheus.gitlab.com](https://prometheus.gitlab.com/alerts) has alerts for
  the [production team](/handbook/infrastructure/#production-team)

### Feature flags

If you've built feature flags into your code, be sure to read about
[how to use the feature flag to test a feature on GitLab.com](/handbook/infrastructure/#feature-flags).

## Scheduling issues

GitLab Inc has to be selective in working on particular issues.
We have a limited capacity to work on new things. Therefore, we have to
schedule issues carefully.

Product Managers are responsible for scheduling all issues
in their respective [product areas](/handbook/product/#who-to-talk-to-for-what),
including features, bugs, and tech debt. Product managers alone determine the [prioritization](https://about.gitlab.com/handbook/product/#prioritization).
The UX Lead and Engineering Leads are responsible for allocating people making sure things are done on time. Product Managers are _not_ responsible for these activities, they are not project managers.

Direction issues are the big, prioritized new features for each release.
They are limited to a small number per release so that we have plenty of
capacity to work on other important issues, bug fixes, etc.

If you want to schedule an `Accepting Merge Requests` issue, please remove
the label first.

Any scheduled issue should have a team label assigned, and at least one type label.

### Requesting something to be scheduled

To request scheduling an issue, ask the [responsible product manager](/handbook/product/#who-to-talk-to-for-what)

We have many more requests for great features than we have capacity to work on.
There is a good chance we’ll not be able to work on something.
Make sure the appropriate labels (such as `customer`) are applied so every issue is given the priority it deserves.

### Process improvement

There is an informal scheduling process discussion in the #scheduling Slack channel.
Anyone can join and suggest improvements to our scheduling process.

## Product development timeline

Teams (Product, UX, Engineering) continually work on issues according to their respective
workflows. There is no specified process whereby a particular resource should be working
on a set of issues in a given time period. However, there are specific deadlines that
should inform team workflows and prioritization. Suppose we are talking about milestone `m`
that will be shipped in month `M` (on the 22nd). We have the following deadlines:

- By month `M-1, 4th`: Release scope is established.  In-scope issues marked with milestone `m`.
- By month `M-1, 7th`: `m` issues are updated with docs starter blurb. Release post (WIP merge request) created with `m` issues and docs starter blurbs.
- On month `M-1, 8th` (or next business day): Kickoff call with WIP release post.
- By month `M, 7th`: Completed `m` issues with docs have been merged into master. Unstarted or unfinished `m` issues are de-scoped from `m`, with `m` being removed from them.
- On month `M, 22nd`: Release shipped to production. Release post published.

Refer to [release post due dates](/handbook/marketing/blog/release-posts/#due-dates)
for additional deadlines.

Note that release timelines are overlapping. For example, when a release is shipped
to production on the 22nd, the scope for the following release has already been established
earlier in that same month.

An in-scope issue already has a docs starter blurb (written by the PM) by the time
engineers start development. Engineers should create and merge in the updated docs
as part of completing an issue by the 7th. PMs revise the starter docs blurbs in the
release post appropriately before the release post is published.

Refer to [Feature freeze on the 7th for the release on the 22nd](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/PROCESS.md#feature-freeze-on-the-7th-for-the-release-on-the-22nd)
for further timeline details of code releases, including major/minor version releases, as well as patch releases.

## Updating issues throughout development

Team members use labels to track issues throughout development. This gives visibility to 
other developers, product managers, and designers, so that they can adjust their plans
during a monthly iteration. An issue should follow these stages:

- `In dev`: A developer indicates they are developing an issue by applying the `In dev` label.
- `In review`: A developer indicates the issue is in code review and UX review by removing the `In dev` label, and applying the `In review` label.


## Kickoff

At the beginning of each release, we have a kickoff meeting, publicly livestreamed to YouTube.
In the call, the Product Development team (PMs, UX designers, and Engineers) communicate with
the rest of the organization which issues are in scope for the upcoming release.
The call is structured by [product area](../../product/index.html.md#who-to-talk-to-for-what) 
with each PM leading their part of the call.

The notes are available in a publicly-accessible [Google doc](https://docs.google.com/document/d/1ElPkZ90A8ey_iOkTvUs_ByMlwKK6NAB2VOK5835wYK0/edit?usp=sharing).
Refer to the doc for details on viewing the livestream.

## Retrospective

After each release, we have a retrospective meeting, publicly livestreamed to YouTube.
We discuss what went well, what went wrong, and what we can improve for the next release.

The notes are available in a publicly-accessible [Google doc](https://docs.google.com/document/d/1nEkM_7Dj4bT21GJy0Ut3By76FZqCfLBmFQNVThmW2TY/edit?usp=sharing).
Refer to the doc for details on viewing the livestream.