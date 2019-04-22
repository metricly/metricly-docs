---
title: "Delete an Element"
#date: 2018-04-12
draft: false
categories:
tags: ["#getting started", "#metrics", "#elements", "#maintenance", "#cli", "#inventory page"]
author: Lawrence Lane
---
You can delete an element from the [Inventory Explorer page][1]. Deleting an element in Metricly persists only until the next collection cycle **unless** the element is also no longer being _collected_ or _posting_ to Metricly.

- The metadata for a deleted element is retained for 60 days.
- Stale metadata (old metrics no longer collecting, attributes and tags that no longer exist) gets permanently deleted.
- The band analytic history for metrics associated with the deleted element is retained for 90 days.

{{% notice tip %}}
You must update your collectors and ingest API calls for permanent element deletion. Make sure to also update any notifications or policies that are directly associated to the deleted element.
{{% /notice %}}

## How to Delete an Element from the UI

1. Open the Inventory Explorer.
2. Select the **check box** next to as many elements you wish to delete.
3. Select **Delete Element(s)**.
![delete-elements](/images/inventory-delete-element/delete-elements.png)
4. Select **Yes, Delete** in the confirmation modal.


[1]: /data-visualization/inventory/inventory-main-navigation
[2]: /alerts-notifications/policies/
[3]: /alerts-notifications/notifications/
