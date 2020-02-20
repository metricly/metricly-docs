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

`https://app.metricly.com/metrics/crosselementagg?aggregation={aggregation}&statistic={statistic}&rollup={rollup}`

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

`https://app.metricly.com/metrics/elasticsearch/metricAgg/{term}`

### CURL

In the following CURL example, all metric FQNs are being aggregated for the `ALB` **elementTypes** using `fqn` as the **term**.

{{% notice tip %}}
The term is the field we are looking to find aggregate counts for. The only option is ``fqn`` for metric FQN.
{{% /notice %}}

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

`https://app.metricly.com/metrics/elasticsearch/metricQuery`

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

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getMetricFqnsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get a list of metric FQNs for a given set of criteria. Note this is a deprecated method and could be removed at a later date.   

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

`https://app.metricly.com/metrics/fqns?{parameter}={value}`

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

The following response body returns a list of all metric FQNs associated to the value submitted for **elementId** in the first CURL example.
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

The following response body returns a list of all metric FQNs associated to the values submitted for **elementType** and **elementName** in the second CURL example.
```
{
  "fqns": [
    "aws.lambda.duration",
    "aws.lambda.errors",
    "aws.lambda.invocations",
    "aws.lambda.throttles"
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

`https://app.metricly.com/metrics/statistics?fqn={fqn}&startTime={startTime}&endTime={endTime}&rollup={rollup}&showValues={showValues}`

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

`https://app.metricly.com/metrics/statistics?fqn={fqn}&startTime={startTime}&endTime={endTime}&rollup={rollup}&showValues={showValues}`

### CURL

In the following CURL example, statistics are retrieved for a metric having the **fqn** `aws.applicationelb.requestcountpertarget` for two **elementIds** `["861111fd-a348-3f05-92e1-a681d7d3d9e4", "6bdf4fd1-7134-1111-9c36-17eb5f628e46"]`. The **rollup** value is PT5M.

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


## Get Multiple Element IDs and Metric IDs at once

You can quickly get a list of **elementIds** and **metricIds** using the POST method for the **/Metrics/Elasticsearch/MetricQuery** endpoint. This is useful when you know the **elementType** and/or **metricFQN** but need specific IDs.

{{% expand "View Walkthrough." %}}

1. Build a query using CURL that searches your inventory based on **elementType** and **metricFQN**. In this example, we are searching for EC2 elements that have the MetricFqn `aws.ec2.cpuutilization`. Let's also cut down the response body by using an exclusion filter for **DataSourceId**, **unit**, **name**, and **fqn**. All we really want are **elementIds** and **metricIds**.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
     "elementTypes":{ \
        "and":false, \
        "items":[ \
           { \
              "literal":true, \
              "contains":true, \
              "item":"EC2" \
           } \
        ] \
     }, \
     "metricFqns":{ \
        "and":false, \
        "items":[ \
           { \
              "literal":true, \
              "contains":true, \
              "item":"aws.ec2.cpuutilization", \
              "queryType":"EXACT" \
           } \
        ] \
     }, \
    "sourceFilter": { \
      "excludes": [ \
        "dataSourceId", \
        "unit", \
        "name", \
        "fqn" \
      ] \
    } \
  }' 'https://app.metricly.com/metrics/elasticsearch/metricQuery'
