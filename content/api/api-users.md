---
title: "Users API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---



## About the Users API

CloudWisdom's Users API can be used to --- . You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/users) and by clicking the interactive buttons below.


## GET from /users
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/users/listUsersUsingGET" >}} GET {{< /button >}} Use this endpoint to get a list of all users.

{{% expand "View method details."%}}


### Request URL

 `https://app.metricly.com/users`

### CURL

The following example only requires the Request URL to get a list of users.
```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/users'
```

### Response Body

The following Response Body includes only one user. Notice their **role** is set to `Administrator`.

```
{
  "users": [
    {
      "id": 12345,
      "email": "example@yahoo.com",
      "realUser": null,
      "active": true,
      "properties": {
        "arrangeChartsSetting": "grid",
        "seenEventsGraphTooltip": "false",
        "seenNewUserPromo": "false",
        "dailyReportEnabled": "true",
        "seenMetricsChartTooltip": "false",
        "createdDashboard": "false",
        "landingPage": "inventory",
        "seenWidgetLibraryFilterTooltip": "false",
        "timeZone": "UTC",
        "fullName": "Bob Burger",
        "seenIntegrationsTooltip": "false",
        "chartHeight": "xsmall",
        "ebscostTable": "[]",
        "seenMetricsFilterTooltip": "false",
        "inventoryTable": "[]",
        "chartWidth": "tall",
        "seenDashboardsPromo": "false",
        "phone": "phone",
        "theme": "light",
        "seenNewEC2CostPromo": "false",
        "metricsViewSetting": "tree"
      },
      "tenantProperties": {
        "netuitiveAccountId": "765432134567",
        "tenantType": "CUSTOMER",
        "tenantStatus": "ACTIVE",
        "productIds": [
          "monitoring",
          "cost_aws"
        ],
        "trialExpiresAt": null,
        "name": "Metricly Support Testing",
        "datasourceTrialCountLimit": 2
      },
      "customElementTypeIcons": {},
      "roles": [
        "Administrator"
      ],
      "assumedIdentity": false,
      "assumedReadOnlyIdentity": false,
      "administrator": true,
      "globalAdministrator": false,
      "globalReadOnly": false,
      "readOnly": false
    }
  ]
}
```
{{% /expand %}}

---

## POST to /users
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/users/createUserUsingPOST" >}} POST {{< /button >}} Use this endpoint to create a user.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | header | string | User-Agent |
| wrapper  | body  | JSON | JSON that contains the template to build a user  |

### Request URL

 `https://app.metricly.com/users`

### CURL

The following example creates a new user with the **email** `example+02052020%40gmail.com` and **password** `123456789*`. Notice that you can specify default properties, such as **theme** and **landingPage**.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "administrator": true, \
   "readOnly": false, \
   "user": { \
     "active": true, \
     "customElementTypeIcons": {}, \
     "email": "example+02052020%40gmail.com", \
     "password": "123456789*", \
     "properties": {
        "theme": "dark", \
        "landingPage": "dashboards" \
       }, \
     "tenantProperties": { \
       "datasourceTrialCountLimit": null, \
       "name": "Louis Lane", \
       "netuitiveAccountId": "270852171095", \
       "productIds": [ \
         "monitoring", \
         "cost_aws" \
       ], \
       "tenantStatus": "ACTIVE", \
       "tenantType": "CUSTOMER", \
       "trialExpiresAt": null \
     } \
   } \
 }' 'https://app.metricly.com/users'
```

### Swagger Payload

Try the following template for yourself in Swagger.

```
{
   "administrator": true,
   "readOnly": false,
   "user": {
     "active": true,
     "customElementTypeIcons": {},
     "email": "example+02052020%40gmail.com",
     "password": "123456789*",
     "properties": {
        "theme": "dark",
        "landingPage": "dashboards"
       },
     "tenantProperties": {
       "datasourceTrialCountLimit": null,
       "name": "Louis Lane",
       "netuitiveAccountId": "270852171095",
       "productIds": [
         "monitoring",
         "cost_aws"
       ],
       "tenantStatus": "ACTIVE",
       "tenantType": "CUSTOMER",
       "trialExpiresAt": null
     }
   }
 }
