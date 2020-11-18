---
title: "Onboarding Wizard"
draft: false
tags: ["#getting started", "onboarding", "aws", "azure"]
author: Lawrence Lane
description: how to use the onboarding wizard with AWS or Azure cloud resources.
pre:
weight: 5
---

Use the Onboarding Wizard to quickly set up your first cloud resource. This guided tool supports initial setup of both [AWS][6] and [Azure][7] datasources. If you have already set up your first datasource, and would like to use the Onboarding Wizard for additional resources, you can prompt the wizard to begin using this url: `https://app.metricly.com/#/onboarding-wizard/integration`.

## Configure AWS

Before using the Onboarding Wizard, CloudWisdom recommends completing some configuration steps in the AWS console. These steps ensure you have all of the required settings in place to integrate to CloudWisdom.

### 1. Enable Cost Explorer
Cost Explorer must be enabled from the management account---even if already set up on a sub-account. IAM Roles set up with the management account allow CloudWisdom to present reports spanning all of your accounts; IAM Roles set up with a sub-account only reports cost for that one account.

1. Log in to your AWS management account.
2. Navigate to Cost Explorer.
3. Select **Enable Cost Explorer**.
![Enable Cost Explorer](/images/aws-integration/enable-cost-explorer.png)
4. The API is now available for use but has no data; you can request up to a year of cost billing data from AWS.

### 2. Enable Cost & Usage Reports in AWS

Cost & Usage Reports (CUR) have replaced Detailed Billing in AWS. CloudWisdom requires Cost & Usage Report data and no longer supports Detailed Billing files.

{{% notice tip %}}

Already have an existing hourly Cost & Usage Report with GZIP or ZIP compression set up? Great! You can skip this section. You'll need to provide your CUR's Report Path Prefix at a later stage in this setup.

{{% /notice %}}

1. Log in to your AWS Console.
2. Navigate to **Billing** > **Cost & Usage Reports**.
3. Select **Create report**.
![create-report](/images/aws-cur/create-report.png)
4. Name the report `HourlyCSVWithResourceIDs`.
5. Enable the **Include resource IDs** checkbox.
![enable-resource-ids](/images/aws-cur/enable-resource-ids.png)
6. Select **Next**.
7. Select **Configure** to choose (or create) a S3 bucket that will store your files.
![save-s3-bucket](/images/aws-cur/save-s3-bucket.png)
8. Provide a **Report path prefix**, such as `CostAndUsageReports`. Do not include any leading or trailing forward slashes; doing so may distort the file hierarchy output by AWS.
9. Select **Hourly** under Time granularity.
10. Select your preferred Report versioning method. Overwriting the existing report may save on your storage costs in the future.
11. Leave all data integration options unchecked.
12. Select **GZIP** for Compression type.
13. Select **Next**.
14. Review your configurations.
16. Select **Review and Complete** to create the Cost and Usage Report (CUR).

{{% notice tip %}}

It can take up to a few hours for new Cost & Usage Report data to appear in the S3 bucket.

{{% /notice %}}

Initial configuration steps in the AWS console are complete. Now we can begin the Onboarding Wizard steps in CloudWisdom.

#### 1. Create an IAM Role

1. Log in to **CloudWisdom**. You are automatically directed to the Onboarding Wizard.
2. Select **Begin Setup** > **Setup AWS Cloud**.
3. Select **Run Cloudformation Script**. This opens a new tab and is the fastest way to set up your IAM role; you will be prompted to log in to AWS.
4. Enable the **I acknowledge that AWS CloudFormation might create IAM resources** checkbox.
5. Select **Create Stack**. This process may take a few minutes. Wait for the stack to say **CREATE_COMPLETE** before proceeding to the next step.
6. Select the stack you have created. It will start with `CloudWisdom`.
7. Navigate to the **Outputs** tab.
8. Copy the **Role ARN Value**.
![role-arn-value](/images/onboarding-wizard/role-arn-value.png)
9. Return to the CloudWisdom Onboarding Wizard and paste the Role ARN into the field.
10. Select **Next: Cloudwatch**.

#### 2. Configure CloudWatch Data Collection

CloudWisdom collects performance data to power analyses. The elements enabled by default are recommended and can be changed at any time.

1. Approve the list of enabled default collections; uncheck any you wish to disable.
2. Select **Next: Cost and Billing**.

#### 3. Configure Cost & Billing Settings

1. Leave **Enable Cost Explorer** enabled.
2. Select a **Report Path Prefix**. The values listed are a combination of the S3 bucket name where the billing files reside followed by the full Report path prefix of the Cost & Usage report you configured.
![select-report-path](/images/onboarding-wizard/select-report-path.png)
3. Select **Next: Summary**.


{{% notice tip %}}
If the **Report Path Prefix** lookup is not available (and is instead a freeform text input), make sure you are using the most recent IAM role available. You can create the latest IAM role using the our [CloudFormation script](/integrations/aws-integration/aws-cloudformation-installation/).
You also have the option to manually enter the **S3 Bucket Name** (chosen in section 1, step 7) and **Report Path Prefix** (created in section 1, step 8).
{{% /notice %}}

#### 4. Name & Finalize New Datasource

1. Provide a name for your AWS datasource.
2. Select **Confirm & Finish**.

You can create more datasources using the guides in our [Integrations][3] section.

