---
title: "Policies API"
draft: false
categories:
tags: ["#api", "#policy", "#mute", "#disable"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---
The policies API lets you access and manage your policies.  

**Request Header**

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

## POST
### POST to /policies
Creates a policy under your tenant.

**Parameters**

| Parameters | Required/Optional | Description |
|---------------|-------------------|---------------------------|
| policyWrapper | Required | Body parameter; see below |

**Body Attributes**

| Attribute | Required/Optional | Description |
|---------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| policyWrapper | Required | The policyWrapper attribute provides CloudWisdom with the data necessary to create a policy. It contains several attributes: actions (optional) The desired actions for the policy. conditions (optional) The desired conditions for the policy. See Conditions for help with formatting. event conditions (optional) The desired event conditions for the policy. See Conditions for help with formatting. creatorEmail (optional) The email of the person who created the policy. deleted (optional) Whether the policy has been deleted or not. description (optional) Arbitrary description text for the policy. duration (optional) The duration of this policy. enabled (optional) Whether this policy is enabled or not. id (optional) The unique ID for the policy. lastUpdated (optional) The last time the policy was updated. name (optional) The name of the policy. originPolicyId (optional) The Policy ID from which this policy originates. originTenantId (optional) The Tenant ID from which this policy originates. scope (optional) Consists of several additional attributes: elementName (optional), which provides the name of the element. elementNameExclude (optional), which provides a string of characters to not match element names. elementTags (optional), which provides any tags on the element in the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. elementType (optional), which provides the type of element. fqnExcludes (optional), which provides a string of characters to not match FQNs. fqnIncludes (optional), which provides a string of characters to match FQNs. |

```
{
  "policy": {
    "name": "API Test: AWS EC2 - Elevated CPU Activity (Normal Network Activity)",
    "description": "Increases in CPU activity are not uncommon when there is a rise in network activity. Increased traffic to a server means more work for that server to do. This policy is designed to catch cases where CPU activity is higher than than normal, and said behavior cannot be explained by a corresponding increase in network traffic. It may or may not represent a problem, but it is useful to know about.  This policy will not raise an event if CPU is under 20%.",
    "scope": {
      "elementName": null,
      "elementNameExclude": null,
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
    "duration": 1800,
    "conditions": [
      {
        "metric": "aws.ec2.cpuutilization",
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
        "metric": "aws.ec2.cpuutilization",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "contextualDeviation",
        "operator": ">",
        "level": null,
        "level2": null,
        "metricThresholdLevel": null,
        "metricThresholdAnalytic": null
      },
      {
        "metric": "aws.ec2.cpuutilization",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "actual",
        "operator": ">=",
        "level": 20,
        "level2": null,
        "metricThresholdLevel": null,
        "metricThresholdAnalytic": null
      },
      {
        "metric": "aws.ec2.bytesinpersec",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "baselineDeviation",
        "operator": "undefined",
        "level": null,
        "level2": null,
        "metricThresholdLevel": null,
        "metricThresholdAnalytic": null
      },
      {
        "metric": "aws.ec2.bytesinpersec",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "contextualDeviation",
        "operator": "undefined",
        "level": null,
        "level2": null,
        "metricThresholdLevel": null,
        "metricThresholdAnalytic": null
      },
      {
        "metric": "aws.ec2.bytesoutpersec",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "baselineDeviation",
        "operator": "undefined",
        "level": null,
        "level2": null,
        "metricThresholdLevel": null,
        "metricThresholdAnalytic": null
      },
      {
        "metric": "aws.ec2.bytesoutpersec",
        "wildcard": null,
        "metricScopeTags": {},
        "analytic": "contextualDeviation",
        "operator": "undefined",
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
    "enabled": true
  }
}
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "policy": { \
     "name": "API Test: AWS EC2 - Elevated CPU Activity (Normal Network Activity)", \
     "description": "Increases in CPU activity are not uncommon when there is a rise in network activity. Increased traffic to a server means more work for that server to do. This policy is designed to catch cases where CPU activity is higher than than normal, and said behavior cannot be explained by a corresponding increase in network traffic. It may or may not represent a problem, but it is useful to know about.  This policy will not raise an event if CPU is under 20%.", \
     "scope": { \
       "elementName": null, \
       "elementNameExclude": null, \
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
     "duration": 1800, \
     "conditions": [ \
       { \
         "metric": "aws.ec2.cpuutilization", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "baselineDeviation", \
         "operator": ">", \
         "level": null, \
         "level2": null, \
         "metricThresholdLevel": null, \
         "metricThresholdAnalytic": null \
       }, \
       { \
         "metric": "aws.ec2.cpuutilization", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "contextualDeviation", \
         "operator": ">", \
         "level": null, \
         "level2": null, \
         "metricThresholdLevel": null, \
         "metricThresholdAnalytic": null \
       }, \
       { \
         "metric": "aws.ec2.cpuutilization", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "actual", \
         "operator": ">=", \
         "level": 20, \
         "level2": null, \
         "metricThresholdLevel": null, \
         "metricThresholdAnalytic": null \
       }, \
       { \
         "metric": "aws.ec2.bytesinpersec", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "baselineDeviation", \
         "operator": "undefined", \
         "level": null, \
         "level2": null, \
         "metricThresholdLevel": null, \
         "metricThresholdAnalytic": null \
       }, \
       { \
         "metric": "aws.ec2.bytesinpersec", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "contextualDeviation", \
         "operator": "undefined", \
         "level": null, \
         "level2": null, \
         "metricThresholdLevel": null, \
         "metricThresholdAnalytic": null \
       }, \
       { \
         "metric": "aws.ec2.bytesoutpersec", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "baselineDeviation", \
         "operator": "undefined", \
         "level": null, \
         "level2": null, \
         "metricThresholdLevel": null, \
         "metricThresholdAnalytic": null \
       }, \
       { \
         "metric": "aws.ec2.bytesoutpersec", \
         "wildcard": null, \
         "metricScopeTags": {}, \
         "analytic": "contextualDeviation", \
         "operator": "undefined", \
         "level": null, \
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
       } \
     ], \
```

## GET

### GET from /policies/{policyId}
Returns a given policy. Replace `{policyId}` in the above URL with a policy ID from any of your policies.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|---------------------------------------|
| policyId | Required | URL (path) parameter. Your policy ID. |

### GET from /policies
Returns a list of policies created for the tenant you are authenticated for.

### GET from /policies/elements
Returns the number of elements associated with a policy ID.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| duration | Optional | Query parameter. Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. The duration parameter will take precedence over startTime and endTime if all attributes are included in your request. |
| startTime | Optional | Query parameter. The start of the window of time from which policies will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which policies will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |

### GET from /policies/events
Returns the number of events occurred for a policy.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| duration | Optional | Query parameter. Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. The duration parameter will take precedence over startTime and endTime if all attributes are included in your request. |
| startTime | Optional | Query parameter. The start of the window of time from which policies will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which policies will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |

### GET from /policies/{policyid}/events
Returns a list of events generated by the specified policy.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| duration | Optional | Query parameter. Gives CloudWisdom an ISO 8601-formatted duration time frame to retrieve data. The duration ends at the current time and begins anytime in the past two weeks. The duration parameter will take precedence over startTime and endTime if all attributes are included in your request. |
| startTime | Optional | Query parameter. The start of the window of time from which policies will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which policies will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |

## PUT
### PUT to /policies/{policyId}
Updates a given policy. Replace `{policyId}` in the above URL with a policy ID from any of your policies.

**Parameters**

| Parameters | Required/Optional | Description |
|---------------|-------------------|---------------------------------------|
| policyId | Required | URL (path) parameter. Your policy ID. |
| policyWrapper | Required | Body parameter; see below |

**Body Attributes**

| Attribute | Required/Optional | Description |
|---------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| policyWrapper | Required | The policyWrapper attribute provides CloudWisdom with the data necessary to create a policy. It contains several attributes: actions (optional) The desired actions for the policy. conditions (optional) The desired conditions for the policy. See Conditions for help with formatting. event conditions (optional) The desired event conditions for the policy. See Conditions for help with formatting. creatorEmail (optional) The email of the person who created the policy. deleted (optional) Whether the policy has been deleted or not. description (optional) Arbitrary description text for the policy. duration (optional) The duration of this policy. enabled (optional) Whether this policy is enabled or not. id (optional) The unique ID for the policy. lastUpdated (optional) The last time the policy was updated. name (optional) The name of the policy. originPolicyId (optional) The Policy ID from which this policy originates. originTenantId (optional) The Tenant ID from which this policy originates. scope (optional) Consists of several additional attributes: elementName (optional), which provides the name of the element. elementNameExclude (optional), which provides a string of characters to not match element names. elementTags (optional), which provides any tags on the element in the format of [{“name”:”key1″, “value”:”value1″}, {“name”:”key2″, “value”:”value2″}, (etc.)]. elementType (optional), which provides the type of element. fqnExcludes (optional), which provides a string of characters to not match FQNs. fqnIncludes (optional), which provides a string of characters to match FQNs. |

## DELETE
### DELETE from /policies/{policyId}
Replace `{policyId}` in the above URL with a policy ID from any of your policies.

| Parameters | Required/Optional | Description |
|------------|-------------------|---------------------------------------|
| policyId | Required | URL (path) parameter. Your policy ID. |

## Other Actions

You can use the [Metricly CLI][1] or interact directly with the CloudWisdom API to manipulate policies. A common need from some of our users is to temporarily disable their policies while building, testing, or modifying them. This short guide walks you through how to do that via the Policy API directly.

### Disable a Policy

**Get Policy ID**

1. In CloudWisdom, navigate to the policy you want to edit.
2. Copy the policy’s ID from the url.
![policy-id](/images/api-policies/policy_id.png)

**Get & Put the Policy Document via Swagger**

1. GET from `/policies/getPolicyUsingGET`
  ```
  {
  "policy": {
    "id": "12345a123-ab12-12345-bc12-23456a78",
    "name": "RabbitMQ: Messages in the dead letter queues",
    "description": "RabbitMQ: Messages in the dead letter queues",
    "scope": {
      "elementName": null,
      "elementNameExclude": null,
      "fqnIncludes": [
        "RabbitMQ-Prod-001"
      ],
      "fqnExcludes": [

      ],
      "elementType": null,
      "elementTypes": [

      ],
      "elementTags": [

      ],
      "elementTagsAll": true,
      "excludedElementTags": [

      ],
      "elementAttributes": [

      ],
      "elementAttributesAll": true,
      "excludedElementAttributes": [

      ]
    },
    "duration": 300,
    "conditions": [
      {
        "metric": null,
        "wildcard": "rabbitmq.queues.*(_dl|_dlq).messages",
        "metricScopeTags": {

        },
        "analytic": "actual",
        "operator": ">",
        "level": 1,
        "level2": null,
        "metricThresholdLevel": null,
        "metricThresholdAnalytic": null
      }
    ],
    "eventConditions": [

    ],
    "checkCondition": null,
    "actions": [
      {
        "type": "event",
        "category": 3
      },
      {
        "type": "notification",
        "id": 12345,
        "enabled": true,
        "notifyFrequencyMin": 1234,
        "sendOnClear": true
      }
    ],
    "enabled": true,
    "deleted": false,
    "creatorEmail": "user.name@username.com",
    "lastUpdated": "2018-06-01T20:32:05Z"
  }
}
  ```
2. Change `"enabled": true`, to `"enabled": false` in the policy document.
3. PUT to `/policies/updatePolicyUsingPUT`.

**Done!**

You can repeat section 2 to re-enable your policy.


### Mute a Policy

**Get Policy ID**

1. In CloudWisdom, navigate to the policy you want to mute.
2. Copy the policy’s ID from the url.
![policy-id](/images/api-policies/policy_id.png)

**POST the Mute Order to the API**

1. Use this cURL template:

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: */*' --header 'Authorization: Basic {YOUR_BASE64_ENCODED_CREDS}' 'https://us.cloudwisdom.virtana.com/policies/{policyId}/mute/{muteMs}'
```
2. Insert the **policy ID** into the template at `####policy-ID-here####`
3. POST to `/policies/{policyId}/mute/{muteMs}`

The policy stays muted for the millisecond duration given.

{{% notice tip %}}
The Request URL is the same policy URL from the cURL sample.
{{% /notice %}}

**To Delete a Mute Order:**

DELETE from `/policies/{policyId}/mute` with the following cURL:

```
curl -X DELETE --header 'Accept: */*' 'https://us.cloudwisdom.virtana.com/policies/####policy-ID-here####/mute'
```


[1]: /api/api-cli
