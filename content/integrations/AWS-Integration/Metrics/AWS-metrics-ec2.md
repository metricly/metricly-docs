---
title: "EC2 Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["#aws", "#metrics", "#ec2"]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name (FQN)         | AWS Metric                 | Statistic | Units   | Max  | BASE | CORR | UTIL |
|------------------------------------|----------------------------|-----------|---------|------|------|------|------|
| aws.ec2.cpucreditbalance           | CPUCreditBalance           | average   |         | none | yes  | no   | no   |
| aws.ec2.cpucreditusage             | CPUCreditUsage             | sum       |         | none | yes  | no   | no   |
| aws.ec2.cpuutilization             | CPUUtilizationPercent      | average   | percent | 100  | yes  | yes  | yes  |
| aws.ec2.diskreadbytes              | DiskReadBytes              | sum       | bytes   | none | no   | no   | no   |
| aws.ec2.diskreadops                | DiskReadOps                | sum       |         | none | no   | no   | no   |
| aws.ec2.diskwritebytes             | DiskWriteBytes             | sum       | bytes   | none | no   | no   | no   |
| aws.ec2.diskwriteops               | DiskWriteOps               | sum       |         | none | no   | no   | no   |
| aws.ec2.networkin                  | NetworkIn                  | sum       | bytes   | none | no   | no   | no   |
| aws.ec2.networkout                 | NetworkOut                 | sum       | bytes   | none | no   | no   | no   |
| aws.ec2.statuscheckfailed          | StatusCheckFailed          | sum       |         | 5    | yes  | no   | no   |
| aws.ec2.statuscheckfailed_instance | StatusCheckFailed_Instance | sum       |         | 5    | yes  | no   | no   |
| aws.ec2.statuscheckfailed_system   | StatusCheckFailed_System   | sum       |         | 5    | yes  | no   | no   |

## Computed

| Fully Qualified Name (FQN)             | Description                                                                                                                                                                                                                                                  | Units             | BASE | CORR | Related Global Policies                                                           |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|------|------|-----------------------------------------------------------------------------------|
| netuitive.aws.ec2.diskreadbytespersec  | This metric expresses the number of bytes read per second from the ephemeral disk of an EC2 instance. This metric is useful for monitoring ephemeral disk read activity.Computation:metricly.aws.ec2.diskreadbytespersec / 300                               | bytes/second      | yes  | yes  |                                                                                   |
| netuitive.aws.ec2.diskwritebytespersec | This metric expresses the number of bytes written per second to the ephemeral disk of an EC2 instance. This metric is useful for monitoring ephemeral disk write activity.Computation:metricly.aws.ec2.diskwritebytespersec / 300                            | bytes/second      | yes  | yes  |                                                                                   |
| netuitive.aws.ec2.diskreadopspersec    | This metric expresses the number of read operations per second from the ephemeral disk of an EC2 instance. This metric is useful for monitoring ephemeral disk read activity.Computation:metricly.aws.ec2.diskreadopspersec / 300                            | operations/second | yes  | yes  | Elevated EC2 Ephemeral Disk Activity                                              |
| netuitive.aws.ec2.diskwriteopspersec   | This metric expresses the number of write operations per second to the ephemeral disk of an EC2 instance. This metric is useful for monitoring ephemeral disk write activity.Computation:metricly.aws.ec2.diskwriteopspersec / 300                           | operations/second | yes  | yes  | Elevated EC2 Ephemeral Disk Activity                                              |
| netuitive.aws.ec2.disktotalops         | This metric expresses the total number of read and write operations against the ephemeral disk of an EC2 instance. This metric is useful for monitoring ephemeral disk I/O activity.Computation:metricly.aws.ec2.diskreadops + metricly.aws.ec2.diskwriteops | operations        | yes  | no   |                                                                                   |
| netuitive.aws.ec2.diskiops             | This metric expresses the total IOPS performed against the ephemeral disk of an EC2 instance. This metric is useful for monitoring ephemeral disk I/O activity.Computation:(metricly.aws.ec2.disktotalops) / 300                                             | operations/second | no   | no   |                                                                                   |
| netuitive.aws.ec2.bytesinpersec        | This metric expresses the number of network bytes received per second by an EC2 instance. This metric is useful for monitoring network receive activity.Computation: aws.ec2.networkin / 300                                                                 | bytes/second      | yes  | yes  | Elevated EC2 CPU Activity (Normal Network Activity) Elevated EC2 Network Activity |
| netuitive.aws.ec2.bytesoutpersec       | This metric expresses the number of network bytes written per second by an EC2 instance. This metric is useful for monitoring network transmit activity.Computation: aws.ec2.networkout / 300                                                                | bytes/second      | yes  | yes  | Elevated EC2 CPU Activity (Normal Network Activity) Elevated EC2 Network Activity |
