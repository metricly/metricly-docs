---
title: "Diamond Diskspace Metrics"
#date: 2018-12-11
draft: false
tags: ["#diamond", "#integrations", "#agents", "#diskspace" ]
author: Lawrence Lane
---
## Collected
| Fully Qualified Name(FQN)         | Description               | Statistic | Units   | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|-----------------------------------|---------------------------|-----------|---------|-----|-----|----------------------------|------|------|------|
| diskspace.<disk>.byte_percentfree | Percentage of free bytes. | average   | percent | 0   | 100 | none                       | yes  | no   | no   |

## Computed
| Fully Qualified Name(FQN)                       | Description                                                                    | Units   | Min | Max | BASE | CORR | UTIL |
|-------------------------------------------------|--------------------------------------------------------------------------------|---------|-----|-----|------|------|------|
| netuitive.linux.diskspace.*.byte_percentused | Percentage of disk space used. Computation: 100 – diskspace.*.byte_percentfree | percent | 0   | 100 | no   | no   | yes  |
