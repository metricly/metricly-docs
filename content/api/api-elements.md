---
title: "Elements API"
draft: false
categories:
tags: ["#api", "#elements"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

## About the Elements API

CloudWisdom's Elements API can be used create, edit, delete and review elements. Users can also update tags and policies associated to these elements. You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/elements).

## POST to /elements/elasticsearch/elementAgg/{term}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/aggregateElementsUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to find a count of objects based on the fields chosen for aggregation.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The element field you want to aggregate. |
| elasticsearchQuery | body | JSON | A JSON query. |

### Request URL

```
https://app.metricly.com/elements/elasticsearch/elementAgg/{term}

```

### CURL

In the following CURL example the **term** is defined in the request URL as **elementType**. This means the response body returns a list of element types with aggregated totals for each type which match the search criteria. In this example, we are searching for **elementNames** that match `west`.  

{{% notice tip %}}
The term is the field we are looking to find aggregate counts for. Options are ``elementType`` for element types, ``attributes`` for element attributes ,``tags`` for element tags, and ``collectors.name`` for element collectors.
{{% /notice %}}

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "page": 0, \
   "pageSize": 100, \
   "startDate": "2020-01-27T12:33:28-05:00", \
   "endDate": "2020-01-27T13:33:28-05:00", \
   "elementNames": { \
     "and": false, \
     "items": [ \
       { \
         "literal": false, \
         "contains": true, \
         "item": "west" \
       } \
     ] \
   } \
 }' 'https://app.metricly.com/elements/elasticsearch/elementAgg/elementType'
```

### Response Body

The following response body found 6 total elements with names that contain `west` in their **elementName**: 5 S3 buckets and 1 RDS element.
```
{
  "aggregations": [
    {
      "fieldValue": "S3 Bucket",
      "count": 5
    },
    {
      "fieldValue": "RDS",
      "count": 1
    }
  ]
}
```

{{% /expand %}}

---

## POST to /elements/elasticsearch/elementQuery

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/elasticsearchElementQueryUsingPOST" theme="success" >}} POST {{< /button >}}  Use this endpoint to query elements by datasource, type, and more. Supports filtering.

{{% expand "View Method Details." %}}  

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The the element field you want to aggregate. |

### Request URL

```
https://app.metricly.com/elements/elasticsearch/elementQuery
```

### CURL

The following CURL example submits a query for **elementTypes** matching EC2. This example filters **metrics** and **attributes** from the response body.

{{% notice tip %}}
The `items` key here is contextual to its parent object. In this example, an item is the value of an elementType key (EC2). You can search for elementFQNs, elementIds, elementNames ---but the _items_ value changes for each. If the response body returns `"totalElements": 0,` verify that you are submitting an item value matching its parent object.
{{% /notice %}}

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{  "sort": { \
     "field": "name", \
     "order": "asc", \
     "missing": "_last" \
   }, \
   "page": 0, \
   "pageSize": 35, \
   "startDate": "2020-01-24T01:00:00-05:00", \
   "endDate": "2020-01-24T02:00:00-05:00", \
   "elementTypes": { \
     "and": false, \
     "items": [ \
       { \
         "literal": true, \
         "contains": true, \
         "item": "EC2" \
       } \
     ] \
   }, \
   "sourceFilter": { \
     "excludes": [ \
       "metrics", \
       "attributes" \
     ] \
   } \
 }' 'https://app.metricly.com/elements/elasticsearch/elementQuery'
```

### Response Body

The following response body found 2 elements with the **elementType** `EC2`.  You can easily find an element's **Id** and **FQN** by looking for `"type": "EC2"`.

```
{
  "page": {
    "content": [
      {
        "netuitiveTags": {
          "n.analysis.status": null
        },
        "sourceTags": {
          "Name": "test-element-abc1",
          "n.collectors": "EC2"
        },
        "state": {
          "netuitive.metrics.collected.percent": null
        },
        "eventCount": {
          "total": 0,
          "topCategory": null
        },
        "relations": [
          {
            "id": 11a031a5-011a-3976-84be-d0d1cbe281fe",
            "dataSourceId": 31845,
            "fqn": "501119301101:EBS:us-east-1:vol-01ab111bfa2c63111"
          }
        ],
        "fqn": "11179301106:EC2:us-east-1:i-011adb1a4a45ab111",
        "name": "Testing (10.13.10.83)",
        "location": "us-east-1c",
        "id": "91bb19b6-012c-1111-aede-dda4e12c111a",
        "type": "EC2"
      },
      {
        "netuitiveTags": {
          "n.analysis.status": null,
          "n.backfill.status": "false",
          "n.state.maintenance": "false",
          "n.state.maintenance_end": "-1"
        },
        "sourceTags": {
          "Name": "Netuitive-colo: Domain Controller",
          "app": "hq",
          "n.collectors": "EC2"
        },
        "state": {
          "netuitive.metrics.collected.percent": 100
        },
        "eventCount": {
          "total": 0,
          "topCategory": null
        },
        "relations": [
          {
            "id": "c6ccd4ac-ea3f-11be-ac98-11112aecf04c",
            "dataSourceId": 31845,
            "fqn": "502111101106:EBS:us-east-1:vol-9eba111e"
          }
        ],
        "fqn": "112111101106:EC2:us-east-1:i-b4e87f28",
        "lastProcessed": "2020-01-26T16:50:00Z",
        "name": "Domain Controller (10.14.11.30)",
        "location": "us-east-1a",
        "id": "c48df6c2-111c-3542-11be-17b0472a7d12",
        "type": "EC2"
      },     
    ],
    "last": true,
    "totalElements": 2,
    "totalPages": 1,
    "sort": null,
    "first": true,
    "numberOfElements": 2,
    "size": 35,
    "number": 0
  }
}
```

