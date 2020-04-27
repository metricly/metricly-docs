---
title: "Azure Portal"
#date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#installation"]
author: Lawrence Lane
---

{{% notice tip %}}
Virtana recommends using the [Azure CLI](/integrations/microsoft-azure/azure-cli-installation) for the best integration experience. 
{{% /notice %}}

## 1. Contact the CloudWisdom Sales Team
1. Contact [CloudWisdom Sales](mailto:dl-sales-metricly@virtualinstruments.com) to get a link for accessing the new Azure integration page.
2. Wait for an email containing the link.
3. Once you receive the link, open it in a new tab.

## 2. Create an Active Directory Application in Azure

1. In a separate tab, open the [Azure portal](https://portal.azure.com/) and select **Azure Active Directory** from the left or top menu.
![azure-active-directory](/images/azure-installation/azure-active-directory.png)
2. Select **App registrations** from the Manage options.
![app-registrations](/images/azure-installation/app-registrations.png)
3. Select **+ New Registration** at the top.
![new-registration](/images/azure-installation/new-registration.png)
4. Provide a name for the application (e.g., `CloudWisdom-Integration`).
5. Select **Accounts in this organizational directory only (Default Directory only - Single tenant)** for Supported Account Types.
6. Find the **Redirect URI (optional)** section. Select **Web** and input `https://us.cloudwisdom.virtana.com`.
![redirect-uri-url](/images/azure-installation/redirect-uri-url.png)
7. Select **Register** at the bottom of the window.

## 3. Get the Application ID, Application Key, & Tenant ID from Azure

Once you have completed part 2, you are redirected to the `CloudWisdom-Integration`'s overview page.

1. Copy the **Application (client) ID** and paste the ID into the _Client ID_ field in CloudWisdom. Then Copy the **Directory (tenant) ID** and paste it into the **Tenant ID** field.
![ids](/images/azure-installation/ids.png)
3. Select **Certificates & secrets**.
![certs-secrets](/images/azure-installation/certs-secrets.png)
4. Select **+ New client secret**
5. Provide a **description** and select an **Expiration** for the key.
![add-desc-expiration](/images/azure-installation/add-desc-expiration.png)
6. Select **Add**. The Secret is now listed in the **Client secrets** section.
7. Copy the secret's Value and return to the tab with CloudWisdom open. Paste it into the **Access Key** field. Once it’s pasted, return to the Azure tab.
   - **Note**: the access key is only shown in the Azure portal for a few minutes.
![copy-secret-value](/images/azure-installation/copy-secret-value.png)

## 4. Set Delegated Permissions in Azure
1. In Azure, navigate to the **API Permissions** section of your `CloudWisdom-Integration`.
![api-permissions](/images/azure-installation/api-permissions.png)
2. Select **+ Add a permission**. A side panel appears.
3. Select the **Azure Service Management** card.
![azure-service-management](/images/azure-installation/azure-service-management.png)
4. Select **Delegated Permissions**.
 - **Note**: Granting delegated permissions authorizes the registered application (CloudWisdom) to make requests to the Azure API only. Details of what data can be read is configured in the next step.
5. Enable the **user_impersonation** permission.
![user-impersonation](/images/azure-installation/user-impersonation.png)
6. Select **Add permissions**.

## 5. Collect Subscription ID and Set Role

To assign a role to the application, you’ll need the **Owner** or **User Access Administrator** role in Azure (the Contributor role will not work) or a custom role that grants write access for `Microsoft.Authorization`.

1. Navigate to **Home** > **Subscriptions** in Azure.
2. Select the **Subscription Name** your new app belongs to. {{% notice tip %}}
While here, ensure the **microsoft.insights** resource provider is registered as it's needed to gather performance metrics for your Azure objects.
![enable-microsoft-insights](/images/azure-installation/enable-insights.png){{% /notice %}}

3. Copy the **Subscription ID** and return to the tab with CloudWisdom open. Paste it into the appropriate field. Once it’s pasted, return to the Azure tab.
![copy-subscription-id](/images/azure-installation/copy-subscription-id.png)
4. Navigate to this subscription's **Access Control (IAM)** tab.
![access-control-tab](/images/azure-installation/access-control-tab.png)
5. Select **Add** > **Add role assignment**. A side panel appears.
![add-role-assignment](/images/azure-installation/add-role-assignment.png)
6. Complete the following fields:
 - **Role**: Reader
 - **Assign access to**: Azure AD user, group, or service principal
 - **Select**: Enter the name of the app you created in section 2 and select the app.
7. Select **Save**.

 - **Note**: You can verify the permissions by selecting Role Assignments and searching for the CloudWisdom application.

8. Return to CloudWisdom, verify each field has been filled in accurately, and then click the **Save** button.

{{% notice info %}}
Follow the instructions on [Guest OS Diagnostic Metrics] (https://docs.metricly.com/integrations/microsoft-azure/azure-enable-guest-os-diagnostic/) to enable guest OS diagnostic metrics on your VMs. These metrics are required for CloudWisdom's Azure cost reports.
{{% /notice%}}
