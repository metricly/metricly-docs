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

CloudWisdom's Users API can be used to list and create users. You can also update your own user password and profile through the API, as well as monitor an account's setup status. You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/users) and by clicking the interactive buttons below.


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

The following response body includes only one user. Notice their **role** is set to `Administrator`.

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

The following example creates a new user with the **email** `example+02052020@gmail.com` and **password** `123456789*`. Notice that you can specify default properties, such as **theme** and **landingPage**.

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
     "email": "example+02052020@gmail.com",
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

The following response body includes confirmation the user has been created with the specified properties and a unique **id**. Note the full template shows all available properties that can be included during user creation.

```
{
  "user": {
    "id": 84990,
    "email": "example+02052020@gmail.com",
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
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/users/getCurrentUserUsingGET" >}} GET {{< /button >}} Use this endpoint to get a list of currently active users.  

{{% expand "View method details."%}}


### Request URL

 `https://app.metricly.com/users/current`

### CURL

The following example only requires the Request URL to make the API call.
```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/users/current'
```

### Response Body

The following response body includes the only active user in the example environment.

```
{
  "user": {
    "id": 12345,
    "email": "exampleactiveuser@gmail.com",
    "realUser": null,
    "active": true,
    "properties": {
      "seenEventsGraphTooltip": "true",
      "dailyReportEnabled": "false",
      "leftNavEnabled": "true",
      "seenAwsCostReportTour": "true",
      "seenIntegrationsTooltip": "true",
      "ebsOnStoppedEc2EmailEnabled": "false",
      "chartHeight": "tall",
      "seenWelcomeTour": "false",
      "seenAnnouncements": "[]",
      "theme": "light",
      "favoriteDashboards": "[\"55f573b7-1111-22222-3333-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]",
      "arrangeChartsSetting": "grid",
      "unattachedEbsEmailEnabled": "true",
      "leftNavLockedOpen": "true",
      "seenWelcomeModal": "false",
      "seenMetricsChartTooltip": "true",
      "createdDashboard": "true",
      "landingPage": "inventory",
      "timeZone": "UTC",
      "fullName": "L.B. Lane",
      "ebscostTable": "[]",
      "seenMetricsFilterTooltip": "true",
      "inventoryTable": "[{\"id\":\"created\",\"columnType\":\"attribute\",\"header\":\"Created\",\"isDefault\":true},{\"id\":\"lastProcessed\",\"columnType\":\"attribute\",\"header\":\"Last Processed\",\"isDefault\":true}]",
      "chartWidth": "xsmall",
      "unattachedElbEmailEnabled": "false",
      "campaign": null,
      "alertBadgeEnabled": "true",
      "metricsViewSetting": "tree"
    },
    "tenantProperties": {
      "netuitiveAccountId": "8765432356543",
      "tenantType": "CUSTOMER",
      "tenantStatus": "ACTIVE",
      "productIds": [
        "monitoring",
        "cost_aws"
      ],
      "trialExpiresAt": null,
      "name": "Metricly",
      "datasourceTrialCountLimit": 2
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
## DELETE to /users/{id}
{{< button theme="danger" href="https://app.metricly.com/swagger-ui.html#!/users/deleteUserUsingDELETE" >}} DELETE {{< /button >}} Use this endpoint to delete a user.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | header | string | User-Agent |
| id  | path  | long  | Unique ID of the user  |

### Request URL

 `https://app.metricly.com/users`

### CURL

The following example only requires the user's unique **id** be added to the Request URL.
```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/users/84330'
```

### Response Body

The following response body returns no content along with a 204 successful response code.
```
no content
```
{{% /expand %}}

---
## GET from /users/{id}
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/users/getUserUsingGET" >}} GET {{< /button >}} Use this endpoint to get the full template of a user.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| id  | path  | long  | Unique ID of the user  |

### Request URL

 `https://app.metricly.com/users/{id}`

### CURL

The following example only requires the user's unique **id** be added to the Request URL.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/users/12345'