{{% /expand %}}

---

## POST to /elements/name/preview

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/namePreviewUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to preview custom display names for elements within the CloudWisdom UI.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------------|----------------|-----------|-------------|
| elementTemplate | Body | JSON | ?? |

### Request URL

```
https://app.metricly.com/elements/name/preview
```

### CURL

The following CURL example displays the element's name, location, and type. See [Element Display Name page] (https://docs.metricly.com/capacity-monitoring/inventory/inventory-element-display-name/) for more  display options.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "elementId": "095a50a0-2b5c-3eb9-b25b-48f81de11038", \
   "template": "${tags.Name} ${meta.location} ${meta.type}" \
 }' 'https://app.metricly.com/elements/name/preview'
```

### Response Body

The following response body prints a preview of the element name created by merging `${tags.Name}`, `${meta.location}`, and `${meta.type}`.

```
{
  "preview": "Element-Name us-east-1c EBS"
}
```

{{% /expand %}}

---

## POST to /elements/search

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/getElementsPOSTUsingPOST" theme="success" >}} POST {{< /button >}} This is a deprecated method. Use **/elements/elasticsearch/elementQuery** instead.

---

## GET from /elements/{elementId}/events

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getEventsUsingGET" >}} GET {{< /button >}} Use this endpoint to discover events within certain time frames (days, hours, minutes).

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|----------------------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| duration | query | string | Follows ISO8601 duration format. Example options include: PT1h, PT1m, PT10s, P3D |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |

### Request URL

```
https://app.metricly.com/elements/11160111-0111-392f-adbe-71c85111bd40/events

```

### CURL

The following CURL example uses a YYYYMMDD **startTime** and **endTime** value.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/11160111-0111-392f-adbe-71c85111bd40/events?startTime=20191201&endTime=20191202'

```

The following CURL example uses the suggested YYYY-MM-DDT00:001Z format instead (must include time zone). This is better for looking at a specific, narrow time frames.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/11160111-0111-392f-adbe-71c85111bd40/events?startTime=2019-12-01T03%3A30Z&endTime=2019-12-01T07%3A30Z'
```

### Response Body

The following response body contains only one event, but many events can be returned.

```
{
  "events": [
    {
      "id": "f0b4c111-9402-1111-a3be-111d6971f4dc",
      "timestamp": "2019-12-01T06:50:00Z",
      "category": {
        "id": "1",
        "name": "INFO",
        "color": "#0000FF"
      },
      "data": {
        "metricIds": [
          {
            "fqn": "aws.ec2.cpuutilization",
            "id": "1b111b41-e6a6-3a41-8b0a-b1111111fce7"
          }
        ],
        "policyName": "Test-DY-PolicyCreationTime",
        "metrics": [
          "aws.ec2.cpuutilization"
        ],
        "results": "{\"violating\":true,\"conditions\":[{\"id\":\"0\",\"violating\":true,\"expression\":\"The current value of aws.ec2.cpuutilization is 99.27; this is above the static threshold of 99.\"}],\"metrics\":[\"aws.ec2.cpuutilization\"]}"
      },
      "elementId": "11111156-0111-392f-adbe-71c11155bd40",
      "elementFqn": "502111101106:EC2:us-west-2:i-1b1d3a41",
      "elementType": "EC2",
      "elementName": "vpn01-usw2a (10.12.11.6)",
      "elementLocation": "us-west-2a",
      "elementTags": {
        "app": "vpn",
        "n.analysis.status": "",
        "Tenant": "internal",
        "n.collectors": "EC2",
        "n.backfill.status": "false",
        "Netuitive": "True",
        "Name": "vpn01-usw2a"
      },
      "policy": {
        "id": "fe8bd11b-586f-401e-1111-d891aebda10f",
        "name": "Test-DY-PolicyCreationTime",
        "description": null,
        "scope": null,
        "duration": null,
        "anyCondition": false,
        "conditions": [],
        "eventConditions": [],
        "checkCondition": null,
        "actions": [],
        "enabled": true,
        "deleted": false
      },
      "source": null,
      "title": null,
      "tags": [],
      "type": null,
      "isExternal": false,
      "processedTime": null,
      "eventTags": {}
    }
    ]
}
```


{{% /expand %}}

---

## GET from /elements/{elementId}/metrics

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricMetadataUsingGET" >}} GET {{< /button >}} Use this endpoint to obtain one or many metric details associated to an element.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|--------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |
| metricFQN | query | string | The metricFQN can be found by viewing metrics in CloudWisdom. |

### Request URL

```
https://app.metricly.com/elements/11110956-1111-392f-adbe-71c11115bd40/metrics
```

### CURL

The following CURL example returns a list of all metrics associated to the **elementId**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/11110956-1111-392f-adbe-71c11115bd40/metrics'
```

