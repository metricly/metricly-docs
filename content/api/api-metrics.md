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

CloudWisdom's Metrics API can be used to review metrics.  You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/metrics) and by clicking the interactive buttons below.

## POST to /metrics/crosselementagg

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getCrossElementMetricAggregationUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to   query for elements with given metric FQNs and aggregate the found metrics across the elements to get one value per period.
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
https://app.metricly.com/metrics/crosselementagg?aggregation={aggregation}&statistic={statistic}&rollup={rollup}

```

### CURL

In the following CURL example, **metricFqns** matching `cpu.percent` are aggregated across all `SERVER` **elementTypes**. This query uses a **rollup** of `ZERO` and the `avg` **statistic**.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
     "startDate":"2020-01-30T02:00:00-04:00", \
     "endDate":"2020-01-30T03:00:00-04:00", \
     "elementTypes":{ \
        "and":false, \
        "items":[ \
           { \
              "literal":true, \
              "contains":true, \
              "item":"SERVER" \
           } \
        ] \
     }, \
     "metricFqns":{ \
        "and":false, \
        "items":[ \
           { \
              "literal":true, \
              "contains":true, \
              "item":"cpu.percent", \
              "queryType":"EXACT" \
           } \
        ] \
     } \
  } \
 ' 'https://app.metricly.com/metrics/crosselementagg?aggregation=avg&statistic=actual&rollup=ZERO'

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
    "startDate":"2020-01-30T02:00:00-04:00",
    "endDate":"2020-01-30T03:00:00-04:00",
    "elementTypes":{
       "and":false,
       "items":[
          {
             "literal":true,
             "contains":true,
             "item":"SERVER"
          }
       ]
    },
    "metricFqns":{
       "and":false,
       "items":[
          {
             "literal":true,
             "contains":true,
             "item":"cpu.percent",
             "queryType":"EXACT"
          }
       ]
    }
 }

```

### Response Body

The following response body found 3 metrics that matched the `cpu.percent` **metricFqn** across all `SERVER` **elementTypes**.

```
{
  "metricFqn": "cpu.percent",
  "rollup": "ZERO",
  "aggregation": "avg",
  "statistic": "actual",
  "data": {
    "jobId": "3797f68e-b9b1-4280-9cdb-d4047ce3b587",
    "result": {
      "status": "SUCCESS",
      "message": "Job Completed in 0.548s",
      "data": []
    }
  },
  "foundMetrics": 3,
  "aggregatedMetrics": 3
}

```

{{% /expand %}}

---

## POST to /metrics/elasticsearch/metricAgg/{term}

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/aggregateMetricsUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to  query for aggregation lists from metric documents which match all of the given criteria.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| elasticsearchQuery | body | json | A JSON query. |
| term | path | string | The element field you want to aggregate. |


### Request URL

```
https://app.metricly.com/metrics/elasticsearch/metricAgg/{term}

```

### CURL

In the following CURL example, all **metricFQNs** (**term**: `fqn`) are being aggregated for `ALB` **elementTypes**.  

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "sort": { \
     "field": "name", \
     "order": "asc", \
     "missing": "_last" \
   }, \
   "page": 0, \
   "pageSize": 10000, \
   "startDate": "2020-02-05T14:52:07+02:00", \
   "endDate": "2020-02-05T15:52:07+02:00", \
   "elementTypes": { \
     "and": false, \
     "items": [ \
       { \
         "literal": true, \
         "contains": true, \
         "item": "ALB" \
       } \
     ] \
   } \
 } \
 ' 'https://app.metricly.com/metrics/elasticsearch/metricAgg/fqn'

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
  "sort": {
    "field": "name",
    "order": "asc",
    "missing": "_last"
  },
  "page": 0,
  "pageSize": 10000,
  "startDate": "2020-02-05T14:52:07+02:00",
  "endDate": "2020-02-05T15:52:07+02:00",
  "elementTypes": {
    "and": false,
    "items": [
      {
        "literal": true,
        "contains": true,
        "item": "ALB"
      }
    ]
  }
}

