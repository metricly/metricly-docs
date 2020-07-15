---
title: "Ingest API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

The ingest API allows you to send raw data to CloudWisdom. At least one integration must be set up in your CloudWisdom account to use the ingest endpoint. We recommend using the unique API key (found on the API keys page under the Account Profile drop-down menu) for the Custom integration automatically created for your account as your go-to for anything related to using our API.

This API is used to send CloudWisdom custom data. Two types of custom payloads can be created with this API:

- Custom elements
- Custom external event messages

## Prerequisites  

To properly use the ingest endpoint, you should first understand the following concepts:

- **Elements**: Elements are the physical or logical components that CloudWisdom monitors. An element can be a physical entity, such as a server or network element, a virtual entity, such as a transaction, or a business entity, such as a company traded on the stock market. Elements are the base component that CloudWisdom uses to analyze metrics and determine the status of your environment.
- **Metrics**: Metrics are quantifiable measurements whose values are monitored by CloudWisdom and used to assess the performance of an element. Metrics are always associated with one or more elements. Examples of metrics include CPU utilization, Network Bytes Per Second, and Response Time.
- **Attributes**: Attributes are pieces of metadata associated with elements and/or metrics. Attributes are usually received from an integration. For example, Amazon EBS elements have a variety of attributes, including size, region, createTime (the time stamp when the volume was created), and state.
- **Samples**: A sample is a raw data value that is delivered from an ingestion service (integration) to CloudWisdom.
- **Tags**: A tag is a key-value pair that is applied to an entity in CloudWisdom.
- **Relationships**: A uni- or bi-directional relationship between two elements.


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
### Request Body

| Attribute | Required/Optional | Description |
|--------------------------------------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| relations | Optional | Defines a relationship between two elements. It contains one attribute: fqn (optional) The FQN of the element you want to create a relationship with. |
| id | Required | The FQN of the element. The valid character regex for this field is[a-zA-Z0-9\\._-]. Spaces are replaced with _ and all other invalid characters are removed. |
| metrics | Required | Tells CloudWisdom which metric you are passing data to. See the Metric Attributes section for more details. |
| samples | Required | Tells CloudWisdom what data to pass to the metric you defined in the metrics attribute.  Only one of the six sample inputsare required.  Min/max/avg/cnt/sum are sent if aggregation is happening on the client side prior to sending the data to CloudWisdom. Val represents a raw observation of some type. To enable analytics, either send in val by itself or min, max, sum, avg, and cnt. You will not get any bands if you send in min, max, sum, avg, or cnt by itself. See the Sample Attributes section for more details. |  |  |
| attributes | Optional | The attributes attribute provides CloudWisdom with metadata about the element. You can pass in attributes the same way you would pass in tags: [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)] |
| type | Required | The type of element (e.g., server, database, etc.) used for filtering and applying policies in CloudWisdom. |
| location | Optional | The location of the element is used for filtering and display purposes in CloudWisdom. The location can reflect either the element’s physical location or business needs. |
| tags | Optional | Used for filtering in CloudWisdom. In the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. |
| name | Optional | The text displayed as the name for the element in CloudWisdom. |

