---
layout: markdown_page
title: "Analytics"
---

Finance has the company wide responsibility for analytics.
Examples of the types of metrics we want to track are below per department.

## Cross department metrics

Cross department metrics are essential to measure our [journeys](/handbook/journeys).

## Department metrics

### Sales

1. Incremental ACV
1. ARR
1. TCV
1. ARR
1. Renewal rate
1. Win rate and time for every sale stage and the overall process.
1. Time to close
1. Pipeline created
1. Pipeline Requirement Projection
1. [Sales efficiency (above 0.8)](http://tomtunguz.com/magic-numbers/)
1. [Pipeline coverage (above 3)](https://pipetop.com/saas-glossary/sales-terms/sales-pipeline-coverage/)
1. Up-sell (EES to EEP, EEP to EEU)
1. Average deal size

### Peopleops

1. Inbound applications per week
1. Interviews per applicant
1. eNPS score of team members
1. Applicant score per requirement and value
1. Declined applicant NPS score
1. Offer accept rate
1. Accepted offers/hires
1. Cycle time (apply to accepted offer)
1. Terminations (Voluntary regrettable, Voluntary PIP, Involuntary)
1. Share of people on PIPs

### Marketing

1. Visitors to the website
1. Downloads
1. MQL
1. SQL
1. Blended CAC
1. Program spend / Total spend (above 0.5)
1. Conversion percentages, cycle time, and CAC per channel
1. New contributers from the wider community per release/month

### Engineering

1. Merge requests (total, community, ours)
1. Cycle time
1. Time to review
1. Bug fixes (cherry-picks into stable)

### Finance

1. Order to cash time
1. Runway (above 12 months)
1. [40 rule (above 40%)](http://www.feld.com/archives/2015/02/rule-40-healthy-saas-company.html)
1. [Magic number (above 0.7)](https://davidcummings.org/2009/09/21/saas-magic-number/)

### Product

1. A/B test new features
1. Money made with new features
1. Re-tweets for release tweet
1. Usage per feature
1. Usage stats
1. Bottlenecks to increased customer sophistication

Many of the metrics you would normally track outside of the product we collect inside of the product so it is also useful to our self hosted users. This includes cohort analytics, conversational development analytics, and cycle time analytics.

### Data sources

1. Salesforce
1. Zuora
1. Marketo
1. Zendesk
1. NetSuite
1. Mailchimp
1. Google Analytics
1. Discover.org
1. Lever
1. GitLab version check
1. GitLab usage ping
1. [GitLab.com](https://about.gitlab.com/handbook/engineering/workflow/#getting-data-about-gitlabcom)

We want a single data warehouse and a central data model. We bring all relevant data to single storage place. Make it platform agnostic, so for example do not build it into Salesforce. We want to build data model to be used consistently across tools and teams. For example something as simple as unique customer ID, product or feature names/codes.

On the other hand we're open to pragmatic solutions linking for example Salesforce and Zendesk, if there are boring solutions available we'll adopt them instead of creating our own.

### Tools

These are still to be decided, some suggestions below.

1. Ingestion/ETL: Fivetran, Alooma, [Segment and Looker](https://looker.com/blog/segment-and-looker), [StitchData](https://www.stitchdata.com/) (open source), Snaplogic
1. Warehouse: BigQuery
1. Display/analytics: Looker, Redash, [Superset](https://github.com/airbnb/superset) (Apache open source), Tableau, or Metabase (open source)
