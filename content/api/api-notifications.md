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

CloudWisdom's Metrics API can be used to review metrics.  You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/notifications) and by clicking the interactive buttons below.

## GET to /notifications

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/listUsingGET_2" theme="info" >}} GET {{< /button >}} Use this endpoint to get a list of all notifications (and their templates).
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
| notificationWrapper | body | JSON | A notification wrapper. |



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

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/deleteUsingDELETE_3" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent  | header  | string  | User-Agent  |
| id | path | long | Notification's unique ID.|



### Request URL

`https://app.metricly.com/notifications/{id}`

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

## GET from /notifications/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/getSingleUsingGET_2" theme="info" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| id | path | long | Notification's unique ID.|




### Request URL

`https://app.metricly.com/notifications/{id}`

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



## PUT to /notifications/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/notifications/replaceUsingPUT" theme="warning" >}} PUT {{< /button >}} Use this endpoint to
{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|---------------|------------------------------------------------------------------------------------|
| User-Agent  | header  | string  | User-Agent  |
| id | path | long | Notification's unique ID.|
| Notification   | body  | JSON  |  JSON instructions to edit or build notifications. |


### Request URL

`https://app.metricly.com/notifications/{id}`

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
