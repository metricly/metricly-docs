---
title: "Metrics API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---
The metrics API allows you access to your element’s metrics.

**Request Header**

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

## GET
### GET from /metrics
Returns a list of metrics that match given parameters.

**Parameters**
| Parameters | Required/Optional | Description |
|------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startTime | Required | Query parameter. The start of the window of time from which metrics will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Required | Query parameter. The end of the window of time from which metrics will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |

### GET from /metrics/fqns
Returns a list of fully qualified names (FQNS) for metrics matching given parameters.

| Parameters | Required/Optional | Description |
|------------------|-------------------|---------------------------------------------------------------------------------------------------------------------------|
| elementId | Optional | Query Parameter. The ID of the element. |
| elementFqn | Optional | Query Parameter. The fully qualified name (FQN) of the element. |
| elementName | Optional | Query Parameter. The friendly name of the element. |
| elementType | Optional | Query parameter. The type of the element (e.g. SERVER, EC2, etc.) |
| elementAttribute | Optional | Query parameter. An attribute associated with the element. elementAttribute={"foo":["one","two"], "bar":["three","four"]} |
| elementTag | Optional | Query parameter. The name of the tag on the element. elementTag={"foo":["one","two"], "bar":["three","four"]} |
| metricFqn | Optional | Query parameter. The fully qualified name (FQN) of the metric. |
| metricTag | Optional | Query parameter. The tag-value pair associated with the metric. metricTag={"foo":["one","two"], "bar":["three","four"]} |

### GET from /metrics/statistics
Returns metric data based on the parameters given.

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| fqn | Required | Query parameter. The unique FQN of the metric. |
| duration | Optional | Query parameter. Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. The duration parameter will take precedence over startTime and endTime if all attributes are included in your request. |
| startTime | Optional | Query parameter. The start of the window of time from which metric stats will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which metric stats will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |
| rollup | Optional | Query parameter. Select the data aggregation roll-up you wish to receive: ZERO (none), PT5M (past 5 minutes), PT1H (past 1 hour), or PT24H (past 24 hours). |
| showValues | Optional | Query parameter. Provides the values for the metric statistics (if set to true) or only displays zeroes for the statistics (if set to false). |

### GET from /metrics/statistics/aggregate
returns aggregate statistics for a metric.

**Parameters**

| Parameters | Required/Optional | Description |
|---------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| fqn | Required | Query parameter. The FQN of the metric. |
| duration | Optional | Query parameter. Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. |
| rollupInput | Optional | Query parameter. Select the data aggregation roll-up to specify: ZERO (none), PT5M (past 5 minutes), PT1H (past 1 hour), or PT24H (past 24 hours). |
| elementScopeWrapper | Required | Body parameter; see below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|--------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| attributes | Optional | The attributes associated with an element. Attributes contains several options: attributeType (optional) The type of attribute. Valid inputs are TEXT, BOOLEAN, BIGINT, DOUBLE, or TIMESTAMP. dataSourceId (optional) The ID of the integration that is associated with the attribute. id (optional) The ID for the attribute. name (optional) The name of the attribute. value (optional) The value of the attribute. |
| dataSourceId | Optional | The ID of the integration that associated with the given FQN. |
| endTime | Optional | The end of the window of time from which metric stats will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |
| fqnExcludes | Optional | The string of characters you’d like to exclude from element FQN matching. |
| fqnIncludes | Optional | The string of characters you’d like to include in element FQN matching. |
| ids | Optional | The ID(s) of the elements associated with the given metric FQN. |
| nameContains | Optional | The string of characters you’d like to exclude from element name matching. |
| nameExcludes | Optional | The string of characters you’d like to include in element name matching. |
| startTime | Optional | The start of the window of time from which metric stats will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| tags | Optional | The collectors associated with a particular integration. Collectors contains several attributes: attributeType (optional) The datasource ID for the datasource the collector is associated with. dataSourceId (optional) A comma-delimited list of element IDs that are associated with this collector. id (optional) The ID for the collector. name (optional) The name for the collector. value (optional) The name for the collector. |
| tenantId | Optional | The ID of the tenant the element is associated with. |
| types | Optional | The type of the element. Read more about element types here. |

### GET from /metrics/statistics
Returns descriptive statistics for a metric.

**Parameters**
| Parameters | Required/Optional | Description |
|---------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| fqn | Required | Query parameter. The FQN of the metric. |
| duration | Optional | Query parameter. Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. |
| rollupInput | Optional | Query parameter. Select the data aggregation roll-up to specify: ZERO (none), PT5M (past 5 minutes), PT1H (past 1 hour), or PT24H (past 24 hours). |
| elementScopeWrapper | Required | Body parameter; see below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|--------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| attributes | Optional | The attributes associated with an element. Attributes contains several options: attributeType (optional) The type of attribute. Valid inputs are TEXT, BOOLEAN, BIGINT, DOUBLE, or TIMESTAMP. dataSourceId (optional) The ID of the integration that is associated with the attribute. id (optional) The ID for the attribute. name (optional) The name of the attribute. value (optional) The value of the attribute. |
| dataSourceId | Optional | The ID of the integration that associated with the given FQN. |
| endTime | Optional | The end of the window of time from which metric stats will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |
| fqnExcludes | Optional | The string of characters you’d like to exclude from element FQN matching. |
| fqnIncludes | Optional | The string of characters you’d like to include in element FQN matching. |
| ids | Optional | The ID(s) of the elements associated with the given metric FQN. |
| nameContains | Optional | The string of characters you’d like to exclude from element name matching. |
| nameExcludes | Optional | The string of characters you’d like to include in element name matching. |
| startTime | Optional | The start of the window of time from which metric stats will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| tags | Optional | The collectors associated with a particular integration. Collectors contains several attributes: attributeType (optional) The datasource ID for the datasource the collector is associated with. dataSourceId (optional) A comma-delimited list of element IDs that are associated with this collector. id (optional) The ID for the collector. name (optional) The name for the collector. value (optional) The name for the collector. |
| tenantId | Optional | The ID of the tenant the element is associated with. |
| types | Optional | The type of the element. Read more about element types here. |

