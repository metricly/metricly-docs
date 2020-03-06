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

CloudWisdom's Policies API can be used to list, inspect, create, delete, mute, and unmute policies.  You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/policies) and by clicking the interactive buttons below.

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

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPolicyElementCountsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to retrieve element counts for all policies within the time frame specified.
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

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPolicyEventCountsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to retrieve event counts for all policies within the time frame specified.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|---------------|---------------------------------------------------------------|
| duration | query | string | Follows ISO8601 duration format. Example options include: PT1h, PT1m, PT10s, P3D |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |


### Request URL

`https://app.metricly.com/policies/events?startTime={startTime}&endTime={endTime}`

### CURL

In the following CURL example, the endpoint is queried for an element count between the **startTime** `2020-02-28T15:53:00Z` and **endTime** `2020-03-01T15:54:00Z`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies/events?startTime=2020-02-28T15%3A53%3A00Z&endTime=2020-03-01T16%3A54%3A00Z'
```

### Response Body

The following response returns only one policy, with 31 events occurring within the specified time frame.

```
{
  "fe8bd66b-0000-1111-2222-d898aebda30f": 31
}
```

{{% /expand %}}

---

## GET from /policies/mute

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPolicyMutesUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get a list of currently muted policies.
{{% expand "View Method Details." %}}

### Request URL

`https://app.metricly.com/policies/mute`

### CURL

In the following CURL example, only the Request URL is needed to make the API call.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies/mute'
```

### Response Body

The following Response Body returns 3 muted policies and the mute duration in milliseconds.

```
{
  "f7d50ff4-1111-0000-0000-3ea1832f841b": 1583108010423,
  "fac1361a-2222-0000-0000-f139f5655992": 1583108005374,
  "fb1950a1-3333-0000-0000-0496180a020d": 1583108000823
}
```

{{% /expand %}}

---

## DELETE to /policies/{policyId}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/deletePolicyUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to delete a policy.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent | header | string | User-Agent. |
| policyId  | path  | string  | Unique ID for a policy.  |

### Request URL

`https://app.metricly.com/policies/{policyId}`

### CURL

In the following CURL example, only the **policyId** must be added to the Request URL to delete the policy.

```
curl -X DELETE --header 'Accept: application/json' --header 'User-Agent: none' 'https://app.metricly.com/policies/fb1950a1-3333-0000-0000-0496180a020d'
```

### Response Body

The following Response Body returns no content with a 204 success code.

```
no content
```

{{% /expand %}}

---

## GET from /policies/{policyId}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getPolicyUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to retrieve a specific policy.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| policyId  | path  | string  | Unique ID for a policy.  |

### Request URL

`https://app.metricly.com/policies/{policyId}`

### CURL

In the following CURL example, only the **policyId** must be added to the Request URL.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies/2cf1fb85-bf7b-438a-9e9d-001f374b5eb7'
```


### Response Body

The following response returns the specified policy belonging to id `2cf1fb85-1111-2222-3333-001f374b5eb7`.

```
{
  "policy": {
    "id": "2cf1fb85-1111-2222-3333-001f374b5eb7",
    "name": "WINSRV Example 2",
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
    "lastUpdated": "2020-03-01T23:27:43Z"
  }
}
```

{{% /expand %}}

---

## PUT to /policies/{policyId}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/updatePolicyUsingPUT" theme="warning" >}} PUT {{< /button >}} Use this endpoint to update a policy.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent | header | string | User-Agent. |
| policyId  | path  | string  | Unique ID for a policy.  |
|  policyWrapper  | body   |  JSON | Policy Wrapper (includes policy template)  |


### Request URL

`https://app.metricly.com/policies/{polciyId}`

### CURL

In the following CURL example, the WINSRV policy used in the previous example is updated. Now it is an AWS EC2 policy.

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "policy": { \
     "id": "2cf1fb85-bf7b-438a-9e9d-001f374b5eb7", \
     "name": "AWS EC2 Example", \
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
         "EC2" \
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
         "metric": "aws.ec2.cpuutilization", \
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
  \
     ], \
     "enabled": true, \
     "deleted": false, \
     "creatorEmail": "mrlawrencelane+supportaccount%40gmail.com", \
     "lastUpdated": "2020-03-01T23:27:43Z" \
   } \
 }' 'https://app.metricly.com/policies/2cf1fb85-bf7b-438a-9e9d-001f374b5eb7'
```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
  "policy": {
    "id": "2cf1fb85-bf7b-438a-9e9d-001f374b5eb7",
    "name": "AWS EC2 Example",
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
        "EC2"
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
        "metric": "aws.ec2.cpuutilization",
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

    ],
    "enabled": true,
    "deleted": false,
    "creatorEmail": "mrlawrencelane+supportaccount@gmail.com",
    "lastUpdated": "2020-03-01T23:27:43Z"
  }
}
```

