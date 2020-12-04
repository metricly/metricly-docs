---
title: "Kinesis Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "kinesis"]
author: Lawrence Lane
---
Currently, CloudWisdom only supports Kinesis Streams, but additional support for Kinesis Firehose may come in the future.

## Collected
| Fully Qualified Name (FQN)                     | AWS Metric                         | Statistic | Units | Sparse Data Strategy (SDS) | BASE | CORR |
|------------------------------------------------|------------------------------------|-----------|-------|----------------------------|------|------|
| aws.kinesis.getrecords.bytes                   | GetRecords.Bytes                   | average   | bytes | zero                       | yes  | yes  |
| aws.kinesis.getrecords.iteratoragemilliseconds | GetRecords.IteratorAgeMilliseconds | average   | ms    | zero                       | yes  | no   |
| aws.kinesis.getrecords.latency                 | GetRecords.Latency                 | average   | ms    | zero                       | yes  | yes  |
| aws.kinesis.getrecords.records                 | GetRecords.Records                 | sum       | ops   | zero                       | yes  | yes  |
| aws.kinesis.getrecords.success                 | GetRecords.Success                 | sum       | ops   | zero                       | yes  | yes  |
| aws.kinesis.incomingbytes                      | IncomingBytes                      | sum       | bytes | zero                       | yes  | yes  |
| aws.kinesis.incomingrecords                    | IncomingRecords                    | sum       | ops   | zero                       | yes  | yes  |
| aws.kinesis.putrecord.bytes                    | PutRecord.Bytes                    | sum       | bytes | zero                       | yes  | yes  |
| aws.kinesis.putrecord.latency                  | PutRecord.Latency                  | average   | ms    | zero                       | yes  | yes  |
| aws.kinesis.putrecord.success                  | PutRecord.Success                  | sum       | ops   | zero                       | yes  | yes  |
| aws.kinesis.putrecords.bytes                   | PutRecords.Bytes                   | sum       | bytes | zero                       | yes  | yes  |
| aws.kinesis.putrecords.latency                 | PutRecords.Latency                 | average   | ms    | zero                       | yes  | yes  |
| aws.kinesis.putrecords.records                 | PutRecords.Records                 | sum       | ops   | zero                       | yes  | yes  |
| aws.kinesis.putrecords.success                 | PutRecords.Success                 | sum       | ops   | zero                       | yes  | yes  |
| aws.kinesis.readprovisionedthroughputexceeded  | ReadProvisionedThroughputExceeded  | sum       | ops   | zero                       | no   | no   |
| aws.kinesis.writeprovisionedthroughputexceeded | WriteProvisionedThroughputExceeded | sum       | ops   | zero                       | no   | no   |
