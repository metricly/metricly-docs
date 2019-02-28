---
title: "Microsoft SQL Metrics"
#date: 2018-12-11
draft: false
tags: ["#metrics", "#integrations", "#microsoft sql" ]
author: Lawrence Lane
---
## Collected

| Category           | Instance  | Fully Qualified Name (FQN)            | Description                                                               |
|--------------------|-----------|---------------------------------------|---------------------------------------------------------------------------|
| Process            | sqlserver | sql_server.percent_processor_time     | The percentage of time the processor is busy.                             |
| General Statistics | N/A       | sql_server.user_connections           | The number of users currently connected to the SQL Server.                |
| General Statistics | N/A       | sql_server.processes_blocked          | The number of processes that are blocked.                                 |
| Locks              | _Total    | sql_server.total_lock_waits_per_sec   | The number of locks per second that had to wait for resources.            |
| SQL Statistics     | N/A       | sql_server.batch_requests_per_sec     | The number of batches the server is receiving per second.                 |
| SQL Statistics     | N/A       | sql_server.sqL-compilations_per_sec   | The number of SQL compiles per second.                                    |
| SQL Statistics     | N/A       | sql_server.sql_recompilations_per_sec | The number of SQL recompiles per second.                                  |
| Buffer Manager     | N/A       | sql_server.checkpoint_pages_per_sec   | The number of pages written to disk per second by a checkpoint operation. |
| Buffer Manager     | N/A       | sql_server.buffer_cache_hit_ratio     | The ratio of how many pages are going to memory versus the disk.          |
| Buffer Manager     | N/A       | sql_server.page_life_expectancy       | The number of seconds a page is in the buffer pool without references.    |
| Access Methods     | N/A       | sql_server.page_splits_per_sec        | The number of page splits occurring per second.                           |

## Computed

| Fully Qualified Name (FQN)                          | Description                                                                                                                                                                                                | Units   | Min | Max  | BASE | CORR | UTIL |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|------|------|------|------|
| metricly.linux.mongo.connections.utilizationpercent | The percentage of available connections currently being utilized. Computation: (mongo.connections.current / (mongo.connections.current +mongo.connections.available)) * 100                                | percent | 0   | 100  | yes  | no   | yes  |
| metricly.linux.mongo.opcounters.totalreads          | The total number of read operations currently taking place (reads include both query and getmore requests). Computation: mongo.opcounters.query + mongo.opcounters.germore                                 | count   | 0   | none | yes  | no   | no   |
| metricly.linux.mongo.opcounters.totalwrites         | The total number of write operations currently taking place (writes include insert, update, and delete requests). Computation: mongo.opcounters.insert + mongo.opcounters.update + mongo.opcounters.delete | count   | 0   | none | yes  | no   | no   |
