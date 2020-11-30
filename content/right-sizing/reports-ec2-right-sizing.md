---
title: "AWS EC2 Right Sizing"
draft: false
categories:
tags: ["#tools", "#ec2", "ec2 recommendations", "#getting started" ]
author: Lawrence Lane
---
Use the AWS EC2 Right Sizing report to analyze cost data found in your AWS Cost & Usage Report across all of your consolidated or linked AWS accounts. This report provides 3 important dimensions of your EC2 utilization: cost-to-memory, cost-to-CPU, and CPU-to-memory.

Each recommendation found in your AWS EC2 Right Sizing report compares your EC2's attributes and utilization against the most currently available AWS SKU Library to determine what combination woud best suit your existing workload needs. You can also add optional constraints (such as CPU utilization not exceeding a particular level) to guide our recommendation results and discover other use-case driven savings opportunities.

By default, this report shows your top 10 recommendations.

## Visualization Options

You can switch between views by selecting the View buttons **Cost vs CPU**, **Cost vs Memory**, **CPU vs Memory**, and **None**.

![toggle views](/images/reports-ec2-right-sizing/toggle-aws-ec2-rightsizing-views.gif)

## Projected Savings

You can view projected savings by expanding a row in the EC2 results table.

![projected savings](/images/reports-ec2-right-sizing/projected-savings.png)

## Configuration

There are five main categories for configuration options. As you define your report's criteria, the preview of your report updates with sample data based on your constraints.

### 1. Scope of Analysis

The following constraint options are available for both inclusion and exclusion statements.

- **Name**: A text-input that selects resources with that match any text provided, such as a prefix (e.g., `west-app`).
- **EC2s**: A dropdown of all EC2s for manual selection with the option to select all.
- **Attributes**: A dropdown of all attributes for manual selection with the option to select all.
- **Tags**: A dropdown of all tags for manual selection with the option to select all.

### 2. CPU and Memory Constraints

The following constraint options are available for both CPU and Memory statements.

- **No Constraint**: Returns all possible recommendations for the given resource.
- **Cannot Increase CPU/Memory**: Returns recommendations where maximum resource utilization is at or below the input amount.
- **Minimum CPU/Memory**: Returns recommendations where minimum resource utilization is at or above the input amount.
- **Resize based on historical utilization**: Returns recommendations based on historical utilization of the given resource type.

#### Resource Specific Constraints

- **Target CPU Utilization**: Returns recommendations that closely match the target CPU utilization percentage.
- **Default memory utilization when diagnostic monitoring not enabled**: Returns recommendations based on an assumption (as a percentage) of memory utilization.
- **Target memory utilization**: Returns recommendations that closely match the target memory utilization percentage.

#### Data Aggregation Method

Options include Maximum, Mean, and 95th percentile.

### 3. Other Resource Constraints

#### Disk I/O Constraints

- **No Constraint**: Returns all possible recommendations for the given resource.
- **Peak IOPS cannot decrease**: Returns recommendations where IOPs are at or above existing level.
- **Minimum peak IOPS**: Returns recommendations where IOPs does not go below the peak level.

#### Network Constraints

- **No Constraint**: Returns all possible recommendations for the given resource.
- **Network performance cannot decrease**: Returns recommendations where network performance is at or above existing level.
- **Minimum peak network performance**: Returns recommendations where network performance does not go below the input peak level.

#### Tenancy Constraints

- **No Constraint**: Returns all possible recommendations for the given attribute.
- **Shared**: Returns only shared tenancy options.
- **Dedicated**: Returns only dedicated tenancy options.
- **Host**: Returns only host tenancy options.

#### Term Type Constraints

- **No Constraint**: Returns all possible term recommendations for the given attribute.
- **Reserved**: Returns only recommendations with reservation terms.
  - **Reservation Offering Class**: Options include Any, Standard, or Convertible.
  - **Reservation Contract Length**: Options include Any, 1 year, or 3 years.
  - **Reservation Purchase Option**: Options include Any, No Upfront, All Upfront, Partial Upfront.
  - **MS SQL Server**: Options include Any, NA, SQL Ent, SQL Std, SQL Web.
- **OnDemand**: Returns only recommendations with On-Demand terms.


### 4. Instance Type Constraints

You can specify target instance types (e.g., a series) that can be proposed by the AWS EC2 Right Sizing Report. Options include:

- No Constraints
- Include
- Exclude

### 5. Display Options

- **Limit Results**: Options include Top 10 or All.
- **Visualization**: See visualization options.
- **Sorting**: Supports all table columns and ascending/descending.

## Report Options

### Save & Send Reports

To save a report:

1. Select the **SAVE AS** button in the navigation panel; A _Save Report_ modal appears.
2. Input the **Saved Report Name**.
    - At this point, you may also enable **Send Weekly Email** notifications for this report by toggling the feature to active.
    - Emails are sent to your account email address by default, however, you can input any email address in the **Send Email** field.
3. Hit **Save**.

![save as](/images/reports-ec2-right-sizing/save-as.png)
