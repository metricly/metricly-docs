---
title: "EC2 Recommendations"
#date: 2018-12-03
draft: false
categories:
tags: ["#reports", "#ec2", "ec2 recommendations", "#getting started" ]
author: Lawrence Lane
---
This report compares your EC2s and utilization data to the most currently available SKU library in AWS to determine what combination would best suit your existing workload needs. You can also add optional constraints (such as CPU utilization not exceeding a particular level) to filter down recommendation results and highlight different savings opportunities. By default, this report shows your top 10 recommendations.

## Access (Currently in Beta)
To use the updated EC2 Recommendation report, navigate to the Beta page.

1. Hover over your username and select **Beta**.
2. Find the EC2 Recommendation Report and click **Try It**.

## Visualization Options

### How to Switch Between Views

1. Click **CONFIGURE**.
2. Choose a visualization.
3. Click **Apply**.

![switch-views](/images/reports-ec2-recommendations/switch-views.png)

#### Cost vs CPU

![cost-v-cpu](/images/reports-ec2-recommendations/cost-v-cpu.png)

#### Cost vs Memory

![cost-v-memory](/images/reports-ec2-recommendations/cost-v-memory.png)

#### Report Table

![report-table](/images/reports-ec2-recommendations/report-table.png)

## Filtering & Other Options

### Scope of Analysis

- Names
- Attributes
- Tags

### Utilization Preferences

Select your preferences for resource utilization of the recommended instances according to historic usage levels

### Type Preferences

- Classes
- Types
- Exclusions


### Save & Send Reports

To save a report:

1. Click the **SAVE** button in the navigation panel; A _Save AWS Service Cost Report_ modal appears.
2. Input the Saved Report Name
    - At this point, you may also enable Send Daily Email notifications for this report by toggling the feature to active.
    - Emails are sent to your account email address by default, however, you can input any email address in the Send Email field.
3. Hit **SAVE**.

![send-email](/images/reports-ec2-recommendations/send-email.png)
