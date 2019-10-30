---
title: "Ingest API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---
This API is used to send CloudWisdom custom data. Two types of custom payloads can be created with this API:

- Custom elements
- Custom external event messages


## Custom Payloads

### Custom Elements
Custom elements can have metrics, tags, attributes, and relationships.

**POST request**: `http://api.us.cloudwisdom.virtana.com/ingest/{apiId}`

```
[
  {
    "attributes": [
      {
        "name": "string",
        "value": "string"
      }
    ],
    "id": "string",
    "location": "string",
    "metrics": [
      {
        "id": "string",
        "name": "string",
        "sparseDataStrategy": "None",
        "tags": [
          {
            "name": "string",
            "value": "string"
          }
        ],
        "type": "string",
        "unit": "string"
      }
    ],
    "name": "string",
    "relations": [
      {
        "fqn": "string"
      }
    ],
    "samples": [
      {
        "avg": 0,
        "cnt": 0,
        "max": 0,
        "metricId": "string",
        "min": 0,
        "sum": 0,
        "timestamp": "2018-04-27T01:00:44.792Z",
        "val": 0
      }
    ],
    "tags": [
      {
        "name": "string",
        "value": "string"
      }
    ],
    "type": "string"
  }
]

```

### Custom External Event Messages
**POST request**: `https://api.us.cloudwisdom.virtana.com/ingest/events/{apiId}`

```
[
  {
    "data": {},
    "source": "string",
    "tags": [
      {
        "name": "string",
        "value": "string"
      }
    ],
    "timestamp": "2018-04-27T01:00:44.758Z",
    "title": "string",
    "type": "string"
  }
]
```

We also support sending in custom checks to the API, but we have a separate dedicated page covering this topic.

## Request Header X-Netuitive-Api-Options
Options are sent to the Ingest API via HTTP Request Headers. The name of the request header is X-Netuitive-Api-Options and it takes a comma separated list of options.

```
curl -X POST -H "Content-Type: application/json" -H "X-Netuitive-Api-Options: SEND_RESPONSE_BODY,INJECT_TIMESTAMP" -d @- $endpoint*
Connected to localhost (::1) port 8000 (#0)
> POST /ingest/api0custom0100000000000000000101 HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.43.0
> Accept: */*
> Content-Type: application/json
> X-Netuitive-Api-Options: SEND_RESPONSE_BODY,INJECT_TIMESTAMP
> Content-Length: 859
```

The table below describes the implemented options.

| Option | Description |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SEND_RESPONSE_BODY | When present, the Ingest API sends a detailed “Success Response” body. See the sample Success Response below. When this option is not present, no response body is sent. A response body is always sent when there is an error. |
| INJECT_TIMESTAMP | When present, the Ingest API service injects the current server timestamp into the element sample’s “timestamp” property. This will overwrite any passed-in timestamps if they exist.Ws |

## Ingest Responses
There are two types (not including 500 errors) of responses returned from the Ingest API: 202 and 400.


### 202 : ACCEPTED
CloudWisdom has received the request and queued it for processing. This does not mean the Element will appear in CloudWisdom. The service is not validating if the timestamp sent to CloudWisdom is in a valid time range.


### 400 : BAD_REQUEST
CloudWisdom is not able to process the request due to some sort of error in the message:

- **Validation Error**: There was an error in validating the message. The error will be returned in the message.
- **Parsing Error**: There was an error parsing the message passed into CloudWisdom.

There are a few instances in which an error code is received:

- The timestamp is not properly formatted.
- The timestamp is properly formatted; however, it is not within a period of time that will be processed by CloudWisdom.
- Metrics or Samples have been sent without wrapping them in a valid Element consisting of an `Element.id`, `Metric.id`, and a `Sample.metricId`.

The responses delivered to the client have been standardized. Except for the case of a 500 error, the responses are the same minus one exception: the Error Response contains a field named “errors” that has an array of error messages.

