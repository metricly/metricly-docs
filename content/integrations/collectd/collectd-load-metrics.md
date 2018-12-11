---
title: "Load Metrics"
date: 2018-12-11
draft: true
tags: ["collectd", "integrations", "metrics", "load" ]
author: Lawrence Lane
---

## Collected
| Fully Qualified Name(FQN) | Description                                                 | Statistic | Units            | Min | Max  | Sparse Data Strategy(SDS) | BASE | CORR | UTIL |
|---------------------------|-------------------------------------------------------------|-----------|------------------|-----|------|---------------------------|------|------|------|
| load.load.longterm        | The is the average run queue size over the past 15 minutes. | average   | queued processes | 0   | none | none                      | yes  | no   | no   |
| load.load.midterm         | The is the average run queue size over the past 5 minutes.  | average   | queued processes | 0   | none | none                      | yes  | yes  | no   |
| load.load.shortterm       | The is the average run queue size over the past minute.     | average   | queued processes | 0   | none | none                      | yes  | no   | no   |
