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
https://app.metricly.com/metrics/fqns?{parameter}={value}
```

### CURL

In the following CURL example, one **elementId** is used to obtain a list of all metricFQNs.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/metrics/fqns?elementId=6bdf4fd1-7134-3959-9c36-17eb5f628e46'

```

In the following CURL example, the **elementType** and **elementName** parameters are used. **These values are case sensitive.**

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/metrics/fqns?elementName=Destalinator&elementType=Lambda'

```

### Swagger Payload

You can test this endpoint with Swagger by populating the provided parameter fields. Select the method icon to open this specific endpoint.


### Response Body

The following response body returns a list of all metricFQNs associated to the values submitted.
```
{
  "fqns": [
    "aws.applicationelb.activeconnectioncount",
    "aws.applicationelb.clienttlsnegotiationerrorcount",
    "aws.applicationelb.consumedlcus",
    "aws.applicationelb.forwardedinvalidheaderrequestcount",
    "aws.applicationelb.http_redirect_count",
    "aws.applicationelb.httpcode_elb_3xx_count",
    "aws.applicationelb.httpcode_elb_4xx_count",
    "aws.applicationelb.httpcode_target_2xx_count",
    "aws.applicationelb.httpcode_target_3xx_count",
    "aws.applicationelb.httpcode_target_4xx_count",
    "aws.applicationelb.httpcode_target_5xx_count",
    "aws.applicationelb.newconnectioncount",
    "aws.applicationelb.processedbytes",
    "aws.applicationelb.requestcount",
    "aws.applicationelb.requestcountpertarget",
    "aws.applicationelb.targetresponsetime",
    "netuitive.aws.alb.httpcodeelb4xxerrorpercent",
    "netuitive.aws.alb.httpcodeelb5xxerrorpercent",
    "netuitive.aws.alb.httpcodeelberrorpercent",
    "netuitive.aws.alb.requestspersecond",
    "netuitive.aws.alb.totalelbhttperrors",
    "netuitive.aws.alb.totaltargethttperrors",
    "netuitive.aws.alb.unhealthyhostpercent",
    "netuitive.metrics.collected.percent"
  ]
}
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
https://app.metricly.com/metrics/statistics?fqn=aws.applicationelb.httpcode_elb_4xx_count&startTime=2020-01-30T01%3A00%3A00-05%3A00&endTime=2020-01-31T01%3A00%3A00-05%3A00&rollup=PT5M&showValues=false
```

### CURL

In the following CURL example  

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/metrics/statistics?fqn=aws.applicationelb.httpcode_elb_4xx_count&startTime=2020-01-30T01%3A00%3A00-05%3A00&endTime=2020-01-31T01%3A00%3A00-05%3A00&rollup=PT5M&showValues=false'

```

### Swagger Payload

You can test this endpoint with Swagger by populating the provided parameter fields. Select the method icon to open this specific endpoint.


### Response Body

The following response body
```
{
  "metricFqn": "aws.applicationelb.httpcode_elb_4xx_count",
  "timeSpan": {
    "startTime": "2020-01-30T06:00:00Z",
    "endTime": "2020-01-31T06:00:00Z",
    "duration": {
      "seconds": 86400,
      "nano": 0,
      "zero": false,
      "negative": false,
      "units": [
        "SECONDS",
        "NANOS"
      ]
    }
  },
  "metrics": [
    {
      "elementId": "6bdf4fd1-7134-3959-9c36-17eb5f628e46",
      "metricId": "71d31aac-c1ad-30e1-bd1a-8f3d4ee816fd",
      "statistics": {
        "avg": 1,
        "min": 1,
        "median": 1,
        "max": 1,
        "percentile75": 1,
        "percentile95": 1,
        "count": 43,
        "sum": 43,
        "stddev": 0,
        "percentile5": 1,
        "percentile25": 1
      }
    },
    {
      "elementId": "861687fd-a348-3f05-92e1-a681d7d3d9e4",
      "metricId": "5ed2adcc-0a1e-3919-91fc-38b159f9d4c1",
      "statistics": {
        "avg": 1,
        "min": 1,
        "median": 1,
        "max": 1,
        "percentile75": 1,
        "percentile95": 1,
        "count": 41,
        "sum": 41,
        "stddev": 0,
        "percentile5": 1,
        "percentile25": 1
      }
    }
  ]
}

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
https://app.metricly.com/metrics/statistics?fqn=aws.applicationelb.requestcountpertarget&startTime=2020-02-04T00%3A25%3A46.872Z&endTime=2020-02-05T00%3A25%3A46.872Z&rollup=PT5M&showValues=false

```
### CURL

In the following CURL example grabs statistic on the **fqn** `aws.applicationelb.requestcountpertarget` matching two **elementIds** `["861111fd-a348-3f05-92e1-a681d7d3d9e4", "6bdf4fd1-7134-1111-9c36-17eb5f628e46"]`. The **rollup** value is PT5M.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '["861111fd-a348-3f05-92e1-a681d7d3d9e4", "6bdf4fd1-7134-1111-9c36-17eb5f628e46"]' 'https://app.metricly.com/metrics/statistics?fqn=aws.applicationelb.requestcountpertarget&startTime=2020-02-04T00%3A25%3A46.872Z&endTime=2020-02-05T00%3A25%3A46.872Z&rollup=PT5M&showValues=false'

```

### Swagger Payload

You can test this endpoint with Swagger by populating the provided parameter fields. Select the method icon to open this specific endpoint.


### Response Body

The following response body shows data on the specified metric FQN for both elementIds in the given timeframe.
```
{
  "metricFqn": "aws.applicationelb.requestcountpertarget",
  "timeSpan": {
    "startTime": "2020-02-04T00:25:46Z",
    "endTime": "2020-02-05T00:25:46Z",
    "duration": {
      "seconds": 86400,
      "nano": 0,
      "zero": false,
      "negative": false,
      "units": [
        "SECONDS",
        "NANOS"
      ]
    }
  },
  "metrics": [
    {
      "elementId": "6bdf4fd1-7134-1111-9c36-17eb5f628e46",
      "metricId": "4f57398a-ea9e-3941-bc22-39b9209647be",
      "statistics": {
        "avg": 0.16414192643887693,
        "min": 0,
        "median": 0.15,
        "max": 0.5185185185185185,
        "percentile75": 0.2,
        "percentile95": 0.25,
        "count": 288,
        "sum": 47.27287481439661,
        "stddev": 0.07248948034849102,
        "percentile5": 0.05,
        "percentile25": 0.1
      }
    },
    {
      "elementId": "861111fd-a348-3f05-92e1-a681d7d3d9e4",
      "metricId": "078caa77-2f38-32e0-8a63-28738a95805e",
      "statistics": {
        "avg": 0.011353147154777584,
        "min": 0,
        "median": 0,
        "max": 0.30434782608695654,
        "percentile75": 0,
        "percentile95": 0.0748809523809529,
        "count": 288,
        "sum": 3.269706380575945,
        "stddev": 0.04143012686391845,
        "percentile5": 0,
        "percentile25": 0
      }
    }
  ]
}
```

{{% /expand %}}

---