The following CURL example returns the `aws.ec2.networkpacketsout` metric associated to the **elementId**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/11110956-1111-392f-adbe-71c11115bd40/metrics?metricFQN=aws.ec2.networkpacketsout'

```

### Response Body

The following response body returns one metric, but many metrics can be returned.

```
{
  "id": "21110956-1111-392f-adbe-71c81115bd40",
  "metricMeta": [
    {
      "id": "bb2116ed-2868-3c76-b1b6-a4111a4eda2f",
      "fqn": "aws.ec2.networkpacketsout",
      "state": {
        "baselined": true,
        "created": "2017-10-02T13:57:06Z",
        "lastResults": {
          "actual": 5.6,
          "avg": 5.6,
          "min": 4,
          "max": 7,
          "baselineMean": 31.103688690165836,
          "cnt": 5,
          "sum": 28,
          "baselineStddev": 115.32111156038707,
          "baselineUpper": 492.3881349317141,
          "baselineLower": 0
        },
        "historicalMin": 0.8,
        "lastActual": 669.4,
        "updated": "2019-12-20T03:10:00Z",
        "correlated": false,
        "historicalMax": 288606
      },
      "configuration": {
        "validmax": null,
        "sparsedatastrategy": "None",
        "validmin": 0
      }
    }
  ]
}
```

{{% /expand %}}

---

## GET from /elements/{elementId}/metrics/{metricId}/samples

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricResultsUsingGET" >}} GET {{< /button >}} Use this endpoint to grab metric samples in a given rollup frequency for a specific period of time.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|---------------|----------------|
| elementId | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| metricId | Path | String | Metric Ids can be found by viewing metrics in CloudWisdom. |
| duration | Path | String | Follows ISO8601 duration format. Example options include: PT1h, PT1m, PT10s, P3D. |
| startTime | Path | Date-Time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone).|
| endTime | Path | Date-Time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| rollup | Path | Array[string] | Determines frequency of metric sampling. Options are: ZERO, PT5M, PT1H, PT24H. |

### Request URL

```
https://app.metricly.com/elements/24661111-1111-1111-adbe-71c85255bd40/metrics/bb1111ed-1111-3c76-b1b6-a4111a4eda2f/samples?
```

### CURL

The following CURL example includes a **Duration** of `PT30M` and **Rollup** value of `PT5M`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/24661111-1111-1111-adbe-71c85255bd40/metrics/bb1111ed-1111-3c76-b1b6-a4111a4eda2f/samples?duration=PT30m&rollup=PT5M'

```

### Response Body

The following response body contains 5 metric samples for the **metricId** `bb1111ed-1111-3c76-b1b6-a1111a4eda2f`.

```
{
  "samples": [
    {
      "metricId": "bb1111ed-1111-3c76-b1b6-a1111a4eda2f",
      "timestamp": "2019-12-20T16:25:00Z",
      "rollup": "PT5M",
      "data": {
        "actual": 10.2,
        "avg": 10.2,
        "min": 9,
        "max": 13,
        "baselineMean": 53.129704892436585,
        "cnt": 5,
        "sum": 51,
        "baselineStddev": 145.18387878356057,
        "baselineUpper": 633.8652200266789,
        "baselineLower": 0
      }
    },
    {
      "metricId": "bb1111ed-1111-3c76-b1b6-a1111a4eda2f",
      "timestamp": "2019-12-20T16:30:00Z",
      "rollup": "PT5M",
      "data": {
        "actual": 11.6,
        "avg": 11.6,
        "min": 10,
        "max": 13,
        "baselineMean": 52.819651418304396,
        "cnt": 5,
        "sum": 58,
        "baselineStddev": 143.5165646715427,
        "baselineUpper": 626.8859101044752,
        "baselineLower": 0
      }
    },
    {
      "metricId": "bb1111ed-1111-3c76-b1b6-a1111a4eda2f",
      "timestamp": "2019-12-20T16:35:00Z",
      "rollup": "PT5M",
      "data": {
        "actual": 10.8,
        "avg": 10.8,
        "min": 10,
        "max": 12,
        "baselineMean": 52.45982914038505,
        "cnt": 5,
        "sum": 54,
        "baselineStddev": 141.77574214465326,
        "baselineUpper": 619.5627977189981,
        "baselineLower": 0
      }
    },
    {
      "metricId": "bb1111ed-1111-3c76-b1b6-a1111a4eda2f",
      "timestamp": "2019-12-20T16:40:00Z",
      "rollup": "PT5M",
      "data": {
        "actual": 9.8,
        "avg": 9.8,
        "min": 9,
        "max": 11,
        "baselineMean": 53.09643273302771,
        "cnt": 5,
        "sum": 49,
        "baselineStddev": 141.27593059022965,
        "baselineUpper": 618.2001550939463,
        "baselineLower": 0
      }
    },
    {
      "metricId": "bb1111ed-1111-3c76-b1b6-a1111a4eda2f",
      "timestamp": "2019-12-20T16:45:00Z",
      "rollup": "PT5M",
      "data": {
        "actual": 10.4,
        "avg": 10.4,
        "min": 9,
        "max": 12,
        "baselineMean": 53.57279368703339,
        "cnt": 5,
        "sum": 52,
        "baselineStddev": 146.9486822676629,
        "baselineUpper": 641.3675227576849,
        "baselineLower": 0
      }
    }
  ]
}
```

