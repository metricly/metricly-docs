---
title: "Application Gateway"
date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["microsoft", "azure", "integrations", "metrics"]
author: Lawrence Lane
---

| Fully Qualified Name (FQN)          | Type  | Units        | Statistic | Min | Max  | Sparse Data Strategy | BASE | CORR | UTIL | Description                                                    |
|-------------------------------------|-------|--------------|-----------|-----|------|----------------------|------|------|------|----------------------------------------------------------------|
| azure.applicationgateway.throughput | GAUGE | bytes/second | average   | 0   | none | none                 | yes  | no   | no   | The number of bytes per second being processed by the gateway. |
