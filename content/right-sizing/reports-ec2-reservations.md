---
title: "EC2 Reservation Recommendations"
#date: 2018-12-03
draft: false
categories:
tags: ["#reports", "#ec2", "#cost", "#ec2 reservations", "#getting started"]
author: Lawrence Lane
---

Avoid overbuying reserved resources with the EC2 Reservation Recommendation report. This report uses instance-hour usage data to compile multi-dimensional visualizations and provide tailor-fit purchasing recommendations to help you achieve longterm savings.

{{% notice tip %}}
An AWS integration with Detailed Billing must be enabled before using this report.
{{% /notice %}}

**This report helps you:**

- Avoid overbuying reserved resources
- Decide on adequate reservation types for your use cases
- Get solid recommendations
- Visualize your total resource usage across multiple dimensions

## Visualization Options

![visualization-options](/images/reports-ec2-reservations/visualization-options.png)

### Switch Between Views
1. Click **CONFIGURE**.
2. Choose a visualization.
3. Click **Apply**.

### Stacked Timeseries
Shows historical data as a stacked hourly, concurrent timeline.

### Timeseries
Shows historical data as an hourly, concurrent timeline.

### Summary
Shows historical data as a general summary.

## Report Table
Every report comes with a simple table of the visualized data. You can toggle ascending/descending across the columns; changes made to the table are automatically reflected in the visualization above. A CSV file containing this table can be obtained by clicking the Download button.

## Configuration Options

![config-visualization](/images/reports-ec2-reservations/config-visualization.png)

### Reservation Preference

![reservation-preference](/images/reports-ec2-reservations/reservation-preference.png)

### Filter Elements

![filter-elements](images/reports-ec2-reservations/filter-elements.png)

### Filter Types

![filter-types](/images/reports-ec2-reservations/filter-types.png)

### Other Options

![other-options](/images/reports-ec2-reservations/other-options.png)

## Save & Send Reports

###  Save As
1. Click the **SAVE AS** button in the navigation panel; A Save AWS Service Cost Report modal appears.
2. Input the **`Saved Report Name`**
3. Hit **Save**.

![save-send-report](/images/reports-ec2-reservations/save-send-report.png)

### Save
By clicking **SAVE** instead of **SAVE AS**, you an overwrite an existing report that has been loaded via the saved report drop-down panel.

![standard-save](/images/reports-ec2-reservations/standard-save.png)
