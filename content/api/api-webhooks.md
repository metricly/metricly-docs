---
title: "Webhooks API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---


## About the Webhooks API

CloudWisdom's Webhooks API can be used to .

## POST to /webhook{apiId}
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/widgets/listWidgetsUsingGET" >}} GET {{< /button >}} Use this endpoint to
{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| dashboardId | query | string | Unique ID of the dashboard this widget is associated to. |

### Request URL

 ` `

### CURL

The following example only requires the dashboard's **id** to return the widgets.

```

```

### Response Body

The following response body returns 4 widgets that belong to the chosen dashboard. This does not include **gridstackContents** found by interacting with the Dashboards API directly.

```

```
{{% /expand %}}

---





The Webhooks API allows you to use webhooks to send events to CloudWisdom. Sending events via the Webhook API can be used to generate external events in CloudWisdom’s Event Explorer, meaning you could create policies based on the content of those messages. See external event policy conditions for more information.

**Request Headers**

| Header Name | Header Value |
|--------------|------------------|
| Content-Type | application/json |

## PUT
### PUT a New Event /webhook/{apild}

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------------|
| body | Optional | Body parameter; your event message as a string. |
| apiId | Required | URL (path) parameter; your API key. |

**Body Attributes**

No strict format.

{{% notice warning %}}
The Webhook endpoint will take any text you place in the body and use it as the event message in CloudWisdom, so it’s not necessary to include proper JSON formatting (unless you want your message to include brackets and attribute-value pairs).
{{% /notice %}}