```

### Response Body

The following response body includes the full user template.

```
{
  "user": {
    "id": 12345,
    "email": "exampleactiveuser@gmail.com",
    "realUser": null,
    "active": true,
    "properties": {
      "seenEventsGraphTooltip": "true",
      "dailyReportEnabled": "false",
      "leftNavEnabled": "true",
      "seenAwsCostReportTour": "true",
      "seenIntegrationsTooltip": "true",
      "ebsOnStoppedEc2EmailEnabled": "false",
      "chartHeight": "tall",
      "seenWelcomeTour": "false",
      "seenAnnouncements": "[]",
      "theme": "light",
      "favoriteDashboards": "[\"55f573b7-1111-22222-3333-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]",
      "arrangeChartsSetting": "grid",
      "unattachedEbsEmailEnabled": "true",
      "leftNavLockedOpen": "true",
      "seenWelcomeModal": "false",
      "seenMetricsChartTooltip": "true",
      "createdDashboard": "true",
      "landingPage": "inventory",
      "timeZone": "UTC",
      "fullName": "L.B. Lane",
      "ebscostTable": "[]",
      "seenMetricsFilterTooltip": "true",
      "inventoryTable": "[{\"id\":\"created\",\"columnType\":\"attribute\",\"header\":\"Created\",\"isDefault\":true},{\"id\":\"lastProcessed\",\"columnType\":\"attribute\",\"header\":\"Last Processed\",\"isDefault\":true}]",
      "chartWidth": "xsmall",
      "unattachedElbEmailEnabled": "false",
      "campaign": null,
      "alertBadgeEnabled": "true",
      "metricsViewSetting": "tree"
    },
    "tenantProperties": {
      "netuitiveAccountId": "8765432356543",
      "tenantType": "CUSTOMER",
      "tenantStatus": "ACTIVE",
      "productIds": [
        "monitoring",
        "cost_aws"
      ],
      "trialExpiresAt": null,
      "name": "Metricly",
      "datasourceTrialCountLimit": 2
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
## PUT to /users/{id}
{{< button theme="warning" href="https://app.metricly.com/swagger-ui.html#!/users/updateUserUsingPUT" >}} PUT {{< /button >}} Use this endpoint to update your own user or to manage the **roles** and **permissions** of other users (must be an admin to do this).

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | header | string | User-Agent |
| id  | path  | long  | Unique ID of the user  |
| wrapper  | body  | JSON | JSON that contains the template to build a user |

### Request URL

 `https://app.metricly.com/users/{id}`

### CURL

The following example, the **theme** has been updated to dark.  

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "user": { \
     "id": 12345, \
     "email": "exampleemail%40gmail.com", \
     "realUser": null, \
     "active": true, \
     "properties": { \
       "seenEventsGraphTooltip": "true", \
       "dailyReportEnabled": "false", \
       "leftNavEnabled": "true", \
       "seenAwsCostReportTour": "true", \
       "seenIntegrationsTooltip": "true", \
       "ebsOnStoppedEc2EmailEnabled": "false", \
       "chartHeight": "tall", \
       "seenWelcomeTour": "false", \
       "seenAnnouncements": "[]", \
       "theme": "dark", \
       "favoriteDashboards": "[\"55f573b7-3c97-3e2e-9f3e-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]", \
       "arrangeChartsSetting": "grid", \
       "unattachedEbsEmailEnabled": "true", \
       "leftNavLockedOpen": "true", \
       "seenWelcomeModal": "false", \
       "seenMetricsChartTooltip": "true", \
       "createdDashboard": "true", \
       "landingPage": "inventory", \
       "timeZone": "UTC", \
       "fullName": "L.B. Lane", \
       "ebscostTable": "[]", \
       "seenMetricsFilterTooltip": "true", \
       "inventoryTable": "[{\"id\":\"created\",\"columnType\":\"attribute\",\"header\":\"Created\",\"isDefault\":true},{\"id\":\"lastProcessed\",\"columnType\":\"attribute\",\"header\":\"Last Processed\",\"isDefault\":true}]", \
       "chartWidth": "xsmall", \
       "unattachedElbEmailEnabled": "false", \
       "campaign": null, \
       "alertBadgeEnabled": "true", \
       "metricsViewSetting": "tree" \
     }, \
     "tenantProperties": { \
       "netuitiveAccountId": "270852171095", \
       "tenantType": "CUSTOMER", \
       "tenantStatus": "ACTIVE", \
       "productIds": [ \
         "monitoring", \
         "cost_aws" \
       ], \
       "trialExpiresAt": null, \
       "name": "Metricly Support Testing", \
       "datasourceTrialCountLimit": 2 \
     }, \
     "customElementTypeIcons": {}, \
     "roles": [ \
       "Administrator" \
     ], \
     "administrator": true, \
     "globalAdministrator": false, \
     "globalReadOnly": false, \
     "assumedIdentity": false, \
     "assumedReadOnlyIdentity": false, \
     "readOnly": false \
   } \
 }' 'https://app.metricly.com/users/76502'
```

## Swagger Payload

```
{
  "user": {
    "id": 12345,
    "email": "exampleemail@gmail.com",
    "realUser": null,
    "active": true,
    "properties": {
      "seenEventsGraphTooltip": "true",
      "dailyReportEnabled": "false",
      "leftNavEnabled": "true",
      "seenAwsCostReportTour": "true",
      "seenIntegrationsTooltip": "true",
      "ebsOnStoppedEc2EmailEnabled": "false",
      "chartHeight": "tall",
      "seenWelcomeTour": "false",
      "seenAnnouncements": "[]",
      "theme": "dark",
      "favoriteDashboards": "[\"55f573b7-3c97-3e2e-9f3e-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]",
      "arrangeChartsSetting": "grid",
      "unattachedEbsEmailEnabled": "true",
      "leftNavLockedOpen": "true",
      "seenWelcomeModal": "false",
      "seenMetricsChartTooltip": "true",
      "createdDashboard": "true",
      "landingPage": "inventory",
      "timeZone": "UTC",
      "fullName": "L.B. Lane",
      "ebscostTable": "[]",
      "seenMetricsFilterTooltip": "true",
      "inventoryTable": "[{\"id\":\"created\",\"columnType\":\"attribute\",\"header\":\"Created\",\"isDefault\":true},{\"id\":\"lastProcessed\",\"columnType\":\"attribute\",\"header\":\"Last Processed\",\"isDefault\":true}]",
      "chartWidth": "xsmall",
      "unattachedElbEmailEnabled": "false",
      "campaign": null,
      "alertBadgeEnabled": "true",
      "metricsViewSetting": "tree"
    },
    "tenantProperties": {
      "netuitiveAccountId": "270852171095",
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
    "administrator": true,
    "globalAdministrator": false,
    "globalReadOnly": false,
    "assumedIdentity": false,
    "assumedReadOnlyIdentity": false,
    "readOnly": false
  }
}
```

### Response Body

The following response body includes a full user template that shows the changes made.

```
{
  "user": {
    "id": 12345,
    "email": "exampleemail@gmail.com",
    "realUser": null,
    "active": true,
    "properties": {
      "seenEventsGraphTooltip": "true",
      "dailyReportEnabled": "false",
      "leftNavEnabled": "true",
      "seenAwsCostReportTour": "true",
      "seenIntegrationsTooltip": "true",
      "ebsOnStoppedEc2EmailEnabled": "false",
      "chartHeight": "tall",
      "seenWelcomeTour": "false",
      "seenAnnouncements": "[]",
      "theme": "dark",
      "favoriteDashboards": "[\"55f573b7-3c97-3e2e-9f3e-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]",
      "arrangeChartsSetting": "grid",
      "unattachedEbsEmailEnabled": "true",
      "leftNavLockedOpen": "true",
      "seenWelcomeModal": "false",
      "seenMetricsChartTooltip": "true",
      "createdDashboard": "true",
      "landingPage": "inventory",
      "timeZone": "UTC",
      "fullName": "L.B. Lane",
      "ebscostTable": "[]",
      "seenMetricsFilterTooltip": "true",
      "inventoryTable": "[{\"id\":\"created\",\"columnType\":\"attribute\",\"header\":\"Created\",\"isDefault\":true},{\"id\":\"lastProcessed\",\"columnType\":\"attribute\",\"header\":\"Last Processed\",\"isDefault\":true}]",
      "chartWidth": "xsmall",
      "unattachedElbEmailEnabled": "false",
      "campaign": null,
      "alertBadgeEnabled": "true",
      "metricsViewSetting": "tree"
    },
    "tenantProperties": {
      "netuitiveAccountId": "270852171095",
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
## GET from /users/{id}/featureusage
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/users/getFeatureUsageUsingGET" >}} GET {{< /button >}} Use this endpoint to check the setup status and feature usage of a user account.

{{% expand "View method details."%}}


### Request URL

 `https://app.metricly.com/users/{id}/featureusage`

### CURL

The following example includes the users unique **id** in the Request URL.
```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/users/76502/featureusage'
```

### Response Body

The following response body shows a breakdown of actions available in CloudWisdom that have been taken by the user. This user has created at least one policy, dashboard, datasource, and notification. This account has been 100% configured.
```
{
  "featureUsage": {
    "id": 76502,
    "featuresUsed": {
      "createdPolicy": true,
      "createdDatasource": true,
      "createdDashboard": true,
      "createdNotification": true
    },
    "configuredPercentage": 100
  }
}
```
{{% /expand %}}

---
## POST to /users/{id}/password
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/users/updatePasswordUsingPOST" >}} POST {{< /button >}} Use this endpoint to update the password of a user.

{{% expand "View method details."%}}

### Request URL

 `https://app.metricly.com/users/{id}/password?oldPassword={OLDPASS}&newPassword={NEWPASS}`

### CURL

The following example includes the user's unique **id**, old password, and new password.
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' 'https://app.metricly.com/users/12345/password?oldPassword=MySafePW1&newPassword=MYsaferPW2!'

```

### Response Body

The following response body returns the user template but does not reveal the new password.

```
{
  "user": {
    "id": 12345,
    "email": "exampleemail@gmail.com",
    "realUser": null,
    "active": true,
    "properties": {
      "seenEventsGraphTooltip": "true",
      "dailyReportEnabled": "false",
      "leftNavEnabled": "true",
      "seenAwsCostReportTour": "true",
      "seenIntegrationsTooltip": "true",
      "ebsOnStoppedEc2EmailEnabled": "false",
      "chartHeight": "tall",
      "seenWelcomeTour": "false",
      "seenAnnouncements": "[]",
      "theme": "dark",
      "favoriteDashboards": "[\"55f573b7-3c97-3e2e-9f3e-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]",
      "arrangeChartsSetting": "grid",
      "unattachedEbsEmailEnabled": "true",
      "leftNavLockedOpen": "true",
      "seenWelcomeModal": "false",
      "seenMetricsChartTooltip": "true",
      "createdDashboard": "true",
      "landingPage": "inventory",
      "timeZone": "UTC",
      "fullName": "L.B. Lane",
      "ebscostTable": "[]",
      "seenMetricsFilterTooltip": "true",
      "inventoryTable": "[{\"id\":\"created\",\"columnType\":\"attribute\",\"header\":\"Created\",\"isDefault\":true},{\"id\":\"lastProcessed\",\"columnType\":\"attribute\",\"header\":\"Last Processed\",\"isDefault\":true}]",
      "chartWidth": "xsmall",
      "unattachedElbEmailEnabled": "false",
      "campaign": null,
      "alertBadgeEnabled": "true",
      "metricsViewSetting": "tree"
    },
    "tenantProperties": {
      "netuitiveAccountId": "123456776543",
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

## How to Preconfigure a New User

Admins can create new users through the User API by sending a POST call to **/users**. In addition to basic setup, admins can use **properties** to define config such as the user's landing page, theme, and even set them up with a favorite dashboard. Follow this walkthrough to learn how to preconfigure a user.

{{% expand "View Walkthrough." %}}

1\. Build a basic JSON template for creating a user. This is an end user, so set the user to **ReadOnly** `True`.

{{% notice tip %}}

Do not send a basic template to create the user; you cannot edit the user's preference details once it has been created -- only the  and **roles** and **permissions** (administrator, globalAdministrator, readOnly, etc) settings. Finish setting up all properties first.
{{% /notice %}}

```
{
  "user": {
    "id": "",
    "email": "email@domain.com",
    "active": true,
    "properties": {
    }
  },
  "readOnly": true
}

```

2\. Add all the properties you want to preconfigure. Below we have defined their **timeZone**, **theme**, **landingPage**, **fullName**, and created a placeholder for **favoriteDashboards**.


```
{
  "user": {
    "id": "",
    "email": "email@domain.com",
    "active": true,
    "properties": {
      "timeZone": "UTC",
      "landingPage": "dashboards",
      "fullName": "John Doe",
      "theme": "dark",
      "favoriteDashboards": "[]"
    }
  },
  "readOnly": true
}

```

3\. Build a CURL query to GET a list of dashboardIds from **/dashboards**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards'
```

4\. Select one or many **ids** belonging to dashboards the user would find most useful.

5\. Add the **ids** to the JSON payload you built for creating the new user.


```
{
	"user": {
		"id": "",
		"email": "email@domain.com",
		"active": true,
		"properties": {
			"timeZone": "UTC",
			"landingPage": "dashboards",
			"fullName": "John Doe",
			"theme": "dark",
			"favoriteDashboards": "[\"55f573b7-3c97-3e2e-9f3e-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]"
		}
	},
	"readOnly": true
}

```

6\. Send to **/users** as a POST CURL query.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
 	"user": { \
 		"id": "", \
 		"email": "emaily%40domain.com", \
 		"active": true, \
 		"properties": { \
 			"timeZone": "UTC", \
 			"landingPage": "dashboards", \
 			"fullName": "John Doe", \
 			"theme": "dark", \
 			"favoriteDashboards": "[\"55f573b7-3c97-3e2e-9f3e-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]" \
 		} \
 	}, \
 	"readOnly": true \
 }' 'https://app.metricly.com/users'
```
7\. Review the response body.

```
{
  "user": {
    "id": 84394,
    "email": "email@domain.com",
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
      "favoriteDashboards": "[\"55f573b7-3c97-3e2e-9f3e-ba4b15d6b59d\",\"54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5\"]",
      "leftNavLockedOpen": "true",
      "unattachedEbsEmailEnabled": "false",
      "arrangeChartsSetting": "grid",
      "seenWelcomeModal": "false",
      "seenMetricsChartTooltip": "false",
      "createdDashboard": "false",
      "landingPage": "dashboards",
      "timeZone": "UTC",
      "fullName": "John Doe",
      "ebscostTable": "[]",
      "seenMetricsFilterTooltip": "false",
      "inventoryTable": "[]",
      "chartWidth": "xsmall",
      "unattachedElbEmailEnabled": "false",
      "alertBadgeEnabled": "true",
      "metricsViewSetting": "tree"
    },
    "tenantProperties": {
      "netuitiveAccountId": "9876543",
      "tenantType": null,
      "tenantStatus": null,
      "productIds": [],
      "trialExpiresAt": null,
      "name": null,
      "datasourceTrialCountLimit": null
    },
    "customElementTypeIcons": {},
    "roles": [
      "Read Only"
    ],
    "administrator": false,
    "globalAdministrator": false,
    "globalReadOnly": false,
    "assumedIdentity": false,
    "assumedReadOnlyIdentity": false,
    "readOnly": true
  }
}
```


{{% /expand %}}
