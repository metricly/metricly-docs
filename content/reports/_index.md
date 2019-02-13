---
title: "Reports"
#date: 2018-12-03
draft: false
categories:
tags: ["#reports", "#directory page",]
author: Lawrence Lane
alwaysopen: false
weight: 5
pre: "<i class='icon-reports'></i> &nbsp;"
---
Reports provide a quick glance at some of the most important parts of your environment, including utilization, policy violation, and estimated cost of your inventory. Report Explorer allows you to toggle between different reports on the elements in your environment.

## Required Integrations for Metricly Reports

| Report Name                            | AWS w/ Cost Explorer | AWS w/ CloudWatch | AWS w/ Detailed Billing | List Price Estimation w/out Detailed Billing | Time from activation to first report |
| -------------------------------------- | -------------------- | ----------------- | ----------------------- | -------------------------------------------- | ------------------------------------ |
| AWS Services Cost                      | x                    |                   |                         |                                              | Immediate                            |
| Resource Utilization                   |                      | x                 |                         |                                              | Immediate                            |
| EC2 Cost                               |                      | x                 | x                       | x                                            | 1 day                                |
| RDS Cost                               |                      | x                 | x                       |                                              | 1 day                                |
| S3 Cost                                |                      | x                 | x                       |                                              | 1 day                                |
| EC2 Reservation Recommendations (Beta) |                      | x                 | x                       |                                              | 1 day                                |
| EC2 Recommendations                    |                      | x                 | x                       | x                                            | 1 week                               |
| ASG Recommendations                    |                      | x                 | x                       | x                                            | 1 week                               |
