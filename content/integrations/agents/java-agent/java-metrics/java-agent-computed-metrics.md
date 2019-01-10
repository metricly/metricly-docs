---
title: "Computed Metrics"
#date: 2018-12-11
draft: false
tags: ["#java", "#integrations", "#metrics", "#agents"]
author: Lawrence Lane
---


## Computed
| Fully Qualified Name (FQN)                | Description                                                                                                                                                                                                          | Statistic | Units   | Min | Max | BASE | CORR | UTIL |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|---------|-----|-----|------|------|------|
| netuitive.jvm.heap.utilizationpercent     | Percentage of the allocated heap memory that is currently in use.Computation:(Heap Used / Heap Committed) * 100                                                                                                      | average   | percent | 0   | 100 | yes  | yes  | yes  |
| netuitive.jvm.non-heap.utilizationpercent | Percentage of the allocated non-heap memory that is currently in use.Computation:(Metaspace or PermGen Used + CodeCache Used / Metaspace or PermGen Committed + CodeCache Committed) * 100                           | average   | percent | 0   | 100 | yes  | yes  | yes  |
| netuitive.jvm.total.utilizationpercent    | Percentage of the total allocated memory that is currently in use.Computation:(Heap Used + Metaspace or PermGen Used + CodeCache Used / Heap Committed + Metaspace or PermGen Committed + CodeCache Committed) * 100 | average   | percent | 0   | 100 | yes  | yes  | yes  |
| netuitive.method.*.errorpercent           | The percentage of method calls that resulted in errors.Computation:(Method Calls == 0) ? 0 : (Method Errors / Method Calls) * 100                                                                                    | average   | percent | 0   | 100 | yes  | no   | no   |
