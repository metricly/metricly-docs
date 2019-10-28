---
title: "Access Key"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#access key"]
author: Lawrence Lane
#pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 3
---
## Access key

Setting up an AWS integration is a two step process:  

1. Create a new AWS integration in CloudWisdomand share the **Access Key ID** and **Secret Access Key** of the desired IAM read-only user.  
2. Optionally, filter your AWS elements for inclusion in CloudWisdomby creating or choosing an existing tag (key-value pair), then assigning that tag to the desired elements in AWS.  

### Step 1: Create a new AWS integration
1. From the top navigation menu, select Integrations.  
2. Click the Amazon Web Services card.  
3. Type a name for the new AWS integration. Ensure that Data Collection is selected.  
4. For AWS Authentication, select Access Key. If you want to create a role that has full access to your AWS data, expand the full permissions instructions and follow those. If you want to create a role that only has access to four AWS 7. elements, expand the modified permissions instructions and follow those.  

### Step 2a: Creating a Read Only User (with standard permissions)
1. Log in to your AWS Identity & Access Management (IAM) Console.
2. Once in the IAM dashboard, navigate to the Users section.
3. Click Add user.  
4. For a User Name, type Metricly. Select the Programmatic access checkbox in the Select AWS access type section.  
5. Click Next: Permissions.  
6. Click Attach existing policies directly.  
7. Search “read only,” then select ReadOnlyAccess. You may need to change the  Filter type to have the correct policy show.  
8. Click Next: Review.  
9. Review the details to ensure you’ve selected all the correct options for the user, and then click Create User.  
10. Download and/or copy the User Security Credentials.  
11. You will not be able to access the Secret Access Key again unless you download the credentials.  
12. Click **Close**.  

### Step 2b: Creating a Read Only User (with minimal permissions)
1. If you want to use a limited read only access policy, you’ll need to create a custom policy first.
2. Log in to your AWS Identity & Access Management (IAM) Console.
3. Once in the IAM dashboard, navigate to the Policies section.
4. Click Create Policy in the top left-hand corner.
5. Click Select next to Create Your Own Policy.
6. Type a Policy Name into the field.
7. Type a description of the policy.
8. Copy and paste the following code into the Policy Document section.  

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "autoscaling:Describe*",
        "ce:*",
        "cloudwatch:Describe*",
        "cloudwatch:Get*",
        "cloudwatch:List*",
        "dynamodb:Describe*",
        "dynamodb:Get*",
        "dynamodb:List*",
        "ec2:Describe*",
        "ec2:GetConsoleOutput",
        "ecs:Describe*",
        "ecs:List*",
        "elasticache:Describe*",
        "elasticache:List*",
        "elasticloadbalancing:Describe*",
        "elasticmapreduce:Describe*",
        "elasticmapreduce:List*",
        "iam:Get*",
        "kinesis:DescribeStream",
        "kinesis:Get*",
        "kinesis:List*",
        "lambda:List*",
        "rds:Describe*",
        "rds:ListTagsForResource",
        "redshift:Describe*",
        "s3:Describe*",
        "s3:Get*",
        "s3:List*",
        "sqs:Get*",
        "sqs:List*",
        "tag:Get*"
      ],
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}
```
#### Validate Policy
9. Click **Validate Policy** to ensure you’ve filled out each section properly.  
10. Click **Create Policy**. The policy will now be available under Customer Managed Policies.  
11. Return to the IAM dashboard and navigate to the Users section.  
12. Click **Create New Users**.  
13. For a User Name, type `Metricly`. Select the **Programmatic access** checkbox in the Select AWS access type section.  
14. Click **Next: Permissions**.  
15. Click **Attach existing policies directly**.  
16. Select the policy you created in step 1.7. It should be near the top of the list.  
17. Click **Next: Review**.  
18. Review the details to ensure you’ve selected all the correct options for the user, and then click Create User.  
19. Download and/or copy the User Security Credentials.  
{{% alert theme="warning" %}}You will not be able to access the Secret Access Key again unless you download the credentials. {{% /alert %}}
21. Click **Close**.  
22. Copy and paste the **Access Key ID** and **Secret Access Key** for the desired read-only user into the appropriate fields on the AWS Setup page in Metricly.  
23. Include or exclude as many AWS element types as you want. ASG, EC2, EBS, ELB, RDS, and SQS are enabled by default; everything else is disabled by default.  
{{% alert theme="warning" %}} The AWS SQS API limits responses to 1000 queues. Thus if your environment has 1000 or more queues, Metricly won’t gather queues that match your regex filter but exceed the 1000 queue limit. {{% /alert %}}
 - If you enable AWS Custom Metrics note that each category you create in Cloudwatch will create a matching element in Metricly. All the metrics under each category will be included in the corresponding element; this means, if you want the metrics divided amongst your dimensions (e.g., App1 errors, App2 errors, App3 errors), you’ll need to create separate categories for each element. To read more about creating and using custom Cloudwatch metrics, go here.  
26. Optionally, filter elements or change the display name of your AWS instances.  
 - If you install our Linux agent or Windows agent on an EC2 server, the EC2’s power state (it will come in as the attribute hostRunning with a value of true or false) and tags are copied over to the corresponding Linux SERVER element / Windows WINSRV element. You can then use this information to create policies.  
28. Click **Save**.  

 This integration’s package (computed metrics, dashboards, and policies that will give you important events and alerts) will be automatically enabled and provisioned to your account as soon as Metricly receives data from the integration.  
