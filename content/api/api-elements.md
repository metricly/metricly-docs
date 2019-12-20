---
title: "Elements API"
draft: false
categories:
tags: ["#api", "#elements"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---


## POST to /elements/elasticsearch/elementAgg/{term}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/aggregateElementsUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The element field you want to aggregate. |
| elasticsearchQuery | body | json | A json query. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/elasticsearch/elementQuery

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/elasticsearchElementQueryUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The the element field you want to aggregate. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/name/preview

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/namePreviewUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------------|----------------|-----------|-------------|
| elementTemplate | Body | json | ?? |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/search

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/getElementsPOSTUsingPOST" theme="warning" >}} POST {{< /button >}} This is a deprecated method. Use **/elements/elasticsearch/elementQuery** instead.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|----------------------|----------------|-----------|---------------|
| elementSearchWrapper | Body | json | a json query; add field parameters you want returned in the response body and use ids to search for specific elements. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/events

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getEventsUsingGET" >}} GET {{< /button >}} Use this endpoint to discover events within certain time frames (days, hours, minutes).

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|----------------------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| duration | query | string | ?? |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |

### Request URL

```
https://app.metricly.com/elements/11160111-0111-392f-adbe-71c85111bd40/events

```

### CURL

The following example uses a YYYYMMDD startTime and endTime value.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/11160111-0111-392f-adbe-71c85111bd40/events?startTime=20191201&endTime=20191202'

```

The following example uses YYYY-MM-DDT00:001Z format (must include time zone). This is better for looking at a specific, narrow time frames.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/elements/11160111-0111-392f-adbe-71c85111bd40/events?startTime=2019-12-01T03%3A30Z&endTime=2019-12-01T07%3A30Z'
```

### Response Body


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

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricMetadataUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|--------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |
| metricFQN | query | string | The metricFQN can be found by viewing metrics in CloudWisdom. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/metrics/{metricId}/samples

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricResultsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|---------------|----------------|
| elementId | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| metricId | Path | String | Metric Ids can be found by viewing metrics in CloudWisdom. |
| duration | Path | String |  |
| startTime | Path | Date-Time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone).|
| endTime | Path | Date-Time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| rollup | Path | Array[string] | Determines frequency of metric sampling. Options are: ZERO, PT5M, PT1H, PT24H. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/metrics/{metricId}/tags

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricTagsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|--------------------------|
| elementId | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| metricId | Path | String | Metric Ids can be found by viewing metrics in CloudWisdom. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/{elementId}/metrics/{metricId}/tags

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/createMetricTagUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|------------|
| User-Agent | Header | String | Default value: none. |
| elementId | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| metricId | Path | String | Metric Ids can be found by viewing metrics in CloudWisdom. |
| tagWrapper | Body | JSON | Inject a new tag using JSON: "tag-name":"tag-value". |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## PUT to /elements/{elementId}/metrics/{metricId}/tags/{tagName}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/updateMetricTagUsingPUT" theme="info" >}} PUT {{< /button >}}

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

### CURL

### Response Body

{{% /expand %}}

---

## DELETE from to /elements/{elementId}/metrics/{metricId}/tags/{tag}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteMetricTagUsingDELETE" theme="danger" >}} DELETE {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|---------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |
| metricId | path | string | Metric Ids can be found by viewing metrics in CloudWisdom. |
| tag | path | string | Used to specify which tag to delete. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/policies

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getPoliciesUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/tags

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementTagsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46). |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/{elementId}/tags

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/createElementTagUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|-----------------------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| tagWrapper | body | JSON | Inject a new tag using JSON. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## PUT to /elements/{elementId}/tags/{tagName}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/updateElementTagUsingPUT" theme="info" >}} PUT {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|-----------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| tagName | path | string | Use this value to update the existing tag. |
| tagWrapper | body | JSON | Inject a new tag using JSON. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## DELETE from /elements/{elementId}/tags/{tag}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteElementTagUsingDELETE" theme="danger" >}} DELETE {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|----------------------------------|
| User-Agent | header | string | Default value: none. |
| elementId | path | string | Element Ids can be found in by selecting an element in CloudWisdom and viewing the URL (/#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| tag | path | string | Used to specify which tag to delete. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## DELETE from /elements/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteElementUsingDELETE" theme="danger" >}} DELETE {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|-----------|----------------------------------|
| User-Agent | header | string | Default value: none. |
| Id | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{id}

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|-------------------------------------------------|
| Id | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{id}/relationships

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementRelationshipsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|-------------------------|
| id | Path | String | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| levels | Query | Integer | Depth of relationships. |
| startTime | Query | Date-Time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | Query | Date-Time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---
