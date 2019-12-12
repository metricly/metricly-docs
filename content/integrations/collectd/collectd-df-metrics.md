---
title: "Collectd DF Metrics"
#date: 2018-12-11
draft: false
tags: ["#collectd", "#integrations", "#metrics", "#df", "#collectors" ]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name(FQN)            | Description                                 | Statistic | Units | Min | Max  | Sparse Data Strategy(SDS) | BASE | CORR | UTIL |
|--------------------------------------|---------------------------------------------|-----------|-------|-----|------|---------------------------|------|------|------|
| `df-<mount>.df_complex-free.value`     | Free disk space in bytes.                   | average   | bytes | 0   | none | none                      | yes  | no   | no   |
| `df-<mount>.df_complex-reserved.value` | Disk space reserved for root user in bytes. | average   | bytes | 0   | none | none                      | yes  | no   | no   |
| `df-<mount>.df_complex-used.value`     | Used disk space in bytes.                   | average   | bytes | 0   | none | none                      | yes  | no   | no   |

## Computed

| Fully Qualified Name(FQN)           | Description                                                                        | Statistic | Units   | Min | Max  | BASE | CORR | UTIL |
|-------------------------------------|------------------------------------------------------------------------------------|-----------|---------|-----|------|------|------|------|
| `netuitive.collectd.df-*.total-space`  | **Computation**: df-*.df_complex-free + df-*.df_complex-reserved + df-*.df_complex-used | average   | bytes   | 0   | none | no   | no   | no   |
| `netuitive.collectd.df-*.used-percent` | **Computation**: (df-*.df_complex-used / netuitive.collectd.df-*.total-space) * 100      | average   | percent | 0   | 100  | no   | no   | yes  |
