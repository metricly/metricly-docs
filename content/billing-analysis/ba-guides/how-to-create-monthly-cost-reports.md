---
title: "Create a Monthly Cost Reports"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#aws services", "#cost", "#getting started", "guides"]
author: Lawrence Lane  
weight: 1
---

To use the Billing Analysis tool, login to Metricly and navigate to **Cost Management** > **Billing Analysis**.


## Create and Save a Monthly Total Cost Report

Let’s say you want to explore a breakdown of your bill across AWS Availability Zones for the past month (30 days). How would you do that?

1. Select **Latest 30 days** in the _Quick ranges_ dropdown.
2. Select **CONFIGURE** to open the configuration modal.
3. Select **Stacked View** for the visualization, as we aren’t looking to compare periods in this report. Stacked View also allows you to see a color-coded breakdown of spend which is useful later.
4. Don’t choose a filter for this report. We want to see everything to get a high-level view of our costs.
5. For the _Group By_ dropdown, select **Availability Zone**.
6. **Apply** the configuration to view the report.

Your report might look something like this:

![monthly-cost-img-1](/images/how-to-create-monthly-cost-reports/monthly-cost-img-1.png)

Notice the NoAZ bar is substantially higher. Curious why? Hover over the bar for a line-itemed breakdown, like so:

![monthly-cost-img-2](/images/how-to-create-monthly-cost-reports/monthly-cost-img-2.png)

Let’s save this report by selecting **SAVE**.

Name your report so that it’s clear what kind of data should be expected. At this point you can provide an email — either your own, or a shared email (like to your team) and enable **Send Daily Email** updates. Email updates can be turned off later by editing the saved report.

![monthly-cost-img-3](/images/how-to-create-monthly-cost-reports/monthly-cost-img-3.png)

## Practice
EC2 - Other is a large spending category for many AWS users. Let’s take what you learned from the above and create a report that breaks that spending down more.

### Configuration Settings
- **Quick Range**: `Latest 30 Days`
- **Visualization**: `Stacked View`
- **Filter**: `Service >  EC2 - Other`
- **Other**: `Group By > Usage Type`
- **Other**: `Limit > 10`

Your Configuration modal should look like this:

![monthly-cost-img-4](/images/how-to-create-monthly-cost-reports/monthly-cost-img-4.png)

### Result
Now you can see a breakdown of _EC2 - Other spend by Usage Type_.

![monthly-cost-img-5](/images/how-to-create-monthly-cost-reports/monthly-cost-img-5.png)

You can contextualize this data even further by using Period Comparisons. Using a Period Comparison allows you to see whether your spending is increasing or decreasing over time across different dimensions. Below is a Period Comparison for the report you just made.

![monthly-cost-img-6](/images/how-to-create-monthly-cost-reports/monthly-cost-img-6.png)

It’s helpful to save various reports that slice your billing data using different dimensions and levels of granularity so that you can discover cost trends, cost deltas, and highlight saving success over time. Go ahead and save this report too, as it’s a great base for exploring cost deltas.
