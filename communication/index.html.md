---
layout: markdown_page
title: "GitLab Communication"
extra_js:
  - libs/moment.min.js
  - libs/moment-timezone-with-data.min.js
  - team-call.js
---

## On this page
{:.no_toc}

- TOC
{:toc}

我们是一个 **分布式的**，**仅远程工作** 的公司We're a **distributed**, **remote-only** company where people work remotely without missing out.
For this, we use **asynchronous communication** and are as open as we can be by communicating through public issues, chat channels,
and placing an emphasis on ensuring that conclusions of offline conversations are written down.
These communication guidelines are meant to facilitate smooth communication in an
ever-growing remote-only company.
Please keep in mind that you represent GitLab and our culture, also on Social Media.
When commenting on posts please keep in mind: "Don't argue but represent."

### 内部沟通

1. 所有沟通都应该使用中文或英文，即使是一对一沟通的时候也一样，因为有时候你需要转发email或者聊天记录。
1. 使用 **异步沟通** 如果可以的话 (用issues和email代替聊天工具), 使用issues比电子邮件更好, 电子邮件比聊天工具更好, 公告在进行团队议程时发布, 并且 [大家应该在没有聊天工具打扰的情况下工作](https://m.signalvnoise.com/is-group-chat-making-you-sweat-744659addf7d#.21t7089jk). 使用邮件代替聊天工具。就像和使用聊天工具一样，使用内部的短邮件来发送信息和沟通。不要发送像hi Emma这样的浪费时间的信息，首先复制粘贴email的主题到邮件正文中。因为不是随时有时间，一边按照计划工作一边等邮件回复或聊天工具提醒是非常好的工作方法。
1. 有时候异步沟通是比较好的选择，但是不是默认的沟通方式。面对面或视频[guidelines on video chats](#video-chats)沟通是更好的方式。
1. 尽量多问问题，但是问的时候，尽量多带些人，人越多回答的就越多，也会有更多人看到答案。(所以使用issues或开一个聊天群来代替一对一的email)，并且一定要把答案记到文档中。
1. 如果你提醒一些事情(合并请求，issue，提交内容，网页，评论或其他)，请附上链接。
1. 所有公司的文档应该默认 **共享** ，不要使用本地文件而要在对应的issue上提交评论或说明。

#### Email

1. 当使用电子邮件时，每封邮件发送一封电子邮件，因为一封邮件中的多个项目会导致延误(需要回复所有事情)或遗漏(忘记其中的一项内容)。
1. 回复电子邮件，即使什么都不用干。这样可以让其他人知道你收到了。你简单的回复了OK、谢谢或已完成，这事就完了。
1. 如果你转发了一个没有回复的电子邮件，那么加上FYI (for your information) 或 FYA (for your action)。如果你转发了一个包含FYA的外部的请求，这不代表公司必须做上面提出的要求，只是代表了那个转发的人不跟踪这个请求了，希望你来代替他跟踪这事。
1. 详细的邮件转发规则请参考：暂无
1. 电子邮件时异步的，例如：如果你经理周末给你发邮件，那么你到工作时间再回复邮件也是可以的。
1. 如果邮件很紧急，那么通过即时聊天工具来讨论邮件内容也是可以的。

#### Chat

1. 如果你使用聊天工具，请尽可能使用公共频道，如果需要的话，请提醒你要联系的人。这样可以保证其他人很容易提出意见，如果需要的话也很容易让其他人参与进来。
1. 在聊天中，尽量少用提醒全部人员的功能。这个功能只用在那些紧急且重要的事情上，而不只是重要的事情。如果全员提醒用的太多，会导致对单个人员的提醒淹没在大量的提醒中，使之变得不能及时看到。
如果哪些事情紧急且重要:
   * 使用 `@here` 提醒这个房间所有 _在线_ 成员。
   * 使用 `@channel` 提醒 _所有_ 这个房间的人员, 不管是不是不在线状态。
1. 如果要开视频电话，别人问你要不要视频电话，要么直接发起视频电话或说完"好"以后就等那边建立会话。而不要说完"好"以后等5秒你也开始建立会话，这样就会导致你们同时建立会话，而造成连不上的问题。


#### Google Docs

1. Never use a Google Doc / Presentations for something non-confidential that has to end up on the website or the **handbook**. Work on these edits via commits to a merge request. Then link to the merge request or diff to present the change to people. This prevents a duplication of effort and/or an out of date handbook.
1. If you _do_ need a Google Doc, create one with your company G Suite (formerly Google
Apps) account. By default, share it with the whole company using the _Anyone at GitLab can find and access_ link sharing permission
and the _Anyone within GitLab can edit_ access permission (preferred) or the _Anyone within GitLab can comment_ access permission.
Easily do this by creating Google Docs within a Shared Folder in Google Drive.
1. When referring to a Google Doc in the handbook, refrain from directly linking it. Instead, indicate the name of the doc.
(In the past, linking a Google Doc has led to inadvertently opening the sharing settings beyond what was intended.)
This also helps prevent spam from people outside GitLab requesting accessing to a doc when clicking its link.
1. If you are having trouble finding a shared Google Doc, make sure you [Search &lt;your domain&gt;](https://support.google.com/a/answer/3187967?hl=en) in Google Drive.
1. In our handbook, if you find yourself wondering whether it is better to provide a public link to a Google Doc vs. writing out the content on the website, use the following guideline: Is this document frequently adapted / customized? If yes, then provide a link, making sure that the document can be _commented on_ by _anyone_ with the link. For instance, this is how we share our employment [contracts](/handbook/contracts/). If the document is rarely customized, then provide the content directly on the site and deprecate the Google Doc.

#### Video Chats

1. Use video calls if you find yourself going back and forth in an issue/via email
or over chat. Rule of thumb: if you have gone back and forth 3 times, it's time
for a video call.
1. Having pets, children, significant others, friends, and family visible during
video chats is encouraged. If they are human, ask them to wave at your remote
team member to say "Hi".

#### Say Thanks

1. Thank people that did a great job in our "Thanks" chat channel. If someone is
a team member just @ mention them. If multiple people were working on something
try mentioning each person by "@name". "Thanks everyone" does not say much.
1. To thank someone who is not a team member, mention your manager, our People Ops Coordinator, the name of the person, a quirky gift
and link to their work. For example, "@manager, @peopleopscoordinator: Joe deserves a lawnmower for _link_".
With your manager's blessing, the People Ops Coordinator will approach the person in question for their address saying we want to send
some swag. We'll ship it in gift wrap with "Thanks for your great work on _link_, love
from @gitlab".
1. Don't thank the CEO or other executives for something that the company paid for, thank GitLab instead.

#### 不知道去哪？(Not sure where to go?)

如果有些事情想讨论，但觉得和你的主管或经理讨论都不太合适，你可以直接联系任何你觉得合适讨论的人。

### 工作流

#### 所有的事情开始于建立issue(事务、工单、问题)

1. 要干任何事前都要 **建立** 一个issue。如果这个事情值得花时间做，那么就值得花一点时间建立一个issue，这样的话，其他人就可以知道你在干啥，并且帮助你。你可以根据事情的进展随时修改描述或者关闭这个issue。
1. 如果有人提出了功能提升的建议，那么就想办法找找有没有哪个issue和他们的建议相似，或者建立一个新issue。然后找他们看能不能把改进建议提交到这个issue上。
1. 双链接issues 会造成内部混乱，导致无法给reporters汇报。例如xxx......如果你不负责汇报，请不要关闭这个issue，而是重新指派这个issue。**Double link** issues to prevent internal confusion and us failing to report back to the reporters. For example, open an issue with a link to ZenDesk and close the issue with a copy of the response. Or add "Report: " lines to the description with links to relevant issues and feature requests and ensure they are closed and note this with a comment. If you are not responsible for reporting back please do not close an issue, instead re-assign it.
1. 如果两个issue相关，则给他们建立一个 **交叉链接** (在相关的两个issue上都建立对方的链接)。 做法是：在两个issue的最顶端放上链接，并对他们之间的关系进行简短描述(报告或其他东西)。 如果不止两个issues，将一个issue当作中心issue，并建立把所有issue的交叉连接都连到这个issue上。
1. 在讨论完功能后，一定要把达成的共识或结论 **更新到issue中** 。 这样才更容易看到这个issue的状态。 并且每个包括没有一起讨论的人，以后都可以根据这个更新内容来实现功能。 而且可以避免混乱和再次讨论。
1. 提交 **最小的**工作项是比较合理的。 创建issue时，尽可能地描述一个比较小的修补程序(可以比较快完成)。 针对不同的issues提出改进建议，并将它们联系起来。 如果要写文档或说明，请首先提交一个最多20行的合并请求。
1. 不要让issues打开以后好长时间没人管，issues应该是 **可操作** 和 **可实现** 的。 如果被指派一个issue但没时间去做，请将它指派给其他人。
1. 要有意识地 **优先** 考虑你的工作。 每项工作的优先级取决于多个因素： 有没有团队成员在等候回答？ 这个工作延迟以后的影响是什么？ 有多少人被这事影响？ 有没有其他方面的影响？ 这个是详细的[Engineering Workflow](../engineering/workflow)。
1. 使用公共issue跟踪页面，来跟踪所有的事情。每个项目都有各自相关的issue跟踪页面。
1. 选择目前 **里程碑** 中的issues进行工作。例如：[milestone](https://gitlab.com/groups/gitlab-org/milestones).
1. 一般情况下尽量不指派issues，让大家在里程碑中 **自己选issues**。
1. 如果准备做哪个issue，那么就先指派给自己。 但不要晚于你开始工作的时间。 如果完成了这个issue的一部分，并且需要其他人再做下一步工作，那么就 **重新指派** 这个issue给那个人。
1. 在重新指派一个issue前，要确保issue中有最新的进展信息。 issue的内容应该是 **唯一正确的信息来源**。
1. 在处理一个issue时，尽量 **寻求同事的反馈** 例如：如果你是设计师，并且提出了一个设计，让一个同事复查(review)一下你的设计。如果他们赞同了，那么就可以进行下一步工作了。如果提出了建议，你就有机会提升你的设计了。 这样促进了协作，提升了每个人的技能。
1. 我们信守 **诺言**，但不达成 **内部共识** 就不对外许诺言。
1. 在一个issue **[完成][d-o-d]** 前，不允许关闭它。
1. 在 **关闭** 一个issue时，提交一个说明解释一下为什么关闭这个issue。

[d-o-d]: ../engineering/development/CONTRIBUTING.md#definition-of-done

#### 使用合并请求来实现一个功能(Implement it with a merge request)

给贡献者编制的合并请求的指南请参考：[Contribution guide][mr-guidelines].

给评审者和维护人员编制的代码评审指南请参考： [Code Review Guidelines][code-review-guidelines].

下面是给公司内人员的额外的指南:

1. 在开始某项工作的时候，即使还有些事情没完成，可以先提交一个 **先行** 的合并请求来把工作内容分享出来，这样大家就可以尽早提交和避免返工。 提交这个没完成的合并请求时，在合并请求的标题前加一个 **[WIP(Work In Progress)]前缀** 这样的话这个没完工的合并请求就不会被意外的合并进主线了。WIP相关内容可以参考： **[Work In Progress](https://about.gitlab.com/2016/01/08/feature-highlight-wip/)**
1. 如果还有后续的工作(比如给客户反馈或编写文档)，请在提交合并请求的时候不要选择自动关闭issue。
1. 如果 __你__ 完成了一个合并请求，请去掉issue上的WIP前缀。 然后根据 [Code Review Guidelines][code-review-guidelines] 进行代码评审.
1. 在去掉“WIP”前缀后也可以根据反馈来修改内容，去掉“WIP”只是说明主体工作已经完成。

[mr-guidelines]: ../engineering/development/CONTRIBUTING.md#merge-request-guidelines
[code-review-guidelines]: ../engineering/development/code_review.md

### Team Call

1. Schedule
   * PST: <span id="main-PST"></span>
   * UTC: <span id="main-UTC"></span>
   * <span id="main-abbr"></span>: <span id="main-USER"></span>
1. APAC schedule
   * PST: <span id="apac-PST"></span>
   * UTC: <span id="apac-UTC"></span>
   * <span id="apac-abbr"></span>: <span id="apac-USER"></span>
1. Everyone at GitLab is invited to the team call.
1. There is an additional makeup team call on Fridays where anyone who missed their weekend update can share what they have been up to. Optionally, team members can share an update if they feel so inclined. Please add your name to the list for that day. 
1. We also have a team call for GitLabbers in the APAC region to share their weekend update. This call will also be recorded so the rest of the team can see what their colleagues have been up to! Everyone is encouraged to join this call as well, but it is not mandatory.
1. Every last Friday of the month we have an AMA to talk about anything our team is thinking about.
1. We use [Zoom](https://zoom.us) for the call since Google Hangouts is capped at 15 people (please be sure to mute your microphone). The link is in the calendar invite and also listed at the top of the team agenda Google Doc called _Team Agenda_.
1. The call is recorded automatically, and all calls are transferred every hour to a Google Drive folder called "GitLab Videos". There is a subfolder called "GitLab Team Call", which is accessible to all users with a GitLab.com e-mail account.
1. We start on time and will not wait for people.
1. The person who has the first item on the agenda starts the call.
1. If you are unable to attend just add your name to the team agenda as "Not attending".
1. We start by discussing the subjects that are on the agenda for today.
   * Everyone is free to add subjects. Please start with your name and be sure to link to an issue, merge request or commit if it is relevant.
   * When done with a point mention the subject of the next item and hand over to the next person.
   * When someone passes the call to you, no need to say, “Can you hear me?” Just begin talking. If we can’t hear you, we’ll let you know.
1. New team members should connect to their first team call 10 minutes before the call starts to make sure Zoom, your camera, and your microphone are all working properly. The new team member's manager will introduce them and ask the following questions: "Tell us about where you were before GitLab, why you wanted to join our team, and what you like to do in your spare time."
1. We ask 15-20 people per day to share updates about the most exciting thing from your past or upcoming week/weekend. If anyone has something they'd like to talk about, last person in the list will ask the group if they have anything else to share.
   * The team agenda lists who is meant to speak on which day; this can be altered daily if conflicts arise.
   * There is no need to excuse yourself with "I didn't do anything interesting", "I just watched television" or "That's all". It is not a competition. Instead share the most interesting detail, for example what television show you watched, book you are reading, video game you played or what recipe you cooked.
1. The sequence of asking people is in a random order where each team member is assigned a day. Since we are growing rapidly, GitLabbers share their weekend update every two weeks. Days are split into group A and group B, which alternates depending on the week. People Ops will denote on the agenda which group will share that day. New GitLabbers will share every week for the first three months on Wednesdays. If there are non-team page people in the call we end with those.
1. It is OK to talk over people or interrupt people to ask questions, cheer for them or show your compassion. This to encourage more conversation and feedback in the call.
1. Please look if the person you hand over to is present in the participant list so you don't hand over to someone who is not present.
1. The last person wishes everyone a good day.
1. Even if you cannot join the call, consider reviewing the recorded call or at minimum read through the team agenda and the links from there. We often use the team call to make announcements or discuss changes in processes, so make sure to catch up on the news if you have missed a team call (or more).

### 发布回顾和启动(Release Retrospectives and Kickoffs)
{: #kickoffs}

在每月22号发布完新版本后，我们要在下一个工作日进行一个30分钟的会议，反思一下我们哪些方面可以做的更好:

1. 这个月什么事情比较顺利?
2. 这个月出了什么问题?
3. 什么事情我们可以做的更好?

在回顾会议上，第一部分是对上个月的工作项进行回顾。

在回顾会议完成后，就立即进入启动会议环节。 产品团队和其他领导已经进行了一些讨论，内容是使用“meta”作为标签的issue：[meta issue on the GitLab.com CE tracker](https://gitlab.com/gitlab-org/gitlab-ce/issues?scope=all&state=opened&label_name=meta)。 这些issue是每个发布版本中要优先做的工作。 这个启动会议的目的是统一所有人对工作状况的了解，并对issue进行评论。

启动会议和回顾会议完成后，他们的录像和笔记会发布到共享服务器上以便查阅。

### Random Chat and Room
{: #random-room}

1. 公司或部门的微信群中可以分享一些灵光一闪的想法、图片、文章或其他内容。 如果需要让脑子休息一下可以到这些频道去逛逛。
1. 只要加了公司微信群的话，就可以到这些地方逛逛：公司微信群、部门微信群。

### 安排会议(Scheduling Meetings)

1. 如果需要确认某个人是否有时间开会，请通过公司邮箱的日历功能给相关人员发送约会。 这样可以更简单的确认他们是否有空并且将这个会议安排到他们的工作日历上。 即使没有打开邮件，这个会议在他们的日历上也会自动显示出来。 根据每个人对会议邀请的出席反馈就可以简单的确认每个人的状态。 请尽快回复开会的邀请以便邀请人安排工作计划。
1. 每个预定好的会议，都应该有相关PPT或文档的链接。 如果是文档，则需要一个议程表，表内包含所有准备好的(可以展示的)材料。 给每个参会人共享一份可以编辑的议程表。 在会议邀请中写入这个文档链接。 大家要在会议期间记录要点和待办事项。 因为在事后没有人愿意再去写一个会议记录，这有助于组织思维过程，而且每个人都能对记录做出贡献。 因为能够实时构造结论和跟进行动，使用视频通话比亲自开会更有效。 如果是重要到要开会的事情，那么提供一个文档也是很重要的。 如果要大家保持同步，那么大家就应该看同一份文档。
1. 如果需要外部人员开会，请先给内部人员通过日历发约会邀请，等他们恢复 **同意** 后再邀请外部人员。
1. 当安排与多个人会议时，请使用自己的日历或专人来邀请他们，这样日历项就不会(不必要的)出现在其他人的日历上。
1. 如果需要调整会议，不要通过其他途径进行调整，而是直接调整日历上的日历项即可。请将变更内容写到描述的最顶端。
1. 请选择'Guests can modify event'项， 这样大家都可以通过调整日历上的时间来进行变更，避免了通过其他途径来说明变更情况。
1. 如果只是和某个人开会请使用[Calendly](#calendly).
1. When scheduling a meeting we value people's time and prefer the "speedy meetings" setting in our Google Calendar. This gives us meetings of, for example, 25 or 50  minutes leaving some time to write notes etc before continuing to our next call or meeting. (This setting can be found under the calendar Settings menu at "default event duration")
1. When creating a calendar event that will be used company wide, please place it on the GitLab Availability Calendar. That way the event is easily located by all individuals.
1. 如果需要取消/拒绝一个会议，一定要在删除/拒绝会议时选择 **Delete & update guests** 确保每个人都能知晓你不能出席并且不用等候你了。

### Video Calls

1. For smaller meetings we use Google Hangouts or [Appear.in](https://appear.in/), for larger meetings we prefer [Zoom](https://gitlab.zoom.us/) (Google Hangouts technical limit is 15 for scheduled meetings).
1. For meetings that are scheduled via calendar there is automatically a Google Hangout URL added, this is the meeting place. Having a url in advance is much more reliable than trying to call via hangouts as the meeting start.
1. Google Calendar also has a [Zoom plugin](https://chrome.google.com/webstore/detail/zoom-scheduler/kgjfgplpablkjnlkjmjdecgdpfankdle?hl=en-US) where you can easily add a Zoom link for a videocall to the invite
1. For meetings that are scheduled with Zoom, make sure to take out the Google Hangout link to avoid confusion.
   1. If you need more privileges on Zoom (longer meeting times, more people in the meeting, etc.), please contact People Ops as described [specifically for Zoom](/handbook/tools-and-tips/#sts=Zoom).
   1. Note that if you select to record meetings to the cloud (setting within Zoom), they will be automatically placed in the GitLab Videos folder in Google Drive; on an hourly basis. You can find these videos in Google Drive by entering in the search bar: `title:"GitLab Videos" source:domain`.
   1. Note also that after a meeting ends, Zoom may take some to process the recording before it is actually available. The sync to Google Drive happens on the hour mark, so if the recording is not available, it may take another hour to be transferred.
1. Use a headset with a microphone, [Apple Earpods](http://www.apple.com/shop/product/MD827LL/A/apple-earpods-with-remote-and-mic) are great. Do not use computer speakers, they cause an echo. Do not use your computer microphone, it accentuates background noise. If you want to use your [Bose headphones](https://www.bose.com/en_us/products/headphones/over_ear_headphones/quietcomfort-25-acoustic-noise-cancelling-headphones-apple-devices.html#v=qc25_black) that is fine but please ensure the microphone is active.
1. Consider using a utility to easily mute/unmute yourself, see [Shush](#shush) in the tools section.
1. In video calls everyone should own camera and headset, even when they are in the same room. This helps to see the person that is talking clearly on the camera and their name in the list. It also allows people to easily talk and mute themselves. And using a headset prevents an echoing. You wouldn't share an office seat together, don't share your virtual seat at the table.

### 用户沟通指南(User Communication Guidelines)

1. 保持谈话积极、友好、真诚和具有建设性的同时增加价值。
1. 如果犯错了，就承认错误。 要诚实的和快速的改正。 就像你发了一个有问题的博客，你会去更改以前发布的内容，只要改好了就行。
1. 坦率的交换意见和争论之间只有一线之隔，试着在不会激怒别人的情况下表达你写的东西是欢迎不同观点的。不需要回应每个批评和坏话，请小心并且考虑周到的沟通。
1. 回答问题时，也要对那些只写了几个字的人表示感谢。要确保双向沟通。
1. 对别人提出的建议和反馈应心存感激。
1. 无法实现的诺言请不要轻易承诺。
1. 给予寻求帮助的人以指导，并且给他们建议和提供链接。 促进每个人进行开放的开发[Improving Open Development for Everyone](https://about.gitlab.com/2015/12/16/improving-open-development-for-everyone/), [Types of requests](https://about.gitlab.com/2014/12/08/explaining-gitlab-bugs/).
1. 面对负面的评论，要有耐心的反馈并且要将每个人视作单独的个体，最有意见的人可以变成最坚定的支持者。 [the strongest supporters](https://about.gitlab.com/2015/05/20/gitlab-gitorious-free-software/).

### 写作风格指南(Writing Style Guidelines)

1. {: #简体中文} 在公司中, 简体中文是标准协作语言，也可以配合一定量的英文。
1. 不要使用富文本(word文档一类的文本)，因为这些文本复制粘贴到其他地方就会变形。 使用 [Markdown](../product/technical-writing/markdown-guide/index.html.md) 在git中存储文档。 如果使用MS Word，则在Word中使用默认文档的风格中的各类风格，粘贴时请不要带格式粘贴。
1. 在英文中，不要使用全部大写的文字，因为看起来好像在喊叫。
1. 在一行结尾使用windows style换行(crlf)而不是用Unix style换行(lf)或者Mac style换行(cr)，请确保 `*.md text eol=crlf` 写在代码库的 `.gitattributes` 中并且在客户端中运行 `git config --global core.autocrlf input`。
1. 不要建立一个链接命名为“点这”。 所有的连接都应该有一个相关的文本来描述链接的东西，例如： "CI资源安装文档".
1. 在所有书写的文档和法律文书中使用 [ISO日期格式](https://en.wikipedia.org/wiki/ISO_8601#Calendar_dates)。 其他的格式[会造成误解](http://xkcd.com/1179/)，所以使用 `yyyy-mm-dd`，例如：2015-04-13, 不要用04-13-2015、13-04-2015或2015/04/13。
1. 如果在评论或邮件中有多个观点，请给他们编号以便更容易针对性回复。
1. 当引用一个issue、合并请求、评论、页面、文档或其他东西，并且有对应链接，请把链接粘贴到引用处。
1. 在编写链接的时候，用连字符比用下划线好，并且链接中使用英文小写字母。 尽量不要在链接中使用中文，就算是用中文也不要使用转码后的中文，应该使用原始中文文字。
1. The community include users, contributors, core team members, customers, people working for GitLab Inc., and friends of GitLab. If you want to refer to 'people not working for GitLab Inc.' just say that and don't use the word community. If you want to refer to people working for GitLab Inc. you can also use 'the GitLab Inc. team' but don't use the 'GitLab Inc. employees'.
1. When we refer to the GitLab community excluding GitLabbers please say 'wider community' instead of 'community'.
1. All people working for GitLab the company are the [GitLab team](https://about.gitlab.com/team/), we also have the [Core team](https://about.gitlab.com/core-team/) that consists of volunteers.
1. Please always refer to GitLab Inc. people as GitLabbers, not employees.
1. Use inclusive and gender-neutral language in all writing. So for example, write "they, their" instead "he, his".
1. Always write GitLab with a capitalized G and L, even when writing GitLab.com.
1. Always capitalize the names of GitLab [features](https://about.gitlab.com/features/)
1. Do not use a hyphen when writing the term "open source."
1. 货币中不应该只有一位小数，所以写成 $19.90 比 $19.9 更好。
1. 如果邮件需要回复，请在邮件顶端写明回复要求。
1. Use the future version of words, just like we don't write internet with a capital anymore, we write frontend and webhook without a hyphen or space.
1. Our homepage is https://about.gitlab.com/ (with the `about.` and with `https`).
1. Try to use the [active voice](https://writing.wisc.edu/Handbook/CCS_activevoice.html) whenever possible.
1. Please refer to self-hosted installations as on-premises, not on-premise.
1. 如果使用标题格式 (`##` in Markdown, Word中的"标题 2")，使用第二级标题，因为第一级是给主题使用的。不要在标题末尾使用冒号。
1. Always use an [Oxford comma](https://en.wikipedia.org/wiki/Serial_comma) in lists of three or more terms.
1. Always use a single space between sentences rather than two.
1. 写文档前先读一下我们的 [文档风格指南](../engineering/development/doc_styleguide.md)。
1. 不要使用首字母缩写，要不然别人可能就不知道你到底要说什么，比如：不要用 `MR` 而是写 `merge request`。
2. 我们将客户/愿景分为4段 [战略,巨大的,中端市场和中小企业](../sales/index.html.md#market-segmentation).

### Beamy Guidelines

Beamy is our company conference call robot. It lives in the San Francisco Howard St. office.
Its main purpose is to allow those outside of the office a view into the space and people.
When you call in to the beam your face will appear on the screen (so make sure your webcam
works) and you can drive the robot around the office. It simulates being in the space without
physically being there. It is really cool and everyone should try it and have fun with it.

* You need an invite email to connect and to download a desktop client, please @mention Emily in the #general channel if you don't have the invite yet.
* **Beamy times**: 8am until 6pm Pacific time. [Please check the current time!](https://time.is/San_Francisco) on workdays and during all company events, for other times please @mention Sytse in the Slack #valley channel to see if it is OK. It is on auto connect so you'll beam right in.
* The email invite will come from "Suitable Tech". Once you are sent an invite you can beam in at any time and drive around our beam. Don’t forget to park it back on the charger when you are done. You can do so by driving up to the charger, when you see a green outline press AND HOLD 'p' until it's parked. Make sure it is charging, otherwise try again.
* If you don't use headphones be careful about your volume and microphone placement, it might start singing, if so immediately mute your microphone and switch to headphones.
* More info can be found at https://www.suitabletech.com/
* Please report any questions or issues you have about the beam in the Slack #peopleops channel.

### Company phone number
{: #phone-number}

If you need to provide the details of GitLab's contact information you can take the [address of the office](https://about.gitlab.com/visiting/) for reference; or the [mailing address](https://about.gitlab.com/handbook/people-operations/#addresses) of the office in the Netherlands if that is more applicable.

If a phone number is required, leave this field empty by default. If that is not possible, then use
the general number (+1-415-761-1791), but be aware that this number simply guides to a voice message that refers the caller back to contacting us via email.