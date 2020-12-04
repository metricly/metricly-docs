---
title: "Microsoft NET Metrics"
#date: 2018-12-11
draft: false
tags: ["metrics", "integrations", "microsoft net" ]
author: Lawrence Lane
---
| Friendly Name                | FQN                         | Description                                                                                                                                                                                                                                                                                          |
|------------------------------|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exceptions Thrown/sec        | CLR_count_exceptions_thrown | The number of exceptions thrown per second. This includes both .NET exceptions and unmanaged exceptions that are converted into .NET exceptions.                                                                                                                                                     |
| % Time in Garbage Collection | CLR_percent_time_in_GC      | The percentage of elapsed time spent performing garbage collection since the last garbage collection cycle.                                                                                                                                                                                          |
| Application Restarts         | ASP_application_restarts    | The number of times an application has been restarted during the server’s lifetime.                                                                                                                                                                                                                  |
| Requests Current             | ASP_requests_current        | The current number of requests, including those that are queued, currently executing, or waiting to be written to the client. Under the ASP.NET process model, when this counter exceeds requestQueueLimit defined in the processModel configuration section, ASP.NET will begin rejecting requests. |
| Request Wait Time            | ASP_request_wait_time       | The time (in ms) that the most recent request waited in the processing queue.                                                                                                                                                                                                                        |
| Requests Queued              | ASP_requests_queued         | The number of requests waiting for service from the queue.                                                                                                                                                                                                                                           |
| Request Execution Time       | ASP_request_execution_time  | The time it took (in ms) to execute the most recent request.                                                                                                                                                                                                                                         |
To see a full list of metrics for the [Windows Agent][1], see [this page][1].
[1]: /integrations/agents/windows-agent/
[2]: /integrations/agents/windows-agent/windows-agent-metrics
