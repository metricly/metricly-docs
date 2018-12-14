---
title: "AWS DynamoDB Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "dynamoDB", "aws"]
author: Lawrence Lane
---
{{% notice info %}}
Policy names are prefixed with **AWS DynamoDB –**
{{% /notice %}}

| Policy Name                         | Duration | Condition 1                                                                                                                              | Cat.    | Description                                                                                                                            |
|-------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------|
| Elevated Read Capacity Utilization  | 30 Min   | metricly.aws.dynamodb.readcapacityutilization has an upper baseline deviation + an upper contextual deviation + a static threshold ≥ 50. | WARNING | Read Capacity Utilization has been higher than expected for over 30 minutes; also, the actual value has been above 50% for that time.  |
| Elevated Write Capacity Utilization | 30 Min   | metricly.aws.dynamodb.writecapacityutilizationhas an upper baseline deviation +an upper contextual deviation, + a static threshold ≥ 50. | WARNING | Write Capacity Utilization has been higher than expected for over 30 minutes; also, the actual value has been above 50% for that time. |
