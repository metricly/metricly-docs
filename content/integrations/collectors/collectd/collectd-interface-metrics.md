---
title: "Interface Metrics"
date: 2018-12-11
draft: false
tags: ["collectd", "integrations", "metrics", "interface", "collectors" ]
author: Lawrence Lane
---

## Collected
| Fully Qualified Name(FQN)     | Description                  | Statistic | Units          | Min | Max  | Sparse Data Strategy(SDS) | BASE | CORR | UTIL |
|-------------------------------|------------------------------|-----------|----------------|-----|------|---------------------------|------|------|------|
| `interface-<int>.if_errors.rx`  | Errors per second received.  | average   | errors/second  | 0   | none | none                      | yes  | no   | no   |
| `interface-<int>.if_errors.tx`  | Errors per second sent.      | average   | errors/second  | 0   | none | none                      | yes  | no   | no   |
| `interface-<int>.if_octets.rx`  | Bytes per second received.   | average   | bytes/second   | 0   | none | none                      | yes  | no   | no   |
| `interface-<int>.if_octets.tx`  | Bytes per second sent.       | average   | bytes/second   | 0   | none | none                      | yes  | no   | no   |
| `interface-<int>.if_packets.rx` | Packets per second received. | average   | packets/second | 0   | none | none                      | yes  | no   | no   |
| `interface-<int>.if_packets.tx` | Packets per second sent.     | average   | packets/second | 0   | none | none                      | yes  | no   | no   |

## Computed

| Fully Qualified Name(FQN)                       | Description                                                                                                                                   | Statistic | Units          | Min | Max  | BASE | CORR | UTIL |
|-------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------------|-----|------|------|------|------|
| `metricly.collectd.interface-*.if_errors.total`   | Errors per second received.Computation:interface-*.if_errors.tx + interface-*.if_errors.rx                                                    | average   | errors/second  | 0   | none | yes  | no   | no   |
| `metricly.collectd.interface-*.if_octets.total`   | Bytes per second received.Computation:interface-*.if_octets.tx + interface-*.if_octets.rx                                                     | average   | bytes/second   | 0   | none | yes  | no   | no   |
| `metricly.collectd.interface-*.if_packets.total`  | Packets per second received.Computation:interface-*.if_packets.tx + interface-*.if_packets.rx                                                 | average   | packets/second | 0   | none | yes  | yes  | no   |
| `metricly.collectd.interface-*.if_errors.percent` | Percentage of packet errors.Computation:(metricly.collectd.interface-*.if_errors.total /metricly.collectd.interface-*.if_packets.total) * 100 | average   | percent        | 0   | 100  | yes  | yes  | no   |
