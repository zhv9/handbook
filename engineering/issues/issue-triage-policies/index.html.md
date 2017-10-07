---
layout: markdown_page
title: Issue甄别策略
---

公司相信 [开放式开发][open-development]，并且鼓励客户提交issues(问题、建议)，有能力的话，还欢迎提交代码。 他们的贡献是非常有价值的，我们应该尽可能的有效的处理这些贡献。 其中最关键的就是甄别--`根据类型和严重程度分类的过程`。

每个公司成员都可以对issue进行甄别。 让没有甄别过的issue维持在较低的水平是可维护性的重点，和大家的职责。 请甄别一些不属于你的职责范围的issue，或者安排一些时间作为日常工作来做。

## 甄别issues

最初的甄别设计(最少)适当的添加标签，所以没有甄别过的issues可以通过查找没有标签的issues来找到。
以下是相关的链接：

* [GitLab CE][ce-issues-query]
* [GitLab EE][ee-issues-query]
* [GitLab Omnibus][omnibus-issues-query]
* [GitLab.com Support Tracker][support-issues-query]

选一个issue，一般优先选择issue表中最早的。 然后用挑剔的眼光进行评估，评估时要在脑中考虑甄别 [策略](#策略)，向自己问一些问题：

* 你明白这个issue中描述了什么吗？
* 使用哪个标签比较合适？ 要考虑到 [团队, 从属, 和类型](../../../engineering/workflow/index.html.md#workflow-labels) 标签。
* 看起来有多严重？ 是否需要把它提交给一个主管或者工程副总？
* `安全` 标签是否合适？
* 是否要作为机密？ 这类通常是 `安全` 类或包含私人资料的issue。

添加的每个标签要看起来比较合适。 具有安全影响的需要特殊对待，参见： [安全问题披露程序](../../../support/channels/index.html.md#security-disclosures).

如果issue看起来不太清楚--你不知道该加哪个标签的话，请直接询问请求者来澄清。 请时刻依照 [用户沟通准则](../../../communication/index.html.md#用户沟通准则) 进行沟通，同时致力于保持对话，直到有足够的信息来完成甄别。

检查重复项！ 通过搜索一些关键词获取的简短列表来审查一下。 要检查包括打开的和关闭的issues，说不定他们就是和已解决问题重复了。

考虑一下这个issue是否还是有效，特别是对于比较老的issues，一个 `bug` 可能在报告前就已经解决了。 或者一个 `功能建议` 可能已经实现了。

一定要检查来自其他issue的交叉引用说明或合并请求，他们是巨大的信息来源。 例如，通过查看交叉引用的合并请求，你可以看到 “已选入 `8-13-stable`，会通过`8.13.6`发布”，这说明这个issue已经在 `8.13.6` 版中修复了。

如果这个issue是个需求，它比较适合去做 [排期请求](../../../engineering/workflow/#scheduling-issues) - 请使用你自己的判断来确认是否这样做！

至此你完成了甄别！ 这个issue已经有了合适的标签，并且可能已经在backlog中、关闭、等待排期、或等待提问者反馈的状态。 如果有时间，再选另一个issue做甄别。

## 策略

### 过时的issues

对于那些有“等待反馈”标签的，至少三个月都没有更新的issue，应该添加这个标签(过时的)。 在经过14天后，如果仍然没有任何人回应，这个issue就应该关闭掉。 很多其他的软件对于过时的issue也是这样的策略。

如果对于这个功能有任何微小回应，则应该算作有回应。 如果无法确认一个issue是否还存在于目前版本的软件，那么这只是给issue tracker添加了噪音。

### 重复的

在提交一个新issue前，确保已经通过 **关键词搜索** 并且检查将提交的issue没有重复。

在发现重复项后请检查并且/或报告它们。

万物是平等的，按理说最早提交的issue应该是标准版。 但如果一个重复的issue相对于早期的那个有一个更好的标题、描述、或更多的评论和积极反应，那么它应该优先于早前的那个issue。

### 需要关闭的

我们不能让每个人都满意。 我们必须尽量每个用户的满意度间保持平衡，来保证项目可以持续的进行下去。

- 如果一个issue是一个bug但是没有重现步骤或版本信息，关闭这个issue并且请求报告人提供更多信息。
- 如果确定不会添加一个功能/变更，那么就这么回复并且关闭这个issue。

### 在有新issues后添加标签

如果有新issue提交进来，那么就应该进行甄别和添加标签。 没有标签的issue很难找并且经常会遗漏。

### 处理属于自己的issues

用 "Author: your username" 进行排列，关闭那些已经解决的和因为其他原因变得不相干的issues。 给没有加标签的issue添加标签。

### 问题/支持issues

如果是问问题的issue，或一些模糊的东西导致开发团队(无论任何原因)没有办法定位，那么就关闭它然后指导他们去我们相关的支持资源(例如：我们的帮助文档、论坛或邮件支持)。

### 新标签

如果在大量的issue中发现了通用的模式(例如：一个新功能还没有专用的标签)，那么给管理员提出添加新标签的建议。

公司有人专门管这个标签，在添加新标签前一定要让他批准。 这样的话就不会有一堆重复/没有用/前后矛盾的标签了。

## 活动

我们定期举行社区季度活动，核心团队成员和团队成员可以有助于处理一下还没有解决的issue。 请查看 [the dedicated page](/community/issue-bash) 获取更多信息和即将举行的活动。


## Notes

原始的策略是 [#17693][17693]。 我们会同公司的进步一同提升这个策略。

以下项目、资源、和博客对我们理解策略是非常有帮助的：

- [CodeTriage][code-triage]
- [How to be an open source gardener][open-source-gardener]
- [Managing the Deluge of Atom Issues][atom-issues]
- [Handling Large OSS Projects Defensively][handling-big-projects]
- [My condolences, you’re now the maintainer of a popular open source project][my-condolences]
- [The Art of Closing][art-of-closing]

[open-development]: https://about.gitlab.com/2015/12/16/improving-open-development-for-everyone/
[ce-issues-query]: https://gitlab.com/gitlab-org/gitlab-ce/issues?scope=all&state=opened&utf8=%E2%9C%93&label_name%5B%5D=No+Label&assignee_id=0
[ee-issues-query]: https://gitlab.com/gitlab-org/gitlab-ee/issues?scope=all&state=opened&utf8=%E2%9C%93&label_name%5B%5D=No+Label&assignee_id=0
[omnibus-issues-query]: https://gitlab.com/gitlab-org/omnibus-gitlab/issues?scope=all&state=opened&utf8=%E2%9C%93&label_name%5B%5D=No+Label&assignee_id=0
[support-issues-query]: https://gitlab.com/gitlab-com/support-forum/issues?scope=all&state=opened&utf8=%E2%9C%93&label_name%5B%5D=No+Label&assignee_id=0
[17693]: https://gitlab.com/gitlab-org/gitlab-ce/issues/17693
[code-triage]: https://www.codetriage.com/
[open-source-gardener]: http://words.steveklabnik.com/how-to-be-an-open-source-gardener
[atom-issues]: http://blog.atom.io/2016/04/19/managing-the-deluge-of-atom-issues.html
[handling-big-projects]: http://artsy.github.io/blog/2016/07/03/handling-big-projects/
[my-condolences]: https://runcommand.io/2016/06/26/my-condolences-youre-now-the-maintainer-of-a-popular-open-source-project/
[art-of-closing]: https://blog.jessfraz.com/post/the-art-of-closing/
