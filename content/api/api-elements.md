---
title: "Elements API"
draft: false
categories:
tags: ["#api", "#elements"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---
**Request Header**

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

## GET

### GET Element by ID from /elements/{id}
This method returns a specified element’s information.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------|
| id | Required | URL (path) parameter. The ID of the element. |


### Get Element IDs from /elements/ids
This method returns a list of element IDs for elements seen within a given timeframe.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startTime | Optional | Query parameter. The start of the window of time from which elements will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which elements will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |


### GET Element List from /elements
This method returns a list of elements filtered by any parameters you pass into the method call.


**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id | Optional | Query parameter. The FQN of the element(s). |
| name | Optional | Query parameter. The name of the element. |
| type | Optional | Query parameter. The type of element. |
| location | Optional | Query parameter. The location of the element is used for filtering and display purposes in CloudWisdom. The location can reflect either the element’s physical location or business needs. |
| tags | Optional | Query parameter. The name of the tag. |
| startTime | Optional | Query parameter. The start of the window of time from which elements will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which elements will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |
| state | Optional | Query parameter. The state of the element reflected by the metricly.metrics.collected.percent metric. False means no metrics are being collected; True means any number of metrics are being collected. |


### GET Metric Metadata from /elements/{elementid}/metrics
This method returns a list of metadata for a metric.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-----------------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |
| metricFQN | Optional | Query parameter. The metric’s fully qualified name. |

### GET Metric Results For an Element from /elements/{elementid}/metrics/{metricid}/samples

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startTime | Optional | Query parameter. The start of the window of time from which metric results will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| rollup | Optional | Query parameter. Select the data aggregation roll-up you wish to receive: ZERO (none), PT5M (past 5 minutes), PT1H (past 1 hour), or PT24H (past 24 hours). |
| metricId | Required | URL (path) parameter. The ID of the metric associated with the element. |
| endTime | Optional | Query parameter. The end of the window of time from which metric results will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |
| elementId | Required | URL (path) parameter. The ID of the element. |
| duration | Optional | Query parameter. Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. The duration parameter will take precedence over startTime and endTime if all attributes are included in your request. |

### GET Element's Metric Tags from /elements/{elementId}/metrics/{metricId}/tags
This method returns a list of tags for a given metric associated with a given element.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |
| metricId | Required | URL (path) parameter. The ID of the metric associated with the element. |


### GET Element's Associated Policies from /elements/{elementId}/policies
This method returns a list of policies associated with a given element.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |

### GET Element's tags from /elements/{elementId}/tags
This method returns a list of tags for a given element.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |

### GET Element Relationships from /elements/{id}/relationships
This method returns a list elements that are related to the given element.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the element. |
| levels | Optional | The number of levels of relationships returned, e.g., 2 would return an element related to a listed element related to the given element. |
| startTime | Optional | Query parameter. The start of the window of time from which elements will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which elements will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |

## DELETE

### DELETE a Metric Tag for an Element from /elements/{elementId}/metrics/{metricId}/tags/{tag}
This method deletes a specified tag for a given metric associated with a given element.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |
| metricId | Required | URL (path) parameter. The ID of the metric associated with the element. |
| tag | Required | URL (path) parameter. The name of the tag associated with the metric. |

### DELETE an Element from /elements/{id}
This method deletes a specified element.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------|
| id | Required | URL (path) parameter. The ID of the element. |

## POST

### POST Metric Tag for Element to /elements/{elementId}/metrics/{metricId}/tags

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |
| metricId | Required | URL (path) parameter. The ID of the metric associated with the element. |
| tagWrapper | Optional | Body parameter. See below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| tagWrapper | Optional | Tags used for filtering in CloudWisdom. In the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. |


### POST Element Name Preview to /elements/name/preview
This method returns a name preview for an element using the given template.

**Parameters**

| Parameters | Required/Optional | Description |
|-----------------|-------------------|----------------------------|
| elementTemplate | Required | Body parameter; see below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|-----------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| elementTemplate | Required | Template for creating a custom element display name. It contains two attributes: elementId (optional) The ID of the element you want to create a custom display name for. template (optional) The template used to parse your element name. |

### POST Tag for an Element to /elements/{elementId}/tags
This method creates a tag for a given element.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |
| tagWrapper | Required | Body parameter. See below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| tagWrapper | Required | Tags used for filtering in CloudWisdom. In the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. |

## PUT

### PUT Update a Metric Tag for an Element to /elements/{elementId}/metrics/{metricId}/tags/{tagName}

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------------------------------------|
| elementId | Required | URL (path) parameter. The ID of the element. |
| metricId | Required | URL (path) parameter. The ID of the metric associated with the element. |
| tagName | Required | URL (path) parameter. The name of the tag associated with the metric. |
| tagWrapper | Required | Body parameter. See below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|-----------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| elementTemplate | Required | Template for creating a custom element display name. It contains two attributes: elementId (optional) The ID of the element you want to create a custom display name for. template (optional) The template used to parse your element name. |
