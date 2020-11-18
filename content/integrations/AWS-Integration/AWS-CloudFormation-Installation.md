---
title: "CloudFormation"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#iam role", "#cloudFormation script"]
author: Lawrence Lane
#pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 1
---
This installation method leverages a CloudFormation script which can be viewed [here](https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-www/assets/cloudformation/cloudwisdom-read-only-role.template). You can also [view a list of permissions](/images/AWS-CloudFormation-Installation/cloudformation-permissions.png) granted by the IAM role.

After you make a new AWS integration in CloudWisdom, the script populates a read-only IAM role in your AWS account and links it using the integration’s Account ID and External ID. Once created, it may take a few minutes for the status to be updated.

## 1. Create an AWS Integration in CloudWisdom
1. Open CloudWisdom and navigate to **Integrations** > **Amazon Web Services**.  
   - If this is not your first AWS integration, select **+ Add Integration**.
   ![add-integration](/images/AWS-CloudFormation-Installation/add-integration.png)
3. Enable **Cost Explorer API** if applicable to this integration.
   - **Note**: Only one AWS datasource may have Cost Explorer API enabled; CloudWisdom recommends enabling Cost Explorer on your management account.
4. Enable **Cost & Usage Reports** if applicable to this integration.
 - See the [Cost and Usage Report steps](/integrations/aws-integration/aws-cur).
![cost-explorer-CUR](/images/AWS-CloudFormation-Installation/cost-explorer-cur.png)
5. Select the **CloudFormation script** link under Configure AWS Permissions. This opens a new tab in AWS.  
6. Check **I acknowledge that AWS CloudFormation might create IAM resources**.  
7. Select **Create Stack**. This process may take a few minutes. Wait for the stack to say **CREATE_COMPLETE** before proceeding to the next section.

## 2.  Add RoleARN to the New AWS Integration
1. Select the stack you have created. It will start with `CloudWisdom`.
2. Navigate to the **Outputs** tab.
3. Copy the **Role ARN Value**.
![role-arn-value](/images/onboarding-wizard/role-arn-value.png)
4. Return to CloudWisdom.   
5. Input the Role ARN into **IAM Role ARN**. Make sure there are no extra spaces once you have pasted the value into the field.
![iam-role-arn](/images/AWS-CloudFormation-Installation/iam-role-arn.png)
6. **Save**.  