{{% /expand %}}

---

## GET from /elements/{elementId}/metrics/{metricId}/tags

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricTagsUsingGET" >}} GET {{< /button >}} Use this endpoint to get a list of tags associated to a specified metric for a given element.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|--------------------------|
| elementId | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| metricId | Path | String | Metric Ids can be found by viewing metrics in CloudWisdom. |

### Request URL

```
https://app.metricly.com/swagger-ui.html#!/elements/getMetricTagsUsingGET
```

### CURL

The following CURL example includes the required **elementId** and **metricId**.

- You can find an elementId while viewing a metric in CloudWisdom by selecting the _Card Title_ > Element Detail.
- You can find metricIds for an element in your inventory by selecting the _Card Title_ > View all Metrics for this Element.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/metrics/3a1a2fb7-b274-3120-84bd-d7781401894f/tags'
```

### Response Body

The following response body returns a list of tags for the specified **metricId**. Notice how the response lists tags added from CloudWisdom (`netuitiveTags`) and from AWS (`sourceTags`).

```
{
  "netuitiveTags": {
    "n.statistic": "AVG"
  },
  "sourceTags": {
    "awsDimensions": "{\"LoadBalancer\":\"app/bamboo/5f973fddb1e0c653\"}",
    "awsNamespace": "AWS/ApplicationELB"
  }
}
```

{{% /expand %}}

---

## POST to /elements/{elementId}/metrics/{metricId}/tags

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/createMetricTagUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to post new tags (key-value pairs) to a specified metric.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|------------|
| User-Agent | Header | String | Default value: none. |
| elementId | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| metricId | Path | String | Metric Ids can be found by viewing metrics in CloudWisdom. |
| tagWrapper | Body | JSON | Inject a new tag using JSON: "tag-name":"tag-value". |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/metrics/3a1a2fb7-b274-3120-84bd-d7781401894f/tags

```

### CURL

The following CURL example creates the key `Color` and tag value `Blue`, associated to the metric specified in the Request URL.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "netuitiveTag":  \
 { "Color":"Blue"} \
 }' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/metrics/3a1a2fb7-b274-3120-84bd-d7781401894f/tags'
```

### Response Body

The following response body returns confirmation that the key:value pair has been created and assigned.

```
{
  "netuitiveTag": {
    "Color": "Blue"
  }
}
```

{{% /expand %}}

---

## PUT to /elements/{elementId}/metrics/{metricId}/tags/{tagName}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/updateMetricTagUsingPUT" theme="warning" >}} PUT {{< /button >}} Use this endpoint to update the value of a tag for a specified metric.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|------------------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| metricId | path | string | Metric Ids can be found by viewing metrics in CloudWisdom. |
| tagName | path | string | Use this value to update the existing tag. |
| tagWrapper | body | JSON | Inject a new tag using JSON: "tag-name":"tag-value". |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/metrics/3a1a2fb7-b274-3120-84bd-d7781401894f/tags/Color

```

### CURL