```


### Response Body

The following Response Body includes confirmation the user has been created with the specified properties and a unique **id**. Note the full template shows all available properties that can be included during user creation.

```
{
  "user": {
    "id": 84990,
    "email": "example+02052020%40gmail.com",
    "realUser": null,
    "active": true,
    "properties": {
      "seenEventsGraphTooltip": "false",
      "dailyReportEnabled": "false",
      "leftNavEnabled": "true",
      "seenIntegrationsTooltip": "false",
      "ebsOnStoppedEc2EmailEnabled": "false",
      "chartHeight": "tall",
      "seenWelcomeTour": "false",
      "seenAnnouncements": "[]",
      "theme": "dark",
      "favoriteDashboards": "[\"7fa6a515-1111-2222-3333-ea27bce9e563\"]",
      "leftNavLockedOpen": "true",
      "unattachedEbsEmailEnabled": "false",
      "arrangeChartsSetting": "grid",
      "seenWelcomeModal": "false",
      "seenMetricsChartTooltip": "false",
      "createdDashboard": "false",
      "landingPage": "dashboards",
      "timeZone": "UTC",
      "fullName": "Louis Lane",
      "ebscostTable": "[]",
      "seenMetricsFilterTooltip": "false",
      "inventoryTable": "[]",
      "chartWidth": "xsmall",
      "unattachedElbEmailEnabled": "false",
      "alertBadgeEnabled": "true",
      "metricsViewSetting": "tree"
    },
    "tenantProperties": {
      "netuitiveAccountId": "270852171095",
      "tenantType": null,
      "tenantStatus": null,
      "productIds": [],
      "trialExpiresAt": null,
      "name": null,
      "datasourceTrialCountLimit": null
    },
    "customElementTypeIcons": {},
    "roles": [
      "Administrator"
    ],
    "administrator": true,
    "globalAdministrator": false,
    "globalReadOnly": false,
    "assumedIdentity": false,
    "assumedReadOnlyIdentity": false,
    "readOnly": false
  }
}

```
{{% /expand %}}

---
## GET from /users/current
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/users/getCurrentUserUsingGET" >}} GET {{< /button >}} Use this endpoint to  

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| packageId | query | string | ID of the package e.g. netuitive.packages.linux. |

### Request URL

 ``

### CURL

The following example
```

```

### Response Body

The following response body includes

```

```
{{% /expand %}}

---
## DELETE to /users/{id}
{{< button theme="danger" href="https://app.metricly.com/swagger-ui.html#!/users/deleteUserUsingDELETE" >}} DELETE {{< /button >}} Use this endpoint to

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| packageId | query | string | ID of the package e.g. netuitive.packages.linux. |

### Request URL

 ``

### CURL

The following example
```

```

### Response Body

The following response body includes a
```

```
{{% /expand %}}

---
## GET from /users/{id}
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/users/getUserUsingGET" >}} GET {{< /button >}} Use this endpoint

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| packageId | query | string | ID of the package e.g. netuitive.packages.linux. |

### Request URL

 ``

### CURL

The following example
```

```

### Response Body

The following response body includes
```

```
{{% /expand %}}

---
## PUT to /users/{id}
{{< button theme="warning" href="https://app.metricly.com/swagger-ui.html#!/users/updateUserUsingPUT" >}} PUT {{< /button >}} Use this endpoint to

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| packageId | query | string | ID of the package e.g. netuitive.packages.linux. |

### Request URL

 ``

### CURL

The following example
```

```

### Response Body

The following response body includes a

```

```
{{% /expand %}}

---
## GET from /users/{id}/featureusage
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/users/getFeatureUsageUsingGET" >}} GET {{< /button >}} Use this endpoint to

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| packageId | query | string | ID of the package e.g. netuitive.packages.linux. |

### Request URL

 ``

### CURL

The following example
```

```

### Response Body

The following response body includes
```

```
{{% /expand %}}

---
## POST to /users/{id}/password
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/users/updatePasswordUsingPOST" >}} POST {{< /button >}} Use this endpoint to

{{% expand "View method details."%}}

### Request URL

 ``

### CURL

The following example
```

```

### Response Body

The following response body includes a

```

```
{{% /expand %}}

---
