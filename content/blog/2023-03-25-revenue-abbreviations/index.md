---
title: Revenue Abbreviations - What's the Difference?
author: Oz Guner
date: '2023-03-25'
slug: revenue-abbreviations
categories:
  - revenue
  - metrics
  - class notes
tags:
  - arr
  - mrr
  - revenue
  - cash
  - acv
  - tcv
subtitle: ''
excerpt: 'SaaS has no shortage of abbreviations to measure revenue. At the end, the whole point is to allow us to employ imperfect analysis for decision making.'
draft: yes
series: ~
layout: single
thumbnail: '/img/featured.jpg'
---


In the central forum of ancient Rome stands a Roman monument known as the *Milliarium Aureum*, or golden milestone, which was erected by Emperor Caesar Augustus. It served as the starting point for measuring all distances in the Roman Empire and was regarded as the site from which all principal roads diverged. 

![Milliarium Aureum. Source: Wikimedia Commons](img/featured.jpg)


Just as all roads led to the *Milliarium Aureum*, all roads in SaaS leads to revenue. It is the ultimate destination and measurement of success for any business. For SaaS businesses, there are several key revenue metrics that serve as essential markers on the road to success. In this series, we will explore these revenue metrics in detail and provide a clear understanding of what they mean and how they can be used to evaluate the performance of a SaaS business.

In this article, we'll go over some of the metrics that are used predominantly across the industry. A lot of abbreviations have been thrown around; these ones seem to have stuck the most so far.

##### The Agreement
For simplicity, we'll assume that we just built our very niche SaaS business: an inventory management system for small and mid-sized boat retailers. We picked up the phone and we seem to be about to win our first client, **Swell Boats, Inc.** We closed-won that opportunity in our newly built sleek CRM and we sent out an agreement to Swell. The terms of this agreement, dated January 15, dictate that Swell pay `\(€12,000\)` per year to our business upfront for 3 years. We will charge Swell a one-time additional `\(€5,000\)` for set up and training. We are now waiting for Swell to sign this contract.

##### Bookings
At this point, the only thing that we got is commitment to spend money. A letter of intent. An agreement. Something waiting to be signed. In the end, we recorded a **booking**. The paid version of the software and its benefits is not yet provided to the customer. How businesses record bookings may differ slightly, but "first year bookings" seem to be typical across SaaS businesses. We will include them both here:

Our overall bookings are:

`$$€36,000 + €5,000 = \underline{\underline{€41,000}}$$`

Our first year bookings are 

`$$€12,000 + €5,000 = \underline{\underline{€17,000}}$$`
<table>
 <thead>
  <tr>
   <th style="text-align:left;"> Table </th>
   <th style="text-align:right;"> Jan </th>
   <th style="text-align:right;"> Feb </th>
   <th style="text-align:right;"> Mar </th>
   <th style="text-align:right;"> Apr </th>
   <th style="text-align:right;"> May </th>
   <th style="text-align:right;"> Jun </th>
   <th style="text-align:right;"> Jul </th>
   <th style="text-align:right;"> Aug </th>
   <th style="text-align:right;"> Sep </th>
   <th style="text-align:right;"> Oct </th>
   <th style="text-align:right;"> Nov </th>
   <th style="text-align:right;"> Dec </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> First Year Bookings (€) </td>
   <td style="text-align:right;"> 17000 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
</tbody>
</table>


The single-source-of-truth for bookings is your system of records, such as Salesforce.

##### Billings
Let's assume that Swell is really happy with the contract we sent out. They signed it the same day. This allows us to send over an invoice and actually bill the customer. Depending on the financial processes, the bookings and billings might happen at the same time or at different timeframes. Bookings is a forecasting metric that signifies a commitment from the customer. Billings is strictly an accounting metric and it signifies the money you are owed. While it's important not to get too bogged down in the weeds of the definitions, the difference between bookings and billings might be important: If you have customers from a variety of payment terms, the difference between bookings and billings might be bigger and vice versa. Moreover, the ownership within the organization might differ: Bookings might be owned by the in-house sales or analytics team while billings might exclusively be owned by Finance.

In our case, since the client will pay yearly, we will only bill for the Year 1 portion for now. The first year billings are

`$$€12,000 + €5,000 = \underline{\underline{€17,000}}$$`
The single-source-of-truth for billings is probably your system of records for quotes, such as Salesforce or ERP software such as Netsuite.

