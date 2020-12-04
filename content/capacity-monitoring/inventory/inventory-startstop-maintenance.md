---
title: "Start or Stop Maintenance"
#date: 2018-04-12
draft: false
categories:
tags: ["getting started", "metrics", "elements", "maintenance", "cli", "inventory page"]
author: Lawrence Lane
weight:  5
---

You can place elements into maintenance mode from the Inventory Explorer or via the Metricly CLI (Command Line Interface). While an element is in maintenance mode, learning for that element is disabled (i.e. no contextual or baseline bands will be displayed) and events will not be generated for the element.

1. Open the Inventory Explorer.
2. Select the check box next to as many elements as desired.
3. Click **Start** or **Stop Maintenance** at the top of the Inventory Explorer table. A summary page displays.
4. Select a duration via the **Expire After** dropdown.
![Start Stop Maintenance](/images/inventory-actions/start-stop-maintenance.png)
5. Click **Confirm**.

{{% notice tip %}}
If you do not want to set a duration for the maintenance mode, you can still return to the inventory page at a later time and manually end maintenance via selecting the elements and clicking the Stop Maintenance button.
{{% /notice %}}
