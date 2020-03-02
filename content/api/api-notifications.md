---
title: "Notifications API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---


## About the Notifications API

CloudWisdom's Notifications API can be used to list, create, delete, inspect, and edit notifications.  You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/notifications) and by clicking the interactive buttons below.

## GET to /notifications

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/listUsingGET_2" theme="info" >}} GET {{< /button >}} Use this endpoint to get a list of all notifications and their templates.
{{% expand "View Method Details." %}}


### Request URL

`https://app.metricly.com/notifications`

### CURL

In the following CURL example only the Request URL is needed.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/notifications'
```


### Response Body

The following response is a shortened list of notifications. Typical responses produce the full library of notifications. Notice that the **bodyTemplate** property uses the  [FreeMarker Template Language](https://freemarker.apache.org/) to format a notification's contents.

```
{
  "notifications": [
  {
     "id": 24870,
     "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
     "enabled": true,
     "type": "pagerduty",
     "properties": {
       "payloadType": "default",
       "postContentTemplate": "{\"description\":\"${eventCategory.name}: ${elementFqn} : ${policyName}\",\"client\":\"Netuitive Cloud Service\",\"details\":{\"elementFqn\":\"${elementFqn}\",\"category\":\"${eventCategory.name}\",\"elementType\":\"${elementType}\"},\"contexts\":[{\"type\":\"link\",\"href\":\"https://app.netuitive.com/#/element/${elementId}/events\"}],\"service_key\":\"12345678965433456789954/Z4TJFTYEq4nQ==\",\"incident_key\":\"${policyName}\",\"event_type\":\"trigger\",\"client_url\":\"https://app.netuitive.com\"}",
       "name": "Support PagerDuty",
       "serviceKey": "******",
       "url": "https://events.pagerduty.com/generic/2010-04-15/create_event.json",
       "awsAuthentication": "role"
     }
   },
    {
      "id": 25096,
      "tenantId": "0fa5384a-1111-2222-ad68-43e7c6af54f6",
      "enabled": true,
      "type": "webhook",
      "properties": {
        "payloadType": "custom",
        "postContentTemplate": "{\"text\": \"${eventTimestamp}: The CPU on ${elementId} has exceeded 5% for at least 5 minutes. \\n Event Category: ${eventCategory.name} \\n Fqn: ${elementFqn} \\n location: ${elementLocation}\"}",
        "name": "Slack Webhook (#app-notifications)",
        "url": "https://hooks.slack.com/services/8765432456765432/hgewrtyjhgsftre",
        "webhookType": "event"
      }
    },
    {
      "id": 42119,
      "tenantId": "0fa5384a-1111-2222-ad68-43e7c6af54f6",
      "enabled": true,
      "type": "email",
      "properties": {
        "templateType": "default",
        "address": "example.email@gmail.com",
        "payloadType": "default",
        "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>",
        "name": "example.email@gmail.com",
        "subjectTemplate": "Metricly Event [${policyName}]",
        "awsAuthentication": "role"
      }
    }
  }

```

{{% /expand %}}

---


## POST to /notifications

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/createUsingPOST_1" theme="success" >}} POST {{< /button >}} Use this endpoint to create notifications.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent | header | string | User-Agent |
| notification |  body | JSON   |  JSON instructions to build a notification. |



### Request URL

`https://app.metricly.com/notifications`

### CURL

In the following CURL example a simple notification is created with the **type** `email`. The **bodyTemplate** creates a conditional body that states if the payload is an event, provide the **eventCategory.name**; if the event has  been cleared, send the string CLEAR in the body.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "notification": { \
     "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6", \
     "enabled": true, \
     "type": "email", \
     "properties": { \
       "templateType": "default", \
       "address": "example.email@gmail.com", \
       "payloadType": "default", \
       "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>", \
       "name": "my test email", \
       "subjectTemplate": "Test Event [${policyName}]", \
       "awsAuthentication": "role" \
     } \
   } \
 }' 'https://app.metricly.com/notifications'

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
  "notification": {
    "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
    "enabled": true,
    "type": "email",
    "properties": {
      "templateType": "default",
      "address": "example.email@gmail.com",
      "payloadType": "default",
      "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>",
      "name": "my test email",
      "subjectTemplate": "Test Event [${policyName}]",
      "awsAuthentication": "role"
    }
  }
}

