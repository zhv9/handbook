---
layout: markdown_page
title: "Content"
---

## On this page
* [Campaigns](#campaigns)
* [Campaign Brief Process](#campaignbrief)
* [Webcasts](#webcasts)

## Campaigns<a name="campaigns"></a>
Leadgen is responsible for executing marketing campaigns for GitLab.  We define a campaign as any programmed interaction with a user, customer, or prospect.  For each campaign, we will create a campaign brief that outlines the overall strategy, goals, and plans for the campaign.

## Campaign Brief Process<a name="campaignbrief"></a>
To create a campaign brief, first start with the [campaign brief template](https://docs.google.com/a/gitlab.com/document/d/1GttZqr7sjuvP9kWuIPfbif2b2VyNJtbN8CbL4tKJX2Q/edit?usp=sharing).  Fill out all fields in the brief as completely as possible.  Certain fields might not be applicable to a particular campaign.  For example, an email nurture campaign leveraging text based emails won’t have a visual design component.  This field can be left blank in that example.

Once the campaign brief is filled out, create an issue in the GitLab Marketing project and link to the campaign brief.

On the GitLab issue, make sure to:
* Tag all stakeholders
* Use the Marketing Campaign label
* Set the appropriate due date (the due date should be the campaign launch date)
* If there are specific deliverables, create a todo list in the issue description for each stakeholder along with a due date

## Webcasts<a name="webcasts"></a>

Webcasts are one the greatest tools we have to communicate with our audience.
GitLab webcasts aim to be informative, actionable, and interactive.

### Best Practices

1. Give yourself **at least** 15 days of promotion.
2. Send invitation emails 3 weeks out, 2 weeks out, 1 week out, and 2 hours before event.
3. Only send promotional emails Tuesday, Wednesday, or Thursday for optimal results.
4. Send reminder emails to registrants 1 week out, day before, and one hour before the event.
5. Host webcasts on a Wednesday or Thursday.
6. Post links to additional, related resources during the event.
7. Include "contact us" information at the end of the presentation.
8. Send the recording to all registrants, whether they attended or not.
9. Publish a post-webcast blog post capturing some key insights to encourage on-demand registrations.
10. Add webcast to the GitLab resources page.

### Speaker Approval

The Lead Generation team depends on GitLab's subject matter experts to deliver webcast presentations. However, we must ensure that
when we ask a speaker to participate on a webcast that the work is approved. Please use the following process when asking someone outside of marketing
to participate on a webcast.

1. Have an abstract of the content prepared before asking for a presenter.
2. Send the abstract to both the proposed speaker and their manager to review. **A speaker is not considered booked unless they have approval from their manager.**
3. Address and resolve any concerns regarding the abstract.
4. Once the manager approves and the speaker accepts, you can move forward with the webcast.

### Tips for Speakers

Here are some basic tips to help ensure that you have a good experience preparing for and presenting on a webcast.

#### Before committing
Ask us any questions you have about the time commitment etc. and what exactly our expectations are. Talk about it with your manager if you're on the fence about your availability, bandwidth, or interest. Make sure you're both on the same page. We want this to be a meaningful professional development exercise for you, not a favor to us that you're lukewarm about — if you feel that way, none of will be able to do our best job. We'll be honest with you, so please do the same for us.

#### Before the dry run
Select and set up your presentation space. Pick a spot with good wifi, and we recommend setting up an external mic for better audio quality, although this is optional. If you will be presenting from your home, alert your spouse/roommates of the time/date & ask them to be out of the house if necessary. Depending on your preferences and comfort level with public speaking, run through the script several times.

#### Before the presentation
Try to get a good sleep the night before, and, if the presentation is in the morning, wake up early enough to run through your notes at least once. Review our [Positioning FAQ](https://about.gitlab.com/handbook/positioning-faq/), or keep the page handy in case you are asked in the Q&A about how GitLab compares to our competitors.

### Logistical set-up

1. Create webcast in Zoom
   - Make sure the registration confirmation email and the reminder emails are set to send from Zoom. As Zoom implements their more robust Marketo integration, we will send from Marketo, but for now we need to send from Zoom to ensure that the correct unique link is sent to registrants.
1. Create the webcast program in Marketo
   - Title the webcast in the following format: `YYYYMMDD_{Webcast Title}`. For example, 20170418_MovingToGit
1. Update `My Tokens` at the webcast program level
   - DO NOT UPDATE THE `apiKey` or `apiSecret`. These should be the same for every webcast
   - Update the `{{my.zoomWebinarId}}` token with the webinar ID from the Zoom webcast created in step 1
   - Update the add to calendar tokens
      - Copy the Google Calendar link from the webinar page on Zoom
      - Update the information in the iCal and Outlook calendar files (these will be identical)
   - Update the event date and time
   - Update the email body with the description of the webcast
1. Turn on smart campaigns in Marketo
   - Activate the `Zoom Attended` campaign
   - Activate the `Webcast_Registered` campaign
   - Activate the `Registered From Zoom` campaign
   - Schedule the `Zoom Absent Attendees` campaign to run after the webcast will be finished (give the campaign a few hour buffer minimum)
1. Set up Marketo integration within Zoom
   - Log in to Zoom, and select the webcast from the `Webinars` tab
   - Scroll down and click on the `Integration` tab
   - Click `Edit` next to `Generate Leads in Marketo`
   - Turn on `Send registration information to a Smart Campaign` and select the `Registered From Zoom` smart campaign for the proper webcast program
   - Turn on `Send attendee information to a Smart Campaign` and select the `Zoom Attended` smart campaign for the proper webcast program
   - Select the `ZoomWebinarOtherInfo` custom object, check the following boxes, and select the corresponding Marketo Custom Object Fields:
      - Webinar ID
      - Webinar Topic
      - Q&A
      - Poll
1. Edit the landing page to have the appropriate webcast description, date, and time.