```

### Response Body

The following response body returns aggregations of all metrics matching the given criteria. From the data in this example, you can assume CloudWisdom is ingesting metrics for two ALB elements; one of them is not sending data for `aws.applicationelb.httpcode_elb_4xx_count`.
```
{
  "aggregations": [
    {
      "fieldValue": "aws.applicationelb.activeconnectioncount",
      "count": 2
    },
    {
      "fieldValue": "aws.applicationelb.clienttlsnegotiationerrorcount",
      "count": 2
    },
    {
      "fieldValue": "aws.applicationelb.consumedlcus",
      "count": 2
    },
    {
      "fieldValue": "aws.applicationelb.forwardedinvalidheaderrequestcount",
      "count": 2
    },
    {
      "fieldValue": "aws.applicationelb.http_redirect_count",
      "count": 2
    },
    {
      "fieldValue": "aws.applicationelb.httpcode_elb_3xx_count",
      "count": 2
    },
    {
      "fieldValue": "aws.applicationelb.httpcode_elb_4xx_count",
      "count": 1
    }
  ]
}

```

{{% /expand %}}

---

## POST to /metrics/elasticsearch/metricQuery

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/elasticsearchMetricQueryUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to query for metric documents which match all of the given criteria.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| elasticsearchQuery | body | json | A JSON query. |


### Request URL

```
https://app.metricly.com/metrics/elasticsearch/metricQuery

```

### CURL

In the following CURL example, an **elementType** of `ALB` is specified in combination with the **metricFQN** `aws.applicationelb.targetresponsetime`.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
     "elementTypes":{ \
        "and":false, \
        "items":[ \
           { \
              "literal":true, \
              "contains":true, \
              "item":"ALB" \
           } \
        ] \
     }, \
     "metricFqns":{ \
        "and":false, \
        "items":[ \
           { \
              "literal":true, \
              "contains":true, \
              "item":"aws.applicationelb.targetresponsetime", \
              "queryType":"EXACT" \
           } \
        ] \
     } \
  } \
 ' 'https://app.metricly.com/metrics/elasticsearch/metricQuery'
```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
    "elementTypes":{
       "and":false,
       "items":[
          {
             "literal":true,
             "contains":true,
             "item":"ALB"
          }
       ]
    },
    "metricFqns":{
       "and":false,
       "items":[
          {
             "literal":true,
             "contains":true,
             "item":"aws.applicationelb.targetresponsetime",
             "queryType":"EXACT"
          }
       ]
    }
 }

```

### Response Body

The following response body returns matches for 2 elements that contain the specified metric FQN.

```
{
  "page": {
    "content": [
      {
        "netuitiveTags": {
          "n.statistic": "AVG",
          "unit": "s"
        },
        "sourceTags": {
          "awsDimensions": "{\"LoadBalancer\":\"app/bamboo/5f111fddb1e0c653\"}",
          "awsNamespace": "AWS/ApplicationELB"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "fqn": "aws.applicationelb.targetresponsetime",
        "unit": "Seconds",
        "dataSourceId": 12345,
        "elementId": "6bdf4fd1-7134-2222-9c36-22eb5f628e46",
        "name": "TargetResponseTime",
        "id": "c5fd666d-4444-3333-b4cd-8a2b28dc1fed"
      },
      {
        "netuitiveTags": {
          "n.statistic": "AVG",
          "unit": "s"
        },
        "sourceTags": {
          "awsDimensions": "{\"LoadBalancer\":\"app/ria-deploys/a8e1b18ecda823b7\"}",
          "awsNamespace": "AWS/ApplicationELB"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "fqn": "aws.applicationelb.targetresponsetime",
        "unit": "Seconds",
        "dataSourceId": 12345,
        "elementId": "864444fd-a348-3f05-92e1-a681d7d3d9e4",
        "name": "TargetResponseTime",
        "id": "cf0efe4a-e36d-1111-a5e4-0b3cc0f7d4c2"
      }
    ],
    "last": true,
    "totalElements": 2,
    "totalPages": 1,
    "sort": null,
    "first": true,
    "numberOfElements": 2,
    "size": 10,
    "number": 0
  }
}

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

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getMetricStatisticsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get metric statistics for all elements with given metric FQN.

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
https://app.metricly.com/metrics/statistics?fqn={fqn}&startTime={startTime}&endTime={endTime}&rollup={rollup}&showValues={showValues}
```

### CURL

In the following CURL example, statistics are returned for the **FQN** `aws.applicationelb.httpcode_elb_4xx_count`. The **rollup** is `PT5M`.

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

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getMetricStatisticsPageUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to get metric statistics for given set of elements. Note this is a deprecated method and could be removed at a later date.  

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
 https://app.metricly.com/metrics/statistics?fqn={fqn}&startTime={startTime}&endTime={endTime}&rollup={rollup}&showValues={showValues}

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
