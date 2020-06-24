---
title: "Azure CLI"
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#installation"]
author: Lawrence Lane
---
This installation method is recommended by Virtana for setting up your Azure integration with CloudWisdom.

## 1. Install the Azure CLI
1. [Download the Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest) (Windows 10 users may have this already installed and available through the Windows PowerShell).
2. Install the CLI.

## 2. Obtain Azure Credentials

Use the CLI to obtain your Azure Client ID, Password, Subscription ID, and Tenant ID. All of these values must be provided to set up an Azure integration within CloudWisdom.

1. Open the Windows PowerShell (or any command line shell).
2. Use the command `az login`. This prompts a browser sign-in request to Azure.
3. Return to the CLI.
4. Save the following account values:
   - **TenantId**: Used for the Tenant ID in CloudWisdom.
   - **Id**: Used for the Subscription ID in CloudWisdom.
![azure-cli](/images/azure-cli-installation/azure-cli.png)
5.  Run the following command to create read permissions for CloudWisdom in Azure adding in your id for **subscription-id** :
```
az ad sp create-for-rbac --role "Monitoring Reader" --name CloudWisdomReader --scopes /subscriptions/<subcription-id>
```
6. Save the following values:
 - **appId**: Used for the Client ID in CloudWisdom.
 - **password**: Used for the Access Key in CloudWisdom.
![azure-read-permissions](/images/azure-cli-installation/azure-read-permissions.png)

## 3. Create Azure Integration in CloudWisdom

1. Open **CloudWisdom** in a separate tab.
2. Navigate to **Integrations** > **Microsoft Azure**.
3. Use the Azure IDs provided in the CLI to set up the integration.
![save-azure-integration](/images/azure-cli-installation/save-azure-integration.png)
4. **Save**.

You can review the app from your Azure Portal by following [this link](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) and navigating to the **All applications** tab.

![cw-app-az-portal](/images/azure-cli-installation/cw-app-az-portal.png)

{{% notice info %}}
Follow the instructions on [Guest OS Diagnostic Metrics] (https://docs.metricly.com/integrations/microsoft-azure/azure-enable-guest-os-diagnostic/) to enable guest OS diagnostic metrics on your VMs. These metrics are required for CloudWisdom's Azure cost reports.
{{% /notice%}}
