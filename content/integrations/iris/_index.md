---
title: "Iris"
#date: 2018-12-11
draft: false
tags: ["#iris", "#integrations", "#java"]
author: Lawrence Lane
---
Iris is a Java library that allows your Java applications to communicate with Metricly’s REST API. You can use Iris to send metrics from your applications to Metricly, create dashboards, tags, elements, and much more.


## Configuration
1. Include the proper dependency from [Maven](https://search.maven.org/#search|ga|1|g:%22com.netuitive%22%20AND%20a:%22iris%22) for the appropriate build manager.
2. Invoke the REST API client interface in a central location that your various Java classes can access while ensuring you replace username and password with the appropriate values.

```
MetriclyElementClient elementClient = new MetriclyElementRestClient
("username", "password");
```

3\. You may now send requests to the Metricly REST API. To read more about our API, find links to explore our API, and test some requests, see the API help section. Links to each client.java file follow where you can find the types of requests you can make and what parameters you can pass in:

- **Elements**:
  - [Element client (request types)](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/element/NetuitiveElementClient.java) / [Element REST client (params)](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/element/NetuitiveElementRestClient.java)  
- **Events**:
  - [Event client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/event/NetuitiveEventClient.java) / [Event REST client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/event/NetuitiveEventRestClient.java)
  - [Ingest Event client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/event/NetuitiveIngestEventClient.java) / [Ingest Event REST client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/event/NetuitiveIngestEventRestClient.java)  
- **Metrics**:
  - [Ingest Metric client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/metric/NetuitiveIngestMetricClient.java) / [Ingest Metric REST client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/metric/NetuitiveIngestMetricRestClient.java)
  - [Metric client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/metric/NetuitiveMetricClient.java) / [Metric REST client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/metric/NetuitiveMetricRestClient.java)
  - [Notification client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/notification/NetuitiveNotificationClient.java) / [Notification REST client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/notification/NetuitiveNotificationRestClient.java)
  - [Policy client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/policy/NetuitivePolicyClient.java) / [Policy REST client](https://github.com/netuitive/Iris/blob/master/src/main/java/com/netuitive/iris/client/policy/NetuitivePolicyRestClient.java)


### Example Requests

#### Element

```
elementClient.listElements(new ListElementsRequest()
  .withStartDate([date])
  .withEndDate([date]));
```

#### Event

```
eventClient.getEvents(new GetEventsRequest()
  .withIsExternal(true)
  .withCategory("CRITICAL"));
```

#### Metric

```
metricClient.getMetricStatistics(new GetMetricStatisticsRequest()
  .withRollup("5M")
  .withFqn("aws.ec2.cpuutilization"));
```
