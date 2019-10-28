---
title: "AWS SNS Notifications"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#sns"]
author: Lawrence Lane
---

You can leverage AWS’s Simple Notification Service as one of your notification methods in Metricly. There are two ways to accomplish this: through an **IAM Role** or **Access Key**. It is recommended that you have first set up the AWS Integration and are familiar with terms such as **ARN (Amazon Resource Names)**, which are needed to complete setup.


**Inbound & Outbound**
This guide tackles outbound SNS setup, however you can also ingest inbound SNS notifications. Check out how we leverage [SNS to ingest CloudWatch logs][1] for a great example of inbound usage.

## Configuration Methods

### IAM Role Setup

#### 1. Add SNS Permissions to your AWS IAM Role
You must add SNS permissions to your AWS IAM Role in order to complete setup. Completing this section provides you with the required **IAM Role ARN** for section 4. Haven’t created an IAM Role? Complete our [AWS setup documentation][2].

1. In a separate tab from Metricly, log in to your AWS Identity & Access Management (IAM) Console.
2. Once in the IAM dashboard, navigate to the **Roles** section.
3. Search for your AWS Metricly IAM Role.
4. Select your AWS Metricly IAM role.
5. Click **Attach Policy**.
6. For Attach Policy, search `sns`, then select **AmazonSNSFullAccess**.
![Attach Policy](/images/notifications-aws-sns/attach-policy.png)
7. Click Attach Policy to add the policy.
8. Return to step 2.5 in the previous section and input the IAM Role ARN.

#### 2. Obtain Topic ARN
You must have a **Topic ARN** set up in AWS to use SNS with Metricly. Completing this section provides you with that number.

1. Navigate to the SNS console.
2. Click **Topics** on the left-hand menu.
3. Copy the ARN from the ARN column next to the desired topic. Paste the value into the **Topic ARN** field in the SNS Notification window in Metricly.
4. Back in the SNS console, select the same topic, and then click **Edit topic policy** in the Actions menu.
5. Under the _Allow these users to publish messages to this topic_ section, select Only these AWS users and add the `Account ID` from Metricly to the field.
6. Click **Update Policy**.
7. Return to CloudWisdom and optionally select **Custom** from the Payload drop-down menu. A text field will open after selecting Custom. Create a custom JSON payload in the textbox. You can use the following variables to make your notification more dynamic.
8. Click **Save**.

| Variable              | Description                                              |
|-----------------------|----------------------------------------------------------|
| ${event.data.results} | The description of the event as a policy violation.      |
| ${event.id}           | The ID of the event                                      |
| ${eventCategory.name} | The event category ( (Info), (Warning), or (Critical)).  |
| ${elementFqn}         | The Fully Qualified Name (FQN) of the element.           |
| ${elementId}          | The type of element (e.g., SERVER, ELB, EC2, RDS, etc.). |
| ${elementType}        | The type of element (e.g, SERVER, ELB, RUBY, etc.)       |
| ${elementLocation}    | The location of the element.                             |
| ${elementName}        | The friendly name for the element.                       |
| ${policyId}           | The policy identification number.                        |
| ${policyName}         | The name of the policy.                                  |
| ${eventTimestamp}     | The time (in UTC) the event occurred.                    |
| ${policyDescription}  | The description of the policy that generated the event.  |

Below is the default payload used in the SNS integration, but it’s a good starting place for creating a custom JSON payload.

```
{
  "timestamp": "${eventTimestamp}",
  "category": "${eventCategory}",
  "element": {
    "fqn": "${elementFqn}",
    "name": "${elementId}",
    "location": "${elementLocation}"
  },
  "policy": {
    "name": "${policyName}",
    "description": "${policyDescription}"
  }
}
```

#### 3. Navigate to Integrations
1. Click your **Username** > **Notifications**.
2. Click **SNS**.
3. Click **Add SNS**.
![add-sns](/images/notifications-aws-sns/add-sns.png)

