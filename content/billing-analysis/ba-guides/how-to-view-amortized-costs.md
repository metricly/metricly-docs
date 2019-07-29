---
title: "View Amortized Costs"
#date: 2019-07-29
draft: false
categories:
tags: ["#tools", "#aws services", "#cost", "#getting started", "guides"]
author: Andrew Paine
weight: 3
---

When you purchase EC2 reservations with no upfront payment or partial upfront payment, the monthly installments appear as a single charge on the first day of each month:

![view-amortized-costs-img1](/images/how-to-view-amortized-costs/amortized-costs-img1.png)

This distorts the scale of the cost axis and makes it difficult to see spending trends.

Even worse, when you purchase EC2 reservations with Partial or All Upfront payment the upfront costs are recorded at the time they are charged rather than at the time of associated usage and they typically do not show up in the graphs at all. If the upfront payments were made during the time period of the report then the other EC2 usage costs can be so much lower than the reservation fees that they almost disappear from the chart.

The solution to this problem is to view **Amortized** costs. When the **Amortized** view is selected any upfront fees and monthly installments are distributed evenly across the reservation period:

![view-amortized-costs-img2](/images/how-to-view-amortized-costs/amortized-costs-img2.png)

To view the amortized costs:

1. Navigate to **Cost Management** > [**Billing Analysis**](https://app.metricly.com/#/reports/awscostall/latest).
2. Select **CONFIGURE**. A configuration modal appears.
3. Under _Show Costs As_ choose **Amortized**.
4. Select **Apply**.

## Unblended and Blended Costs
As well as  **Amortized** costs, you can also choose **Blended** (the default) and **Unblended** costs.
![view-amortized-costs-img3](/images/how-to-view-amortized-costs/amortized-costs-img3.png)

Blended and Unblended refer to different ways of incorporating reservation costs in **Consolidate Billing Accounts** where multiple AWS accounts are consolidated into a single billing account.

{{% notice tip %}}
If you only have one account or you do not have consolidated billing setup or you do not use reserved instance then the blended costs are the same as the unblended costs and are the simple usage costs.
{{% /notice %}}

**Unblended** costs are the sum of the applicateble rates times the usage for each AWS resource and represent the common understanding of incurred cost.

**Blended** costs attempt to present a fair allocation of RI costs across different accounts by taking into account the relative RI usage. The grand-total of blended costs always matches the unblended, simple total but the sub-totals allocated to each AWS account may differ according to relative RI usage by that account, so accounts that make more use of reserved instances will be allocated a higher proportion of the overall costs. This takes into account the fact that reserved instances purchases can be shared within consolidate accounts.

