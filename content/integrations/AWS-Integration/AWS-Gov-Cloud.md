---
title: "Gov Cloud"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#gov cloud"]
author: Lawrence Lane
weight: 6
---
AWS GovCloud (US) is a segment of Amazon Web Services cloud offerings that restrict physical and logical administrative access to U.S. citizens only. The region meets the requirements for U.S. International Traffic in Arms Regulations (ITAR), and allows users to move Controlled Unclassified Information (CUI) into the cloud. Check out our blog post, Monitor AWS GovCloud With Metricly, or the official AWS Guide for more information.

## Configuration

{{% alert theme="warning"%}} Leave GovCloud disabled unless you have signed up for and are using a GovCloud-restricted AWS account. {{% /alert %}}

1. Log in to your AWS Identity & Access Management (IAM) Console.
2. Navigate to the Users section and **Add User**.
3. For User Name, input `Metricly`.
4. In the Select AWS Access Type section, enable **Programmatic Access**.
5. Add **Read Only** permissions to the user.
6. Copy the User Security Credentials. These will be used in Metricly.
7. Open Metricly and navigate to **Integrations** > **AWS**.
8. Select the relevant AWS account.
9. Toggle **In GovCloud** to enable.
10. Input the **AWS Access Key** and **AWS Secret Access Key**.
11. Click **Save**.
