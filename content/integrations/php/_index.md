---
title: "PHP"
#date: 2018-12-12
draft: false
tags: ["#php", "#integrations" ]
author: Lawrence Lane
---
 You can monitor your PHP applications using our PHP client library, the Linux Agent, and the Metricly StatsD server.

## Prerequisites
- [Linux Agent][1]

## Configure

1. Navigate to the `metricly-agent.conf` file.
2. Update the **statsd** setting to `enabled = True`.

```
# local statsd server
[[[statsd]]]
enabled = True
```
3\. StatsD requires a client library to push metrics. You can use our [PHP client library](https://github.com/Netuitive/Netuitive_PHP_Client) or an open source alternative.
4. Include the client library file on any page you want to collect metrics, or you can reference the file globally.
```
include 'StatsD_Client.php';
```
5\. Instrument your application code by calling the appropriate functions. Check out the example below or the timer example included in the library repo.

```
//add a gauge in any section of your code
.gauge('test.data.gauge', 20);

//to add this time you must first add code to
calculate the start and end time.
//typically we use epoch time.  And add code at
the start and end of the code you want to
measure.
//the timing function expects time in
 milliseconds
.timing('test.data.timer', 1000, 1);


//you can add or subtract from any metric with
these functions
.increment('test.data.counterup', 1);
.decrement('test.data.counterdown', 1);
```

6\. **Save** and **restart** both your application and the Linux Agent.




[1]: /integrations/agents/linux-agent
