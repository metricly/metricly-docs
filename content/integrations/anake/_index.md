---
title: "Anake"
#date: 2018-12-11
draft: false
tags: ["anake", "integrations", "custom metrics", "java"]
author: Lawrence Lane
---

Ananke is a Java library that allows Java applications to communicate with and send information to a StatsD listener. You can use Ananke to send metrics from your Java applications to a StatsD server, which will then send the metrics to CloudWisdom.


## Configuration
1. Setup the Metricly StatsD integration or the Etsy StatsD integration if you haven’t already. We recommend setting up the Metricly StatsD integration if you don’t have a StatsD server already; if you have a StatsD server setup, we recommend setting up the Etsy StatsD integration.
2. Include the proper dependency from Maven for the appropriate build manager.
3. Invoke the StatsD client interface in a central location that your various Java classes can access.

```
StatsDClient client = new NetuitiveStatsDClient("localhost", "8000");
```
4\. Utilize code instrumentation to send metrics, events, service checks, and more into CloudWisdom (basic examples included below each type). CloudWisdom supports the following metric types:
 - **Decrement (Counter – Down)**: Decrease the count of how many times something happened per second.

 ```
 client.decrement(new DecrementRequest()
  .withMetric("tokens_left.count")
  .withValue(-1));
  ```
 - **Event**: A log of something that happened, including a title and a description of the event.

 ```
 client.event(new EventRequest()
  .withTitle("Event Title")
  .withText("Send help!"));
  ```
 - **Gauge**: An arbitrary, persistent value (e.g., a fuel meter).

 ```
 client.gauge(new GaugeRequest()
  .withMetric("gas_tank.level")
  .withValue(1L));
  ```
 - **Histograms**: The statistical distribution of a set of values.

 ```
 client.histogram(new HistogramRequest()
  .withMetric("file.upload.size")
  .withValue(2MB));
  ```
 - **Increment (Counter – Up)**: Increase the count of how many times something happened per second.

 ```
 client.increment(new IncrementRequest()
  .withMetric("page_view.count")
  .withValue(1));
  ```
 - **Service Check**: A check to see if a service is either up or down.

 ```
 client.servicecheck(new ServiceCheckRequest()
  .withName("my_service")
  .withStatus(1));
  ```
 - **Sets**: A number of unique elements received over a set interval.

 ```
 client.set(new SetRequest()
  .withName("users.unique")
  .withValue(user.id));
  ```
 - **Timed**: Pass in a callable function that Ananke will time how long it takes to run and then passes the value on.

 ```
 client.timed(new TimedRequest()
  .withFunc("pageloadtime()");
  ```
 - **Timing**: Measure in milliseconds how long an action took.

 ```
 client.timing(new TimingRequest()
  .withMetric("x")
  .withValue(xms));
  ```
## Java Integration Options
We have several different options for monitoring Java applications. Each method varies in terms of setup difficulty and the amount / type of information it collects.  

| Method     | Description                                                                                                                                                                       |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ananke     | Java library you can use to push metrics to the StatsD listener embedded in our Linux agent. This approach requires that you integrate the StatsDReporter into your applications. |
| Dropwizard | Integrate the dropwizard-metrics library into your Dropwizard application and configure it to send metrics to the StatsD listener embedded in our Linux agent.                    |
| Iris       | Java library you can use to push metrics directly to CloudWisdom’s REST API.                                                                                                         |
| Java Agent | Open-source and open-license Java agent the does the byte-code instrumentation for you. No changes to source code required.                                                       |
| JMX        | Integration that relies on our Linux agent to collect JVM metrics (e.g., heap size, garbage collection, etc.) without code-level instrumentation.                                 |
