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

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPoliciesUsingGET_1" theme="info" >}} GET {{< /button >}} Use this endpoint to get a list of policies.
{{% expand "View Method Details." %}}


### Request URL

`https://app.metricly.com/policies`

### CURL

In the following CURL example, only the Request URL is needed.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies'

```

### Response Body

The following response is a shortened list of policies. Normally the Response Body returns a full list of policies.

```
{
  "policies": [
    {
      "id": "543211234-0000-1111-0000-8492ce003668",
      "name": "Docker Container - Elevated CPU Utilization",
      "description": "CPU usage on the Docker container has been higher than expected for 30 minutes or longer.",
      "scope": {
        "elementName": null,
        "elementNameRegex": false,
        "elementNameExclude": null,
        "elementNameExcludeRegex": false,
        "fqnIncludes": [],
        "fqnExcludes": [],
        "elementType": null,
        "elementTypes": [
          "Docker Container"
        ],
        "elementTags": [],
        "elementTagsAll": true,
        "excludedElementTags": [],
        "elementAttributes": [],
        "elementAttributesAll": true,
        "excludedElementAttributes": []
      },
      "duration": 1800,
      "anyCondition": false,
      "conditions": [
        {
          "metric": "netuitive.docker.cpu.container_cpu_percent",
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
          "metric": "netuitive.docker.cpu.container_cpu_percent",
          "wildcard": null,
          "metricScopeTags": {},
          "analytic": "contextualDeviation",
          "operator": ">",
          "level": null,
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
          "category": 1
        }
      ],
      "enabled": true,
      "deleted": false,
      "creatorEmail": "research@netuitive.com",
      "lastUpdated": "2019-02-04T17:05:08Z"
    },
    {
      "id": "0147c5b4-2222-3333-4444-f6de20427775",
      "name": "Consul - Unusually Low Number of Nodes",
      "description": "Please, check your nodes: total number of nodes is less than usual. Some nodes might be lost.",
      "scope": {
        "elementName": null,
        "elementNameRegex": false,
        "elementNameExclude": null,
        "elementNameExcludeRegex": false,
        "fqnIncludes": [],
        "fqnExcludes": [],
        "elementType": null,
        "elementTypes": [
          "SERVER"
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
          "metric": "consul.catalog.total_nodes",
          "wildcard": null,
          "metricScopeTags": {},
          "analytic": "baselineDeviation",
          "operator": "<",
          "level": null,
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
          "category": 2
        }
      ],
      "enabled": false,
      "deleted": false,
      "creatorEmail": "research@netuitive.com",
      "lastUpdated": "2019-04-09T21:29:57Z"
    }
  ]
}
```

{{% /expand %}}

---

## POST to /policies

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/savePolicyUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to create policies and assign conditions, notifications.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent | header | string | User-Agent. |
|  policyWrapper  | body   |  JSON | Policy Wrapper (includes policy template)  |


### Request URL

`https://app.metricly.com/policies`

### CURL

In the following CURL example, a WINSRV policy is created. This template references an existing notification and has one set of conditions for the **metric** `diskspace.root.byte_percentfree`.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "policy": { \
     "name": "WINSRV Example", \
     "description": null, \
     "scope": { \
       "elementName": null, \
       "elementNameRegex": false, \
       "elementNameExclude": null, \
       "elementNameExcludeRegex": false, \
       "fqnIncludes": [], \
       "fqnExcludes": [], \
       "elementType": null, \
       "elementTypes": [ \
         "WINSRV" \
       ], \
       "elementTags": [], \
       "elementTagsAll": true, \
       "excludedElementTags": [], \
       "elementAttributes": [], \
       "elementAttributesAll": true, \
       "excludedElementAttributes": [] \
     }, \
     "duration": 300, \
     "anyCondition": false, \
     "conditions": [ \
       { \
         "metric": "diskspace.root.byte_percentfree", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "actual", \
         "operator": "<", \
         "level": 5, \
         "level2": null, \
         "metricThresholdLevel": null, \
         "metricThresholdAnalytic": null \
       } \
     ], \
     "eventConditions": [], \
     "checkCondition": null, \
     "actions": [ \
       { \
         "type": "event", \
         "category": 1 \
       }, \
       { \
         "type": "notification", \
         "id": 26649, \
         "enabled": true, \
         "notifyFrequencyMin": 2147483647, \
         "sendOnClear": true \
       } \
     ], \
     "enabled": true, \
     "deleted": false, \
     "creatorEmail": "support-testing%40netuitive.com", \
     "lastUpdated": "2019-07-31T21:44:03Z" \
   } \
 }' 'https://app.metricly.com/policies'
