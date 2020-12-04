---
title: "Email Notifications"
#date: 2018-05-12
draft: false
categories:
tags: ["alerts", "notifications", "email"]
author: Lawrence Lane
---

You can create email templates with custom messaging that are re-usable across multiple policies, or simply choose CloudWisdom’s default email notifications. Read below for configuration steps.

## Configuration
1. Click your **Username** > **Notifications**.
2. Click **Add Notification**.
3. Select **Email** for _Notification Type_. The following modal appears:
![New Email](/images/notifications-emails/new-email.png)
4. Choose your frequency via the **Re-notify every** field.
5. Check **Notify on clear** if you want to be notified when the alert has ended.
6. Click **New Email** to create a new email template. The following modal appears:
![Custom Notification](/images/notifications-emails/custom-notification.png)
7. Provide a `Name` for the template. A list of these show up in the **Email** dropdown.
8. Provide an `Email Address` to send this notification to.
9. Choose a **Default** or **Custom Template**.
   - **Default**: Sends a CloudWisdom pre-formatted message.
   - **Custom**: Allows you to customize the Subject and Body of the email.
10. Click **Test and Save**.
11. Select your template from the **Email** dropdown.
![Select Template](/images/notifications-emails/select-template.png)
12. Click **Save**.

## Customization Variables
You can use the following variables to make your notification more dynamic.

| Variable              | Description                                              |
|-----------------------|----------------------------------------------------------|
| ${elementFqn}         | The Fully Qualified Name (FQN) of the element.           |
| ${elementId}          | The element’s unique UUID. |
| ${elementLocation}    | The location of the element.                             |
| ${elementName}        | The friendly name for the element.                       |
| ${elementType}        | The type of element (e.g, SERVER, ELB, RUBY, etc.)       |
| ${event.data.results} | The description of the event as a policy violation.      |
| ${event.id}           | The ID of the event                                      |
| ${eventCategory.name} | The event category ( (Info), (Warning), or (Critical)).  |
| ${eventTimestamp}     | The time (in UTC) the event occurred.                    |
| ${policyDescription}  | The description of the policy that generated the event.  |
| ${policyId}           | The policy identification number.                        |
| ${policyName}         | The name of the policy.                                  |
