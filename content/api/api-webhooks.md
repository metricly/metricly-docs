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

CloudWisdom's Webhooks API can be used to ingest external events. You can also create policies (via [Policies API](/api/api-policies)) triggered by the contents of these external events. This endpoint is not available in Swagger.

## POST to /webhook{apiId}
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/" >}} GET {{< /button >}} Use this endpoint to ingest external events.
{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| apiId | query | string | Your Webhook API key. This is found in Integrations > Webhook. |
| body | body  | JSON  | JSON template for the webhook.  |

### Request URL

 `https://app.metricly.com/ingest/webhook/{apiId}`

### CURL

The following example sends an external event to CloudWisdom to be ingested and accounted for.

{{% notice tip %}}
The Webhooks endpoint accepts any text you place in the body and uses that input as the event message in CloudWisdom. It is not necessary to include proper JSON formatting unless you want your message to include brackets and attribute-value pairs.
{{% /notice %}}

```
curl -X POST 'https://api.app.metricly.com/ingest/webhook/2e9b8ed4f12345fdca11af3a443172a4' \
-H 'Content-Type: application/json' \
-H 'X-Netuitive-Api-Options: INJECT_TIMESTAMP' \
-H 'Authorization: Basic XXX' \
-H ‘Accept: application/json’ \
--data '
{ "category": "WARN", "elementId": 12345, "elementType": "SERVER", "policy": "EXTERNAL SYSTEM A", "title": "XYZ" }
'

### Response Body

The following response body returns no content and a 202 success code. 

```
no content

```
{{% /expand %}}

---