```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
  "policy": {
    "name": "WINSRV Example",
    "description": null,
    "scope": {
      "elementName": null,
      "elementNameRegex": false,
      "elementNameExclude": null,
      "elementNameExcludeRegex": false,
      "fqnIncludes": [],
      "fqnExcludes": [],
      "elementType": null,
      "elementTypes": [
        "WINSRV"
      ],
      "elementTags": [],
      "elementTagsAll": true,
      "excludedElementTags": [],
      "elementAttributes": [],
      "elementAttributesAll": true,
      "excludedElementAttributes": []
    },
    "duration": 300,
    "anyCondition": false,
    "conditions": [
      {
        "metric": "diskspace.root.byte_percentfree",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "actual",
        "operator": "<",
        "level": 5,
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
        "category": 1
      },
      {
        "type": "notification",
        "id": 26649,
        "enabled": true,
        "notifyFrequencyMin": 2147483647,
        "sendOnClear": true
      }
    ],
    "enabled": true,
    "deleted": false,
    "creatorEmail": "support-testing@netuitive.com",
    "lastUpdated": "2019-07-31T21:44:03Z"
  }
}
```

### Response Body

The following Response Body includes a new unique **id** and updates the **creatorEmail** to your user email address.

```
{
  "policy": {
    "id": "aa77637d-1870-442e-94a3-3b06a1424120",
    "name": "WINSRV Example",
    "description": null,
    "scope": {
      "elementName": null,
      "elementNameRegex": false,
      "elementNameExclude": null,
      "elementNameExcludeRegex": false,
      "fqnIncludes": [],
      "fqnExcludes": [],
      "elementType": null,
      "elementTypes": [
        "WINSRV"
      ],
      "elementTags": [],
      "elementTagsAll": true,
      "excludedElementTags": [],
      "elementAttributes": [],
      "elementAttributesAll": true,
      "excludedElementAttributes": []
    },
    "duration": 300,
    "anyCondition": false,
    "conditions": [
      {
        "metric": "diskspace.root.byte_percentfree",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "actual",
        "operator": "<",
        "level": 5,
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
        "category": 1
      },
      {
        "type": "notification",
        "id": 26649,
        "enabled": true,
        "notifyFrequencyMin": 2147483647,
        "sendOnClear": true
      }
    ],
    "enabled": true,
    "deleted": false,
    "creatorEmail": "mrlawrencelane+supportaccount@gmail.com",
    "lastUpdated": "2019-07-31T21:44:03Z"
  }
}

```

{{% /expand %}}

---

## GET from /policies/elements

{{< button href="https://app.metricly.com/swagger-ui.html#!/metrics/getCrossElementMetricAggregationUsingPOST" theme="info" >}} GET {{< /button >}} Use this endpoint to retrieve element counts for all policies within time frame specified.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|---------------|---------------------------------------------------------------|
| duration | query | string | Follows ISO8601 duration format. Example options include: PT1h, PT1m, PT10s, P3D |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |

### Request URL

`https://app.metricly.com/policies/elements?startTime{startTime}&endTime={endTime}`

### CURL

In the following CURL example, the endpoint is queried for an element count between the **startTime** `2020-02-29T15:53:00Z` and **endTime** `2020-02-29T15:54:00Z`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies/elements?startTime=2020-02-29T15%3A53%3A00Z&endTime=2020-02-29T15%3A54%3A00Z'
```

### Response Body

The following Response Body lists all **policyIds** and a count of elements monitored by them.

```
{
  "a16bbe53-1111-3277-0000-91fe9ebc7c2f": 3,
  "5ae4f7be-2222-48d5-9999-c521048c5822": 0,
  "ad6e5f73-3333-4440-8888-f94d2e531d6f": 2,
  "02f5b89e-4444-3bb5-7777-fc82a4175706": 2,
  "5a87596d-5555-3aa3-6666-7399c41037a1": 7,
  "011cf660-6666-3f8f-5555-8492ce003668": 0,
  "95b947fc-7777-3c65-4444-1aa3b1a454a4": 3,
  "a9b64afc-8888-4b36-3333-9df46284eb25": 0,
  "94303ae5-9999-476f-2222-8be9e33daa26": 27,
  "b5585ce9-1010-476f-1111-d7be3a4708a7": 171,
  "8b2ea134-1212-3fcb-0909-d251ad8043eb": 3
}

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