### Response Body

The following Response Body returns the updates reflected in the policy template.

```
{
  "policy": {
    "id": "2cf1fb85-bf7b-438a-9e9d-001f374b5eb7",
    "name": "AWS EC2 Example",
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
        "EC2"
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
        "metric": "aws.ec2.cpuutilization",
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
    "actions": [],
    "enabled": true,
    "deleted": false,
    "creatorEmail": "mrlawrencelane+supportaccount@gmail.com",
    "lastUpdated": "2020-03-01T23:27:43Z"
  }
}
```

{{% /expand %}}

---

## GET from /policies/{policyId}/events

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/getNumberOfEventsByPolicyUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get a count of events by policy.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|---------------|---------------------------------------------------------------|
| policyId | path  | string  | Unique ID for a policy.  |
| duration | query | string | Follows ISO8601 duration format. Example options include: PT1h, PT1m, PT10s, P3D |
| startTime | query | date-time | Start time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |
| endTime | query | date-time | End time for the query. YYYY-MM-DDT00:001Z format (must include time zone). |

### Request URL

`https://app.metricly.com/policies/{policyId}/events`

### CURL

In the following CURL example, a policy with the **policyId** `fe8bd66b-586f-401e-9982-d898aebda30f` is checked for events occurring between **startTime** `2020-02-28T15:53:00Z` and **endTime** `2020-03-02T15:53:00Z`.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies/fe8bd66b-586f-401e-9982-d898aebda30f/events?startTime=2020-02-28T15%3A53%3A00Z&endTime=2020-03-02T15%3A53%3A00Z'
```

### Response Body

The following Response Body returns a count of 31 events.

```
31
```

{{% /expand %}}

---

## DELETE to /policies/{policyId}/mute

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/clearMutePolicyUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to unmute a policy.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|---------------|---------------------------------------------------------------|
| policyId | path  | string  | Unique ID for a policy.  |

### Request URL

`https://app.metricly.com/policies/{policyId}/mute`

### CURL

In the following CURL example, only the **policyId** needs to be added to the Request URL to unmute the policy.

```
curl -X DELETE --header 'Accept: */*' 'https://app.metricly.com/policies/fe8bd66b-586f-401e-9982-d898aebda30f/mute'

```

### Response Body

The following Response Body returns no content and a 200 success code.

```
no content
```

{{% /expand %}}

---

## POST to /policies/{policyId}/mute/{muteMs}

{{< button href="https://app.metricly.com/swagger-ui.html#!/policies/mutePolicyUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to mute a policy (and define the mute's duration).
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|---------------|---------------------------------------------------------------|
| policyId | path  | string  | Unique ID for a policy.  |
| muteMs   | path | long  |  Mute duration in milliseconds. |


### Request URL

`https://app.metricly.com/policies/{policyId}/mute/58000`

### CURL

In the following CURL example, a policy with the **policyId** `fe8bd66b-1111-2222-3333-d898aebda30f` is muted for 58000 milliseconds.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: */*' 'https://app.metricly.com/policies/fe8bd66b-1111-2222-3333-d898aebda30f/mute/58000'
```


### Response Body

The following Response Body returns no content and a 200 success code.

```
no content
```

{{% /expand %}}

---

## How to Mute a Policy Over a Weekend

Having all of your policies unmuted during off-hours isn't always necessary. You can use the Policy API (**/policies/{policyId}/mute{muteMS}**) to mute specified policies until resuming regular hours of operation. This allows for you to still track events that occur while the policy is muted (versus being disabled). Read this walkthrough to learn how to mute a Policy over the weekend.

{{% expand "View Walkthrough." %}}

1\. Build a CURL query to GET from **/policies**. This lists all policies so you can select the right ones to mute.
```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies'
```

2\. Grab the **Id** for each policy you wish to mute. In this example two policies are muted using the IDs `fcc6aed6-0a54-3cbd-be5a-43ded16a3750` and `fac1361a-825d-35cb-8a1c-f139f5655992`.  

3\. Build two separate CURL queries to POST to **/policies/{policyId}/mute{ms}**. Let's mute these policies at Friday at 5pm until Monday 9am. That's `230400000` milliseconds.   

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: */*' 'https://app.metricly.com/policies/fcc6aed6-0a54-3cbd-be5a-43ded16a3750/mute/230400000'

```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: */*' 'https://app.metricly.com/policies/fac1361a-825d-35cb-8a1c-f139f5655992/mute/230400000'

```

4\.  Your policies are now muted. You can confirm they have been muted by making an API GET call to **/policies/mute**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies/mute'
```

5\. The Response Body should look similar to this:

```
{
  "fcc6aed6-0a54-3cbd-be5a-43ded16a3750": 1583108010423,
  "fac1361a-825d-35cb-8a1c-f139f5655992": 1583108005374,
}

```


{{% /expand %}}
