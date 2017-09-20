---
layout: markdown_page
title: "Marketing Operations"
---
Welcome to the Marketing Operations Handbook.

[Up one level to the Marketing & Sales Development Handbook](https://about.gitlab.com/handbook/marketing/marketing-sales-development/)    

----

## On this page
* [Overview](#overview)
* [Marketing Tech Stack](#techstack)
* [Leads](#leads)  
* [Email Management](#email)
 

----


## Overview <a name="overview"></a>

Marketing Operations (Mktg OPS) supports the entire Marketing team as well as other teams within GitLab. Mktg OPS works closely with Sales Operations to ensure information between systems is seamless and we are using consistent terminology in respective systems. 	


## Marketing Tech Stack <a name="techstack"></a>

Our current marketing tech stack consists of the following tools: 
- Clearbit: Enrichment tool to add details to customer & prospect record to aide in sales process and overall database segmentation.
- DiscoverOrg: Industry specific data enrichment for leads/contacts/accounts
- FunnelCake: Buyer lifecycle and funnel analytics tool
- Google Analytics: Web analytics tool that tracks and reports website traffic
- Google Tag Manager: Tool to add/update website tags, incl. conversion tracking, site analytics, remarketing, without needing to edit website code
- InsideView: Lead enrichment tool
- Lean Data: Lead routing and account matching tool
- Marketo: Marketing automation and database management tool  
- Olark: Real-time chat function for customer engagement
- Outreach.io: Email communication tool for the BDR/SDR/AEs to manage communication with leads/contacts
- Piwik: Open source web analytics platform used to measure web performance
- Salesforce: Customer Relationship Management (CRM) tool used to manage all customer & prospect data
- Terminus: Account-based Marketing (ABM) advertising tool to drive B2B demand
- Unbounce: Custom landing page tool specific for driving conversions
- Zoom: Video and Web Conferencing tool used for webcasts and online demos

### [Tech stack contract details and admins](https://about.gitlab.com/handbook/marketing/marketing-sales-development/marketing-operations/contracts) 


## Leads <a name="leads"></a>  

Mktg OPS is responsible for setting up and maintaining the lead routing for all inbound leads and also managing the database. There are two main tools used for lead routing: Marketo for form fillouts, lead enrichment and scoring, and Lean Data for account matching and routing based on account type (customer, prospect, strategic, etc), region and sales segment.  

[Lead routing rules](https://about.gitlab.com/handbook/sales/sales_ops/leandata/#lead-routing-rules) can be found in the Sales Operation section of the handbook.

As leads are created they are scored based on a collection of demographic information, engagement and/or behavioural data. Once a lead reaches a score of 90 points or more they are considered a Marketing Qualified Lead (MQL). Currently there are two MQL buckets: (1) hand raisers (A leads) and (2) passive leads. Detailed information about the [Lead definition](https://about.gitlab.com/handbook/marketing/business-development/#mql) can be found in the Business Development section of the Handbook.    

The [MQL Scoring Model](https://docs.google.com/a/gitlab.com/document/d/1_kSxYGlIZNNyROLda7hieKsrbVtahd-RP6lU6y9gAIk/edit?usp=sharing) is based on a 100-point system. Positive and negative points are assigned to a lead based on their demographic and firmographic information, and their behaviour and/or engagement with the GitLab website and marketing campaigns.  
This model was implemented on 13 February 2017 and only impacted leads moving forward. For reporting purposes, it was decided not to retroactively adjust scores and MQL dates. 


## Email Management <a name="email"></a> 
Email database management is a core responsibility for Mktg OPS. Ensuring GitLab is following email best practices, in compliance with International spam laws and overall health of active database are all priorities.  


### Requesting an Email
To request an email, create an issue in Marketing and assign it to JJ Cordz and tagging Mitchell Wright (in addition to whomever else needs to be aware of email). Required request information, please be as complete as possible in providing detail related to the email:
- **Sender Name**: Typically we use GitLab Team for most outgoing communications; for Security Alerts we use GitLab Security. Choosing a name that is consistent with the type and/or content of email being sent is important, if unsure make a note and we will make recommendation  
- **Sender Email Address**: What email address should be used? [List of available email aliases](#emailalias)
- **Subject Line**: 50 character max is preferred 
- **Email Body Copy**: Can be a text snippet within issue, clearly identified comment on issue or attach a Google doc with copy 
- **Target Date to Send Email**: at a minimum a few days notice is preferred because we need to balancing the number of emails being sent to our database so they are not perceived (or marked) as spam; however, a simple email can be turned in a few hours if absolutely necessary
- **Recipient List**: Emails can be sent to one of the [existing segments](#emailsegment) or a recipient list can be provided as a .csv file


### Email Segments <a name="emailsegment"></a> 
Reoccuring database segments and how someone is subscribes to specific segment:  

- **Newsletter**: All users who sign up for a GitLab.com account are automatically added to this segment and users can subscribe to the newsletter through the blog, Contact Us page and CE download page.
- **Security Alerts**: Subscribe on the GitLab [Contact Us page](https://about.gitlab.com/contact/)
- **Webcasts**: When someone registers to a live or on-demand webcast
- **Live Events**: When someone registers to attend a live event, meet up or in-person training. Use of this segment is narrowed down by geolocation so notification and invitation emails are specific to related area.  



### Aliases <a name="emailalias"></a> 
Current list of email aliases used in Marketo to send email: 
- News@ company domain: external email address used to send newsletter. Replies go to Online Marketing Manager  
- SecurityAlerts@ company domain: external email address used to send security alerts. Replies go to Online Marketing Manager
- Webcasts@ company domain: external email address for sending webcast related emails. Replies go to Content Marketing Team and Online Marketing Manager
- Events@ company domain: external email address for sending live, VIP &amp; in-person training related emails. Replies go to Feild Marketing Manager and Marketing OPS Manager
- Community@ company domain: external email address for sending confirmation emails related to GitLab products. Replies are forwarded to Zen Desk support.
- Leads@ company domain: external email address for internal Lead alerts. Replies go to Marketing OPS Manager and Online Marketing Manager
- Support@ company domain: external email address for sending Breaking Change and/or support related customer communications. Replies go to Zen Desk support.


### Types of Email
**Breaking Change Emails**  
These are operation emails that can be sent on a very selective as needed basis. This is an operational-type email that overrides the unsubscribe and does not provide the opportunity for someone to opt-out. Usage example: GitLab Hosted billing change, Release update 9.0.0 changes, GitLab Page change and Old CI Runner clients. 
It is very important to have Engineering and/or Product team (whoever is requesting this type of email) help us narrow these announcements to the people that actually should be warned so we are communicating to a very specific targeted list. 


**Newsletter**  
Sent bi-monthly (every 2 weeks). Content Team is responsible for creating the content for each Newsletter.  


**Security Alerts**  
Sent on an as needed basis containing important information about any security patches, identified vulnerabilities, etc related to the GitLab platform. These emails are purely text based. 


**Webcasts**   
Invitation and/or notification emails sent about future webcasts.   


**Live Events**   
Invitation emails to attend a live event (VIP or Executive Lunch), meetup, or in-person training. These emails are sent to a geolocational subset of the overall segment. This type of email is also used when we are attending a conference and want to make people aware of any booth or event we may be holding and/or sponsoring.   


### Alert Emails   
Alert emails are sent directly to the Lead Owner on record. If Lead is owned by a Partner, the alert email is sent to the BDR Email Address on record.    
APAC & NCSA -> To: Molly Young, Kyla Gradin, Jameson Burton (evenly distributed)    
EMEA -> To: Conor Brady    
Federal -> To: Brent Caldwell; cc: Paul Almeida  

**New Trial Lead Alert**    
Sender: ALERT - Lead    
From Email/Reply-to: leads@    
Subject Line: Enterprise Premium Trial: {{lead.Last Name}} from {{company.Company Name}}   


**Contact Request**   
Sender: ALERT - Contact   
From Email/Reply-to: leads@      
Subject Line: Contact Sales Request: {{lead.Last Name}} from {{company.Company Name}}   


**Consultancy Request**   
Sender: ALERT - Consultancy   
From Email/Reply-to: leads@   
Subject Line: Consultancy Request: {{lead.Last Name}} from {{company.Company Name}}   


**Development Request**   
Sender: ALERT - Development    
From Email/Reply-to: leads@    
Subject Line: Development Request: {{lead.Last Name}} from {{company.Company Name}}   


**Federal Contact Sales Request**  
Sender: ALERT - Federal Contact  
From Email/Reply-to: leads@   
Subject Line: Federal Contact Sales: {{lead.Last Name}} from {{company.Company Name}}   


**New Lead MQL**  
Sender: ALERT - New MQL Lead  
From Email/Reply-to: leads@  
Subject Line: New MQL Lead: {{lead.Last Name}} from {{company.Company Name}}  


