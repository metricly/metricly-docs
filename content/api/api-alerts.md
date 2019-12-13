---
title: "Alerts API"
draft: false
categories:
tags: ["#api", "#alerts"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

[Alerts][1] group anomalous behavior and are informed by multi-conditional policies you select or build in CloudWisdom. Through the Alerts API, you can:

- Get a list of alerts, filterable by properties
- Close an alert via ID
- Get an alert via ID

## Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| policyId | Query | String | Each alert is tied to a policy. The policyID can be found in the URL, such as https://app.metricly.com/#/alerts/fda75bec-b25a-4e7f-b714-64ceb0976f2c?tab=all |
| elementId | Query | String | An alert's scope can be one or many elements; use the elementID to filter results. |
| elementName | Query | String | An alert's scope can be one or many elements; use the elementName to filter results. |
| startDate | Query | Date-Time | The first moment the policy conditions were met; YYYY-MM-DDTHH:MM:SSZ |
| endDate | Query | Date-Time | The last moment the policy conditions were met; YYYY-MM-DDTHH:MM:SSZ |
| isClosed | Query | Boolean | When the alert was closed by a user; YYYY-MM-DDTHH:MM:SSZ |
| limit | Query | Integer | Query return limit. |
| offset | Query | Integer | Number of alerts skipped in the query. |
| incidentId | Path | String | Used to DELETE or close alerts; found in response body of alert queries. |

## GET an Alerts List from /incidents

Use alert parameter values to filter results and get a list of exactly what you need.

**Request URL:** `https://app.metricly.com/incidents`

**CURL:**

The following example uses the **policyID** and **limit** parameters:

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/incidents?policyId=fe1bd11b-111f-111e-9982-d898aebda30f&limit=10'
```

The following example adds the **elementName** and **isClosed** parameters to the same query:

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/incidents?policyId=fe1bd11b-111f-111e-9982-d898aebda30f&elementName=stash&isClosed=true&limit=10'
```

**Response Body:**

```
{
  "incidents": [
    {
      "incidentId": "11a1d111-1e11-1fe1-b1e1-1fe1db1111",
      "tenantId": "1fa1111a-1b11-1111-ad11-11e1c1af11f1",
      "policyId": "fe1bd11b-111f-111e-1111-d111aebda111",
      "elementId": "1111111-1111-111f-adbe-11c11111bd11",
      "elementName": "vpn11-usw1a (11.11.11.1)",
      "tsFirstFired": "2019-12-12T20:10:00Z",
      "tsLastFired": "2019-12-12T22:45:00Z",
      "tsStarted": null,
      "tsAcked": null,
      "tsClosed": "2019-12-12T22:56:01Z",
      "eventIds": [
        "1fada100-a11d-111a-bfda-11111aff111c",
        "011ad11a-da11-1ca1-b111-e00a5d1111ef",
        "011111d9-05d8-1111-acb5-9a7a2b3d38d4",
        "064f62d6-c86a-111e-b179-562149c25579",
        "01111f11-bc4d-1111-a42b-a985e611111f",
        "2efab5fd-3397-111b-81c7-dcb1b2db35f0",
        "3d5a5b64-2b95-1deb-b86f-7f30556dfcc6",
        "40386550-cc3d-111b-9614-89c2e7d36dac",
        "29c202cc-d742-1e3c-ac7d-0111cda00bc5",
        "111d3202-e174-111a-8fb0-b5c23a4f6a46"
      ],
      "violatingMetricFqns": [
        "aws.ec2.cpuutilization"
      ],
      "closed": true,
      "acked": false
    }
  ]
}
```
---

## DELETE an Alert from /incidents/{id}

You can close out an alert using the **incidentId** found in the response body of an alert query.

**Request URL:** `https://app.metricly.com/incidents/{id-value-here}`

**CURL:**

```
curl -X DELETE --header 'Accept: */*' 'https://app.metricly.com/incidents/11a1d1117-1e01-1fe1-b1e0-1fe1db111111'

```
---

## Get an Alert from /incidents/{id}

You can use an **incidentId** to pull all information about an alert, such as violating metrics, specific events, elements affected, and start/stop timestamps. The incidentId can be found by querying for a list of alerts.

**Request URL:** `https://app.metricly.com/incidents/{id-value-here}`

**CURL:**

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/incidents/11a1d111-1e01-1fe1-b1e0-1fe1db111111'
```

**Response Body:**

```
{
  "incident": {
    "incidentId": "11a1d111-1e01-1fe1-b1e0-1fe1db111101",
    "tenantId": "0fa1111a-1b11-1111-ad11-11e1c1af11f1",
    "policyId": "fe1bd11b-111f-101e-1111-d111aebda11f",
    "elementId": "1111111-1111-1111f-adbe-11c11111bd40",
    "elementName": "vpn11-usw1a (11.11.11.1)",
    "tsFirstFired": "2019-12-12T20:10:00Z",
    "tsLastFired": "2019-12-12T22:45:00Z",
    "tsStarted": null,
    "tsAcked": null,
    "tsClosed": "2019-12-13T01:20:26Z",
    "eventIds": [
      "1aff7da1-c11c-111a-1a1f11f3111111c6d",
      "1aff7da1-c11c-111a-1a1f11f3222222c6d",
      "1aff7da1-c11c-111a-1a1f11f3333333c6d",
      "1aff7da1-c11c-111a-1a1f11f3444444c6d",
      "1aff7da1-c11c-111a-1a1f11f5555555c6d",
      "1aff7da1-c11c-111a-1a1f11f6666666c6d",
      "1aff7da1-c11c-111a-1a1f11f77777777c6d",
      "1aff7da1-c11c-111a-1a1f11f88888888c6d",
      "1aff7da1-c11c-111a-1a1f11f99999999c6d",
      "1aff7da1-c11c-111a-1a1f11f3111111c6d",
      "c883dbb5-b356-4f01-8241-4bc1111111111"
    ],
    "violatingMetricFqns": [
      "aws.ec2.cpuutilization"
    ],
    "acked": false,
    "closed": true
  }
}
```


[1]: /capacity-monitoring/alerts-page
