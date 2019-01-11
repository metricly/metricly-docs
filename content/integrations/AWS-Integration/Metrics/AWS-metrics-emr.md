---
title: "EMR Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["#aws", "#metrics", "#nlb"]
author: Lawrence Lane
---

AWS groups EMR metrics into different categories (cluster status, node status, IO, etc.), but this has no impact on how Metricly monitors EMR.

## Collected
| Friendly Name  | Fully Qualified Name (FQN)                         | AWS Metric                    | Statistic | Units     | Max  | BASE | CORR | UTIL |
|----------------|----------------------------------------------------|-------------------------------|-----------|-----------|------|------|------|------|
| Cluster Status | aws.elasticmapreduce.appscompleted                 | AppsCompleted                 | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.appsfailed                    | AppsFailed                    | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.appskilled                    | AppsKilled                    | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.appspending                   | AppsPending                   | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.appsrunning                   | AppsRunning                   | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.appssubmitted                 | AppsSubmitted                 | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.containerallocated            | ContainerAllocated ave        | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.containerreserved             | ContainerReserved             | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.containerpending              | ContainerPending              | average   | count     | none | no   | no   | no   |
| Cluster Status | aws.elasticmapreduce.isidle                        | IsIdle                        | average   | count     | 1    | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.corenodesrunning              | CoreNodesRunning              | average   | count     | none | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.corenodespending              | CoreNodesPending              | average   | count     | none | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.livedatanodes                 | LiveDataNodes                 | average   | percent   | 100  | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.mrtotalnodes                  | MRTotalNodes                  | average   | count     | none | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.mractivenodes                 | MRActiveNodes                 | average   | count     | none | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.mrlostnodes                   | MRLostNodes                   | average   | count     | none | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.mrunhealthynodes              | MRUnhealthyNodes              | average   | count     | none | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.mrdecommissionednodes         | MRDecommissionedNodes         | average   | count     | none | no   | no   | no   |
| Node Status    | aws.elasticmapreduce.mrrebootednodes               | MRRebootedNodes               | average   | count     | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.s3byteswritten                | S3BytesWritten                | sum       | bytes     | none | yes  | yes  | no   |
| IO             | aws.elasticmapreduce.s3bytesread                   | S3BytesRead                   | sum       | bytes     | none | yes  | yes  | yes  |
| IO             | aws.elasticmapreduce.hdfsutilization               | HDFSUtilization               | average   | percent   | 100  | yes  | yes  | no   |
| IO             | aws.elasticmapreduce.hdfsbytesRead                 | HDFSBytesRead                 | sum       | bytes     | none | yes  | yes  | no   |
| IO             | aws.elasticmapreduce.hdfsbytesWritten              | HDFSBytesWritten              | sum       | bytes     | none | yes  | yes  | no   |
| IO             | aws.elasticmapreduce.missingblocks                 | MissingBlocks                 | average   | count     | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.corruptblocks                 | CorruptBlocks                 | average   | count     | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.totalload                     | TotalLoad                     | average   | count     | none | yes  | yes  | no   |
| IO             | aws.elasticmapreduce.memorytotalmb                 | MemoryTotalMB                 | average   | megabytes | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.memoryreservedmb              | MemoryReservedMB              | average   | megabytes | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.memoryavailablemb             | MemoryAvailableMB             | average   | megabytes | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.memoryallocatedmb             | MemoryAllocatedMB             | average   | megabytes | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.pendingdeletionblocks         | PendingDeletionBlocks         | average   | count     | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.underreplicatedblocks         | UnderReplicatedBlocks         | average   | count     | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.dfspendingreplicationblocks   | DfsPendingReplicationBlocks   | average   | count     | none | no   | no   | no   |
| IO             | aws.elasticmapreduce.capacityremaininggb           | CapacityRemainingGB           | average   | gigabytes | none | no   | no   | no   |
| HBase          | aws.elasticmapreduce.hbasebackupfailed             | HbaseBackupFailed             | average   | count     | 1    | no   | no   | no   |
| HBase          | aws.elasticmapreduce.mostrecentbackupduration      | MostRecentBackupDuration      | average   | count     | none | yes  | no   | no   |
| HBase          | aws.elasticmapreduce.timesincelastsuccessfulbackup | TimeSinceLastSuccessfulBackup | average   | count     | none | yes  | no   | no   |