```

### Response Body

The following response confirms the creation of the notification and includes a unique **id**.

```
{
  "notification": {
    "id": 83949,
    "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
    "enabled": true,
    "type": "email",
    "properties": {
      "templateType": "default",
      "address": "example.email@gmail.com",
      "payloadType": "default",
      "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>",
      "name": "my test email",
      "subjectTemplate": "Test Event [${policyName}]",
      "awsAuthentication": "role"
    }
  }
}

```

{{% /expand %}}

---


## POST to /notifications/test

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/sendTestNotificationUsingPOST_1" theme="success" >}} POST {{< /button >}} Use this endpoint to send a test a new notification.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| notificationWrapper | body | JSON | A notification wrapper. Includes a notification template. |



### Request URL

`https://app.metricly.com/notifications/test`

### CURL

In the following CURL example, a new notification is being tested. The exact same kind of payload used to create notifications can be input here first to verify it works as intended. Note that a unique name must be entered to test the notification; existing notifications cannot be tested  using this endpoint.

{{% notice tip %}}

Testing custom emails only verifies the address by sending a canned template. Testing other notifications, such as webhooks, sends the full custom body included in the payload.

{{% /notice %}}

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "notification": { \
     "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6", \
     "enabled": true, \
     "type": "email", \
     "properties": { \
       "templateType": "default", \
       "address": "your.email%40gmail.com", \
       "payloadType": "default", \
       "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>", \
       "name": "UNIQUE NAME", \
       "subjectTemplate": "XYZ System Status>", \
       "awsAuthentication": "role" \
     } \
   } \
 }' 'https://app.metricly.com/notifications/test'

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
  "notification": {
    "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
    "enabled": true,
    "type": "email",
    "properties": {
      "templateType": "default",
      "address": "your.email@gmail.com",
      "payloadType": "default",
      "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>",
      "name": "UNIQUE NAME",
      "subjectTemplate": "XYZ System Status>",
      "awsAuthentication": "role"
    }
  }
}
```

### Response Body

The following response confirms the test was processed. Check the notification's destination to verify the subject line and body match your intended layout.

```
{
  "success": true,
  "content": "Successfully processed message"
}
```

{{% /expand %}}

---


## POST to /notifications/test/{notificationId}

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/sendTestNotificationUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to test an existing notification (has an id).
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| notificationId | path | long | Notification's unique ID.|


### Request URL

`https://app.metricly.com/notifications/test/{notificationId}`

### CURL

In the following CURL example, only the **notificationId** needs to be added to the Request URL.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' 'https://app.metricly.com/notifications/test/84005'
```


### Response Body

The following response confirms a test notification has been sent to the defined destination.

```
{
  "success": true,
  "content": "Successfully processed message"
}

```

{{% /expand %}}

---

## Delete from /notifications/{Id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/deleteUsingDELETE_3" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to delete a notification.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent  | header  | string  | User-Agent  |
| id | path | long | Notification's unique ID.|



### Request URL

`https://app.metricly.com/notifications/{id}`

### CURL

In the following CURL example, only the **notificationId** must be included with the Request URL.

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/notifications/84005'

```

### Response Body

The following response returns no content and a 204 success code.

```
no content
```

{{% /expand %}}

---

## GET from /notifications/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/getSingleUsingGET_2" theme="info" >}} GET {{< /button >}} Use this endpoint to get details on a specific notification.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| id | path | long | Notification's unique ID.|


### Request URL

`https://app.metricly.com/notifications/{id}`

### CURL

In the following CURL example, only the **notificationId** must be included with the Request URL.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/notifications/42119'

```

### Response Body

The following response returns the full notification template.

```
{
  "notification": {
    "id": 42119,
    "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
    "enabled": true,
    "type": "email",
    "properties": {
      "templateType": "default",
      "address": "test.email@gmail.com",
      "payloadType": "default",
      "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>",
      "name": "the test notification",
      "subjectTemplate": "Metricly Event [${policyName}]",
      "awsAuthentication": "role"
    }
  }
}
```

{{% /expand %}}

---



## PUT to /notifications/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/replaceUsingPUT" theme="warning" >}} PUT {{< /button >}} Use this endpoint to update notifications.
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent  | header  | string  | User-Agent  |
| id | path | long | Notification's unique ID.|
| notification   | body  | JSON  |  JSON instructions to edit or build notifications. |


### Request URL

`https://app.metricly.com/notifications/{id}`

### CURL

