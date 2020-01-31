---
title: "Metrics API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---



## About the Metrics API

CloudWisdom's Metrics API can be used to create, edit, delete and review metrics.  You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/metrics) and by clicking the interactive buttons below.

## POST to /metrics/crosselementagg

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getCrossElementMetricAggregationUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to  
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| elasticsearchQuery | body | json | A JSON query. |
| aggregation | query | string | Define aggregation method for query. Options are: avg, sum, cnt, min, max, stddev. |
| statistic | query | string | Define statistic. Options include: val, min, avg, max, cnt, sum, actual. |
| rollup | query | Array[string] | Determines frequency of metric sampling. Options are: ZERO, PT5M, PT1H, PT24H. |


### Request URL

```

```

### CURL

In the following CURL example  

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body
```

```

{{% /expand %}}

---

## POST to /metrics/elasticsearch/metricAgg/{term}

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/aggregateMetricsUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to  

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| elasticsearchQuery | body | json | A JSON query. |
| term | path | string | The element field you want to aggregate. |


### Request URL

```

```

### CURL

In the following CURL example  

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body
```

```

{{% /expand %}}

---

## POST to /metrics/elasticsearch/metricQuery

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/elasticsearchMetricQueryUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to  

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| elasticsearchQuery | body | json | A JSON query. |


### Request URL

```

```

### CURL

In the following CURL example  

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body
```

```

{{% /expand %}}

---

## GET from /metrics/fqns

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getMetricFqnsUsingGET" theme="info" >}} GET {{< /button >}} This endpoint is deprecated.   

{{% expand "View Method Details." %}}

### Parameters

| Parameters | Parameter Type | Data Type | Description |
|------------------|----------------|----------------|------------------------------------------------------------------------------------------------------------|
| elementId | query | Array [string] | The ID of the element. |
| elementFqn | query | Array [string] | The fully qualified name (FQN) of the element. |
| elementName | query | Array [string] | The human-readable name of the element. |
| elementType | query | Array [string] | The type of the element (e.g. SERVER, EC2, etc.) |
| elementAttribute | query | string | An attribute associated with the element. elementAttribute={“foo”:[“one”,“two”], “bar”:[“three”,“four”]} |
| elementTag | query | string | The name of the tag on the element. elementTag={“foo”:[“one”,“two”], “bar”:[“three”,“four”]} |
| metricFqn | query | Array [string] | The fully qualified name (FQN) of the metric. |
| metricTag | query | Array [string] | The tag key-value pair associated with the metric. metricTag={“foo”:[“one”,“two”], “bar”:[“three”,“four”]} |


### Request URL

```

```

### CURL

In the following CURL example  

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body
```

```

{{% /expand %}}

---


## GET from /metrics/statistics

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getMetricStatisticsUsingGET" theme="info" >}} GET {{< /button >}} This endpoint is deprecated.   

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|---------------|-----------------------------------------------------------------------------------------|
| fqn | query | string | The fully qualified name for a metric. |
| duration | query | string | Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. The duration parameter will take precedence over startTime and endTime if all attributes are included in your request. |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| rollup | query | Array[string] | Determines frequency of metric sampling. Options are: ZERO, PT5M, PT1H, PT24H. |
| showValues | query | boolean | Provides the values for the metric statistics (if set to true) or only displays zeroes for the statistics (if set to false). |


### Request URL

```

```

### CURL

In the following CURL example  

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body
```

```

{{% /expand %}}

---

## POST to /metrics/statistics

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getMetricStatisticsPageUsingPOST" theme="success" >}} POST {{< /button >}} This endpoint is deprecated.   

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|---------------|-----------------------------------------------------------------------------------------|
| fqn | query | string | The fully qualified name for a metric. |
| duration | query | string | Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. The duration parameter will take precedence over startTime and endTime if all attributes are included in your request. |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| rollup | query | Array[string] | Determines frequency of metric sampling. Options are: ZERO, PT5M, PT1H, PT24H. |
| showValues | query | boolean | Provides the values for the metric statistics (if set to true) or only displays zeroes for the statistics (if set to false). |
|elementIds   | body   | Array[string]  | List of elementIds. |


### Request URL

```

```

### CURL

In the following CURL example  

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body
```

```

{{% /expand %}}

---
