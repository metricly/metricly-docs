---
title: "Explore Cost Deltas"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#aws services", "#cost", "#getting started", "#guides", "#azure"]
author: Lawrence
weight: 2
---

## AWS Bill Analysis Report

Cost deltas are noticeable rises in resource cost discovered when comparing two distinct time periods in your AWS billing history. Measuring your cost deltas against the average application workload cost is a great way to discover opportunities to save.

{{% notice tip %}}
Read the guide on [creating budget alerts](/billing-analysis/ba-guides/how-to-create-budget-alerts/) before using this guide.
{{% /notice %}}

In the [previous guide][1], we created a Bill Analysis report that displays _EC2 - Other_ costs from the Latest 30 Days broken down by Usage Type. This kind of report is an excellent view for discovering cost deltas when changing the visualization from Stacked View to Period Comparison View.

Let’s open that saved report you created.

1. Navigate to **Cost Management** > [**Bill Analysis**](https://us.cloudwisdom.virtana.com/#/reports/awscostall/latest).
2. Select the **Report** dropdown and choose your saved report.

![explore-cost-deltas-img1](/images/how-to-explore-cost-deltas/explore-cost-deltas-img1.png)

Now we are going to update the **Quick range** to `Latest 3 Months`. Doing this gives you a larger frame of reference for spending trends. Here we can identify our larger cost deltas.

![explore-cost-deltas-img2](/images/how-to-explore-cost-deltas/explore-cost-deltas-img2.png)

## Sorting and Filtering

Sorting the data by **Delta %** is a quick way of finding the largest changes percentage wise. The initial results, however, need to be contextualized with some additional filter criteria otherwise you can get less helpful charts like this:

![explore-cost-deltas-img3](/images/how-to-explore-cost-deltas/explore-cost-deltas-img3.png)

None of the information highlighted in this screenshot is incredibly helpful. Let’s filter out some of the noise by setting a Matching Condition in the configuration modal.



1. Select **CONFIGURE**.
2. Navigate to _part 4, Matching Conditions_. Select **Any Group Comparison Cost**  > `Amount` (in this case, `500`).
![explore-cost-deltas-img4](/images/how-to-explore-cost-deltas/explore-cost-deltas-img4.png)
3. Add a second Matching Condition. Select **Any Group Delta % >** `100`.
4. **Apply** the changes.

By doing this you can find more significant deltas across your _EC2 - Other Usage Types_. The data returned shows any cost by Usage Type which is more than $500 and has at least doubled (%100 delta minimum) over the course of the past 3 months.

![explore-cost-deltas-img5](/images/how-to-explore-cost-deltas/explore-cost-deltas-img5.png)

[1]: /billing-analysis/ba-guides/how-to-create-monthly-cost-reports/#practice

## Azure Bill Analysis Report

Cost deltas are noticeable rises in resource cost discovered when comparing two distinct time periods in your Azure billing history. Measuring your cost deltas against the average application workload cost is a great way to discover opportunities to save.

{{% notice tip %}} Read the guide on [creating Azure budget alerts](/billing-analysis/ba-guides/how-to-create-budget-alerts/#azure-practice) before using this guide.
{{% /notice %}}

In the [previous guide](/billing-analysis/ba-guides/how-to-create-budget-alerts/), we created a Bill Analysis report that displays storage costs from the Latest 30 Days broken down by product. This kind of report is an excellent view for discovering cost deltas when changing the visualization from Stacked View to Period Comparison View.

Let's open that saved report you created.

1.  Navigate to **Cost Management** \> [**Azure Bill Analysis**](https://us.cloudwisdom.virtana.com/#/reports/azure-bill).

2.  Select the **Report** dropdown and choose your saved report.

Now we are going to update the **Quick range** to `Latest 3 Months`. Doing this gives you a larger frame of reference for spending trends. Here we can identify our larger cost deltas for each of the storage products.

![azurecostdelta1](images/how-to-explore-cost-deltas/azurecostdelta1.png)

## Sorting and Filtering

Sorting the data by **Delta %** is a quick way of finding the largest changes percentage wise. The initial results, however, need to be contextualized with some additional filter criteria otherwise you can get less helpful charts like this:

![azurecostdelta2](images/how-to-explore-cost-deltas/azurecostdelta2.png)

To make the data more meaningful, let's filter the report to display only cost deltas that exceed a threshold. We'll use the Matching Condition in the configuration modal.

1.  Select **CONFIGURE**.

2.  Navigate to part 4, Matching Conditions. Select **Any Group Delta** \> `10`).

    ![azurecostdelta3.png](images/how-to-explore-cost-deltas/azurecostdelta3.png)

3.  **Apply** the changes.

By doing this you can find more significant deltas across your storage. The data returned shows any cost by product which is 10% or higher over the course of the past 3 months.

![azurecostdelta4](images/how-to-explore-cost-deltas/azurecostdelta4.png)
