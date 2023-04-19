---
title: 'Measuring Success: A Deep Dive into SaaS Revenue Metrics - Part 3'
author: Oz Guner
date: '2023-04-21'
slug: saas-revenue-metrics-part3
categories:
  - class notes
tags:
  - revenue
  - metrics
subtitle: ''
excerpt: ''
draft: yes
series: ~
layout: single
---
### Recognized Revenue
Understanding how SaaS companies recognize revenue is important. Recognizing revenue happens when a critical value of a product is delivered to the software user. This could be a first log in, a first feature usage, or similar. **The day of provisioning the software access to the key value features marks the day of revenue recognition.** 

Let's assume that Swell Boats signed the contract on January 15 and we enabled the software for the client.  In many SaaS businesses, cash collection happens within an agreed timeframe. For accounting purposes, revenue that is recognized but has not been paid will be **deferred revenue**. It means that we will be getting paid later for the services that we provide now.

Typical SaaS contracts are billed annually upfront. This will result in a deferred revenue balance of the amount billed. **Therefore, billings, no matter the frequency and the terms, will be booked on the deferred revenue.** This is important because we have not yet received the cash in the bank. If we get paid monthly, we will wind down that deferred revenue balance by 1/12. If we get paid quarterly, we will do so by 1/4. Or if we get paid yearly, then we will wind down our deferred revenue for the first year by 100%.

In our case, since we started the contract on January 15, the recognized revenue for the remainder of the month will be calculated by pro-rating for the remaining 16 days:

`$$€1,000 / 31 {\text{ days}}\times16 {\text{ days}} = \underline{\underline{\text{€516}}}$$`
And the recognized revenue for the remainder of the year will be calculated by pro-rating for the remaining 11 months:


`$$(\text{€1,000} \times 11) + \text{€516} = \underline{\underline{\text{€11,516}}}$$`
The remaining `\(€484\)` will be recognized during the first 15 days of the last month (January of next year), totaling in `\(€12,000\)`. 

### Cash Collection
We're now at the last stage of our revenue journey: Cash. This happens when we actually cash the check and it is cleared into our bank account. If we assume that Swell Boats paid for all its first-year obligations in a single check, our cash in the bank will be:

`$$\text{€}12,000 + \text{€}5,000 = \underline{\underline{\text{€}17,000}}$$`
### Conclusion
While these are some of the most typical revenue metrics used across the industry, there may
be many more ways to look at revenue and growth from a quantitative perspective. The goal of
this blog is to provide some entry-level information to revenue analysts and sales teams, and I
hope it will help clear some questions.
