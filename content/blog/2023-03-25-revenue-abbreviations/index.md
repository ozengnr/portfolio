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
excerpt: 'SaaS has no shortage of abbreviations to measure revenue. In the end, the whole point is to allow us to employ imperfect analysis for decision making.'
draft: yes
series: ~
layout: single
---

## A Bit of History

In the central forum of ancient Rome stands a Roman monument known as the *Milliarium Aureum*, or golden milestone, which was erected by Emperor Caesar Augustus. It served as the starting point for measuring all distances in the Roman Empire and was regarded as the site from which all principal roads diverged. 

![Milliarium Aureum. Source: Wikimedia Commons](img/featured.jpg)

## Back to Business

Just as all roads led to the *Milliarium Aureum*, so too does every business eventually lead to revenue. Revenue is the ultimate destination and measurement of success for any business, and for Software-as-a-Service (SaaS) companies, there are several key revenue metrics that serve as essential markers on the road to success. In this series, we will explore these SaaS revenue metrics in detail and provide a clear understanding of what they mean and how they can be used to evaluate the performance of a SaaS business.

##### Bookings
For simplicity, we'll assume that we just built our very niche SaaS business: an inventory management system for small and mid-sized boat retailers. We picked up the phone and we seem to be about to win our first client, Swell Boats, Inc. We closed-won that opportunity in our newly built sleek CRM and we sent out an agreement to Swell. At this point, the only thing that we got is commitment to spend money. A letter of intent. An agreement. Something waiting to be signed. In the end, we recorded a **booking**. The paid version of the software and its benefits is not yet provided to the customer.

##### Total Contract Value (TCV)
The terms of this agreement, dated January 15, dictate that Swell pay `\(€12,000\)` per year to our business upfront for 3 years. We will charge Swell an additional `\(€5,000\)` for initial set up and training. In total, we have a `\(€12,000 \times 3 = €36,000\)` in total bookings recurring yearly and `\(€5,000\)` services and consulting bookings, resulting in a Total Contract Value (TCV) of 

`$$€36,000 + €5,000 = \underline{\underline{€41,000}}$$`
##### Annual Contract Value (ACV)
ACV is quite literally the annualized version of any TCV. In our case, our TCV is `\(\€41,000\)`. Therefore, our ACV will be 
`$$€41,000 \div 3 = \underline{\underline{€13,667}}$$`. 

##### Annual Recurring Revenue (ARR)
Another metric that is widely used but is often confused with ACV. ARR only takes the *recurring* revenue into account and naturally leaves one-off charges such as services or irregular consulting fees out. Some SaaS companies might also refer to this as "Software ACV" since annual contract value of a software would typically represent Annual Recurring Revenue. In our case, the ARR would be:

`$$€36,000 / 3 = \underline{\underline{€12,000}}$$`.

##### Monthly Recurring Revenue (MRR)
Monthly recurring revenue shares the same characteristic as ACV in terms of its relationship to the annual metric, ARR. MRR is the monthly recurring portion of ARR. Remember that no matter in what frequency your company gets paid, you can calculate MRR by dividing the ARR in 12, or calculate ARR by multiplying MRR by 12. After all, these metrics are indicators of revenue and growth rather than the cash in the bank. In our case, the MRR would be:

`$$€36,000 / 3 = \underline{\underline{€12,000}}$$`


At this point, here is how that will show up in the report of our system of records. The deal was won on January 15 and will therefore be booked on January bookings with a $1200 annual contract value: 

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
   <td style="text-align:left;"> Swell Boats Inc - ACV Bookings ($) </td>
   <td style="text-align:right;"> 1200 </td>
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



And this is how it would look like in our business intelligence systems (if we have one - *heh heh*):

<img src="{{< blogdown/postref >}}index_files/figure-html/bar chart-1.png" width="672" />

At this point, it's important to remember that we are billing our client yearly. Typical SaaS contracts are billed annually upfront. This will result in deferred revenue balance of the amount billed. In our case,  **Therefore, our billings, no matter the frequency and the terms, will be booked on our deferred revenue.** This point is important because we have not yet recognized revenue, provided services, or received cas in the bank. If we get paid monthly, we will wind down that deferred revenue balance by `\(\frac{1}{12}\)`. 
