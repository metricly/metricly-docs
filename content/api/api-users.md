---
title: "Users API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---
The users API allows you to access and manage your users.

**Request Header**

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

## GET
### Get List of Users From /users
This method will return a list of users associated with a tenant.

### Get Current User From /users/current
This method will return information about the user currently signed in.

### GET a User by ID From /users/{id}
This method will return a user for the given id.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------|
| id | Required | URL (path) parameter. The ID of the user. |

## POST
### POST New User

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|---------------------------|
| wrapper | Optional | Body parameter; see below |

**Body Attributes**

| Attribute | Required/Optional | Description |
|---------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| active | Optional | Whether the user is active or not. |
| administrator | Optional | Whether the user is an administrator for the tenant or not. Only one of either administrator or readOnly may be passed in as true, but if neither the administrator or readOnly attributes are specified, the user will default to being an administrator. |
| email | Optional | The email of the user used for logging in. |
| id | Optional | The ID of the user. |
| password | Optional | The password of the user. |
| properties | Optional | A list of the user’s stored preferences, sorts, selected theme and nav, daily report settings, and modal settings. |
| readOnly | Optional | Whether the user is a read only user. |

## PUT
### PUT an Update to a User /users/{id}
This method will allow you to update a given user’s information.

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------|
| id | Required | URL (path) parameter. The ID of the user. |
| wrapper | Optional | Body parameter; see below |

**Body Attributes**

| Attribute | Required/Optional | Description |
|---------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| active | Optional | Whether the user is active or not. |
| administrator | Optional | Whether the user is an administrator for the tenant or not. Only one of either administrator or readOnly may be passed in as true, but if neither the administrator or readOnly attributes are specified, the user will default to being an administrator. |
| email | Optional | The email of the user used for logging in. |
| id | Optional | The ID of the user. |
| password | Optional | The password of the user. |
| properties | Optional | A list of the user’s stored preferences, sorts, selected theme and nav, daily report settings, and modal settings. |
| readOnly | Optional | Whether the user is a read only user. |

## DELETE
### DELETE a User From /users/{id}

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|-------------------------------------------|
| id | Required | URL (path) parameter. The ID of the user. |
