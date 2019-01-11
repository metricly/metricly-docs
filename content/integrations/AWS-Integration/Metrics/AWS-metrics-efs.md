---
title: "EFS Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["#aws", "#metrics", "#efs"]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name (FQN)  | Description                                                                                                   | Statistic | Units            | Min | Max | BASE | CORR | UTIL |
|-----------------------------|---------------------------------------------------------------------------------------------------------------|-----------|------------------|-----|-----|------|------|------|
| aws.efs.burstcreditbalance  | The number of burst credits that a file system has.                                                           | avg       | bytes            |     |     | no   | yes  | no   |
| aws.efs.clientconnections   | The number of client connections to a file system.                                                            | sum       | bytes            |     |     | no   | yes  | no   |
| aws.efs.datawriteiobytes    | The number of bytes for each file write operation.                                                            | sum       | bytes            |     |     | no   | yes  | no   |
| aws.efs.metadataiobytes     | The number of bytes for each metadata operation.                                                              | sum       | bytes            |     |     | no   | yes  | no   |
| aws.efs.percentiolimit      | Shows how close a file system is to reaching the I/O limit of the General Purpose performance mode.           | percent   | percent          |     |     | no   | no   | yes  |
| aws.efs.permittedthroughput | The maximum amount of throughput a file system is allowed.                                                    | avg       | bytes per second |     |     | no   | yes  | no   |
| aws.efs.totaliobytes        | The number of bytes for each file system operation, including data read, data write, and metadata operations. | sum       | bytes            |     |     | no   | yes  | no   |
