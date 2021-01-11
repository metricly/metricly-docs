---
title: "Create Budget Alerts"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#aws services", "#cost", "#getting started", "#guides", "#azure"]
author: Lawrence
weight: 5
---

Budget Alerts can be set in the Bill Analysis tool using a combination of:

- Saved reports
- Send Daily Email
- Matching Conditions

{{% notice tip %}}
Read the guide on [creating AWS Bill Analysis reports](/billing-analysis/ba-guides/how-to-create-monthly-cost-reports) or [creating Azure Bill Analysis reports](/billing-analysis/ba-guides/how-to-create-monthly-cost-reports/#azure-bill-analysis-report)
{{% /notice %}}


## AWS Practice

Create a daily Budget Alert of cost deltas above $5 for _EC2 - Other Usage Types_.

1. Navigate to **Cost Management** > [**Bill Analysis**](https://us.cloudwisdom.virtana.com/#/reports/awscostall/latest).
2. Select **Quick ranges** > **Latest day**.
3. Select **CONFIGURE**.
4. Select the **EC2 - Other** service.
5. Group By **Usage Type**.
6. Add a **Matching Condition** of `Any Group Delta > 5`.

## Azure Practice

Create a daily Budget Alert of cost deltas above $5 for all services.

1.  Navigate to **Cost Management** > [**Azure Bill Analysis**](https://us.cloudwisdom.virtana.com/#/reports/azure-bill).
2.  Select **Quick ranges** > **Latest day**.
3.  Select **CONFIGURE**.
4.  Group by **Service Name**.
5.  Add a **Matching Condition** of `Any Group Delta > 5`.