{{% notice tip %}}
On a 202 : ACCEPTED response, the response body is only returned when the client requests it via the HTTP header option SEND_RESPONSE_BODY. On a 400 : BAD_REQUEST response, a response body is always returned. There is no option to turn this off.
{{% /notice %}}

### Success Response

```
{
"status": 202,
"message": "ACCEPTED",
"detail": "2 elements received",
"serverTimestamp": 1442604173135,
"iso8601DateTime": "2015-09-18T19:22:40.153Z"
}
```

### Validation Error: Missing Timestamp Without Passing ‘INJECT_TIMESTAMP’ Header

```
{
"status": 400,
"message": "BAD_REQUEST",
"detail": "Input Validation Failed",
"errors": [
"Missing required field on Sample, 'timestamp'. See ingest documentation to see how to send in samples without timestamps."
],
"serverTimestamp": 1442852458120,
"iso8601Dat
```

### JSON Parse Error: Bad Date format

```
{
"status": 400,
"message": "BAD_REQUEST",
"detail": "Error Parsing JSON Request",
"errors": [
"Could not read JSON: Can not construct instance of java.util.Date from String value 'ZZZZZZZZZZZZZZZZZ': not a valid representation (error: Failed to parse Date value 'ZZZZZZZZZZZZZZZZZ': Failed to parse date [\"ZZZZZZZZZZZZZZZZZ']: Invalid number: ZZZZZZZZZZZZZZZZZ)\n at [Source: org.apache.catalina.connector.CoyoteInputStream@8a57dbd; line: 1, column: 240] (through reference chain: java.util.ArrayList[0]->com.metricly.ingest.entity.IngestElement[\"samples\"]->java.util.HashSet[0]->com.metricly.ingest.entity.IngestSample[\"timestamp\"]); nested exception is com.fasterxml.jackson.databind.exc.InvalidFormatException: Can not construct instance of java.util.Date from String value 'ZZZZZZZZZZZZZZZZZ': not a valid representation (error: Failed to parse Date value 'ZZZZZZZZZZZZZZZZZ': Failed to parse date [\"ZZZZZZZZZZZZZZZZZ']: Invalid number: ZZZZZZZZZZZZZZZZZ)\n at [Source: org.apache.catalina.connector.CoyoteInputStream@8a57dbd; line: 1, column: 240] (through reference chain: java.util.ArrayList[0]->com.metricly.ingest.entity.IngestElement[\"samples\"]->java.util.HashSet[0]->com.metricly.ingest.entity.IngestSample[\"timestamp\"])"
],
"serverTimestamp": 1442844006245,
"iso8601DateTime": "2015-09-21T14:00:06.245Z"
```

## Example Scenario
You want to send 2 Elements to the CloudWisdom ingest endpoint: a server named **webhostABC**, and an instance of Tomcat 7 named **webappEFG**.

- **webhostABC**: You need to collect memory utilization and cpu utilization. You also need an attribute noting what datacenter the server is running in.
- **webappEFG**: You need to collect requests-per-second and connection-pool-count. You also need an attribute describing what webserver type the instance is running.

To implement the plan outlined above:

1. Array of Elements (JSON root)
  - **id**: Choose a unique (across your environment) ID for each of your elements.
  - **name**: The name will be displayed in the CloudWisdom UI.
  - **type**: This should describe the type of asset you are using (e.g., server, firewall, database, webserver, storage).
2. **Metrics**: define the metrics you want to capture for each element
  - **id**: The ID of the metric. This should uniquely identify it within the Element. CloudWisdom also uses this as the display name in the UI.
  - **name**: Currently the metric name is not used as the ID is used for the display name in the UI.
3. **Samples**:
  - **metricId**: This relates the sample to the metric.id.
  - **timestamp**: UTC time in milliseconds since the epoch.
  - **val**: The value for this sample.

### Example Payload
In the JSON request below, two Elements are passed whose IDs are **webhost01** and **webapp01**.