#### Metric Attributes
- **id** (required): The unique FQN of the metric (e.g., aws.ec2.cpucreditbalance, cpu.cpu1.guest_nice, diskspace.root.bytefree). The valid character regex for this field is[a-zA-Z0-9\.-]. Spaces are replaced with _ and all other invalid characters are removed.
- **unit** (optional: Arbitrary value used in the CloudWisdom UI for the metric’s unit of measure.
- **sparseDataStrategy** (optional): Defines the strategy for replacing missing data. See the sparseDataStrategy Explained section at the bottom of this guide for more information.
- **type** (optional): Currently only accepts the value “COUNTER” if the metric is a counter type.
- **tags** (optional): Used for filtering in CloudWisdom. In the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. name (optional) The text displayed as the name for the element in CloudWisdom.

#### Sample Attributes

- **metricId** (required): Mapping to the ID field of the metric for this sample.
- **timestamp** (required): A number indicating the point in time at which the sample was collected. The timestamp must be either ISO 8601 formatted, or written as an epoch in milliseconds. Ensure that ISO 8601 formatted dates are quoted.
- **max** (optional):  Maximum value of this metric sample.
- **avg** (optional):  Average value of this metric sample.
- **cnt** (optional):  Count of values of this metric sample.
- **min** (optional):  Minimum value of this metric sample.
- **sum** (optional):  Sum of values of this metric sample.
- **val** (optional): The value of the metric; should NOT be sent with other sample inputs.


### Custom External Event Messages
**POST request**: `https://api.us.cloudwisdom.virtana.com/ingest/events/{apiId}`

```
[
  {
    "data": {
      "elementId": "element-fqn",
      "message": "My message"
      },
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

Please note that the `elementId` is a required attribute. Payloads without `elementId` will be silently discarded. 

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
| INJECT_TIMESTAMP | When present, the Ingest API service injects the current server timestamp into the element sample’s “timestamp” property. This will overwrite any passed-in timestamps if they exist. |

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

## Supported Units

The following tables list all accepted metric units and their corresponding code.

### General

| Code | Unit |
|-------------|-------------------|
| short | short |
| percent | percent (0-100) |
| percentunit | percent (0.0-1.0) |
| humidity | Humidity (%H) |
| ppm | ppm |
| dB | decibel |

### Data

| Code | Unit |
|---------|----------------|
| bits | bits |
| bytes | bytes (base2) |
| bytesd | bytes (base10) |
| kbytes | kilobytes |
| kibytes | kibibytes |
| mbytes | megabytes |
| mibytes | mebibytes |
| gbytes | gigabytes |
| gibytes | gibibytes |

### Data rate

| Code | Unit |
|------|---------------|
| pps | packets/sec |
| bps | bits/sec |
| Bps | bytes/sec |
| kBps | kilobytes/sec |
| mBps | megabytes/sec |
| gBps | gigabytes/sec |

### Time

| Code | Unit |
|-------|-------------------|
| hertz | Hertz (1/s) |
| ns | nanoseconds (ns) |
| µs | microseconds (µs) |
| ms | milliseconds (ms) |
| s | seconds (s) |
| m | minutes (m) |
| hours | (h) |
| d | days (d) |

### Throughput

| Code | Unit |
|------|-------------------|
| ops | ops/sec (ops) |
| rps | reads/sec (rps) |
| wps | writes/sec (wps) |
| iops | I/O ops/sec (iops |

### Memory

| Code | Unit |
|------|------------------|
| fps | faults/sec (fps) |
| Pps | pages/sec (Pps) |

### Currency

| Code | Unit |
|-------------|-------------|
| currencyUSD | Dollars ($) |
| currencyGBP | Pounds (£) |
| currencyEUR | Euro (€) |
| currencyJPY | Yen (¥) |

### Length

| Code | Unit |
|----------|-----------------|
| lengthmm | millimetre (mm) |
| lengthm | meter (m) |
| lengthkm | kilometer (km) |
| lengthmi | mile (mi) |

### Velocity

| Code | Unit |
|--------------|----------|
| velocityms | m/s |
| velocitykmh | km/h |
| velocitymph | mph |
| velocityknot | knot (kn |

### Volume

| Code | Unit |
|--------|-------------|
| mlitre | millilitre |
| litre | litre |
| m3 | cubic metre |

### Energy

| Code | Unit |
|--------|---------------------|
| watt | watt (W) |
| kwatt | kilowatt (kW) |
| watth | watt-hour (Wh) |
| kwatth | kilowatt-hour (kWh) |
| joule | joule (J) |
| ev | electron volt (eV) |
| amp | Ampere (A) |
| volt | Volt (V) |

### Temperature

| Code | Unit |
|-----------|----------------|
| celsius | Celcius (°C) |
| farenheit | Farenheit (°F) |
| kelvin | Kelvin (K) |

### Pressure

| Code | Unit |
|--------------|-------------------|
| pressurembar | Millibars |
| pressurehpa | Hectopascals |
| pressurehg | Inches of mercury |
| pressurepsi | PSI |

---

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

### What is the sparseDataStrategy property?
Metrics marked as Sparse (with any strategy other than None) that do not receive any samples during the current cycle will get actual and sparseValue data injected for that cycle.

There are 5 sparse strategies:

- **None**: does as you would expect, nothing.  This is the default setting.
- **ReplaceWithZero**: will inject a value of 0.
- **ReplaceWithHistoricalMax**: injects the maximum Actual value recorded for the life of this metric.
- **ReplaceWithHistoricalMin**: injects the minimum Actual value recorded for the life of this metric.
- **ReplaceWithLast**: injects the last Actual value recorded for this metric.

There are two ways to set the Sparse Data Strategy for a metric.  The first is to send the strategy via the ingest process as Metric Metadata.  The second is using packages.

```
[{
  "match": "metric0",
  "properties": {
    "sparseDataStrategy": "None"
  }
},{
  "match": "metric1",
  "properties": {
    "sparseDataStrategy": "ReplaceWithHistoricalMax"
  }
}, {
  "match": "metric2",
  "properties": {
    "sparseDataStrategy": "ReplaceWithHistoricalMin"
  }
}, {
  "match": "metric3",
  "properties": {
    "sparseDataStrategy": "ReplaceWithLast"
  }
}, {
  "match": "metric4",
  "properties": {
    "sparseDataStrategy": "ReplaceWithZero"
  }
}]

```
### Are there any rate limits on the Ingest API endpoint?
There are no hard limits, but excessive amounts of data can cause your API key to get throttled and some payloads to get discarded. We recommend a volume of no more than 10 payloads per element per minute.
