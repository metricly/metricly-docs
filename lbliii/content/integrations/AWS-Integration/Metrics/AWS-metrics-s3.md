---
title: "S3 Metrics"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "s3"]
author: Lawrence Lane
---

## Collected

| Friendly Name         | Fully Qualified Name (FQN) | AWS Metric          | Statistic | Units       | BASE |
|-----------------------|----------------------------|---------------------|-----------|-------------|------|
| Bucket Size Bytes     | aws.s3.bucketsizebytes     | BucketSizeBytes     | average   | GiB/KiB     | yes  |
| Number of Objects     | aws.s3.NumberOfObjects     | NumberOfObjects     | average   | K           | yes  |
| 4xx Errors            | aws.s3.4xxerrors           | 4xxErrors           | average   | count       | yes  |
| 4xx Errors            | aws.s3.5xxerrors           | 5xxErrors           | average   | count       | yes  |
| All Requests          | aws.s3.allrequests         | AllRequests         | average   | count       | yes  |
| First Byte Latency    | aws.s3.firstbytelatency    | FirstByteLatency    | average   | miliseconds | yes  |
| Hard Requests         | aws.s3.headrequests        | HeadRequests        | average   | count       | yes  |
| Total Request Latency | aws.s3.totalrequestlatency | TotalRequestLatency | average   | miliseconds | yes  |
