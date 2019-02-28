---
title: "Diamond Network Metrics"
#date: 2018-12-11
draft: false
tags: ["#diamond", "#integrations", "#agents", "#network" ]
author: Lawrence Lane
---

## Computed
| Fully Qualified Name(FQN)                   | Description                                                                                                                                           | Units   | Min | Max  | BASE | CORR | UTIL |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|------|------|------|------|
| metriclyicly.linux.network.*.errors         | The total number of errors, both transmit and receive. **Computation**: network.*.rx_errors + network.*.tx_errors                                           | errors  | 0   | none | yes  | no   | no   |
| metriclyicly.linux.network.*.packets        | The total number of packets, both transmitted and received. **Computation**: network.*.rx_packets + network.*.tx_packets                                    | packets | 0   | none | yes  | yes  | no   |
| metriclyicly.linux.network.*.errors.percent | The percentage of errors, both transmit and receive. **Computation**: (metriclyicly.diamond.network.*.errors /metriclyicly.diamond.network.*.packets) * 100 | percent | 0   | 100  | yes  | no   | no   |
