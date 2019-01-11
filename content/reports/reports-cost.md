---
title: "Cost Reports"
#date: 2018-12-03
draft: false
categories:
tags: ["#reports", "#s3", "#ec2", "#rds" ]
author: Lawrence Lane
---

Cost reports enable you to easily identify expensive instances and compare them against **utilization**, **type**, **elements**, and **tags**. These multi-dimensional reports also break down information like **total versus individual** instance costs and even how much each **instance state** (Reserved, On-Demand) costs. Custom tagging is another easy way to group your instances.

Cost Reports are generated once per week. It may take up to 7 days before your first report is available.

## Report Versions
### Estimated Cost (AWS Integration Only)
If you just have an AWS integration in Metricly, the Estimated Cost report is available. Instance costs are estimated based on current list prices and simple assumptions to fill in missing information. For a more accurate view including reservations, data transfer costs, iops guarantees and other account specific charges, you can add an AWS Cost integration that allows Metricly to use your actual billing files from AWS.

Estimated Cost reports use 7 days of metric results and the current list prices to estimate element instance costs for all instances monitored by Metricly. Estimated Reports do not include data transfer costs and assumes all instances are on-demand.

### Full Cost (AWS+AWS Cost Integration)
If you have both an AWS and AWS Cost integration, the Full Cost report is available and based on your billing files. The Full Cost report reads 7 days of billing data associated with the instances monitored by Metricly.

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

{{% notice tip %}}
5-7 days of analysis is required before you can view your initial report. A splash screen greets you in place of the report until Metricly is done generating it.
{{% /notice %}}
## Report Views
This section outlines all of the available report views.

### Total Cost Pareto
This graph shows the total costs incurred for all the instances monitored by Metricly (or the subset if a filter has been applied). The line is plotted against the right-hand axis and shows a cumulative percent contribution of each of the bars. Use this view to see the total cost of your environment and total contributions by category.

All cost categories are shown in this chart even if you have incurred no costs of a particular type. For the Estimated Cost report, you may see just one bar.
![total cost pareto](/images/reports-cost/total-cost-pareto.png)

### Cost by Element
This graph breaks down how much each element is costing by category. The line is plotted against the right-hand axis and shows the utilization of each element. With this view, you can compare the relative cost of elements versus their level of utilization. This chart only shows the cost categories that you have actually incurred.
![cost by element](/images/reports-cost/cost-by-element.png)

### Cost by Instance Type
This graph breaks down how much each instance size is costing by instance type. The line is plotted against the right-hand axis and shows the maximum of the utilizations of all elements per instance type. This chart only shows the cost categories that you have actually incurred.
![cost by instance type](/images/reports-cost/cost-by-instance-type.png)


### Cost vs. Utilization Scatter
This graph displays a scatter plot of the cost versus utilization for your instances. Hover over a point on the graph to view the instance name, utilization, instance type, tag, and cost. You can zoom into an area of the chart by clicking and dragging the mouse.

This view lets you compare the relative cost and utilization of your instances amongst their peers: elements to the bottom-right have relatively high utilization and lower cost compared with elements in the top-left corner which have lower utilization and higher costs. Elements are given different markers based on their tag. To use this view you need to have tags on your instance elements; these can be source tags (set in AWS) or tags you have created in Metricly.

{{% notice tip %}}
If combinations of your instances represent different applications, you could create a tag called “application” in each instance and set the value accordingly. In this view, you could select the “application” tag to mark the elements according to the grouping you have specified. This is useful for identifying outliers where you expect elements of the same tag to have similar cost/utilization positions on the chart.
{{% /notice %}}

![cost vs utilization scatter](/images/reports-cost/cost-vs-utilization-scatter.png)

### Cost by Tag
This graph lets you group the costs by any custom tag. To use this view you need to have tags on your instance elements. These can be source tags (set in AWS) or tags you have created in Metricly. For example, if combinations of your instances represent different applications you could create a tag called “application” in each instances and set the value accordingly. In this view, you could select the “application” tag to aggregate the costs according to the grouping you have specified. Other examples could include grouping by department or by environment. This chart only shows the cost categories that you have actually incurred.

{{% notice tip %}}
You can zoom into the chart by clicking and dragging your mouse across a set of elements. If you hover the mouse over a bar, you will see a tooltip showing the instance type, total cost, and the cost breakdown.
{{% /notice %}}
![cost zoom](/images/reports-cost/cost-zoom.gif)

## EC2 vs. RDS vs. S3
Cost Reports across instances have largely the same experience, but this section covers the main differences between cost reporting for each.

### Utilization Metrics
#### EC2

- Active Hours
- CPU Utilization %
- Memory Utilization
- Disk I/O %
- Disk Space Used %
- Network I/O %

##### Additional Considerations:

- EC2 elements without a Metricly agent / Windows agent display only two utilization measures: Active Hours and CPU Utilization %.
- EC2 elements with a Metricly agent installed have the following additional utilization metrics available: Memory Utilization %, Disk I/O %, and Disk Space Used %.
- EC2 elements with a Windows agent installed have the Network I/O % metric available.

If you have a mix of elements with and without a Metricly agent, you will see gaps in the utilization figures where values are not available.

#### RDS

- Active Hours
- CPU Utilization
- Disk Space Used %
- IOPS Utilization %

#### S3
- Put Requests
- Get Requests
- Number of Objects
- Bucket Size (bytes)
