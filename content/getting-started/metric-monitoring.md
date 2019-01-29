---
title: "Metric Monitoring"
#date: 2018-12-3
draft: false
categories:
tags:
author: Lawrence Lane
pre:
weight: 2
---

## 1. Integrate with AWS
We strongly recommend all users start by creating an [AWS integration][1]. This takes less than 15 minutes thanks to our quick setup wizard and a CloudFormation script.

## 2. Consider Using the Linux Agent

The [Linux Agent][2] is an optional but very robust addition to both monitoring and cost analysis.

This agent discovers and collects KPI metrics, integrates with CloudWatch, and can leverage other agent metrics. Using various plugins, the Linux Agent can also pull metrics from many different products running on a Linux operating system (in addition to pulling metrics from the host Linux OS).

## 3. Add All Integrations
Use the search bar in the navigation page use the [Integrations][3] tree folder to find instructions for each integration you need installed.

## 4. Create Policies and Notifications
Most of our integrations come with default policies out of the box. If you would like to add more, simply use the [Policy Editor][4] to create new ones.

Use our [Notification guides][5] to set up your preferred contact method for firing policies.

## 5. Build a Custom Dashboards
Got everything set up? Great! Now's a great time to build the dashboard of your dreams. You can do that by following the [Create a New Dashboard][7] guide. 

## 6. Explore the Docs

Curious to know all you can about our Monitoring platform? the [Alerts & Notifications][6] section of this help site has a comprehensive breakdown of alerts, events, checks, and policies.

[1]: /integrations/aws-integration/aws-CloudFormation-Installation
[2]: /integrations/agents/LINUX-agent/linux-standard-install
[3]: /integrations
[4]: /alerts-notifications/policies/create-edit-policies
[5]: /alerts-notifications/notifications
[6]: /alerts-notifications
[7]: /data-visualization/dashboards/create-new-dashboard
