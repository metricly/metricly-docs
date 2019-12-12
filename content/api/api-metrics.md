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

See the [Ingest API][1] for details on how to send raw data to CloudWisdom.

[1]: /api/api-ingest/
