---
layout: markdown_page
title: "Vacancies"
---

## On this page
{:.no_toc}

- TOC
{:toc}

## Vacancy Creation Process

If you want to hire for a position please [make a description of the role](#vacancy-creation-process),
get [approval for the role](#vacancy-creation-process), and ensure there is a
[vacancy](#vacancy-creation-process) on our jobs page before we start interviewing.
A description helps you vet candidates accurately. Opening it up helps people find us.

Your Executive Team member must escalate and obtain authorization for any new
job positions/searches if they are not part of the Hiring Forecast (search for
an internal Google sheet by that name on Google Drive). Typically the Executive
Team member escalates to the CFO and/or the CEO. Roles listed on the
Hiring Forecast will have a status of Open, Closed, Filled, Draining, or Pending
Approval which are defined below:

* Open - vacancy is open and we are actively sourcing and hiring for the role
* Closed - no vacancy, not actively sourcing or hiring for the role
* Filled - vacancy has been filled by internal or external candidate
* Draining - vacancy is closed, no longer accepting new applicants, but will review existing candidates through the hiring process and fill the role if a qualified candidate is identified from existing applicants
* Pending Approval - vacancy has been suggested by executive team member and is pending board, CEO, or CFO approval.

1. Hiring manager identifies the need for a new or replacement team member and contacts the People Ops Generalist to review their strategic hiring plan. If the role is deemed necessary, the team will follow the following steps to open the vacancy for applicants.
1. If a description of the role does not already exist, the hiring manager will create a vacancy description and assign the MR to the People Ops Generalist and tag the Recruiter.
    1. Create the relevant page in `https://about.gitlab.com/jobs/[name-of-job]`, being sure to use only lower case in naming your directory if it doesn't already exist. If the location of the applicant is important, then the location and a compensation range corresponding to that location can be provided as part of the vacancy posting.
1. A Recruiter will use a this [gender decoder](http://gender-decoder.katmatfield.com/) to ensure that the language and structure of the vacancy description is gender neutral. The recruiter will make necessary edits to the vacancy description to create a neutral description.
1. Once a vacancy description exists, hiring managers should update the [Vacancy Requisition Document](https://docs.google.com/a/gitlab.com/spreadsheets/d/12VgxbGXshbbvqtDd2Tg_P9ETAwB82JEa6F6WAJwdV2U/edit?usp=sharing) with the proposed vacancy. Once every column is completed for the role, assign the line item to your People Ops Business Partner (either Generalist or Chief Culture Officer) through the comments. If the role is not already in the hiring forecast, the Business Partner will assign the line item to the CFO/CEO for final approval.
1. After final approval, the People Ops Generalist pings the People Ops Specialist to propose an appropriate NYC benchmark compensation for the role, and they submit the proposal to the [compensation committee](/handbook/people-operations/global-compensation/#compensation-committee) for approval.
   - For any position, filling in the NYC benchmark salary in the `jobs.yml` file will automatically cause the [Compensation Calculator](/handbook/people-operations/global-compensation) to show at the bottom of the position description page.
   - For some positions, it may be possible or desirable to exclusively seek candidates outside of higher cost regions. This is a role by role decision between the Hiring Manager and People Operations. _If_ it is decided to seek candidates outside of higher cost regions, then that needs to be explicitly communicated on the position description page in order to set fair expectations for candidates and recruiters alike. Sample text to consider placing on the position description page: "Globally, xx % of people live in metro areas with a rent index greater than yy, while at GitLab, this is zz % of people in this role currently. Therefore, in line with our value of staying [frugal](/handbook/values), we are now focusing on only hiring in metro areas with a **rent index lower than yy**. Please bear this in mind when using the compensation calculator below." (obviously, fill in the missing numbers).
1. Once the salary benchmark has been determined and posting have been approved, a Recruiter will create the position in [Lever](https://hire.lever.co/jobs), using the exact same job title. If this step is completed out of order, people are able to apply even though the position posting may not have been approved yet.
   * In Lever, click "Create Job Posting" in top right corner.
   * For location, select a specific timezone or "Remote".
   * For department/team, select the appropriate team.
   * For work type, choose full-time or intern.
   * Under "Job Posting Status" you can choose whether this job will be published upon creation, kept internal, or a draft.
   * For the description, copy and paste from the position description on Gitlab.com.
   * Indicate what applicants need to provide with their application. By default, this will include their resumé, a cover letter, but it may also include qualifying questions such as "What timezone are you in?".
   * Once finished, click "Create Posting". If you chose "published" under "Job Posting Status", the job will become live on our jobs page.
   * Add the URL to the application form into the merge request for the `data/jobs.yml` file.
   1. In the [`data/jobs.yml`](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/data/jobs.yml) file, open the position or add a new entry for it. When someone views the vacancy description page, an "Apply" button will be shown for that position if we're currently hiring for it.
     - Adding a new role: add an entry with the following format:

       ```
       - title: "Chief Happiness Officer"
         description: /jobs/chief-happiness-officer/
         salary:
         apply: https://jobs.lever.co/gitlab/12345-123-1234-1234-123456789
         open: true
       ```

     - Opening an existing position: If the position is already listed in the `jobs.yml` file but not "open", simply change `open: false` to `open: true` to have the position appear on the [listings](/jobs/).
     - Closing an existing position: If we're no longer hiring for a particular position change `open: true` to `open: false` for that position to hide it from the listings.
     - Note: You can leave the apply Lever link blank until you have created it (see instructions below).
 1. As soon as the posting is live on our website, People Ops will announce it on the next team call, post it in the `#general` chat channel and on Twitter. Also consider the additional [advertising methods](#publicize-the-job) below as a means to communicate the open position to a desired audience.
 1. All job openings must be posted on our careers page for at least 5 business days before we can make an offer; this includes all new positions and [promotions](/handbook/people-operations/#promotions).

## Publicize the job

The manager should always ask the team for passive referrals for open positions. GitLab team members can refer candidates through our [referral program](/handbook/incentives/#referral-bonuses)

The employment team will **always** publicize the job through the following means:

1. Announce it on team call and on the #general chat channel.
1. Tweet the new job post with the help of the content marketing manager and team.
1. Request "soft” referrals by encouraging all GitLab team members to post links to the jobs site on their LinkedIn profiles.

**Note**: The employment team will advertise the job through the following sites:

1. [PowerToFly](https://www.powertofly.com) Helping us connect with 100k+ women in tech
1. [Hacker News Who's Hiring](https://news.ycombinator.com/ask): On the first of the month, include a note for GitLab in the Hacker News thread of "Who's Hiring" . Template text:
`REMOTE ONLY GitLab - We're hiring production engineers, developers, designers, and more, see https://about.gitlab.com/jobs/ We're a remote only company so everyone can participate and contribute equally. GitLab Community Edition is an open-source Ruby on Rails project with over 1000 contributors.`
1. [Hacker News Jobs](https://news.ycombinator.com/jobs) as a Y Combinator alumni we can post directly to the front page. The EA vault has credentials so ask an EA to post. Template text: `GitLab (YC W15) is hiring XXX and more - Remote Only`
1. [WeWorkRemotely](https://weworkremotely.com) ($200 for 30 days, per position).
1. [RemoteOK](https://remoteok.io) ($200 for 90 days, per position)
1. [RemoteBase](https://remotebase.io/) (Free. Job descriptions are synced directly to our respective job description sites)
1. [StackOverflow](http://stackoverflow.com/jobs) (Able to post 3 jobs simultaneously, please mention to employment team if you want your role listed here)
1. [Indeed Prime](http://www.indeed.com/) (Primarily used for non-engineering roles)

### Sourcing for Open Positions

On difficult or hard-to-fill positions, the employment team will use available tools to source for additional candidates. Please communicate with the employment team if sourcing is needed for a strategic, specialized, or difficult to fill position.

## Closing a vacancy

To close a vacancy:

1. The employment team will clear the pipeline of candidates in all stages of application. Consider adding tags to candidates who were interesting but were passed over in this hiring process. Adding tags makes it easier to find them in Lever later on if you are recruiting for the same or a similar position.
1. Ask a Lever admin (People Ops) to close the position in Lever.
1. The employment team will create a merge request, in which you remove the application URL for Lever, and set the listing flag in the `jobs.yml` file to `open: false`. See ["vacancy creation process"](#vacancy-creation-process) for reference).

If the position was posted on any job site (i.e. Stack Overflow, PowerToFly) the employment team will email the partner or remove the position from that site.
