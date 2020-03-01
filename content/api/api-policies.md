---
title: "Policies API"
draft: false
categories:
tags: ["#api", "#policy", "#mute", "#disable"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---


## About the Policies  API

CloudWisdom's Policies API can be used to -----.  You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/policies) and by clicking the interactive buttons below.

## GET from /policies

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPoliciesUsingGET_1" theme="info" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}


### Request URL

`https://app.metricly.com/policies`

### CURL

In the following CURL example

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies'

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## POST to /policies

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/savePolicyUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent | header | string | User-Agent. |
|  policyWrapper  | body   |  JSON | Policy Wrapper (includes policy template)  |



### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## GET from /policies/elements

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getCrossElementMetricAggregationUsingPOST" theme="info" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|---------------|---------------------------------------------------------------|
| duration | query | string | Follows ISO8601 duration format. Example options include: PT1h, PT1m, PT10s, P3D |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |

### Request URL

`https://app.metricly.com/policies/elements`

### CURL

In the following CURL example

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies/elements'

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## GET from /policies/events

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPolicyEventCountsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|---------------|---------------------------------------------------------------|
| duration | query | string | Follows ISO8601 duration format. Example options include: PT1h, PT1m, PT10s, P3D |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |


### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## GET from /policies/mute

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPolicyMutesUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}



### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## DELETE from /policies/{policyId}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/deletePolicyUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| elasticsearchQuery | body | json | A JSON query. |



### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## GET from /policies/{policyId}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPolicyUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| elasticsearchQuery | body | json | A JSON query. |



### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## PUT to /policies/{policyId}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/updatePolicyUsingPUT" theme="warning" >}} PUT {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## GET from /policies/{policyId}/events

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getNumberOfEventsByPolicyUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters



### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## DELETE from /policies/{policyId}/mute

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/clearMutePolicyUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters


### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---

## POST to /policies/{policyId}/mute/{muteMs}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/mutePolicyUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters


### Request URL

` `

### CURL

In the following CURL example

```


```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```


```

### Response Body

The following response  

```

```

{{% /expand %}}

---
