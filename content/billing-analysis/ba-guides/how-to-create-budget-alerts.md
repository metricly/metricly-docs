---
title: "Create Budget Alerts"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#aws services", "#cost", "#getting started", "guides"]
author: Lawrence
weight: 5
---

Budget Alerts can be set in the Bill Analysis tool using a combination of:

- Saved reports
- Send Daily Email
- Matching Conditions

{{% notice tip %}}
Read the guide on [creating budget alerts](/billing-analysis/ba-guides/how-to-create-monthly-cost-reports) before using this guide.
{{% /notice %}}


## Practice

Create a daily Budget Alert of cost deltas above $5 for _EC2 - Other Usage Types_.

1. Navigate to **Cost Management** > [**Bill Analysis**](https://us.cloudwisdom.virtana.com/#/reports/awscostall/latest).
2. Select **Quick ranges** > **Latest day**.
3. Select **CONFIGURE**.
4. Select the **EC2 - Other** service.
5. Group By **Usage Type**.
6. Add a **Matching Condition** of `Any Group Delta > 5`.
