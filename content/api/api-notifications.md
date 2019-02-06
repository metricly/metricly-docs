---
title: "Notifications API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---
The notifications API allows you to access and create notifications.  

**Request Header**

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

## GET
### GET List of Notifications from /notifications
This method will automatically return a list of notifications created for the tenant you are authenticated for.

### GET a Notification by ID from /notificaitons/{id}
This method will return a notification for the given ID.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|---------------------------------------------|
| id | Required | URL (path) parameter. Your notification ID. |

## POST
### POST Notification to /notifications
This method will create a notification.

**Parameters**

| Parameters | Required/Optional | Description |
|--------------|-------------------|---------------------------|
| notification | Required | Body parameter; see below |

### POST a Notification /notifications/test
This method will allow you to test a notification.

**Body Attributes**

| Attribute | Required/Optional | Description |
|--------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| notification | Required | id (required) The notification ID. tenantId (required) The ID for the tenant that the notification was created for. enabled (optional) True or false; if the notification is enabled. type (required) The type of notification: email, hipchat, webhook, opsgenie, or pagerduty. properties (required) The fields filled out for each notification type. See above for more information. For an email notification, the properties attribute would contain templateType, address, bodyTemplate, and subjectTemplate. |

### POST (replace) a notification from /notificaitons/{id}
This method will allow you to replace a given notification.

**Parameters**

| Parameters | Required/Optional | Description |
|--------------|-------------------|---------------------------|
| notification | Required | Body parameter; see below |

**Body Attributes**

| Attribute | Required/Optional | Description |
|--------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| notification | Required | id (required) The notification ID. tenantId (required) The ID for the tenant that the notification was created for. enabled (optional) True or false; if the notification is enabled. type (required) The type of notification: email, hipchat, webhook, opsgenie, or pagerduty. properties (required) The fields filled out for each notification type. See above for more information. |

## DELETE
### DELETE a Notification from /notifications/{id}
This method will delete a given notification.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|---------------------------------------------|
| id | Required | URL (path) parameter. Your notification ID. |
