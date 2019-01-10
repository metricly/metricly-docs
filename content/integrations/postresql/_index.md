---
title: "PostreSQL"
#date: 2018-12-12
draft: false
tags: ["#postresql", "#integrations" ]
author: Lawrence Lane
---
PostgreSQL is an open-source database management system. Metricly can be used to monitor your PostgreSQL database(s).

## Prerequisites
- [Linux Agent][1]

## Configure

1. Navigate to the collectors folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **PostgresqlCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. Update the **dbname** setting to the `name` of your database.
5. Update the **user** and **password** settings to the proper credentials used to access the database.
6. **Save** the configuration file, and **restart** the Linux Agent.

## Collector Options

| Option                 | Default       | Description                                                                                                                                                                                         |
|------------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE         | Enable collecting PostgreSQL metrics.                                                                                                                                                               |
| host                   | localhost     | Hostname to collect from                                                                                                                                                                            |
| dbname                 | postgres      | Database that contains list of databases in PostgreSQL.                                                                                                                                             |
| user                   | postgres      | Username used for database authentication.                                                                                                                                                          |
| password               | postgres      | Password used for database authentication.                                                                                                                                                          |
| port                   | 5432          | Port to collect from.                                                                                                                                                                               |
| metrics_whitelist      | “^database.*” | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                                                                                          |
| byte_unit              |               | Default numeric output(s).                                                                                                                                                                          |
| extended               |               | Enable collecting extended database stats.                                                                                                                                                          |
| has_admin              |               | Setting that notes if admin privileges are required to run some queries.                                                                                                                            |
| measure_collector_time |               | Measure the collector’s run time in milliseconds.                                                                                                                                                   |
| metrics                |               | List of enabled metrics to collect.                                                                                                                                                                 |
| metrics_blacklist      |               | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                                                                                             |
| password_provider      |               | Tells the agent whether to authenticate with the supplied password orthe .pgpass file password.                                                                                                     |
| pg_version             |               | The version of PostgreSQL you wish to monitor.                                                                                                                                                      |
| sslmode                |               | Defines server certificate verification method to use for SSLconnections (if any). Available values include disable, allow, prefer, require, verify-ca,and verify-full. Full details included here. |
| underscore             |               | Enables converting underscores (“_”) to periods (“.”).                                                                                                                                              |

[1]: /integrations/agents/linux-agent