In the following CURL example, the Slack notification **url** property is updated with a new URL because the old URL belongs to a Slack channel and integration that no longer exist.

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "notification": { \
     "id": 3824451, \
     "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6", \
     "enabled": true, \
     "type": "slack", \
     "properties": { \
       "name": "#cloudwisdom-notifications", \
       "url": "https://hooks.slack.com/services/76543346/7654324/0876543234", \
       "awsAuthentication": "role", \
       "username": "", \
       "payloadType": "default" \
     } \
   } \
 }' 'https://app.metricly.com/notifications/3824451'
```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
  "notification": {
    "id": 3824451,
    "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
    "enabled": true,
    "type": "slack",
    "properties": {
      "name": "#cloudwisdom-notifications",
      "url": "https://hooks.slack.com/services/76543346/7654324/0876543234",
      "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>",
      "awsAuthentication": "role",
      "username": "",
      "payloadType": "default"
    }
  }
}

```

### Response Body

The following response returns the updated notification template.

```
{
  "notification": {
    "id": 3824451,
    "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
    "enabled": true,
    "type": "slack",
    "properties": {
      "address": "mrlawrencelane+supportaccount@gmail.com",
      "bodyTemplate": "<#if payloadType == \"event\">\n  ${eventCategory.name}\n</#if>\n<#if payloadType == \"event_cleared\">\n  CLEAR\n</#if>",
      "payloadType": "default",
      "name": "#cloudwisdom-notifications",
      "url": "https://hooks.slack.com/services/76543346/7654324/0876543234",
      "awsAuthentication": "role",
      "username": ""
    }
  }
```

{{% /expand %}}

---

## How to Find Policy IDs using Notifications

You can use the Notifications API to kickstart a search for policies that are generating notifications. Once you have located the notification's **id**, switch over to the Policies API to inspect the alerting policy and/or update its details.

{{% expand "View Walkthrough." %}}

1\. Build a CURL query to get a list of notifications from **/notifications**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/notifications'

```

2\. Review the Response Body and select a notification to search against. Copy the **id** for later.  Below is a single notification for reference; the Response Body returns a large list.

```
{
    "id": 55406,
    "tenantId": "0fa1234a-0000-1111-4444-12e7c6af54f6",
    "enabled": true,
    "type": "webhook",
    "properties": {
      "payloadType": "custom",
      "postContentTemplate": "{\n   \"message_type\":\"<#if payloadType == \"event\">${eventCategory.name}</#if><#if payloadType == \"event_cleared\">RECOVERY</#if>\", \n   \"entity_id\":\"${elementId}\",\n   \"entity_display_name\":\"${elementName}\",\n     \"state_message\":\"<#if payloadType == \"event\"> [${elementName}] [${policyName}] [${eventTimestamp}] : ${policyDescription}</#if><#if payloadType == \"event_cleared\">The policy ${policyName} has CLEARED for ${elementName} and is no longer generating events as of ${eventTimestamp}</#if>\"\n}",
      "basicPassword": "******",
      "name": "VictorOps",
      "basicUsername": "support-team@example.com",
      "url": "https://alert.victorops.com/integrations/generic/123456/alert/4567-65432-65432-6543/$routing_key",
      "awsAuthentication": "role",
      "webhookType": "event"
    }
  }
```

3\. Build a CURL query to get a list of policies from **/policies**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/policies'
```

4\. Search the Response Body for a policy with **actions** that include `"type": "notification"` and a matching **id**.

```
{
    "id": "2ac7edc4-d1fa-446d-a9ec-36f257d403ca",
    "name": "example policy",
    "description": "Metric collection went below 75%",
    "scope": {
      "elementName": null,
      "elementNameRegex": false,
      "elementNameExclude": null,
      "elementNameExcludeRegex": false,
      "fqnIncludes": [],
      "fqnExcludes": [],
      "elementType": null,
      "elementTypes": [
        "RING"
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
        "metric": "netuitive.metrics.collected.percent",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "actual",
        "operator": "<=",
        "level": 75,
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
      },
      {
        "type": "notification",
        "id": 55406,
        "enabled": true,
        "notifyFrequencyMin": 2147483647,
        "sendOnClear": true
      }
    ],
    "enabled": true,
    "deleted": false,
    "creatorEmail": "example@example.com",
    "lastUpdated": "2018-09-18T20:56:19Z"
  },
```

5\. Once you have located the notification's **id**, you can also grab the policy's **id**. This can be used to update, review, or delete the policy.

{{% /expand %}}
