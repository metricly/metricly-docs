---
title: "MySQL Metrics"
#date: 2018-12-11
draft: false
tags: ["#metrics", "#integrations", "#mysql" ]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name (FQN) | Description | Type | Units | Statistic* | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-------|------------|-----|------|----------------------------|------|------|------|
| mysql.Bytes_received | The total number of bytes received by the server over the interval. | counter | bytes |  | 0 | none | none | yes | yes | no |
| mysql.Bytes_sent | The total number of bytes sent by the server over the interval. | counter | bytes |  | 0 | none | none | yes | yes | no |
| mysql.Connections | The total number of connection attempts made to the server over the previous interval. | counter | count |  | 0 | none | none | yes | no | no |
| mysql.Handler_read | The total number of times that the query handler read various sectionsof the indices. These metrics are important for computing the percentageof full table scans. | counter | count |  | 0 | none | none | no | no | no |
| mysql.Max_used_connections | The maximum number of connections that have ever been open concurrently since the server was started. This will be a relatively static number. | gauge | count | max | 0 | none | none | no | no | no |
| mysql.Open_files | The raw data received every minute represents the number of currently open files at that minute. The 5-minute data is the average number offiles in an open state during the previous 5 minutes. | gauge | count | average | 0 | none | none | no | no | no |
| mysql.Open_tables | The raw data received every minute represents the number of currently open tables at that minute. The 5-minute data is the average number oftables in an open state during the previous 5 minutes. | gauge | count | average | 0 | none | none | no | no | no |
| mysql.Opened_files | The total number of files that were opened during the previous interval.Note that some (or all) of them may have been closed during the intervalas well. | counter | count |  | 0 | none | none | yes | yes | no |
| mysql.Opened_tables | The total number of tables that were opened during the previousinterval. Note that some (or all) of them may have been closed duringthe interval as well. | counter | count |  | 0 | none | none | yes | yes | no |
| mysql.Prepared_stmt_count | The raw data received every minute represents the current number of prepared statements at that minute. The 5-minute data is the averagenumber of prepared statements during the previous 5 minutes. | counter | count |  | 0 | none | none | no | no | no |
| mysql.Queries | The total number of queries made to the server over the previous interval. | counter | count |  | 0 | none | none | yes | yes | no |
| mysql.Slow_launch_threads | The total number of threads that were slow to launch during the previous interval. | counter | count |  | 0 | none | none | no | no | no |
| mysql.Slow_queries | The total number of queries that were slow to execute during the previous interval. | counter | count |  | 0 | none | none | no | no | no |
| mysql.Table_locks_immediate | The total number of requested table locks that the server was able togrant immediately during the previous interval. | gauge | count | sum | 0 | none | none | yes | yes | no |
| mysql.Table_locks_wait | The total number of requested table locks that the server had to wait before granting during the previous interval. | gauge | count | sum | 0 | none | none | yes | yes | no |
| mysql.Threads_cached | The raw data received every minute represents the current number of threads in the thread cache at that minute. The 5-minute data is theaverage number of threads in the cache during the previous 5 minutes. | counter | count |  | 0 | none | none | yes | yes | no |
| mysql.Threads_connected | The raw data received every minute represents the current number of connections at that minute. The 5-minute data is the average number ofconnections during the previous 5 minutes. | counter | count |  | 0 | none | none | yes | yes | no |
| mysql.Threads_created | The raw data received is a counter, representing the total number of threads that have been created since the server was last started. The5-minute data computes the deltas in these values to give the totalnumber of threads created over the past 5 minutes. | counter | count |  | 0 | none | none | yes | yes | no |
| mysql.Threads_.* | The raw data received every minute represents the current number of threads which are running at that minute. The 5-minute data is theaverage number of threads running during the previous 5 minutes. | gauge | count | average | 0 | none | none | yes | yes | no |

### Slave metrics

To collect slave metrics, update the **MySQLCollector.conf** file in the [Linux Agent][1] with the following:
```
slave = True
```
| Fully Qualified Name (FQN) | Description | Type | Units | Statistic* | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-------|------------|-----|------|----------------------------|------|------|------|
| mysql.Connect_Retry | The number of seconds between connect retries (default 60) | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Skip_Counter | The current value of the sql_slave_skip_counter system variable | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Relay_Log_Pos | The position in the current relay log file up to which the SQL thread has read and executed. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Master_Retry_Count | The number of times the slave can attempt to reconnect to the master in the event of a lost connection. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Until_Log_Pos | The values specified in the UNTIL clause of the START SLAVE statement. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Auto_Position | 1 if autopositioning is in use; otherwise 0. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Read_Master_Log_Pos | The position in the current master binary log file up to which the I/O thread has read. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.SQL_Delay | The number of seconds that the slave must lag the master. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Seconds_Behind_Master | The time in seconds a slave is behind its master. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Exec_Master_Log_Pos | The position in the current master binary log file to which the SQL thread has read and executed, marking the start of the next transaction or event to be processed. | counter | none |  | 0 | none | none | yes | no | no |
| mysql.Relay_Log_Space | The total combined size of all existing relay log files. | counter | none |  | 0 | none | none | yes | no | no |


## Computed

| Name                           | Fully Qualified Name (FQN)                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Units   | Min | Max | BASE | CORR | UTIL |
|--------------------------------|------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|------|
| Percentage of Full Table Scans | metricly.linux.mysql.fulltablescans.percentage | A full table scan occurs when a query is unable to use an index toassist with its execution, and therefore is required to parse the entiretable to find all the rows that satisfy the query. This metric reportsthe percentage of queries that needed to perform full table scans.Computation:100 * ((data[‘mysql.Handler_read_rnd_next’].actual +data[‘mysql.Handler_read_rnd’].actual) /(data[‘mysql.Handler_read_rnd_next’].actual +data[‘mysql.Handler_read_rnd’].actual +data[‘mysql.Handler_read_first’].actual +data[‘mysql.Handler_read_next’].actual +data[‘mysql.Handler_read_key’].actual +data[‘mysql.Handler_read_prev’].actual)) | percent | 0   | 100 | yes  | yes  | no   |
| Percentage of Slow Queries     | metricly.linux.mysql.slowqueries.percentage    | Percentage of queries that are running slow.Computation:(data[‘mysql.Queries’].actual == null || data[‘mysql.Queries’].actual ==0) ? 0 : 100 * (data[‘mysql.Slow_queries’].actual /data[‘mysql.Queries’].actual)                                                                                                                                                                                                                                                                                                                                                                                                                               | percent | 0   | 100 | no   | no   | no   |


[1]: /integrations/agents/linux-agent/linux-collectors/
