---
title: "AWS SSM Install"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#agents", "#linux",]
author: Lawrence Lane
weight: 3
---

## Create Document for Install Script

1. Open the AWS SSM Console.
2. Select **Shared Resources** > **Documents** in the navigation pane.
3. Click **Create Document**.
4. Name the document `install-metricly-agents`
4. Keep this window open and create a **new browser tab**.
5. In the new tab, go to [Metricly's GitHub repo for AWS SSM](https://docs.google.com/document/d/1G6BpbE2TDPxcb3l0mg4qTJ3D2P96MWVFz_OWaf3QTcs/edit?usp=sharing).
6. Copy the page body.
7. In the AWS Console, replace the `hello world` page body content with the copied JSON.
![json-install-agents](/images/LINUX-aws-ssm-install/json-install-agents.png)
8. Click **Create Document**.

## Run Command in AWS SSM

1. In the AWS SSM Console, navigate to **Actions** > **Run Command**.
2. Search for `Owner: Equal: Self`. Select the document you created, `install-metricly-agents`.
3. Scroll to **Command Parameters**. You must input your **Linux** and **Windows API Keys** from your cloudwisdom integrations.
  - Open a **separate browser tab** and log into cloudwisdom.
  - Navigate to your **Linux integration**.
  - Copy API Key
  - Paste in corresponding field on AWS SSM page.
  - Repeat for Windows
4. Scroll to **Targets**. Add targets using specific tags or manually identifying them to have the agents added. (You can also run against all instances.)
5. Click **Run**.

{{% notice tip %}}
Ensure that your targets have the required **SSM IAM role** and **SSM agent** installed per [AWS documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html#attach-iam-role).
{{% /notice %}}