The following CURL example changes the previously created `Color` tag's value to `Red`. Notice that you must specify the tagName (key) at the end of the Request URL.

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: */*' --header 'User-Agent: none' -d '{ \
   "netuitiveTag":  \
 { "Color":"Red"} \
 }' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/metrics/3a1a2fb7-b274-3120-84bd-d7781401894f/tags/Color'
```

### Response Body

The following response body has no content; this is typical for a successful call.

```
No Content
```

{{% /expand %}}

---

## DELETE from to /elements/{elementId}/metrics/{metricId}/tags/{tag}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteMetricTagUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to delete a tag (key) from a specified metric.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|---------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |
| metricId | path | string | Metric Ids can be found by viewing metrics in CloudWisdom. |
| tag | path | string | Used to specify which tag to delete. |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/metrics/3a1a2fb7-b274-3120-84bd-d7781401894f/tags/Color
```

### CURL

The following CURL example deletes the `Color` tag used in the previous examples. Note that `tag` here is similar to `tagName`; use the Key string (in this case, _Color_.)

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/metrics/3a1a2fb7-b274-3120-84bd-d7781401894f/tags/Color'

```

### Response Body

The following response body has no content; this is typical for a successful call.

```
No Content
```

{{% /expand %}}

---

## GET from /elements/{elementId}/policies

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getPoliciesUsingGET" >}} GET {{< /button >}} Use this endpoint to get a list of policies associated to an element.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/policies
```

### CURL

The following CURL example queries for a list of policies related to the elementId `6bdf4fd1-7134-3959-9c36-17eb5f628e46`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/policies'
```

### Response Body

The following response body contains only one policy for the sake of simplicity; typical results provide a full list of all policies associated to an element.

```
{
  "policies": [
    {
      "id": "02f5b11e-0e11-3bb1-9c1a-fc82a4175111",
      "name": "AWS ALB - Elevated Load Balancer Error Rate",
      "description": "This is an error rate policy looking at errors from the Load Balancer itself.  In this case, we look for both high traffic volumes (> 1000) as well as error rates that are not just higher than normal, but are above a 2% threshold. In those cases, a Critical event will be generated. You may wish to tune either the 1,000 request count threshold, the 2% error threshold, or both, to better suit your environment.",
      "scope": {
        "elementName": null,
        "elementNameRegex": false,
        "elementNameExclude": null,
        "elementNameExcludeRegex": false,
        "fqnIncludes": [],
        "fqnExcludes": [],
        "elementType": null,
        "elementTypes": [
          "ALB"
        ],
        "elementTags": [],
        "elementTagsAll": true,
        "excludedElementTags": [],
        "elementAttributes": [],
        "elementAttributesAll": true,
        "excludedElementAttributes": []
      },
      "duration": 900,
      "anyCondition": false,
      "conditions": [
        {
          "metric": "netuitive.aws.alb.httpcodeelberrorpercent",
          "wildcard": null,
          "metricScopeTags": {},
          "analytic": "baselineDeviation",
          "operator": ">",
          "level": null,
          "level2": null,
          "metricThresholdLevel": null,
          "metricThresholdAnalytic": null
        },
        {
          "metric": "netuitive.aws.alb.httpcodeelberrorpercent",
          "wildcard": null,
          "metricScopeTags": {},
          "analytic": "contextualDeviation",
          "operator": ">",
          "level": null,
          "level2": null,
          "metricThresholdLevel": null,
          "metricThresholdAnalytic": null
        },
        {
          "metric": "netuitive.aws.alb.httpcodeelberrorpercent",
          "wildcard": null,
          "metricScopeTags": {},
          "analytic": "actual",
          "operator": ">=",
          "level": 2,
          "level2": null,
          "metricThresholdLevel": null,
          "metricThresholdAnalytic": null
        },
        {
          "metric": "aws.applicationelb.requestcount",
          "wildcard": null,
          "metricScopeTags": {},
          "analytic": "actual",
          "operator": ">=",
          "level": 1000,
          "level2": null,
          "metricThresholdLevel": null,
          "metricThresholdAnalytic": null
        }
      ],
      "eventConditions": [],
      "checkCondition": null,
      "actions": [
        {
          "type": "event",
          "category": 3
        }
      ],
      "enabled": true,
      "deleted": false,
      "creatorEmail": "techwriter@cloudwisdom.com",
      "lastUpdated": "2018-08-02T22:07:31Z"
    }, <!!! list of more Ids !!!>
  ]
}
```

{{% /expand %}}

---

## GET from /elements/{elementId}/tags

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementTagsUsingGET" >}} GET {{< /button >}} Use this endpoint to get a list of CloudWisdom and Source tags for a particular element.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags
```

### CURL

The following CURL example queries for a list of tags for an element with the **elementId** `6bdf4fd1-7134-3959-9c36-17eb5f628e46`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags'
```

### Response Body

The following response body contains a brief list of tags. Notice how the response lists tags added from CloudWisdom (`netuitiveTags`) and from the element (`sourceTags`).

```
{
  "netuitiveTags": {
    "Cheese": "Brie ",
    "TstMetriclyTag": "Yes",
    "n.analysis.status": null
  },
  "sourceTags": {
    "n.collectors": "ALB"
  }
}
```

{{% /expand %}}

---

## POST to /elements/{elementId}/tags

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/createElementTagUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to create a new tag (key-value pair) for the specified element.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|-----------------------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| tagWrapper | body | JSON | Inject a new tag using JSON. |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags
```

### CURL

The following CURL example posts a new key-value pair of `"Weekday":"Saturday"` to the element specified in the request URL. Notice it must be wrapped with `netuitiveTag`.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "netuitiveTag": { "Weekday":"Saturday"} \
 } \
  \
 \' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags'
 ```

### Response Body

The following response body prints confirmation of the tag key:value update.

```
{
  "netuitiveTag": {
    "Weekday": "Saturday"
  }
}
```

{{% /expand %}}

---

## PUT to /elements/{elementId}/tags/{tagName}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/updateElementTagUsingPUT" theme="warning" >}} PUT {{< /button >}} Use this endpoint to update tag values for the specified element's tag.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|-----------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| tagName | path | string | Use this value to update the existing tag. |
| tagWrapper | body | JSON | Inject a new tag using JSON. |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags/Weekday
```

### CURL

The following CURL example updates the tag key `Weekday` with a new value,`Sunday`.

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: */*' --header 'User-Agent: none' -d '{ \
   "netuitiveTag": { "Weekday":"Sunday"} \
 } \
 ' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags/Weekday'
