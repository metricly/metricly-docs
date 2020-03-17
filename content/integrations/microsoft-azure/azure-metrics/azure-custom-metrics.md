---
title: "Custom Metrics"
#date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#metrics"]
author: Lawrence Lane
---

| Fully Qualified Name (FQN)                  | Type  | Units          | Statistic | Min | Max  | Sparse Data Strategy (SDS) | BASE | CORR | UTIL | Description                                                                                                                                                                           |
|---------------------------------------------|-------|----------------|-----------|-----|------|----------------------------|------|------|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| azure.virtualmachine.networkin              | GAUGE | bytes          | average   | 0   | none | none                       | yes  | yes  | no   | Bytes received over the network. Note that this metric is the same as the Basic Metric azure.virtualmachine.networkinterface.bytesreceived                                            |
| azure.virtualmachine.networkout             | GAUGE | bytes          | average   | 0   | none | none                       | yes  | yes  | no   | Bytes transmitted over the network. Note that this metric is the same as the Basic Metric azure.virtualmachine.networkinterface.bytestransmitted                                      |
| azure.virtualmachine.diskreadbytes          | GAUGE | bytes          | average   | 0   | none | none                       | yes  | no   | no   | Average bytes read from the physical disks.                                                                                                                                           |
| azure.virtualmachine.diskreadoperationssec  | GAUGE | iops           | average   | 0   | none | none                       | yes  | no   | no   | Average number of read operations per second. Note that this metric is the same as the Basic Metric azure.virtualmachine.physicaldisk.readspersecond. Not available on classic VMs.   |
| azure.virtualmachine.diskwritebytes         | GAUGE | bytes / second | average   | 0   | none | none                       | yes  | no   | no   | Average bytes written to the physical disks.                                                                                                                                          |
| azure.virtualmachine.diskwriteoperationssec | GAUGE | iops           | average   | 0   | none | none                       | yes  | no   | no   | Average number of write operations per second. Note that this metric is the same as the Basic Metric azure.virtualmachine.physicaldisk.writespersecond. Not available on classic VMs. |
| azure.virtualmachine.percentagecpu          | GAUGE | percent        | average   | 0   | 100  | none                       | yes  | yes  | yes  | Percentage of time the processor was not idle. Note that this metric is the same as the Basic Metric  azure.virtualmachine.processor.percentprocessortime                             |
