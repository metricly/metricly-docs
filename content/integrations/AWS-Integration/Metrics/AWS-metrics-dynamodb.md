---
title: "DynamoDB Metrics"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "dynamoDB" ]
author: Lawrence Lane
---

## Collected
| Fully Qualified Name (FQN)                    | AWS Metric                       | Statistic | Units   | Max  | Sparse Data Strategy (SDS) | BASE | CORR |
|-----------------------------------------------|----------------------------------|-----------|---------|------|----------------------------|------|------|
| aws.dynamodb.conditionalcheckfailedrequests   | ConditionalCheckFailedRequests   | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.consumedreadcapacityunits        | ConsumedReadCapacityUnits        | sum       | count   | none | zero                       | yes  | no   |
| aws.dynamodb.consumedwritecapacityunits       | ConsumedWriteCapacityUnits       | sum       | count   | none | zero                       | yes  | no   |
| aws.dynamodb.onlineindexconsumedwritecapacity | OnlineIndexConsumedWriteCapacity | sum       | count   | none | zero                       | yes  | no   |
| aws.dynamodb.onlineindexpercentageprogress    | OnlineIndexPercentageProgress    | max       | percent | 100  | none                       | no   | no   |
| aws.dynamodb.onlineindexthrottleevents        | OnlineIndexThrottleEvents        | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.provisionedreadcapacityunits     | ProvisionedReadCapacityUnits     | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.provisionedwritecapacityunits    | ProvisionedWriteCapacityUnits    | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.readthrottleevents               | ReadThrottleEvents               | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.returnedbytes                    | ReturnedBytes                    | average   | bytes   | none | zero                       | yes  | yes  |
| aws.dynamodb.returneditemcount                | ReturnedItemCount                | average   | count   | none | zero                       | yes  | yes  |
| aws.dynamodb.returnedrecordscount             | ReturnedRecordsCount             | average   | count   | none | zero                       | yes  | yes  |
| aws.dynamodb.successfulrequestlatency         | SuccessfulRequestLatency         | average   | ms      | none | zero                       | yes  | yes  |
| aws.dynamodb.systemerrors                     | SystemErrors                     | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.throttledrequests                | ThrottledRequests                | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.usererrors                       | UserErrors                       | sum       | count   | none | zero                       | no   | no   |
| aws.dynamodb.writethrottleevents              | WriteThrottleEvents              | sum       | count   | none | zero                       | no   | no   |

## Computed

| Fully Qualified Name (FQN)                      | Description                                                                                                                                                                                          | Units   | Max | BASE | CORR | UTIL | Related Global Policies                            |
|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|------|------|------|----------------------------------------------------|
| netuitive.aws.dynamodb.readcapacityutilization  | This metric represents the percentage of the provisioned read capacity being used.Computation:((aws.dynamodb.consumedreadcapacityunits / 300) / aws.dynamodb.provisionedreadcapacityunits) * 100     | percent | 100 | yes  | yes  | yes  | AWS DynamoDB – Elevated Read Capacity Utilization  |
| netuitive.aws.dynamodb.writecapacityutilization | This metric represents the percentage of the provisioned write capacity being used.Computation: ((aws.dynamodb.consumedwritecapacityunits / 300) / aws.dynamodb.provisionedwritecapacityunits) * 100 | percent | 100 | yes  | yes  | yes  | AWS DynamoDB – Elevated Write Capacity Utilization |