---

## Configure Azure

There are two ways to set up Azure with CloudWisdom: using the Azure CLI or through the Azure Portal. Virtana recommends using the CLI, as it's much quicker and easier.

### Via Azure Cli

1. Log in to **CloudWisdom**. You are automatically directed to the Onboarding Wizard.
2. Select **Begin Setup** > **Setup Azure Cloud**.
3. Select **Continue With Azure CLI**.
4. Ensure you have [installed the CLI][4] before proceeding.
5. Select **Continue**.
6. Open Windows PowerShell.
7. Input the following command:
`az login`
8. Log in to your Azure account.
9. Run the following command: `az account show`
10. Locate **id** and **tenantId** in the output.
11. Copy and paste the **tenantId** value into the **Tenant Id** field in CloudWisdom.
![tenant-id](/images/onboarding-wizard/tenant-id.png)
12. Select **Continue**.
13. Return to PowerShell and run the following command, replacing *\<subscription-id>* with the **id** value:
`az ad sp create-for-rbac --role "Monitoring Reader" --name CloudWisdomReader --scopes /subscriptions/<subscription-id>`
14. Copy and paste the **appId** value into the **Client ID** field.
15. Copy and paste the **password** value into the **Access Key** field.
16. Select **Continue**.
17. Optionally [Enable Guest OS Diagnostic Metrics][5].
18. Select **Continue**.
19. Select **Confirm & Finish**.

### Via Azure Portal

1. Log in to **CloudWisdom**. You are automatically directed to the Onboarding Wizard.
2. Select **Begin Setup** > **Setup Azure Cloud**.
3. Select **Continue With the Azure Portal**.
4. **Azure Tab**: Open the [Azure Portal](https://portal.azure.com/) in a separate tab and log in.
5. **Azure Tab**: Navigate to **App Registrations** via search or **Active Directory** > **App Registrations**.
5. **CloudWisdom Tab**: Select **Continue**.
6. **Azure Tab**: Select **+ New registration**.
7. **Azure Tab**: Input and select the following:
   - **Name**: `cloudwisdom-integration`
   - **Supported account types**: Accounts in this organizational directory only - Single tenant
   - **Redirect URI (optional)**: `https://us.cloudwisdom.virtana.com`
8. **Azure Tab**: Select **Register**. You are re-routed to your new apps overview page.
![azure-setup-portal](/images/onboarding-wizard/azure-setup-portal.png)
9. **CloudWisdom Tab**: Select **Continue**.
10. **Azure Tab**: Copy and paste the following into the CloudWisdom's Onboarding Wizard:
   - **Application (client) ID**: maps to Client ID
   - **Directory (tenant) ID**:  maps to Tenant ID
![azure-setup-vid](/images/onboarding-wizard/AZ new gif.gif)
11. **CloudWisdom Tab**: Select **Continue**.
12. **Azure Tab**: Select **Certificates & secrets** > **New client secret**.
13. **Azure Tab**: Describe the secret, set an expiration, and select **Add**.
14. **Azure Tab**: Copy the secret value from the **Client secrets** section.
15. **CloudWistom Tab**: Select **Continue**.
16. **CloudWistom Tab**: Paste the secret in the **Access Key** field.
17. **Azure Tab**: Navigate to your app's **API Permissions**.
18. **Azure Tab**: Select **Add a permission** > **Azure Service Management**.
19. **CloudWisdom Tab**: Select **Continue**.
20. **Azure Tab**: Select **Delegated Permissions** and enable **user_impersonation**.
21. **Azure Tab**: Select **Add Permissions**.
![api-perms](/images/onboarding-wizard/api-perms.png)
22. **CloudWisdom Tab**: Select **Continue**.
23. **Azure Tab**: Navigate to **Home** > **Subscriptions** and select the subscription your app belongs to.
24. **Azure Tab**: Navigate to **Resource providers** and serach for `microsoft.insights`.
25. **Azure Tab**: Select the **microsoft.insights** row and then select **Register**. This may take a few seconds.
26. **CloudWisdom Tab**: Select **Continue**.
27. **Azure Tab**: Navigate to **Access Control (IAM**) and select **+Add** > **Add role assignment**. Complete the following fields:
  - **Role**: Reader
  - **Assign access to**: Azure AD user, group, or service principal
  - **Select**: Enter the name of your Active Directory application and select the app.
28. **Azure Tab**: Select **Save**.
29. **Azure Tab**: Return to your subscription's **Overview** page and copy the **Subscription ID**.
30. **CloudWisdom Tab**: Paste the ID into the **Subscription ID** field. Select **Validate**.
31. **CloudWisdom Tab**: Select **Continue**.
32. **CloudWisdom Tab**: [Enable guest metrics (optional)][8]. Select **Continue**.
33. **CloudWisdom Tab**: Select **Confirm & Finish**.


[1]:/integrations/aws-integration/aws-cur/
[2]:/integrations/aws-integration/#prerequisite-enable-cost-explorer
[3]:/integrations/
[4]: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest
[5]: /integrations/microsoft-azure/azure-enable-guest-os-diagnostic/
[6]: /getting-started/onboarding-wizard/#configure-aws
[7]: /getting-started/onboarding-wizard/#configure-azure
[8]: /integrations/microsoft-azure/azure-enable-guest-os-diagnostic/
