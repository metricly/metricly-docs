---
title: "MySQL"
#date: 2018-12-12
draft: false
tags: ["#mysql", "#integrations" ]
author: Lawrence Lane
---
MySQL is an open source relational database management system that uses the Structured Query Language to navigate its stores. CloudWisdom can help monitor the performance and throughput of your MySQL database.

## Prerequisites

The [Linux Agent][1] must be setup before you proceed with the MySQL integration.

## Configure

1. Open the interface for the database you want to monitor and enter one of the following commands:

For Normal Usage:

```
GRANT REPLICATION CLIENT on *.* TO
'<<username>>'@'<<host>>' IDENTIFIED BY
'<<password>>';
```
If you’re having permission issues with the above command, try this one instead:

```
GRANT ALL PRIVILEGES ON * . * TO
'<<username>>'@'<<host>>';
```

For Innodb Engine Status:

```
GRANT SUPER ON *.* TO
'<<username>>'@'<<host>>' IDENTIFIED BY
 '<<password>>';
 ```

 For Innodb Engine Status on MySQL Versions 5.1.24 and Greater:

 ```
 GRANT PROCESS ON *.* TO
'<<username>>'@'<<host>>' IDENTIFIED BY
''<<password>>';
 ```


2\. Navigate to the **MySQLCollector.conf** file.  
3. The default location is `/opt/netuitive-agent/conf/collectors/MySQLCollector.conf`.  
4. Change the **enabled** setting to `True`.  
5. Change the **hosts** setting to the proper credentials:  

  - `username` is your MySQL user name  
  - `password` is your MySQL password  
  - `127.0.1.1:3306` is your host:port number respectively  
  - `mysql` is the name of your database that you want to monitor

6\. **Save** the file, and **restart** the Linux Agent.  

## Collector Options

| Option                 | Default                                                                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE                                                                                                                                                                                                                                                                                                                                                                | Enable collecting MySQL metrics.                                                                                                                   |
| hosts                  | username:password@127.0.1.1:3306/mysql,                                                                                                                                                                                                                                                                                                                              | List of hosts to collect from. Use db “None” to avoid connecting to a particular database. The format is username:password@host:port/db[/nickname] |
| master                 | TRUE                                                                                                                                                                                                                                                                                                                                                                 | Enable collecting SHOW MASTER STATUS.                                                                                                              |
| metrics_blacklist      | “^Ssl_|^Innodb_|^Com_|^Performance_schema_|^Aria_|^Feature_|^Slave_|^Uptime.*|^Handler_[^r].*|^Handler_rollback$|^Binlog|^Key_|^Qcache_|^Select_|^Sort_|^.*_tmp_.*$|^Tc_log_|^Delayed_|^Aborted_|^Threadpool_|^.*lush.*$|^Access_|^Busy_|^Cpu_|^Empty_|^Executed_|^Last_|^Open_streams$|^.*_table_definitions$|^Opened_views$|^Questions$|^Rows_|^Subquery_|^Syncs$” | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                                            |
| byte_unit              |                                                                                                                                                                                                                                                                                                                                                                      | Default numeric output(s).                                                                                                                         |
| innodb                 |                                                                                                                                                                                                                                                                                                                                                                      | Enable collecting SHOW ENGINE INNODB STATUS.                                                                                                       |
| measure_collector_time |                                                                                                                                                                                                                                                                                                                                                                      | Measure the collector’s run time in milliseconds.                                                                                                  |
| metrics_whitelist      |                                                                                                                                                                                                                                                                                                                                                                      | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                                         |
| publish                |                                                                                                                                                                                                                                                                                                                                                                      | Which SHOW GLOBAL STATUS rows you would like to publish, or leave blank to publish all rows.                                                       |
| slave                  |                                                                                                                                                                                                                                                                                                                                                                      | Enable collecting SHOW SLAVE STATUS.                                                                                                               |

[1]: /integrations/agents/linux-agent
