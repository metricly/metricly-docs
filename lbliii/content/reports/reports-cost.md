---
title: "Cost Reports "
date: 2018-12-03
draft: true
categories:
tags: ["reports", ]
author: Lawrence Lane
alwaysopen: false
weight: 4
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
