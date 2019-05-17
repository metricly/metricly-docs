---
title: "AWS Lambda Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#policies", "#default policies", "#elb", "#aws"]
author: Lawrence Lane
---
{{% notice info %}}
Policy names are prefixed with **AWS Lambda –**
{{% /notice %}}

| Policy name                                 | Duration | Conditions                                                                             | Category | Description                                                               |
|---------------------------------------------|----------|----------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------|
| Elevated Invocation Count                   | 30 min   | aws.lambda.invocations has an upper baseline deviation + an upper contextual deviation | WARNING  | The number of calls to the function (invocations) have been greater than expected for at least the last 30 minutes.  |          |                                                                           |
| Depressed Invocation Count                  | 10 min   | aws.lambda.invocations has a lower baseline deviation + a lower contextual deviation   | WARNING  | The number of calls to the function (invocations) have been lower than expected for at least the last 10 minutes. |          |                                                                           |
| Elevated Latency                            | 30 min   | aws.lambda.duration has an upper baseline deviation + an upper contextual deviation    | WARNING  | The average duration per function call (latency) has been higher than expected for at least the past 30 minutes.         |                                                                           |