## Creating Metric Data
The ingest API allows you to send raw data to CloudWisdom. At least one integration must be set up in your CloudWisdom account to use the ingest endpoint. We recommend using the unique API key (found on the API keys page under the Account Profile drop-down menu) for the Custom integration automatically created for your account as your go-to for anything related to using our API.

To properly use the ingest endpoint, you should first understand the following concepts:

- **Elements**: Elements are the physical or logical components that CloudWisdom monitors. An element can be a physical entity, such as a server or network element, a virtual entity, such as a transaction, or a business entity, such as a company traded on the stock market. Elements are the base component that CloudWisdom uses to analyze metrics and determine the status of your environment. For more information about elements and the properties of elements, see Elements.
- **Metrics**: Metrics are quantifiable measurements whose values are monitored by CloudWisdom and used to assess the performance of an element. Metrics are always associated with one or more elements. Examples of metrics include CPU utilization, Network Bytes Per Second, and Response Time.
- **Attributes**: Attributes are pieces of metadata associated with elements and/or metrics. Attributes are usually received from an integration. For example, Amazon EBS elements have a variety of attributes, including size, region, createTime (the time stamp when the volume was created), and state.
- **Samples**: A sample is a raw data value that is delivered from an ingestion service (integration) to CloudWisdom.
- **Tags**: A tag is a key-value pair that is applied to an entity in CloudWisdom.
- **Relationships**: A uni- or bi-directional relationship between two elements.
## POST
### POST to /ingest/{apiId}
Creates a data sample for a given element.

Replace `{apiId}` in the above URL with the API key from your Custom integration. To access this key, click **Integrations** in the user account drop-down menu in the top right-hand corner of CloudWisdom, then find the CUSTOM integration and copy the API key from the API Key column.

| Parameters | Required/Optional | Description |
|------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ingestElements | Required | Body Parameter; see below |
| apiId | Required | URL (path) parameter; your API key. |
| X-Metricly-Api-Options | Optional | Header parameter. Two values you can include: The value SEND_RESPONSE_BODY if you desire a detailed “Success Response” body. The value INJECT_TIMESTAMP if you want the custom ingest service to inject the current server timestamp into the element sample’s “timestamp” property. |

**Request Body**

| Attribute | Required/Optional | Description |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| relations | Optional | Defines a relationship between two elements. It contains one attribute: fqn (optional) The FQN of the element you want to create a relationship with. |
| id | Required | The FQN of the element. The valid character regex for this field is[a-zA-Z0-9\\._-]. Spaces are replaced with _ and all other invalid characters are removed. |
| metrics | Required | The metrics attribute tells CloudWisdom which metric you’re passing data to. It contains several attributes: unit (optional) Arbitrary value used in the CloudWisdom UI for the metric’s unit of measure. sparseDataStrategy (optional) Defines the strategy for replacing missing data. See the sparseDataStrategy Explained section at the bottom of this guide for more information. id (required) The unique FQN of the metric (e.g., aws.ec2.cpucreditbalance, cpu.cpu1.guest_nice, diskspace.root.byte_free). The valid character regex for this field is[a-zA-Z0-9\\._-]. Spaces are replaced with _ and all other invalid characters are removed.type (optional) Currently only accepts the value “COUNTER” if the metric is a counter type. tags (optional) Used for filtering in CloudWisdom. In the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. name (optional) The text displayed as the name for the element in CloudWisdom. |
| samples | Required | "The samples attribute tells CloudWisdom what data to pass to the metric you defined in the metrics attribute. It contains three attributes that must be present. |
| Only one of the six sample inputs (min, max, avg, cnt, sum, val) are required, but val should not be sent with any of the others. Min/max/avg/cnt/sum are sent if aggregation is happening on the client side prior to sending the data to CloudWisdom. Val represents a raw observation of some type. To enable analytics, either send in val by itself or min, max, sum, avg (optional), and cnt. You will not get any bands if you send in min, max, sum, avg, or cnt by itself. max (see note) Maximum value of this metric sample. avg (see note) Average value of this metric sample. cnt (see note) Count of values of this metric sample. min (see note) Minimum value of this metric sample. sum (see note) Sum of values of this metric sample. metricId (required) Mapping to the ID field of the metric for this sample. timestamp (required) A number indicating the point in time at which the sample was collected. The timestamp must be either ISO 8601 formatted, or written as an epoch in milliseconds. Ensure that ISO 8601 formatted dates are quoted (see example). val (see note) The value of the metric." |  |  |
| attributes | Optional | The attributes attribute provides CloudWisdom with metadata about the element. You can pass in attributes the same way you would pass in tags: [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)] |
| type | Required | The type of element (e.g., server, database, etc.) used for filtering and applying policies in CloudWisdom. |
| location | Optional | The location of the element is used for filtering and display purposes in CloudWisdom. The location can reflect either the element’s physical location or business needs. |
| tags | Optional | Used for filtering in CloudWisdom. In the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. |
| name | Optional | The text displayed as the name for the element in CloudWisdom. |

## sparseDataStrategy Explained
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
