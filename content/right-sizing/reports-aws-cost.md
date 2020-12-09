---
title: "AWS Cost Report"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#s3", "#ec2", "#rds", "#getting started" ]
author: Lawrence Lane
---
Use the AWS Cost report to analyze cost data found in your AWS Cost & Usage Report across all of your consolidated or linked AWS accounts. This report provides a breakdown of your costs for **EC2**, **RDS**, and **S3** resources. The AWS Cost report is generated once per week and may take up to 7 days after setup to display your first analysis.

This report is an ideal place to start your right sizing planning because it allows you to quickly understand your infrastructure spend on an _operational_ level, such as identifying an over-reliance on On-Demand resources used for predictable, long-term workloads (more suited for reservations and savings plans) or those that might be less critical and time sensitive (more suited for Spot instances).

Each resource's visualization supports quick toggling across relevant dimensions, such as:

- **EC2**: On-Demand, Savings Plan, and Data Transfer costs
- **RDS**: On-Demand and Storage
- **S3**: Put Requests, Get Requests, and Data Out

![dimension-toggle-example](/images/reports-aws-cost/dimension-toggle-example.png)

## Cost Aggregation & Categories  

Costs are aggregated, simplified, and reduced to the following categories element:

| Type                 | Cost                              | Description                                                                                                       |
|----------------------|-----------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Hourly Instance Fees | On-Demand Instance                | Hourly fee for an on-demand instance                                                                              |
| Hourly Instance Fees | Spot Instance                     | Hourly fee for a spot instance                                                                                    |
| Hourly Instance Fees | Reserved Instance                 | Hourly fees for partial upfront or no-upfront reserved instances                                                  |
| Hourly Instance Fees | Amortized Upfront Reservation Fee | Amortized upfront fees for partial upfront or all-upfront instances **                                            |
| Hourly Instance Fees | Dedicated Instance                | Hourly fee for a dedicated instance                                                                               |
| Hourly Instance Fees | Instance EBS Optimized Charge     | Hourly incremental fee for EBS optimized instances (applies to certain instance types)                            |
| Hourly Instance Fees | Instance Dedicated Charge         | Hourly incremental fee for dedicated host                                                                         |
| Data Transfer Costs* | Data In – InterZone               | Costs for data transfer to/from another AWS service in another availability zone or peered VPC in the same region |
| Data Transfer Costs* | Data In – InterRegion             | Costs for data transfer to/from another AWS service in another region                                             |
| Data Transfer Costs* | Data In – PublicIP                | Costs for data transfer to/from another AWS service via a public or elastic IP address                            |
| Data Transfer Costs* | Data In – Internet                | Costs for data transfer to/from the instance from/to the internet                                                 |
| Data Transfer Costs* | Data In – CloudFront              | Costs for data transfer to/from the instance via CloudFront                                                       |
| Data Transfer Costs* | Other                             | Other data transfer costs (e.g., Direct Connect)                                                                  |

## Configuration

Report configurations enable you to compare expensive instances against **utilization**, **type**, **elements**, and **tags**. You can also break down information like **total versus individual** instance costs or total **instance state** (Reserved, On-Demand) costs. Custom tagging is another easy way to group your instances.

### 1. Scope of Analysis

The following constraint options are available for EC2, RDS, and S3 reports:

- **Name**: A text-input that selects resources with that match any text provided, such as a prefix (e.g., `west-app`).
- **Elements**: A dropdown of all elements for manual selection with the option to select all.
- **Attributes**: A dropdown of all attributes for manual selection with the option to select all.
- **Tags**: A dropdown of all tags for manual selection with the option to select all.


### 2. Filters

Filters use operators and values to find resource with spend that meets certain conditions.

### EC2

- **Total Cost**: Defines the total cost threshold applied to the operator.
- **On-Demand Instance**: Defines the total On-Demand cost threshold applied to the operator.
- **On-Demand Instance (Savings Plan)**: Defines the total Savings Plan allocation threshold applied to the operator.
- **Data Transfer**: Defines the total Data Transfer cost threshold applied to the operator.
- **Maximum CPU %**: Defines the Maximum CPU % utilization applied to the operator.

### RDS

- **Total Cost**: Defines the total cost threshold applied to the operator.
- **On-Demand Instance**: Defines the total On-Demand cost threshold applied to the operator.
- **Storage**: Defines the total storage cost threshold applied to the operator.
- **Unknown**: Defines the total unknown (not categorized by a standard operation) cost threshold applied to the operator.
- **Maximum CPU %**: Defines the Maximum CPU % utilization applied to the operator.

### S3

- **Total Cost**: Defines the total cost threshold applied to the operator.
- **Data Out**: Defines the total Data Out cost threshold applied to the operator.
- **Put Requests**: Defines the total Put Request cost threshold applied to the operator.
- **Get Requests**:  Defines the total Get Request cost threshold applied to the operator.
- **Maximum Bucket Size (bytes)**: Defines the maximum Bucket Size applied to the operator.

### 3. Report Views

#### Report View & Grouping

Grouping options depend on the initial report view chosen.
  - Grouped by ID
  - Grouped by Element Name
  - Grouped by Attribute
  - Grouped by Tag
  - Grouped by Day
  - Grouped by Week
  - Grouped by Month
  - Grouped by Daily Run Rate

#### Utilization Metric & Metric Statistic

Each Utilization metric supports Mean, Maximum, 95th Percentile, Minimum, Total, and Count statistics.
  - **EC2 & RDS**: Active Hours
  - **EC2 & RDS**: CPU Utilization %
  - **EC2 & RDS**: Disk Space Used %
  - **EC2 & RDS**: Disk I/O %
  - **S3**: Bucket Size (bytes)
  - **S3**: Number of Objects


##### **EC2 Considerations**

- EC2 elements without a Agent / Windows agent display only two utilization measures: Active Hours and CPU Utilization %.
- EC2 elements with a Agent installed have the following additional utilization metrics available: Memory Utilization %, Disk I/O %, and Disk Space Used %.
- EC2 elements with a Windows agent installed have the Network I/O % metric available.

If you have a mix of elements with and without a Agent, you will see gaps in the utilization figures where values are not available.

#### Show

You can limit the results of your report by defining how many records to show.

#### Visualization

You can use this setting to disable the visualization if you wish to only use the results table.

#### Sorting

You can sort all of the follow columns by either ascending or descending.

- Total Cost
- Instance Type
- Maximum CPU %
- Elements
- On-Demand Instance
- Storage
- Unknown


## Report Options

### Save & Send Reports

To save a report:

1. Select the **SAVE AS** button in the navigation panel; A _Save Report_ modal appears.
2. Input the **Saved Report Name**.
3. Hit **Save**.

![aws-cost-report-save-report](/images/reports-aws-cost/aws-cost-report-save-report.png)