```
[
  {
    "id": "webhost01",
    "name": "Web Host 01",
    "type": "server",
    "metrics": [
      {
        "id": "memutilization",
        "name": "Memory Utilization %"
      },
      {
        "id": "cpuutilization",
        "name": "CPU Utilization %"
      }
    ],
    "samples": [
      {
        "metricId": "memutilization",
        "timestamp": 1441465330000,
        "val": 68.0
      },
      {
        "metricId": "cpuutilization",
        "timestamp": 1441465330000,
        "val": 14.0
      }
    ],
    "attributes": [
      {
        "name":"datacenter",
        "value": "aws-east-1a"
      }
    ]
  },
  {
    "id": "webapp01",
    "name": "Web App 01",
    "type": "webapp",
    "metrics": [
      {
        "id": "requestspersecond",
        "name": "Requests per second"
      },
      {
        "id": "connectionpoolcount",
        "name": "Connection Pool Count"
      }
    ],
    "samples": [
      {
        "metricId": "requestspersecond",
        "timestamp": 1441465330000,
        "val": 4.0
      },
      {
        "metricId": "connectionpoolcount",
        "timestamp": 1441465330000,
        "val": 40.0
      }
    ],
    "attributes": [
      {
        "name": "product",
        "value": "tomcat7"
      }
    ]
  }
]
```

## Frequently Asked Questions

### What is the endpoint to get to Ingest API?
Production: https://api.us.cloudwisdom.virtana.com/ingest/{API_KEY}

### What is an API Key, and how do I get one/find mine?
An API Key is generated by CloudWisdom for your account. You can retrieve any of your API Keys from the API Keys page under the Account Profile drop-down menu.


### What format do you require your timestamp to be in when sending samples?
Timestamps must be the number of milliseconds since the Unix Epoch. Now the stand date format on many Linux/Unix systems use seconds since the epoch and therefore require padding to be used. The following examples define ways to calculate the correct time in several circumstances:

- Unix/Linux/Mac OS X using the date command returns seconds, so additional padding is needed to get it to milliseconds.
  - **input**: date +%s000
  - **output**: 144147539000

- Java/Groovy contain the “`System.currentTimeMillis()`” method, which returns a properly formatted timestamp.
  - **input**: System.currentTimeMillis()
  - **output**: 1441475930587

### What are valid timestamps accepted by the Ingest API’s endpoint?

The following formats have been tested successfully:

- Unix epoch in milliseconds
  - 1441475739000
- ISO 8601 formats:
  - 2015-09-07T14:26:47.457-0400
  - 2015-09-07T14:26:47-0400
  - 2015-09-08T13:39:33.948Z

The following ISO 8601 formats do not work:

- 2015-09-07T14:26:47EDT

### Can I send more than one Element at a time?

Yes, the posted JSON message is always an array of Elements. See the sample payload below. It sends two Elements at a time.

### What is the metric name field used for?
Currently it is only used internally. In the future, we plan to use it in the UI similar to the Element name. Currently, the metric ID is also used for its name in the UI.

### What is the element name?
The element name is used as the display name in the UI.

### What client tools can I use to test sending data to the Ingest API endpoint?
- Command Line tools:
  - curl is the de facto command line tool that is available across most OSs. It is available on Linux/Unix/Mac OSs and available as a download on other OSs–including Windows–from the curl website. Examples below will use curl.

- OS Agnostic UI tools:
  - Advanced REST client Chrome app
  - Postman Chrome app

### What happens if the API detects unknown properties in a payload?
The API ignores unknown properties and allows the rest of the message to proceed if it is valid.


### Is it possible to create relationships between elements in the Ingest API’s endpoint?
Yes. Relationships can be added as an array of relations. Relationships can be uni- or bi-directional. CloudWisdom only creates the side of the relationship specified in the JSON payload.

{{% notice tip %}}
If you submit an element with `“id” = “webserver01”` that contained a relationship `“fqn”:”load-balancer-east”`, CloudWisdom would create a relationship from **webserver01** to **load-balancer-east**. It would not automatically create a relationship from **load-balander-east** to **webserver01**; however, you can add the inverse relationship to l**oad-balancer-east** via a separate API call.
{{% /notice %}}
