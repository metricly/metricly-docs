---
title: "Disk Metrics"
date: 2018-12-11
draft: true
tags: ["collectd", "integrations", "metrics", "disk", "collectors" ]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name(FQN)   | Description                         | Statistic | Units             | Min | Max  | Sparse Data Strategy(SDS) | BASE | CORR | UTIL |
|-----------------------------|-------------------------------------|-----------|-------------------|-----|------|---------------------------|------|------|------|
| `disk-<dn>.disk_merged.read`  | Number of merged reads per second.  | average   | operations/second | 0   | none | none                      | yes  | no   | no   |
| `disk-<dn>.disk_merged.write` | Number of merged writes per second. | average   | operations/second | 0   | none | none                      | yes  | no   | no   |
| `disk-<dn>.disk_octets.read`  | Bytes read per second.              | average   | bytes/second      | 0   | none | none                      | yes  | no   | no   |
| `disk-<dn>.disk_octets.write` | Bytes written per second.           | average   | bytes/second      | 0   | none | none                      | yes  | no   | no   |
| `disk-<dn>.disk_ops.read`     | Read operations per second.         | average   | operations/second | 0   | none | none                      | yes  | no   | no   |
| `disk-<dn>.disk_ops.write`    | Write operations per second.        | average   | operations/second | 0   | none | none                      | yes  | no   | no   |
| `disk-<dn>.disk_time.read`    | Average time for read ops.          | average   | milliseconds      | 0   | none | none                      | yes  | no   | no   |
| `disk-<dn>.disk_time.write`   | Average time for write ops.         | average   | milliseconds      | 0   | none | none                      | yes  | no   | no   |

## Computed

| Fully Qualified Name(FQN)                    | Description                                                                                                                                                                                                                                                                                | Statistic | Units             | Min | Max  | BASE | CORR | UTIL |
|----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|-------------------|-----|------|------|------|------|
| `metricly.collectd.disk-*.disk_ops.total`      | Total number of operations in the interval.Computation:(disk-*.disk_ops.read + disk-*.disk_ops.write) * 300                                                                                                                                                                                | sum       | operations        | 0   | none | no   | no   | no   |
| `metricly.collectd.disk-*.disk_ops.readwrite`  | Operations per second (IOPS).Computation:disk-*.disk_ops.read + disk-*.disk_ops.write                                                                                                                                                                                                      | average   | operations/second | 0   | none | yes  | yes  | no   |
| `metricly.collectd.disk-*.disk_time.readwrite` | Average time for all operations (latency).Computation:((disk-*.disk_time.read * (disk-*.disk_ops.read * 300)) +(disk-*.disk_time.write * (disk-*.disk_ops.write * 300))) /metricly.collectd.disk-*.disk_ops.total                                                                          | average   | milliseconds      | 0   | none | yes  | yes  | no   |
| `metricly.collectd.disk-*.disk_busy.percent`   | Percent of five-minute interval the disk is busy serving IO requests.Computation:(((data[‘disk-${1}.disk_ops.read’].actual * 300 * data[‘disk-${1}.disk_time.read’].actual)+ (data[‘disk-${1}.disk_ops.write’].actual * 300 * data[‘disk-${1}.disk_time.write’].actual))/ (300000)) * 100} | average   | percent           | 0   | 100  | yes  | no   | no   |
