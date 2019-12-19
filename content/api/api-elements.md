---
title: "Elements API"
draft: false
categories:
tags: ["#api", "#elements"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

## GET from /elements
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementsUsingGET" >}} GET {{< /button >}} This is a deprecated method. Use **/elements/elasticsearch/elementQuery** instead.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|---------------|-------------|
| ids | Query | Array[string] | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| name | Query | Array[string] | Element Name. |
| type | Query | Array[string] | Type of element. |
| location | Query | Array[string] | Type of resource. |
| tags | Query | String | Tags passed into CloudWisdom. |
| fields | Query | Array[string] | Filter results by adding only the fields you want to see in the response. |
| startTime | Query | Date-Time | Start time for the query. |
| endTime | Query | Date-Time | End time for the query. |
| state | Query | Boolean | ?? |
| eventCount | Query | Boolean | ?? |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/elasticsearch/elementAgg/{term}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/aggregateElementsUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The the element field you want to aggregate. |
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

## GET from /element/ids

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementIdsUsingGET" >}} GET {{< /button >}} This is a deprecated method. Use **/elements/elasticsearch/elementQuery** instead.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------------|----------------|-----------|---------------------------|
| startTime | Query | Date-Time | Start time for the query. |
| endTime | Query | Date-Time | End time for the query. |
| queriesTemporalInventory | Query | Boolean |  |

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

## GET from /elements/search

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/getElementsSearchGetUsingGET" theme="success" >}} GET {{< /button >}} This is a deprecated method. Use **/elements/elasticsearch/elementQuery** instead.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|------------|----------------|---------------|-------------|
| ids | Query | Array[string] | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| name | Query | Array[string] | Element Name. |
| type | Query | Array[string] | Type of element. |
| location | Query | Array[string] | Type of resource. |
| tags | Query | String | Tags passed into CloudWisdom. |
| fields | Query | Array[string] | Filter results by adding only the fields you want to see in the response. |
| startTime | Query | Date-Time | Start time for the query. |
| endTime | Query | Date-Time | End time for the query. |
| state | Query | Boolean | ?? |
| eventCount | Query | Boolean | ?? |

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

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getEventsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-----------|----------------|-----------|----------------------------------|
| elementId | path | string | Element Ids can be found in by selecting an element in  CloudWisdom and viewing the URL ( /#/inventory/6bdf4fd1-1111-1111-1c11-17eb5f628e46) |
| duration | query | string | ?? |
| startTime | query | date-time | Start time for the query. |
| endTime | query | date-time | End time for the query. |

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/metrics

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricMetadataUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/metrics/{metricId}/samples

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricResultsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/metrics/{metricId}/tags

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getMetricTagsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/{elementId}/metrics/{metricId}/tags

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/createMetricTagUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## PUT to /elements/{elementId}/metrics/{metricId}/tags/{tagName}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/updateMetricTagUsingPUT" theme="info" >}} PUT {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## DELETE from to /elements/{elementId}/metrics/{metricId}/tags/{tag}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteMetricTagUsingDELETE" theme="danger" >}} DELETE {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/policies

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getPoliciesUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{elementId}/tags

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementTagsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## POST to /elements/{elementId}/tags

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/createElementTagUsingPOST" theme="warning" >}} POST {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## PUT to /elements/{elementId}/tags/{tagName}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/updateElementTagUsingPUT" theme="info" >}} PUT {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## DELETE from /elements/{elementId}/tags/{tag}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteElementTagUsingDELETE" theme="danger" >}} DELETE {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## DELETE from /elements/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/elements/deleteElementUsingDELETE" theme="danger" >}} DELETE {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{id}

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---

## GET from /elements/{id}/relationships

{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/elements/getElementRelationshipsUsingGET" >}} GET {{< /button >}}

{{% expand "View Method Details." %}}

### Parameters

### Request URL

### CURL

### Response Body

{{% /expand %}}

---
