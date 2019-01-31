---
title: "AWS Services Cost"
#date: 2018-12-03
draft: false
categories:
tags: ["#reports", "#aws services", "#cost"]
author: Lawrence Lane
---

View data across all of your AWS services with the AWS Service Cost Report. This report shows not only services currently used, but all services–including those not currently monitored by Metricly–to provide an overall view of your AWS cost. This report can include data from multiple accounts if consolidated billing has been set up and configured. See the admin guide for any installation and configuration steps.

Like the screenshots found in this guide? Switch over to Dark Theme in the UI.

**This report helps you:**

- Identify cost outliers
- Find unexpected cost changes
- Analyze cost trends


## Visualization Options

You can visualize your data in two ways: via Period Comparison or Stacked View. Switching between views is easy!

How to Switch Between Views

1. Click **CONFIGURE**.
2. Choose a visualization.
3. Click **Apply**.

![switch-between-views](static/images/reports-aws-services-cost/switch-between-views.png)

### Period Comparison
Uses the current determined date interval (e.g. Latest 30 Days) and compares it to the previous interval (in this case, 30 days). See the Time Intervals section for more information on changing the periods compared.

![period-comparison](static/images/reports-aws-services-cost/period-comparison.png)

### Stacked View
Shows all of your services individually; each service can be shown or hidden via toggling on the menu below the graph.

![stacked-view](static/images/reports-aws-services-cost/stacked-view.png)

## Time Intervals
When using the Period Comparison view, you can choose between several Time Intervals to display:

- Latest Day
- Current Month
- Previous Month
- Latest 30 Days
- Latest 3 months
- Latest 6 Months
- Latest 12 Months
- Year to Date

![time-intervals](static/images/reports-aws-services-cost/time-intervals.png)

## Report Table
Every report comes with a simple table of the visualized data. You can toggle ascending/descending across the columns; changes made to the table are automatically reflected in the visualization above. A CSV file containing this table can be obtained by clicking the **Download** button.

![report-table](static/images/reports-aws-services-cost/report-table.png)

## Filtering & Other Options
All filtering and grouping for your report can be done by opening the **CONFIGURE** modal from the navigation panel.

![configure-modal](static/images/reports-aws-services-cost/configure-modal.png)

### Filtering Options

- Services (EC2, Lambda, ELB)
- Attributes (AZ, Instance Type, Entity Name)
- Tags (Owner, Project, Application)

### Grouping  Options

- Group By (Period, Attribute, Service)
- Limit (From One to All)
- Sort By (Service, Total Cost, Delta)
- Sort Order (Ascending or Descending)

### Matching Conditions

The following conditions can be set to display data that is greater or less than the input value (either as a dollar amount or percentage).

- Any Group Current Cost
- Any Group Comparison Cost
- Any Group Delta
- Any Group Delta %

## Save & Send Reports
To save a report:

1. Click the **SAVE** button in the navigation panel; A _Save AWS Service Cost Report_ modal appears.
2. Input the **Saved Report Name**
  - At this point, you may also enable **Send Daily Email** notifications for this report by toggling the feature to active.
  - Emails are sent to your account email address by default, however, you can input any email address in the **Send Email** field.
3. Hit **SAVE**.

![save-send-reports](static/images/reports-aws-services-cost/save-send-reports.png)
