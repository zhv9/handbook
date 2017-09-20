---
layout: markdown_page
title: "Accounts Receivable and Cash"
---

## On this page
{:.no_toc}

- TOC
{:toc}


## Accounts Receivable
<a name="ar"></a>

### Invoicing

1. Log in to Zuora and Salesforce.
1. In Salesforce, click the "+" icon and select "Z-Quotes".
1. Subscriptions to be invoiced are sorted by date. Choose a subscription from today's date and proceed.
1. Still in Salesforce, check the customer account for a current PO number under the notes and attachments.
1. Then in Zuora, search for the corresponding customer subscription and open the record.
1. Check to see if the PO from the file in Salesforce matches that of Zuora. If not, update the record in Zuora with the latest PO number.
1. Verify that the "Bill to" and "Sold to" contacts listed in the Zuora customer record match the related record in Salesforce. If not, update Zuora.
1. Verify that the payment terms and method listed in Zuora match the related record in Salesforce. If not, update Zuora.
1. In Zuora, scroll down to transactions and click "Create Bill Run."
1. It is important to find the subscription start date in Salesforce and enter it in the "Target Date for this bill run" field in Zuora. The invoice date should be today's date.
1. Once these dates agree, click "Create Bill Run."
1. On the following screen, select the bill run that was just created (the bill run files begin with BR- followed by a set of numbers).
1. Scroll down and click on the invoice that was just generated. The PDF file will be at the bottom of the page.
1. Open the PDF file and review every field of the invoice for accuracy.
1. Once the review is complete, close the invoice and click “Post Invoice.”
1. Proceed to bill the remaining subscriptions.

At this point the invoicing process is complete. Now, continue on to the Cash Receipt posting process for those invoices that were paid by credit card.

## Cash Receipt
<a name="cash-receipt"></a>

### Credit card customer

Follow this procedure if the customer paid by credit card.
You may recall from the invoicing process that there was still a balance due when saving the invoice.  The following steps will record the payment and remove the balance due.

1. Login to Stripe dashboard and click on Payments under Transactions (left hand side). You will see a listing of the latest Stripe transactions listed by amount, Recurly transaction, name, date, and time. There is also an option to filter the report by clicking on XXX at the top left. Click on XXX to export to excel. This will give you a workbook area and also a breakdown of the fees which we will work on later.
1. In NetSuite, click on the "Transactions" tab on the left.
    * Click on the orange "OPEN INVOICES " tab. This will bring up all open invoices listed by date, invoice #, customer, etc.
1. Match invoice #s  between the Stripe dashboard and NetSuite. If you click on a transaction in the Stripe dashboard, it will take you to a screen that shows more detail, including the invoice # being paid. You can work your way from the bottom up.
1. In NetSuite, click "Receive Payment" on the matched payment and invoice.
1.  Receiving the payment
    * Enter the payment date, which is the payment date from Stripe dashboard.
    * Payment method = Credit Card.
    * Reference no. = "Recurly Transaction ID:" found under Metadata in Stripe dashboard.
    * Deposit to = Stripe.
    * NetSuite will auto-fill the payment amount with the entire balance due. No need to change this unless the payment amount from Stripe is different.
    * Click on "Save and Close".
    * Repeat the above for all the remaining invoices that were paid by credit card.

1. Post a journal entry to record Stripe Fees.
    * In NetSuite, click on the "+" sign. Under "Other", select "Journal Entry".
    * It is okay to leave the journal date as long as it is within the month the fees were incurred. If not, change it to the last day of the month.
    * NetSuite will auto fill the journal number. Do not change.
    * Account #1 Entry
      * Fill the "Account #1" entry with "Credit Card Transaction fees".
      * Fill the "Debits" entry with the value from the Stripe report that was exported. The value will be the sum of "Column I" in the Stripe report, which is the fee amount. Be sure to only sum the rows which you just posted payments for.
      * Leave the "Credits" entry empty.
      * Fill the "Description" entry with "To record credit card transaction fees for period (enter the date range for the transactions posted)".
      * Leave the "Name" entry empty.
      * Fill the "Class" entry with "Sales".
    * Account #2 Entry
      * Fill the "Account #2" entry with "Stripe".
      * Leave the "Debits" entry empty.
      * The "Credits" entry will autofill. This should be the same amount as the "Debits" entry for Account #1.
      * The "Description" entry will autofill. This should be the same as the "Description" entry for Account #1.
      * Leave the "Name" entry blank.
      * Leave the "Class" entry blank.
      * Click "Save".

This transaction transfers the payment obligation from the customer to Stripe.  The payment obligation from Stripe is removed when Stripe transfers  the funds to GitLab's bank account.

### Posting a payment from Stripe when a transfer is received from Stripe.

Post a journal entry:
1. Fill the "Journal Date" with the date that payment was received in the bank.
1. Fill the "Credit Account" with Stripe.
1. Fill the "Debit Account" with "Comerica Checking - GitLab Inc."
1. Leave "Name" blank.
1. Leave "Class" blank.
1. Fill the "Description" with "To record Stripe transfer (date of transfer)".
1. Click "Save".


### Posting a payment from a “bank customer”

In Netsuite:
1. Click on the “+” sign.
1. Click on “Receive Payment” under Customers.
1. Fill the "Payment Date" with the date payment was received.
1. Fill the "Payment Method" choose from the dropdown menu.
1. Fill the "Reference No." with the check # or bank reference # from incoming wire.
1. Fill the "Deposit to" with "Comerica Checking".
1. Fill the "Amount Received" with the amount received from the incoming wire.