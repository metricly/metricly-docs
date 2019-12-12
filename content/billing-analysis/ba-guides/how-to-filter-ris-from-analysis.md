---
title: "Filter RIs from Cost Analysis"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#aws services", "#cost", "#getting started", "guides"]
author: Dmitry Yashchenko
weight: 3
---
Getting an accurate picture of your entire AWS bill requires looking at your costs from multiple perspectives. Examining dimensions like AWS Services, Reservations, and Storage usage individually often gives you new insights you wouldn’t otherwise have viewing them together as a whole.

In this article, we’re going to show you how to filter out Reservations from your AWS Services Costs analysis. We want to do this because Reserved Instances have a unique pricing model in comparison to On-Demand instances. With Reserved Instances, you pay for the entire term regardless of actual use. To measure reserved instance application in your environment, check out the EC2 Cost tool instead.

{{% notice tip %}}
Read the guide on [creating budget alerts](/billing-analysis/ba-guides/how-to-create-monthly-cost-reports) before using this guide.
{{% /notice %}}



## Selecting Purchase Types  

Removing Reserved Instances from your AWS Cost analysis is easy thanks to the Purchase Type attribute. With this attribute, you can select the ones you want displayed.

1. Open the [Bill Analysis](https://us.cloudwisdom.virtana.com/#/reports/awscostall/latest) tool.
2. Choose a **Quick Range** (for example, 6 months).
![select-quick-range](/images/how-to-filter-ris-from-analysis/select-quick-range.png)
3. Select **CONFIGURE**. A configuration modal appears.
4. Choose your **Visualization**. In this case, we chose _Period Comparison_.
5. Choose a **Service**. In this case, we chose Elastic Compute Cloud - Compute.
6. Input _Purchase Type_ in in the **Attribute** field.
7. Choose **On Demand Instances** and **Spot Instances**.
![purchase-type](/images/how-to-filter-ris-from-analysis/purchase-type.png)
8. Choose a **Group By** dimension to gain more meaningful insights on your spend breakdown. In this example, we wanted to see a monthly period comparison on spend.
![group-by](/images/how-to-filter-ris-from-analysis/group-by.png)
9. Select **Apply**.  
