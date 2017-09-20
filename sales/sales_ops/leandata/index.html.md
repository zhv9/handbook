---
layout: markdown_page
title: "LeanData"
---

---
## On this page
{:.no_toc}

- TOC
{:toc}

---

## LeanData

### What is LeanData?

LeanData enables strategic lead management within Salesforce so leads are assigned to the right reps. This is done by leveraging LeanData's fuzzy logic algorithms and lead-matching database. Whether we introduce a sales process based on named accounts, geographic territories, employee size (or all of the above), LeanData allows us to easily manage seemingly complex lead assignment rules.

### How It Works

LeanData is made up of three primary solutions: Lead/Account Matching, Lead Routing Rules, and Cross-Object Visibility.

#### Lead/Account Matching

The primary feature for LeanData is matching leads to accounts using a number of different criteria: company name, email address, and IP address. If a new lead is created in Salesforce, LeanData will review the criteria to determine if it matches an existing account in the system and will deliver the lead to the correct user as per our defined lead routing rules. Note that our matching criteria will include both the company information and region.

#### Lead Routing Rules

Our lead routing rules are as follows:

1. Any lead created within a region that matches an account that is an existing customer will be routed to the account owner. For instance, if a lead for the Acme Company in the UK is created and there is an existing account for Acme Company in France that is an existing customer, the lead will be assigned to the account owner. If a lead for the Acme Company in New York is created, it will not be assigned to the account owner as this record is not in the same region as the existing account (US East vs. EMEA).
1. Any lead created within a region that matches an account that is not a customer, but has an open opportunity, will be routed to the account owner. For instance, if a lead for Acme Company in the UK is created and there is an existing prospect account for Acme Company in France that that has an open opportunity, the lead will be assigned to the account owner.
1. Any lead created within a region that matches a lead will be routed to the lead owner. If the Acme Company has a lead in the UK and a lead in the US, and a new lead for Acme Company is created for France, the lead will be routed to the owner of the Acme Company UK lead.
1. Any new lead created for Federal prospects in the United States will be routed directly to our Federal Team, regardless of sales segmentation or lead source, unless the lead matches an account owned by a non-Federal AE, in which case, the either the first or second rule will apply.
1. Any lead created that does not match an account or matches an account without an open opportunity will be routed via our routing rules by sales segmentation, region, and lead source.
  * All Strategic leads will be assigned to the Strategic AE Round Robin by Region.
  * Large Contact Requests will be assigned to the Large AE Round Robin by Region. All other lead sources for Large prospects will be assigned via the BDR Round Robin rule by Region.
  * Mid-Market Contact Requests will be assigned to the Mid-Market AE Round Robin by Region. All other lead sources for Mid-Market prospects will be assigned via the regional BDR Round Robin Queue.
  * All SMB leads will be assigned via the BDR Round Robin by Region.

#### Cross-Object Visibility

One of the most widely-known issues with the Salesforce architecture is the lack of relationship between the lead and account/contact objects. LeanData addresses this lack of functionality. A user can be in an account record and see all related lead records. Within the lead object, a user can view all related leads and accounts. 

**LeanData from the Account Page**
 ![](/source/handbook/sales/sales_ops/leandata/leandata-contact.png)

* Merging a Duplicate Account
  * At this time, this feature is not supported. Please send a note via Chatter on the record you would like merged: "Please merge this account with `<URL of original account>`."

* Converting a Lead from the Account Page
  * Click on the "Convert" link for the lead you would like to add to the Account.
  * You can assign the contact to yourself or another user.
  * The account name will default to the account record you were just on. If you want to create a new account, select the "Create New Account" option.
  * "Do not create a new opportunity upon conversion" is defaulted to TRUE. If you want to create a new opportunity, uncheck this box.
  * Click the "Convert" button.

**LeanData from the Lead Page**
 ![](/source/handbook/sales/sales_ops/leandata/leandata-lead.png)
 
 * Merging a Duplicate Lead
  * Before you merge, please visit a Salesforce article regarding merging leads, ["Considerations for Merging Duplicate Leads"](https://help.salesforce.com/articleView?id=leads_merge_considerations.htm&type=0&language=en_US).
  * Click on the "Merge" link for the lead you would like to merge to the current Lead.
  * Select one lead as the “Master Record.” The created date, created by, and read-only fields will retain information from the Master Record.
  * Select the fields that you want to retain from each record.
  * Click "Merge".
  * Click "OK".
 
 * Converting a Lead from the Lead Page
  * Click on the "Convert" link for the lead you would like to add to the Account.
  * You can assign the contact to yourself or another user.
  * The account name will default to the account record you were just on. If you want to create a new account, select the "Create New Account" option.
  * "Do not create a new opportunity upon conversion" is defaulted to TRUE. If you want to create a new opportunity, uncheck this box.
  * Click the "Convert" button.

