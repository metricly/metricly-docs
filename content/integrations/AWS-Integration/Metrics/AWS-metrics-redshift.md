---
title: "Redshift Metrics"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "redshift"]
author: Lawrence Lane
---

For each Redshift cluster, two types of elements are collected:

 - RedshiftCluster: Contains cluster-specific metrics as well as metrics that are averages across all nodes.
 - RedshiftNode: Contains node-specific metrics. There will be one element per Redshift node.

The table below denotes which metrics are cluster- or node-based (or both).

## Collected
| Fully Qualified Name (FQN)             | Cluster | Node | AWS Metric                | Statistic | Units   | Max  | BASE | CORR | UTIL |
|----------------------------------------|---------|------|---------------------------|-----------|---------|------|------|------|------|
| aws.redshift.cpuutilization            | yes     | yes  | CPUUtilization            | average   | percent | 100  | yes  | yes  | yes  |
| aws.redshift.databaseconnections       | yes     | no   | DatabaseConnections       | average   | count   | none | yes  | no   | no   |
| aws.redshift.healthstatus              | yes     | no   | HealthStatus              | average   |         | 1    | no   | no   | no   |
| aws.redshift.maintenancemode           | yes     | no   | MaintenanceMode           | average   |         | 1    | no   | no   | no   |
| aws.redshift.networkreceivethroughput  | yes     | yes  | NetworkReceiveThroughput  | average   | Bps     | none | yes  | yes  | no   |
| aws.redshift.networktransmitthroughput | yes     | yes  | NetworkTransmitThroughput | average   | Bps     | none | yes  | yes  | no   |
| aws.redshift.percetagediskspaceused    | yes     | yes  | PercentageDiskSpaceUsed   | average   | percent | 100  | yes  | no   | yes  |
| aws.redshift.readiops                  | yes     | yes  | ReadIOPS                  | average   | iops    | none | yes  | yes  | no   |
| aws.redshift.readlatency               | yes     | yes  | ReadLatency               | average   | seconds | none | yes  | yes  | no   |
| aws.redshift.readthroughput            | yes     | yes  | ReadThroughput            | average   | Bps     | none | yes  | yes  | no   |
| aws.redshift.writeiops                 | yes     | yes  | WriteIOPS                 | average   | iops    | none | yes  | yes  | no   |
| aws.redshift.writelatency              | yes     | yes  | WriteLatency              | average   | seconds | none | yes  | yes  | no   |
| aws.redshift.writethroughput           | yes     | yes  | WriteThroughput           | average   | Bps     | none | yes  | yes  | no   |

## Computed

| Fully Qualified Name (FQN)             | Description                                                                                                                                    | Units | BASE |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------|------|
| netuitive.aws.redshift.totalthroughput | This metric represents the total throughput, obtained by adding the read and write throughputs. Computation:(ReadThroughput + WriteThroughput) | Bps   | yes  |
