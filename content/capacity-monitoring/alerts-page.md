---
title: "Alerts Page"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "events", "policies"]
author: Lawrence Lane
alwaysopen: false
---
The Alerts page shows a list of all your configured policies, both enabled and disabled. It includes:

- Policy name
- Number of elements in scope
- Filters on the policy
- State of the policy (Enabled/Disabled)
- Current status (OK, Info, Warning, Critical).

This page has additional filters to display all Open and Closed policies.

- Filtering by Open will display only the policies that are currently (Now) violating a set condition(s). We use the term “firing” to refer to policies that are violating a set of conditions.
- Clicking on Closed will show any policies that have fired during the selected time range.

### How to Close an Open Alert

1. Navigate to the Alerts page in CloudWisdom.
2. On the **Open** tab, select the policy that is firing.
![select-policy](/images/alerts-page/select-policy.png)
3. The Policy Details modal appears. Under Impacted Elements, select any (or all) elements affected.
4. Select **Close**.
![close-alerts](/images/alerts-page/close-alerts.png)

You have now successfully closed the alert.

## Search Policies

You can search for a particular policy or filter the policy by using the policy filters.

1. Open the alerts page.
2. At the top of the page, use the available fields to search for the desired policy or filter the list:
  - **Name contains**: Text field used to match characters contained in a policy name.
  - **Created By**: Drop-down menu used for selecting the user that created a policy.
  - **State**: Drop-down menu used for selected if a policy is disabled or enabled.
  - **Type**: Text field used to match an element type used in a policy. You can only select one element type to search for.

## Available Views

### Table View
The table view will display all the policies configured in your tenant account. These are both the CloudWisdom best practices and your user defined policies. In the table you will also see the details (status, state, enabled, notifications) about each policy. To see what is firing right now click on **Open**. By clicking **Closed** you will see all the policies that fired over the selected time range.

![Alert Page Table View](/images/alerts-page/alert-page-table-view.png)

### Slide Out View
Click on the policy name to open more details about the policy. The slide out will display any elements that have **Open** or **Closed** policy violations. Remember the **Closed** policies are tied to the time control. You can click on the graph to see the metrics view. This feature is disabled for the checks because it does not apply. The view can be closed by clicking the the **X** in the top right corner.

![Slide Out View](/images/alerts-page/slide-out-view.png)
