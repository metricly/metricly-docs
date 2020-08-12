---
title: "Azure VM Right Sizing"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#azure", "#right sizing", "#getting started" ]
author: Lawrence Lane
---

Compare your current virtual machines against Azure's most recent SKUs to find the best fit for your workloads and your budget.  The Azure VM Right Sizing report enables you to leverage your historic workloads to truly right-size your resources. You can add optional constraints (such as CPU utilization limits) to further contextualize recommendations and highlight different savings opportunities across your portfolio. By default, this report shows your top 10 recommendations.

## Visualization Options

Toggle between data visualizations by selecting the radio buttons **Cost vs CPU** or **None**.

### Cost vs CPU

![azure-cost-vs-cpu-visualization](/images/reports-azure-right-sizing/azure-cost-vs-cpu-visualization.png)

### None (Table Only)

![table-only-view](/images/reports-azure-right-sizing/table-only-view.png)

## Table Options

Explore your recommendations by drilling into specific VM details, or simply focus on the high-level SKU and pricing information found in the parent row.

### Expand and Collapse Rows

![vm-expand-rows](/images/reports-azure-right-sizing/vm-expand-rows.gif)

### Sort Columns

![vm-toggle-rows](/images/reports-azure-right-sizing/vm-rightsizing-toggle-rows.gif)

---

## Configuration

You can configure the default report by defining a scope, setting constraints, and more.

### 1. Scope of Analysis

The following scope criteria can be used to both include or exclude resources.

- **Names**: Select resources by inserting a string.
- **Virtual Machines**: Select resources from a dropdown.
- **Attributes**: Select resources based on attributes; supports `any` and `all` statements.
- **Tags**: Select resource based on tags; supports `any` and `all` statements.

### 2. CPU and Memory Constraints

- **CPU Constraint**: Define minimum requirements based on numerical or historical constraints.
- **Memory Constraint**: Define minimum requirements based on numerical or historical constraints.
- **Data Aggregation Method**: Defines context for how historical utilization data is applied to recommendations.
  - **Maximum**: Considers the behavioral maximum demonstrated in utilization data, regardless of rarity.
  - **Mean**: Considers the behavioral average demonstrated in all utilization data.
  - **95th Percentile**: Considers the behavioral norm demonstrated in utilization data (without edge cases).


### 3. Other Resource Constraints

This section includes Disk I/O Constraints, including the option to **Require Premium SSD Support**.

### 4. Instance Type Constraints

This section includes a list of all available instance types and their primary use cases (e.g., storage optimized or compute optimized).

![instance-type-constraints](/images/reports-azure-right-sizing/instance-type-constraints.png)

### 5. Display Options

- **Limit Results**: Limit number of records returned in the report.
- **Visualization**: See visualizations section.
- **Group by**: Group by attributes.
- **Sorting**: Sort by instance type, savings, cost, and virtual machine.

### Save & Send Reports

You can save multiple versions of the Azure VM Right Sizing report. These reports can be selected from the report dropdown in the navigation panel.

1. Select the **SAVE AS** button in the navigation panel; a modal appears.
2. Input the **Saved Report Name**.
    - At this point, you may also enable **Send Weekly Email** notifications for this report by toggling the feature to active.
    - Emails are sent to your account email address by default, however, you can input any email address in the **Send Email** field.
3. Select **Save**.

![azure-vm-save-report](/images/reports-azure-right-sizing/azure-vm-save-report.png)
