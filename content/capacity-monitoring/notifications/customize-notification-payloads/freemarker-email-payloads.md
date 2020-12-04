---
title: "Email Payloads"
#date: 2018-05-12
draft: false
categories:
tags: ["alerts", "notifications"]
author: Lawrence Lane
alwaysopen: false
weight:
---
There are two event payload types that can be leveraged with email notification payloads: event and event_cleared. An event is generated when a policy is violating. An event_cleared is generated when a once-violating policy is no longer violating. Your custom event payloads can be setup to notify you on either type with unique messaging and details about the event.

**To create a custom event payload:**

1. Navigate to your **Account** > **Notifications** > **Email**.
2. Click **+ Add Email**.
3. Choose **Custom** in the Template dropdown.
4. Add a subject and input your JSON + FreeMarker writeup in the body of the email.
5. Click **Test & Save**.
6. Open a policy in the policy editor.
7. Go to **Notifications** > **Add Notification** > **Email**.
8. In the Email dropdown, select your newly created template.
9. **Save**.

Alternatively, you can create your new custom email payload in the policy editor on the new notification itself by clicking **+ New Email**.


**Example 1**

This example provides the policy name related to the event in the subject of the email and then provides the event category name of the event firing in the body. When the event clears, it sends another email with `CLEAR` as the body text.

```
CloudWisdom Event [${policyName}]
```

```
<#if payloadType == "event">
  ${eventCategory.name}
</#if>
<#if payloadType == "event_cleared">
  CLEAR
</#if>
```

**Example 2**

This example sends an email with `UP` or `DOWN` as the subject line, with all of the event details in the email body.

```
<#if payloadType == "event">DOWN</#if><#if payloadType == "event_cleared">UP</#if>
```

```
Time: ${eventTimestamp}
Event Category: ${eventCategory.name}
Policy Name: ${policyName}
Policy Description: ${policyDescription}
Event ID: ${event.id}
Element: ${elementName}
Violation: ${event.data.results}
```