```

### Response Body

The following response body has no content; this is typical for a successful call.

```
no content
```

{{% /expand %}}

---

## DELETE from /elements/{elementId}/tags/{tag}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteElementTagUsingDELETE" theme="danger" >}} DELETE {{< /button >}} This endpoint deletes the specified tag for a given element.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|----------------------------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| tag | path | string | Used to specify which tag to delete. |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags/Weekday
```

### CURL

The following CURL example deletes the `Weekday` tag used in our previous examples.

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46/tags/Weekday'
```

### Response Body

The following response body has no content; this is typical for a successful call.

```
No Content
```

{{% /expand %}}

---

## DELETE from /elements/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteElementUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to delete specified elements.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|----------------------------------|
| User-Agent | header | string | Default value: none. |
| Id | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |

### Request URL

```
https://app.metricly.com/elements/111a50a0-2b5c-3eb9-b25b-11f81de11038
```

### CURL

The following CURL example deletes an element with the **elementId** `111a50a0-2b5c-3eb9-b25b-11f81de11038`.

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/elements/111a50a0-2b5c-3eb9-b25b-11f81de11038'

```

### Response Body

The following response body has no content; this is typical for a successful call.


```
no content
```

{{% /expand %}}

---

## GET from /elements/{id}

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementUsingGET" >}} GET {{< /button >}} Use this endpoint to get details of a specified element.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|-------------------------------------------------|
| Id | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46
```

### CURL

The following CURL example uses the **elementId** `/6bdf4fd1-7134-3959-9c36-17eb5f628e46` to get a list of element details.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/6bdf4fd1-7134-3959-9c36-17eb5f628e46'
```

### Response Body

The following response body is a shortened example; typical responses are much longer with several metrics and attributes.

```
{
  "element": {
    "netuitiveTags": {
      "Cheese": "Cheddar",
      "TstMetriclyTag": "Yes",
      "n.analysis.status": null
    },
    "sourceTags": {
      "n.collectors": "ALB"
    },
    "metrics": [
      {
        "netuitiveTags": {
          "n.statistic": "AVG"
        },
        "sourceTags": {
          "awsDimensions": "{\"LoadBalancer\":\"app/bamboo/5f973fddb1e0c653\"}",
          "awsNamespace": "AWS/ApplicationELB"
        },
        "processingFlags": {
          "RAW_AGG": true
        },
        "unit": "Count",
        "dataSourceId": 31845,
        "fqn": "aws.applicationelb.clienttlsnegotiationerrorcount",
        "name": "ClientTLSNegotiationErrorCount",
        "id": "5be97f00-82df-3b63-8751-13a09b1a2269"
      } <!!! more metrics usually listed here !!!>
    ],
    "fqn": "111119301106:ALB:us-east-1:app/bamboo/5f973fddb1e0c111",
    "name": " bamboo - us-east-1",
    "location": "us-east-1",
    "id": "6bdf4fd1-71111-3959-9c36-17eb5f611e11",
    "type": "ALB",
    "attributes": [
      {
        "id": "2e076c28-295d-3827-9638-ef8ecce767a7",
        "dataSourceId": 31845,
        "name": "ipAddressType",
        "value": "ipv4",
        "attributeType": null
      },
      {
        "id": "9124e608-197f-39eb-a35b-15155adc6c9d",
        "dataSourceId": 31845,
        "name": "scheme",
        "value": "internet-facing",
        "attributeType": null
      } <!!! more attributes usually listed here !!!>
      }
    ]
  }
}
```

{{% /expand %}}

---

## GET from /elements/{id}/relationships