```

2\. Review the response body.

```
{
  "page": {
    "content": [
      {
        "netuitiveTags": {
          "n.statistic": "AVG",
          "unit": "percent",
          "utilization": "true"
        },
        "sourceTags": {
          "awsDimensions": "{\"InstanceId\":\"i-7e00b2cf\"}",
          "awsNamespace": "AWS/EC2"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "elementId": "900eb136-4444-3da7-7777-eeb36bf03b9c",
        "id": "a6ebb2b3-9999-8888-8f35-192d5ff863ff"
      },
      {
        "netuitiveTags": {
          "n.statistic": "AVG",
          "unit": "percent",
          "utilization": "true"
        },
        "sourceTags": {
          "awsDimensions": "{\"InstanceId\":\"i-b4e87f28\"}",
          "awsNamespace": "AWS/EC2"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "elementId": "c48df6c2-1111-4444-97be-17b0472a7d12",
        "id": "3c9c8f3d-413c-3d10-8bd6-fdb7178634b8"
      },
      {
        "netuitiveTags": {
          "n.statistic": "AVG",
          "unit": "percent",
          "utilization": "true"
        },
        "sourceTags": {
          "awsDimensions": "{\"InstanceId\":\"i-8fdf0c1c\"}",
          "awsNamespace": "AWS/EC2"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "elementId": "cc1202b5-9900-35c6-1234-5890f2c07f7d",
        "id": "c18d53b9-ae7b-3fca-a3ee-56e9703ab88a"
      },
      {
        "netuitiveTags": {
          "n.statistic": "AVG",
          "unit": "percent",
          "utilization": "true"
        },
        "sourceTags": {
          "awsDimensions": "{\"InstanceId\":\"i-cad14a43\"}",
          "awsNamespace": "AWS/EC2"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "elementId": "fd1952ee-1234-5432-a6e5-469dce782976",
        "id": "873177c6-6fc3-1122-2211-daed5429c84f"
      },
      {
        "netuitiveTags": {
          "n.statistic": "AVG",
          "unit": "percent",
          "utilization": "true"
        },
        "sourceTags": {
          "awsDimensions": "{\"InstanceId\":\"i-0e979e39c64e22b1e\"}",
          "awsNamespace": "AWS/EC2"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "elementId": "787401a0-1928-33f4-0987-470851557694",
        "id": "946c0c97-3344-3c67-0011-69c21a1839c3"
      }
    ],
    "last": false,
    "totalElements": 5,
    "totalPages": 1,
    "sort": null,
    "first": true,
    "numberOfElements": 10,
    "size": 10,
    "number": 0
  }
}
```

3\. You can now use the **elementIds** and **metricIds** listed to take other actions, such as obtain metric statistics from the **/metrics/statistics** endpoint or interact with the [Element API endpoints](/api/api-elements). Let's view the metric statistics.

4\. Grab the **elementIds** and **metricFQN** and build a CURL request like this:

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '["900eb136-4444-3da7-7777-eeb36bf03b9c", \
 "c48df6c2-1111-4444-97be-17b0472a7d12", \
 "cc1202b5-9900-35c6-1234-5890f2c07f7d", \
 "fd1952ee-1234-5432-a6e5-469dce782976", \
 "787401a0-1928-33f4-0987-470851557694"]' 'https://app.metricly.com/metrics/statistics?fqn=aws.ec2.cpuutilization&startTime=2020-02-07T20%3A28%3A08.441Z&endTime=2020-02-08T20%3A28%3A08.441Z&rollup=PT5M&showValues=false'
```

5\.  Submit to the **/metrics/satistics/** endpoint and review the response body.

```
{
  "metricFqn": "aws.ec2.cpuutilization",
  "timeSpan": {
    "startTime": "2020-02-07T20:28:08Z",
    "endTime": "2020-02-08T20:28:08Z",
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
      "elementId": "900eb136-4444-3da7-7777-eeb36bf03b9c",
      "metricId": "a6ebb2b3-9999-8888-8f35-192d5ff863ff",
      "statistics": {
        "avg": 0.296191972049853,
        "min": 0.266138742241768,
        "median": 0.29999999999805976,
        "max": 0.3817217745650538,
        "percentile75": 0.30005788644855513,
        "percentile95": 0.3098193942759116,
        "count": 288,
        "sum": 85.30328795035766,
        "stddev": 0.010466436268679397,
        "percentile5": 0.282513661204118,
        "percentile25": 0.28418079095994414
      }
    },
    {
      "elementId": "c48df6c2-1111-4444-97be-17b0472a7d12",
      "metricId": "3c9c8f3d-413c-3d10-8bd6-fdb7178634b8",
      "statistics": {
        "avg": 0.2527214510460781,
        "min": 0.23225896082133599,
        "median": 0.25002778549597,
        "max": 0.46398999722444445,
        "percentile75": 0.26560155598867985,
        "percentile95": 0.26782439566637944,
        "count": 288,
        "sum": 72.78377790127054,
        "stddev": 0.021541944391382722,
        "percentile5": 0.2328239325728899,
        "percentile25": 0.24918032786880503
      }
    },
    {
      "elementId": "cc1202b5-9900-35c6-1234-5890f2c07f7d",
      "metricId": "946c0c97-bb12-3c67-8611-69c21a1839c3",
      "statistics": {
        "avg": 0.03879795675956283,
        "min": 0,
        "median": 0.0333333333328482,
        "max": 2.1951886276651327,
        "percentile75": 0.033333333334061,
        "percentile95": 0.05188336159835552,
        "count": 288,
        "sum": 11.173811546754091,
        "stddev": 0.13896824157383195,
        "percentile5": 0,
        "percentile25": 0.0080645161289149
      }
    },
    {
      "elementId": "fd1952ee-1234-5432-a6e5-469dce782976",
      "metricId": "873177c6-6fc3-3a3d-b13d-daed5429c84f",
      "statistics": {
        "avg": 1.7315944243770274,
        "min": 1.4878531073293721,
        "median": 1.7007548392993268,
        "max": 2.185815504321736,
        "percentile75": 1.783333333286766,
        "percentile95": 2.0762700287132483,
        "count": 288,
        "sum": 498.69919422058393,
        "stddev": 0.12842823812903692,
        "percentile5": 1.5666666667287519,
        "percentile25": 1.649999999984476
      }
    },
    {
      "elementId": "787401a0-1928-33f4-0987-470851557694",
      "metricId": "c18d53b9-ae7b-3fca-a3ee-56e9703ab88a",
      "statistics": {
        "avg": 1.739921401540746,
        "min": 1.4745762711844688,
        "median": 1.7329721218895568,
        "max": 3.7674076132220167,
        "percentile75": 1.7812138676488627,
        "percentile95": 1.91902426600034,
        "count": 288,
        "sum": 501.0973636437353,
        "stddev": 0.15510405334664015,
        "percentile5": 1.5602834419341518,
        "percentile25": 1.6723027155093602
      }
    }
  ]
}
```


{{% /expand %}}
