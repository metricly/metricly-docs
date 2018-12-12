---
title: "Alert on a Check"
date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "checks", "custom checks"]
author: Lawrence Lane
alwaysopen: false
---

Setting up an alert in Metricly requires the creation of a policy and the system checks are no exception. Any check coming into the system can have a corresponding alert as well as a notification.

1. Click on policies and select **New Policy**.
2. Name the policy and apply any scoping or filtering required (for example, narrowing the scope to `WinServ` in `US-West` region with **Tag** `Environment:Production`).
3. Next click **Conditions** > **Add Condition**, and from the drop down you will see **Add System Check Condition**.
4. Now you just have to select the particular check. As long as the check has been posted at least once to the API, it would automatically show up on this menu. Then save, and you are done.
5. To add notifications, click the tab, and select the notification type. 
