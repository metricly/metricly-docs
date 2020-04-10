---
title: "S3 Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["#aws", "#metrics", "#s3"]
author: Lawrence Lane
---

There are three groups of S3 metrics: Daily storage metrics for buckets, Request metrics, and Replication metrics. The first group includes two metrics: Bucket Size Bytes and Number of Objects. These metrics are free of charge and reported by AWS once daily.

The other metrics are billed additionally by AWS. You can opt in for request metrics through the Management tab of the S3 configuration in the AWS console.

## Collected

| Friendly Name                | Fully Qualified Name (FQN)                | AWS Metric                   | Statistic | Units       | BASE |
|------------------------------|-------------------------------------------|------------------------------|-----------|-------------|------|
| Bucket Size Bytes            | aws.s3.bucketsizebytes                    | BucketSizeBytes              | average   | GiB/KiB     | yes  |
| Number of Objects            | aws.s3.NumberOfObjects                    | NumberOfObjects              | average   | K           | yes  |
| 4xx Errors                   | aws.s3.4xxerrors                          | 4xxErrors                    | average   | count       | yes  |
| 5xx Errors                   | aws.s3.5xxerrors                          | 5xxErrors                    | average   | count       | yes  |
| All Requests                 | aws.s3.allrequests                        | AllRequests                  | average   | count       | yes  |
| First Byte Latency           | aws.s3.firstbytelatency                   | FirstByteLatency             | average   | milliseconds| yes  |
| Head Requests                | aws.s3.headrequests                       | HeadRequests                 | average   | count       | yes  |
| Total Request Latency        | aws.s3.totalrequestlatency                | TotalRequestLatency          | average   | milliseconds| yes  |
| Get Requests                 | aws.s3.getrequests                        | GetRequests                  | average   | count       | yes  |
| Put Requests                 | aws.s3.putrequests                        | PutRequests                  | average   | count       | yes  |
| Delete Requests              | aws.s3.deleterequests                     | DeleteRequests               | average   | count       | yes  |
| Post Requests                | aws.s3.postrequests                       | PostRequests                 | average   | count       | yes  |
| Select Requests              | aws.s3.selectrequests                     | SelectRequests               | average   | count       | yes  |
| Select Scanned Bytes         | aws.s3.selectscannedbytes                 | SelectScannedBytes           | average   | count       | yes  |
| Select Returned Bytes        | aws.s3.selectreturnedbytes                | SelectReturnedBytes          | average   | count       | yes  |
| List Requests                | aws.s3.listrequests                       | ListRequests                 | average   | count       | yes  |
| Bytes Downloaded             | aws.s3.bytesdownloaded                    | BytesDownloaded              | average   | count       | yes  |
| Bytes Uploaded               | aws.s3.bytesuploaded                      | BytesUploaded                | average   | count       | yes  |
| Replication Latency          | aws.s3.replicationlatency                 | ReplicationLatency           | average   | seconds     | yes  |
| Bytes Pending Replication    | aws.s3.bytespendingreplication            | BytesPendingReplication      | average   | GiB/KiB     | yes  |
| OperationsPendingReplication | aws.s3.operationspendingreplication       | OperationsPendingReplication | average   | count       | yes  |
