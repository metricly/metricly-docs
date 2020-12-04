---
title: "AWS EFS Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "efs", "aws"]
author: Lawrence Lane
---
{{% notice info %}}
Policy names are prefixed with **AWS EFS –**
{{% /notice %}}


| Policy name                             | Duration   | Condition 1                    | (and) Condition 2 | (and) Condition 3 | Cat.     | Description                                                                                                                                                                                                            |
|-----------------------------------------|------------|--------------------------------|-------------------|-------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AWS EFS – Depleted Burst Credit Balance | 15 minutes | aws.efs.burstcreditbalance = 0 |                   |                   | Critical | There are no burst credits left. The number of burst credits that a file system has is zero.                                                                                                                           |
| AWS EFS – IO Percentage Critical        | 15 minutes | aws.efs.percentiolimit = 95%   |                   |                   | Critical | File system has almost reached its limit of the General Purpose performance mode. If this metric is at 100% more often than not, consider moving your application to a file system using the Max I/O performance mode. |
