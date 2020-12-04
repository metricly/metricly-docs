---
title: "Lambda Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "lambda"]
author: Lawrence Lane
---

## Collected
| Fully Qualified Name (FQN) | AWS Metric | Statistic | Units        | Sparse Data Strategy (SDS) | BASE | CORR |
|----------------------------|------------|-----------|--------------|----------------------------|------|------|
| aws.lambda.duration        | GAUGE      | average   | milliseconds | zero                       | yes  | yes  |
| aws.lambda.errors          | GAUGE      | sum       | count        | zero                       | no   | no   |
| aws.lambda.invocations     | GAUGE      | sum       | count        | zero                       | yes  | yes  |
| aws.lambda.throttles       | GAUGE      | sum       | count        | zero                       | no   | no   |

## Computed

| Friendly Name    | FQN                                  | Computation                                                                                                                                                                                                             | Units   | Min | Max | Description                                                                                                                                                                                                                                                                                             |
|------------------|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Error Percent    | netuitive.aws.lambda.errorpercent    | (data[‘aws.lambda.invocations’] == null | data[‘aws.lambda.invocations’].actual == 0) ? 0 : (data[‘aws.lambda.errors’].actual / data[‘aws.lambda.invocations’].actual) * 100                                            | percent | 0   | 0   | The percentage of function invocations which resulted in the function returning an error.                                                                                                                                                                                                               |
| Throttle Percent | netuitive.aws.lambda.throttlepercent | (data[‘aws.lambda.invocations’] == null | data[‘aws.lambda.invocations’].actual == 0) ? 0 : (data[‘aws.lambda.throttles’].actual / (data[‘aws.lambda.invocations’].actual + data[‘aws.lambda.throttles’].actual)) * 100 | percent | 100 | 100 | The percentage of total attempted calls to the function which were throttled. Note that the AWS invocation metric does not include a count of requests which were throttled; thus, we must add “throttles” to “invocations” to get the true total number of calls for computing our percentage against. |
