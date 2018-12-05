---
title: "Create or Edit a Policy"
date: 2018-04-12
draft: true
categories:
tags: ["alerts", "notifications", "events", "policies"]
author: Lawrence Lane
weight: 1
---

**Create**, **edit**, **delete**, **enable**, and **disable** policies with the Policy Editor. You can also use Policy Editor to enable and disable notifications.

1. Open the **Policy Editor**.
2. Navigate to **Alerts** > **+ Add New Policy**.
3. Begin crafting your policy at Step 1: **Scope**.
4. You can also open an existing policy and click **Edit Policy**.  Policies that correspond to inactive datasources cannot be edited.

![Edit Policy Walkthrough](/images/create-edit-policies/edit-policy-walkthrough.gif)

The top of your policy has 3 important fields:

- **Name**: Make this human readable, something your team would understand months or years down the road.
- **Enable Policy**: Policies are automatically enabled upon creation. To complete an unfinished policy at a later time, uncheck this field and save.
- **Category**: _Info_, _Warning_, or _Critical_.

| Category | Color  | Description                                                                                                                   |
|----------|--------|-------------------------------------------------------------------------------------------------------------------------------|
| Info     | Blue   | The Info category indicates that a policy has been violated, but the anomalous behavior is not critical.                      |
| Warning  | Yellow | The Warning category indicates that a policy has been violated, and there will likely be a more critical event in the future. |
| Critical | Red    | The Critical category indicates that a policy has been violated, and the cause of the event should be addressed quickly.      |