##### Total Contract Value (TCV)
TCV represents the total value of a customer's contract over the contract's initially agreed lifetime. TCV will include **all revenue** that is expected to be generated from a customer's contract, including recurring and one-time charges. In our case, we have a `\(€12,000 \times 3 = €36,000\)` in total bookings recurring yearly and `\(€5,000\)` services and consulting bookings as a one-time fee. 

Therefore, TCV is

`$$€36,000 + €5,000 = \underline{\underline{€41,000}}$$`

##### Annual Contract Value (ACV)
ACV is quite literally the annualized version of any TCV. Divide TCV in the number of years in the contract and you will find ACV. In our case, our TCV is `\(€41,000\)`. 

Therefore, the ACV is 
`$$€41,000 \div 3 = \underline{\underline{€13,667}}$$` 



Please note that ACV, just like TCV, will include **all revenue** to be generated from a contract; not just the recurring portion. This is an easily missed point. It may sound too academic, but the difference between ACV and the Annual Recurring Revenue could have rather big implications in businesses where services and one-off fees make up a considerable portion of the revenue.


##### Annual Recurring Revenue (ARR)
ARR is a revenue metric that only takes the annualized *recurring* revenue into account and leaves one-off charges such as services or irregular consulting fees out. As mentioned above, the difference between ARR and ACv is that ACV includes non-recurring revenue while ARR does not. Some SaaS companies might also refer to this as "Software ACV" since annual contract value of a software would typically represent Annual Recurring Revenue. If, however, you have annual recurring revenue from services, workshops, or maintenance, you should include them in the ARR portion. 

In our case, the ARR would be the annualized version of our recurring software revenue:

`$$€36,000 / 3 = \underline{\underline{€12,000}}$$`


##### Monthly Recurring Revenue (MRR)
Monthly recurring revenue shares the same characteristic as ACV in terms of its relationship to the annual metric, ARR. MRR is the monthly recurring portion of ARR. Remember that no matter in what frequency your company gets paid, you can calculate MRR by dividing the ARR in 12, or calculate ARR by multiplying MRR by 12. After all, these metrics are indicators of revenue and growth rather than the cash in the bank. 

In our case, the MRR would be

`$$€12,000 / 12 = \underline{\underline{€1,000}}$$`
The single-source-of-truth for ACV, TCV, ARR, and MRR is probably your business intelligence software, such as Domo or Tableau.

##### Recognized Revenue
We've now officially entered the accounting realm. Let's say that Swell signed the contract on January 15 and we enabled the software to the client. The day of the access to the paid features of the software marks the day of revenue recognition. Of course, in many SaaS businesses, the actual cash collection happens on an agreed timeframe (which could be 30, 60, or 90 days). Then, for accounting purposes, the recognized revenue that our company has not yet been paid for will be **deferred revenue**. It means that we will be getting paid later for the services that we provide now.

Typical SaaS contracts are billed annually upfront. This will result in deferred revenue balance of the amount billed. **Therefore, our billings, no matter the frequency and the terms, will be booked on our deferred revenue.** This point is important because we have not yet received the cash in the bank. If we get paid monthly, we will wind down that deferred revenue balance by `\(\frac{1}{12}\)`. If we get paid quarterly, we will do so by `\(\frac{1}{4}\)`. Or if we get paid yearly, then we will wind down our deferred revenue for the first year by `\(100\%\)`.

In our case, since we started the contract on January 15, the recognized revenue for the remainder of the month will be calculated by pro-rating for the remaining 16 days:

$$
\frac{€1,000}{31} \times 16 \approx €516
$$

And the recognized revenue for the remainder of the year will be calculated by pro-rating for the remaining 11 months:

$$
€1,000 \times 11 + €516 = €11,516
$$


##### Cash Collection (Revenue)
We're now at the last stage of our revenue journey: Revenue. This happens when we actually cash the check and it cleared in our bank account. This is the moment our bookings become "revenue". If we assume that Swell paid for all its first-year obligations in a single check, our cash in the bank will be:

`$$€12,000 + €5,000 = \underline{\underline{€17,000}}$$`

### Tracking Revenue Metrics

We want to be able to accurately track and monitor at least some of these metrics so that we can take action to nudge them in the right direction. 

At this point, here is how all of the work we've done will show up in the report of our system of records. Notice that the deal was won on January 15 and this will impact how numbers will appear in the table:


The single-source-of-truth for revenue is your Cloud ERP or business management software, such as Netsuite.

