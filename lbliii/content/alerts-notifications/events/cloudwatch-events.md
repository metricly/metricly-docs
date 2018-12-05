---
title: "CloudWatch Events"
date: 2018-04-12
draft: true
categories:
tags: ["alerts", "notifications", "events", "cloudwatch"]
author: Lawrence Lane
---


Through a combination of SNS Notifications, Metricly’s Webhook integration, and an external event conditions policy filter, you can push event logs from your AWS services to Metricly and act on them in the UI. This works across several AWS services. Once set up, these logs can be divided further on the policy level (through matching value strings in the log message and categorized by severity).  Policies for your event logs can also be set up with various notifications through email, slack, and others. The below instructions use Lambda as an example.

## Configuration

### 1. Create & Subscribe to SNS Topic
You must have AWS SNS setup to complete this section. Read our SNS Guide to complete setup. If you have already set up Amazon’s SNS, continue on.

1. Open your AWS console and navigate to the SNS Dashboard.
2. Click **Topics** > **Create new topic**.
3. `Name` and `describe` the new topic. Click **Create topic**.
4. Select your created topic and click **Actions** > **Subscribe to topic**.
![Subscribe to Topic](/images/cloudwatch-events/subscribe-to-topic.png)
{{% notice tip %}}
For the next step, you need to obtain a Metricly API endpoint and paste it as the URL.
{{% /notice %}}
5. In a separate tab, log into Metricly and navigate to **Integrations** > **Webhooks**.
![Copy POST URL](/images/cloudwatch-events/copy-post-url.png)
6. Copy the `POST URL`.
7. Paste the URL in the **Endpoint** field on your AWS tab and click **Create Subscription**.
![Paste URL to Endpoint](/images/cloudwatch-events/paste-url-to-endpoint.png)
8. AWS sends a validation URL to Metricly, which you then have to locate as an Event item in the UI. Log into Metricly and go to **Events**. In the **Type** filter, you can select **WEBHOOK** to narrow your search. Click on the event to read its details. `"SubscriberURL":` is the link you are looking for.
![SubscriberURL](/images/cloudwatch-events/subscriberurl.png)
9. Copy this `URL`, return to the AWS console.
10. Navigate to **AWS SNS** > **Topics** and select the topic you have created.
11. Click **Actions** > **Confirm a subscription**.
![Confirm a Subscription](/images/cloudwatch-events/confirm-a-subscription.png)
12. Input the URL you pasted from Metricly into the field and click **Confirm subscription**. Note that you can unsubscribe by using the ``"UnsubscribeURL":`` provided in the same messages.

### 2. Create IAM Role
To write logs for Lambda to CloudWatch Logs, you must create a custom IAM Role with the appropriate policies/permissions.

1. Log in to your AWS Identity & Access Management (IAM) Console.
2. Once in the IAM dashboard, navigate to the **Roles** section.
3. Click **Create New Role**.
4. Select **AWS Service** > **Lambda**.
![AWS Service Lambda](/images/cloudwatch-events/aws-service-lambda.png)
5. Click **Next: Permissions**.
6. Click **Create Policy**. This action opens a new tab.
7. Select the **JSON tab** and input the following code in the text field:

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "logs:CreateLogGroup",
                  "logs:CreateLogStream",
                  "logs:PutLogEvents",
                  "logs:DescribeLogStreams"
                  ],
                  "Resource": [
                      "arn:aws:logs:*:*:*"
                      ]
          }]
  }
  ```
8\. Name the policy `CloudWatchLogs` and click **Create Policy**.  
9. In your previous tab with the new Lamba role, look up the newly created policy  `CloudWatchLogs` and select it.  
10. Click **Next: Review**.  
11. Provide a `name`, such as `CloudWatchMetricly`, and a `description` for the role.  
12. Click **Create Role**.

### 3. Create Log Group Filter

1. Open your AWS console and Navigate to **Services** > **Management Tools** > **CloudWatch**.
2. Click **Logs** on the navigation.
3. Click **Create log group** and name your group.
4. Select your log group and click **Create Metric Filter**.
![Create Metric Filter](/images/cloudwatch-events/create-metric-filter.png)
5. Input any string you wish this filter to act upon that appears in the log. `Timed Out` and `Error` are common examples. In this case, we used  `START` in the **Filter Pattern**. This grabs all Lambda functions in particular. To break events down into more specific actionable items, see the final section in this guide, Create Metricly Policies.
6. Click **Assign Metric**.
7. Name the metric. In this case, we call it `CloudWatchEvent`. This name displays in the Metricly UI.
8. Click **Create Filter**.

### 4. Create Alert
Now that you have created a log group and a filter for that group, let’s make an alarm.

1. Open your AWS console and Navigate to **Services** > **Management Tools** > **CloudWatch**.
2. Click **Logs** on the navigation.
3. Click the **1 Filter** link you created earlier.
![Meric Filter](/images/cloudwatch-events/meric-filter.png)
4. Click **Create Alarm**. A modal Appears.
5. Fill out the _Alarm Threshold_, _Additional Settings_, and _Actions sections_.
![Alarm Threshold](/images/cloudwatch-events/alarm-threshold.png)
6. **Name and Description (#1 and #2)** can be named anything.
7. **Is: (#3)** must be `>= 1`; **For: (#4)** must be `1` out of `1`.
8. **Treat missing data as (#5)** must be set to good (_not breaching threshold_).
9. **Whenever this alarm (#6)** must be State is `ALARM`; **Send notification to (#7)** must be the SNS topic you’ve subscribed to in the first section of configuration, _Create & Subscribe to SNS Topic_.
10. Click **Create Alarm** to save it.

### 5. Create Metricly Policies
This is the most dynamic step. When creating Metricly policies, you can filter for strings within the log  message body. If you only want one policy for all logs, for example, you can keep the match criteria generic. If you want multiple policies per certain codes, simply filter for those codes on your policy setup. Remember that you can also create notifications on these policies.

1. Log into Metricly and navigate to **Alerts** > **Add New Policy**.
2. **Name** your policy and select its **Category** (_Info_, _Warning_, or _Critical_).
3. If you want to limit the scope to match the Webhook element, you may do so on the first tab.
4. Click on the **Conditions** tab.
5. Click **Add Condition** > **Add External Event Condition**.
6. Populate the **Message** field to match the messages you want captured in this policy.
![Message](/images/cloudwatch-events/message.png)
7. Click **Save** to activate the policy.
8. Repeat 1-7 for as many policies as you’d like, each with different criteria in the **Message** filter field.
