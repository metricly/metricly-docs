---
title: "AWS ASG Policies"
date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "asg", "aws"]
author: Lawrence Lane
---

{{% notice info %}}
Policy names are prefixed with **AWS ASG –**
{{% /notice %}}

| Policy name                                    | Duration | Condition 1                                                                           | (and) Condition 2                                                                         | (and) Condition 3                                                                             | Cat. | Description                                                                                                                                                                                                                                  |
|------------------------------------------------|----------|---------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Elevated CPUActivity (Normal Network Activity) | 30 min   | aws.ec2.cpuutilization has an upper baseline + upper contextual deviation             | metricly.aws.ec2.bytesinperse does not have a upper baseline + upper contextual deviation | metricly.aws.ec2.bytesoutpersec does not  have a upper baseline + upper contextual deviation. | INFO | This policy is designed to catch cases where CPU activity is higher than than normal and cannot be explained by a corresponding increase in network traffic. Operates on the average CPU and network utilization across all EC2’sin the ASG. |
| Elevated Network Activity                      | 30 min   | metricly.aws.ec2.bytesinpersec has an upper baseline + upper contextual deviation     | metricly.aws.ec2.bytesoutperse has an upper baseline + upper contextual deviation         |                                                                                               | INFO | Indicates an increase in network activity above what is considered to be normal. Operates on the average network utilization across all EC2’s in the ASG.                                                                                    |
| Elevated EphemeralDisk Activity                | 30 min   | metricly.aws.ec2.diskreadopspersec has an upper baseline + upper contextual deviation | metricly.aws.ec2.diskwriteopspersec has an upper baseline + upper contextual deviation    |                                                                                               | INFO | Indicates an increase in disk activity above what is considered to be normal. Operates on the average disk utilization across all EC2’s in the ASG.                                                                                          |
