---
title: "AWS SQS Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "sqs", "aws"]
author: Lawrence Lane
---
{{% notice info %}}
Policy names are prefixed with **AWS SQS –**
{{% /notice %}}

| Policy name                    | Duration | Conditions                                                                            | Category | Description                                                                                                                                                          |
|--------------------------------|----------|---------------------------------------------------------------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AWS SQS – Queue Falling Behind | 2 hours  | metricly.aws.sqs.arrivalrate has a metric threshold > metricly.aws.sqs.completionrate | CRITICAL | The arrival rate for the queue has been greater than the completion rate for at least 2 hours. This is an indication that processing of the queue is falling behind. |
