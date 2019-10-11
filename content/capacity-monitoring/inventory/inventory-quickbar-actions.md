---
title: "Quickbar Actions"
#date: 2018-04-12
draft: false
categories:
tags: ["#getting started", "#metrics", "#elements", "#bulk actions", "#inventory page" ]
author: Lawrence Lane
weight: 3
---
The inventory page allows you to quickly navigate through all of your [elements][1], sort, and perform bulk actions. The Inventory Explorer displays all the elements in your environment that were processed in the last hour. Elements are removed from the elements table roughly seven hours after an associated datasource is disabled.

## Use the Quick Bar
Select the elements you’d like to edit using the checkboxes on the far left of each row. After a checkbox is selected, the Quick Bar appears.

![Quick Bar](/images/inventory-actions/quick-bar.png)

Then, select one of the following actions:

- View [Metrics][2]
- Add/Delete Tag
- Start/Stop Maintenance
- Delete Elements

## Delete Elements
Once you delete an element the metadata will be permanently removed. This cannot be undone. Historic time series data for that element will still be kept. If an element with the exact same metadata appears in Metricly, the available data for the element will be associated with it.

1. Open the Inventory Explorer.
2. Select the check box next to as many elements as desired.
3. Click **Delete Element(s)** at the top of the Inventory Explorer table. .
4. Click **Yes, Delete**.

## Add Tags
1. Open the Inventory Explorer.
2. Select the check box next to as many elements as desired.
3. Click **Add Tag** at the top of the Inventory Explorer table.
4. Type a `Key` and `Value` for the tag. An element can have multiple tags (up to 10), but keys cannot be used more than once.
5. Click **Confirm Changes**.
6. A summary of your changes will display.
7. Click **Save**.

## Delete/Edit tags
1. Open the Inventory Explorer.
2. Select the check box next to as many elements as desired.
3. Click **Add Tag** or **Delete Tag** at the top of the Inventory Explorer table.
4. Type a `key`. Any elements that already have the tag will be highlighted blue in the Element(s) column.
5. Type a `value`. If a tag already exists on an element, the value(s) will be replaced with the values you currently have typed.
6. Click **Confirm Changes**.
7. Click **Save**.




[1]: /capacity-monitoring/inventory/
[2]: /capacity-monitoring/metrics/
