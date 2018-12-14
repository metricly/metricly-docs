---
title: "Metrics"
#date: 2018-12-12
draft: false
tags: ["ngnix", "integrations", "metrics" ]
author: Lawrence Lane
---
## Collected

| Fully Qualified Name (FQN) | Description                                                                          | Statistic | Units | Min | Max  | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------|--------------------------------------------------------------------------------------|-----------|-------|-----|------|----------------------------|------|------|------|
| nginx.act_reads            | The average number of active connections that were reading during theprior interval. | average   | count | 0   | none | none                       | yes  | yes  | no   |
| nginx.act_waits            | The average number of active connections that were waiting during theprior interval. | average   | count | 0   | none | none                       | yes  | yes  | no   |
| nginx.act_writes           | The average number of active connections that were writing during theprior interval. | average   | count | 0   | none | none                       | yes  | yes  | no   |
| nginx.active_connections   | The average number of active connections during the prior interval.                  | average   | count | 0   | none | none                       | yes  | yes  | no   |
| nginx.conn_accepted        | The total number of connections accepted during the prior interval.                  | sum       | count | 0   | none | none                       | yes  | yes  | no   |
| nginx.conn_handled         | The total number of connections handled during the prior interval.                   | sum       | count | 0   | none | none                       | yes  | yes  | no   |
| nginx.req_handled          | The total number of requests handled during the prior interval.                      | sum       | count | 0   | none | none                       | yes  | yes  | no   |

## Computed

| Fully Qualified Name (FQN)             | Description                                                                                                                                                                                                     | Units | Min | Max  | BASE | CORR | UTIL |
|----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|-----|------|------|------|------|
| metricly.nginx.requests_per_connection | The average number of requests handled by each connection during theprior interval.Computation:data[‘nginx.conn_handled’].actual == 0 ? 0: data[‘nginx.req_handled’].actual / data[‘nginx.conn_handled’].actual | count | 0   | none | yes  | no   | no   |
| metricly.nginx.requests_per_second     | The average number of requests per second.Computation:data[‘nginx.req_handled’].actual / 300                                                                                                                    | ops   | 0   | none | yes  | no   | no   |