#### 4. Input Information
1. Input a `Name` for the SNS notification.
2. Ensure **Enabled checkbox** is selected.
3. Provide a **Topic ARN**.
4. Select **IAM Role** for AWS Authentication.
5. Provide existing **IAM role ARN**. (Or, skip to next section to create one).
6. Choose a payload type (**Default** or **Custom**).
![Test and Save](/images/notifications-aws-sns/test-and-save.png)
7. Click **Test and Save**.

### Access Key Setup Method

#### 1. Create a User and **Add SNS Permissions**.
You must have a user with SNS permissions to complete the setup of an SNS with Metricly. Completing this section provides you with the required Access key ID and Secret access key.
1. In the AWS Console, navigate to **Users**.
2. Click **Add a User**.
3. Prove a `Name` and check **Programmatic Access**.
![Programmatic Access](/images/notifications-aws-sns/programmatic-access.png)
4. Click **Next: Permissions**.
5. Click **Attach existing policies directly** and select **AmazonSNSFullAccess**.
![Attach Existing Policies Directly](/images/notifications-aws-sns/attach-existing-policies-directly.png)
6. Click **Next: Review**.
7. Click **Create User**.
8. Copy the **Access key ID** and **Secret access key**.

#### 2. Obtain Topic ARN
You must have a **Topic ARN** set up in AWS to use SNS with Metricly. Completing this section provides you with that number.

1. Navigate to the SNS console.
2. Click **Topics** on the left-hand menu.
3. Copy the **ARN** from the ARN column next to the desired topic. Paste the value into the Topic ARN field in the SNS Notification window in Metricly.
4. Back in the SNS console, select the same topic, and then click **Edit topic policy** in the Actions menu.
5. Under the _Allow these users to publish messages to this topic section_, select **Only these AWS users** and add the `Account ID` from Metricly to the field.
6. Click **Update Policy**.
7. Return to CloudWisdom and optionally select Custom from the Payload drop-down menu. A text field will open after selecting Custom. Create a custom JSON payload in the textbox. You can use the following variables to make your notification more dynamic.
8. Click **Save**.

| Variable              | Description                                              |
|-----------------------|----------------------------------------------------------|
| ${event.data.results} | The description of the event as a policy violation.      |
| ${event.id}           | The ID of the event                                      |
| ${eventCategory.name} | The event category ( (Info), (Warning), or (Critical)).  |
| ${elementFqn}         | The Fully Qualified Name (FQN) of the element.           |
| ${elementId}          | The type of element (e.g., SERVER, ELB, EC2, RDS, etc.). |
| ${elementType}        | The type of element (e.g, SERVER, ELB, RUBY, etc.)       |
| ${elementLocation}    | The location of the element.                             |
| ${elementName}        | The friendly name for the element.                       |
| ${policyId}           | The policy identification number.                        |
| ${policyName}         | The name of the policy.                                  |
| ${eventTimestamp}     | The time (in UTC) the event occurred.                    |
| ${policyDescription}  | The description of the policy that generated the event.  |

Below is the default payload used in the SNS integration, but it’s a good starting place for creating a custom JSON payload.

```
{
  "timestamp": "${eventTimestamp}",
  "category": "${eventCategory}",
  "element": {
    "fqn": "${elementFqn}",
    "name": "${elementId}",
    "location": "${elementLocation}"
  },
  "policy": {
    "name": "${policyName}",
    "description": "${policyDescription}"
  }
}
```

#### 3. Navigate to Integrations in Metricly
1. Click your **Username** > **Notifications**.
2. Click **SNS**.
3. Click **Add SNS**.
![add-sns](/images/notifications-aws-sns/add-sns.png)

#### 4. Input Information
1. Input a `Name` for the SNS notification.
2. Ensure **Enabled checkbox** is selected.
3. Provide the Topic ARN from previous section.
4. Select **IAM Role for AWS Authentication**.
5. Provide the **Access Key** and **Secret Key** from previous section.
6. Choose a payload type (**Default** or **Custom**).

![Test and Save](/images/notifications-aws-sns/test-and-save.png)

[1]: /capacity-monitoring/events/cloudwatch-events
[2]: /integrations/aws-integration/aws-iam-installation