{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementRelationshipsUsingGET" >}} GET {{< /button >}}  Use this endpoint to view an element's relationships.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|-------------------------|
| id | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| levels | Query | Integer | Depth of relationships. |
| startTime | Query | Date-Time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | Query | Date-Time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |

### Request URL

```
https://app.metricly.com/elements/6bdf4fd1-1111-1111-9c36-17eb5f628e46/relationships?levels=2
```

### CURL

The following CURL example gets a list of relationships for an element with the **elementId** `6bdf4fd1-1111-1111-9c36-17eb5f628e46` and a **level** of `2`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/6bdf4fd1-1111-1111-9c36-17eb5f628e46/relationships?levels=2'
```

### Response Body

```
{
  "relationships": {
    "type": null,
    "label": null,
    "directed": true,
    "nodes": [
      {
        "id": "6bdf4fd1-1111-1111-9c36-17eb5f628e46",
        "label": "ECS-ASG-Spot-GREEN",
        "type": "ASG",
        "metadata": {
          "fqn": "501234301106:ASG:us-west-2:ECS-ASG-Spot-GREEN"
        }
      },
      {
        "id": "0f78c417-4fb1-38e9-9b84-0289fc65c9c0",
        "label": "GREEN-JSLAVE (10.12.52.132)",
        "type": "EC2",
        "metadata": {
          "fqn": "501234301106:EC2:us-west-2:i-04dcebc729b34a9dc"
        }
      },
      {
        "id": "a37b3749-8584-39d4-bcd0-46cfd49eb2fa",
        "label": "vol-0fcbb26fd00e33818",
        "type": "EBS",
        "metadata": {
          "fqn": "501234301106:EBS:us-west-2:vol-0fcbb26fd00e33818"
        }
      },
      {
        "id": "ae12b2f7-1111-11c7-836b-73ed9272ebdd",
        "label": "vol-0e0ec86d83b5bbfa8",
        "type": "EBS",
        "metadata": {
          "fqn": "501111301106:EBS:us-west-2:vol-0e0ec00d83b5bbfa8"
        }
      }
    ],
    "edges": [
      {
        "source": "0f11c417-4fb1-38e9-9b84-0111fc65c9c0",
        "relation": "member of",
        "target": "241464d6-f5df-3111-8aeb-30352c0d1108",
        "directed": true,
        "metadata": {}
      },
      {
        "source": "a37b3749-2222-39d4-bcd2-46cfd49eb2fa",
        "relation": "member of",
        "target": "0f78c227-4fb1-38e9-9b22-0111fc65c9c0",
        "directed": true,
        "metadata": {}
      },
      {
        "source": "ae12b2f7-1234-30c7-836b-73ed1172ebdd",
        "relation": "member of",
        "target": "0f11c417-4fb1-38e9-9b84-1111fc65c9c0",
        "directed": true,
        "metadata": {}
      }
    ],
    "metadata": {}
  }
}
```

{{% /expand %}}

---

## How to Find an Element ID and Delete it via the API

You can automate element removal from CloudWisdom using two Element endpoints: **/elasticsearchElementQueryUsingPOST** and **/elements/{id}**. This is useful for keeping a clean inventory and it helps avoid false-positive alerts when routinely shutting down instances that are using the Metricly agent.

{{% expand "View Walkthrough." %}}

1. Build a query using CURL that searches your inventory for an element matching **elementNames** you provide. This query returns information on the element, such as the elementId.  In this example we are searching for `element-name-abc1`. Since we're only really interested in obtaining the **elementId**, let's exclude metrics _and_ attributes using **sourceFilter**:
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{  "sort": { \
     "field": "name", \
     "order": "asc", \
     "missing": "_last" \
   }, \
   "page": 0, \
   "pageSize": 35, \
   "startDate": "2020-01-26T11:29:56-05:00", \
   "endDate": "2020-01-26T12:29:56-05:00", \
   "elementNames": { \
     "and": false, \
     "items": [ \
       { \
         "literal": true, \
         "contains": true, \
         "item": "element-name-abc1" \
       } \
     ] \
   }, \
   "sourceFilter": { \
     "excludes": [ \
       "metrics", \
       "attributes" \
     ] \
   } \
 }' 'https://app.metricly.com/elements/elasticsearch/elementQuery'
```

2.  Review the request body and obtain the **elementId**.
```
{
  "page": {
    "content": [
      {
        "sourceTags": {
          "Name": "element-name-abc1",
          "n.collectors": "EBS"
        },
        "state": {
          "netuitive.metrics.collected.percent": null
        },
        "eventCount": {
          "total": 0,
          "topCategory": null
        },
        "fqn": "501119301106:EBS:us-east-1:vol-08ab171bfa2c63111",
        "name": "element-name-abc1",
        "location": "us-east-1c",
        "id": "115a11a0-2b5c-3eb9-b11b-48f81de11038",
        "type": "EBS"
      }
    ],
    "last": true,
    "totalElements": 1,
    "totalPages": 1,
    "sort": null,
    "first": true,
    "numberOfElements": 1,
    "size": 35,
    "number": 0
  }
}
```
3. Submit a Delete request to **/elements/{id}**.

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/elements/115a11a0-2b5c-3eb9-b11b-48f81de11038'

```

The element is now removed from your inventory, along with its historical data. If you wish to keep the historical data, consider putting the element in maintenance mode instead. This disables alerts during known outages without discarding historical data.

{{% /expand %}}

## Fetch Raw and 5 Min Samples for a Single Element

You can fetch metric samples for a single element using the **/elements/{elementId}/metrics/{metricId}/samples** endpoint. First you must obtain some element details from the **/elements/elasticsearch/elementQuery** endpoint.

{{% expand "View Walkthrough." %}}

1. Build a POST query using CURL that searches your inventory for an element matching **elementNames** you provide. In this example we are searching for `element-name-abc1`. Since we're only really interested in obtaining the **elementId** and **metricNames**, let's exclude attributes using **sourceFilter**:
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{  "sort": { \
     "field": "name", \
     "order": "asc", \
     "missing": "_last" \
   }, \
   "page": 0, \
   "pageSize": 35, \
   "startDate": "2020-01-26T11:29:56-05:00", \
   "endDate": "2020-01-26T12:29:56-05:00", \
   "elementNames": { \
     "and": false, \
     "items": [ \
       { \
         "literal": true, \
         "contains": true, \
         "item": " bamboo - us-east-1" \
       } \
     ] \
   }, \
   "sourceFilter": { \
     "excludes": [ \
       "attributes" \
     ] \
   } \
 }' 'https://app.metricly.com/elements/elasticsearch/elementQuery'
```

2. Review the response body and obtain the **elementId**. Also select the **metricId** corresponding to the metric you want to fetch. For this example, we'll take the ID for **RequestCount**: `4a902433-1111-371c-9a14-d9112c465aa9`.  
```
{
  "page": {
    "content": [
      {
        "netuitiveTags": {
          "TstMetriclyTag": "Yes",
          "n.analysis.status": null
        },
        "sourceTags": {
          "n.collectors": "ALB"
        },
        "state": {
          "netuitive.metrics.collected.percent": 100
        },
        "eventCount": {
          "total": 0,
          "topCategory": null
        },
        "lastProcessed": "2020-01-26T21:35:00Z",
        "metrics": [
          {
            "netuitiveTags": {
              "n.statistic": "AVG"
            },
            "sourceTags": {
              "awsDimensions": "{\"LoadBalancer\":\"app/bamboo/5f973fddb1e0c111\"}",
              "awsNamespace": "AWS/ApplicationELB"
            },
            "processingFlags": {
              "RAW_AGG": true
            },
            "unit": "Count",
            "fqn": "aws.applicationelb.requestcount",
            "dataSourceId": 31845,
            "name": "RequestCount",
            "id": "4a902433-1111-371c-9a14-d9112c465aa9"
          }
        ],
        "fqn": "501119301106:ALB:us-east-1:app/bamboo/5f113fddb1e0c653",
        "name": "element-name-abc",
        "location": "us-east-1",
        "id": "6bdf4fd1-1111-2222-9c36-17eb5f628e46",
        "type": "ALB"
      }
    ],
    "last": true,
    "totalElements": 1,
    "totalPages": 1,
    "sort": null,
    "first": true,
    "numberOfElements": 1,
    "size": 35,
    "number": 0
  }
}
```

3. Build a GET CURL command for the **/elements/{elementId}/metrics/{metricId}/samples**. Include the **elementId** and **metricId** found in the response body. This example adds **startTime** and **endTime** parameters to limit the response body and defines the **rollup** value as `ZERO`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/6bdf4fd1-1111-2222-9c36-17eb5f628e46/metrics/4a902433-1111-371c-9a14-d9112c465aa9/samples?startTime=2020-01-26T11%3A29%3A56-05%3A00&endTime=2020-01-26T11%3A30%3A56-05%3A00&rollup=ZERO'

```
4\. Review the response body for this 1 minute window. This is one metric sample using raw data.

```
{
  "samples": [
    {
      "metricId": "4a902433-1111-371c-9a14-d9112c465aa9",
      "timestamp": "2020-01-26T16:30:00Z",
      "rollup": "ZERO",
      "data": {
        "min": 0,
        "avg": 0.15,
        "max": 1,
        "cnt": 20,
        "sum": 3
      }
    }
  ]
}
```
5\. Compare with the response body of a 10 minute window where the **rollup** value is `PT5M`. This is two metric samples that provide [baseline bands](/capacity-monitoring/analytics/baseline-bands/).

```
{
  "samples": [
    {
      "metricId": "4a902433-1111-371c-9a14-d9112c465aa9",
      "timestamp": "2020-01-26T16:25:00Z",
      "rollup": "PT5M",
      "data": {
        "actual": 0.1,
        "avg": 0.1,
        "min": 0,
        "max": 1,
        "baselineMean": 0.1714443172258489,
        "cnt": 20,
        "sum": 2,
        "baselineStddev": 0.8864747374758107,
        "baselineUpper": 3.717343267129092,
        "baselineLower": 0
      }
    },
    {
      "metricId": "4a902433-1111-371c-9a14-d9112c465aa9",
      "timestamp": "2020-01-26T16:30:00Z",
      "rollup": "PT5M",
      "data": {
        "actual": 0.19047619047619047,
        "avg": 0.19047619047619047,
        "min": 0,
        "max": 1,
        "baselineMean": 0.17387482703660617,
        "cnt": 21,
        "sum": 4,
        "baselineStddev": 0.9182086113131865,
        "baselineUpper": 3.8467092722893526,
        "baselineLower": 0
      }
    }
  ]
}

```

Now you can fetch metric data using two Element endpoints.


{{% /expand %}}
