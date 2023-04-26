---
title: 'Measuring Success: A Deep Dive into SaaS Revenue Metrics - Part 2'
author: Oz Guner
date: '2023-04-25'
slug: saas-revenue-metrics-part2
categories:
  - class notes
tags:
  - revenue
  - metrics
  - goal-setting
subtitle: 'ACV, TCV, ARR, and MRR'
excerpt: 'Distinguishing between recurring and non-recurring revenue is crucial.'
summary: ''
draft: no
series: ~
layout: single-sidebar
---
*This series was inspired by Sara Archer’s “SaaS Metrics Fundamentals” class on [Pavilion](https://www.joinpavilion.com/pavilion-university).*

In [our previous post](blog/2023/04/19/saas-revenue-metrics-part1/), we explored bookings and billings. This post will deal with ACV, TCV, ARR, and MRR and their subtle differences. The post will use the same case study as Part 1:

> *For simplicity, we'll assume that we recently built our niche SaaS business: an inventory
management system for small and mid-sized boat retailers. We picked up the phone and we
won our first client, **Swell Boats, Inc.** We closed-won that opportunity in our CRM, and we
sent out a contract to Swell Boats. The terms of this agreement, dated January 15, dictate that
Swell Boats pay €12,000 per year to our business for 3 years. We will charge Swell a one-time
€5,000 for set up and training.*

### Total Contract Value (TCV)
TCV represents the total value of a customer's contract over the contract's agreed lifetime. TCV will include *all revenue* that a customer's contract generates, including *recurring* and *one-time* charges. In our case, we have €12,000 * 3 = €36,000 in total bookings recurring yearly and €5,000 in services and consulting bookings as a one-time fee. Therefore, TCV is:

`$$\text{€}36,000 + \text{€}5,000 = \underline{\underline{\text{€}41,000}}$$`

### Annual Contract Value (ACV)
ACV is the annualized version of any TCV. Divide TCV by the number of years in the contract and you will find ACV. In our case, our TCV is `\(€41,000\)`. Therefore, the ACV is:

`$$\text{€}41,000 / 3 = \underline{\underline{\text{€}13,667}}$$`
Note that ACV, like TCV, will include **all revenue** that a contract generates, not only the recurring portion. This point is often missed.

### Annual Recurring Revenue (ARR)
ARR is a revenue metric that only takes the annualized *recurring* revenue into account and leaves one-off charges such as services or irregular consulting fees out. As mentioned above, the difference between ARR and ACV is that ACV includes non-recurring revenue while ARR does not. Some SaaS companies might also refer to the ARR as "Software ACV" since the annual contract value of software would typically represent ARR. If, however, you have annual recurring revenue from services, workshops, or maintenance, you should include them in the ARR portion. In our case, the ARR would be the annualized version of our recurring software revenue:
`$$\text{€}36,000 / 3 = \underline{\underline{\text{€}12,000}}$$`
The difference between ACV and the ARR could have rather big implications in businesses where services and one-off fees make up a considerable portion of the revenue.
### Monthly Recurring Revenue (MRR)
MRR is the monthly recurring portion of ARR. No matter in what frequency your company gets paid, you can calculate MRR by dividing the ARR by 12 or calculate ARR by multiplying MRR by 12. In our case, the MRR would be:
`$$\text{€}12,000 / 12 = \underline{\underline{\text{€}1,000}}$$`
These metrics will need some custom calculations using billing data. The single source of truth for ACV, TCV, ARR, and MRR is your business intelligence software, such as Domo or Tableau. The raw data will come from the ERP software.

In the next part of this series, we will talk about how SaaS companies recognize revenue and collect cash.
