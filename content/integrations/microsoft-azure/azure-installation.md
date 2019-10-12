---
title: "Azure Installation"
#date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#installation"]
author: Lawrence Lane
---
## 1. Create a Microsoft Azure Integration Card in Metricly
1. Login to Metricly.
2. Select **Integrations**.
2. Select the **Microsoft Azure** card.
![microsoft-azure](/images/azure-installation/microsoft-azure.png)
3. In a separate, new tab, open the [Azure portal](https://portal.azure.com/).

## 2. Create an Active Directory Application in Azure
1. Once in the Azure portal, select **Azure Active Directory** from the left side menu.
![azure-active-directory](/images/azure-installation/azure-active-directory.png)
2. Select **App registrations** from the Manage options.
![app-registrations](/images/azure-installation/app-registrations.png)
3. Select **+ New Registration** at the top.
![new-registration](/images/azure-installation/new-registration.png)
4. Provide a name for the application (e.g., `Azure-Metricly-Integration`).
4. Select **Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts** for Supported Account Types.
5. Select **Web** and input `https://app.metricly.com` for the **Redirect URI URL**.
![redirect-uri-url](/images/azure-installation/redirect-uri-url.png)
6. Select **Register** at the bottom of the window.

## 3. Get the Application ID, Application Key, & Tenant ID from Azure

Once you have completed part 2, you are redirected to the `Azure-Metricly Integration`'s overview page.

1. Copy the **Application ID** (also known as the **Client ID**).
2. Return to the tab with Metricly open. Paste it into the _Client ID_ field. Once it’s pasted, return to the Azure tab.
![azure-app-id](/images/azure-installation/azure-app-id.png)
3. Select **Certificates & secrets**.
![certs-secrets](/images/azure-installation/certs-secrets.png)
4. Select **+ New client secret**
5. Provide a **description** and select an **Expiration** for the key.
![add-desc-expiration](/images/azure-installation/add-desc-expiration.png)
6. Select **Add**. The Secret is now listed in the **Client secrets** section.
7. Copy the secret's Value and return to the tab with Metricly open. Paste it into the **Access Key** field. Once it’s pasted, return to the Azure tab.
![copy-secret-value](/images/azure-installation/copy-secret-value.png)
8. Return to Azure and select **Overview**.
9. Copy the **Directory(tenant)ID**. Open your Metricly tab and paste the ID into the **Tenant ID** field.
![tentant-id](/images/azure-installation/tentant-id.png)

Return to the Azure tab once you have added the Directory (Tenant) ID to your Metricly integration.

## 4. Set Delegated Permissions in Azure
1. In Azure, navigate to the **API Permissions** section of your `Azure-Metricly-Integration`.
![api-permissions](/images/azure-installation/api-permissions.png)
2. Select **+ Add a permission**. A side panel appears.
3. Select the **Azure Service Management** card.
![azure-service-management](/images/azure-installation/azure-service-management.png)
4. Select **Delegated Permissions**.
5. Enable the **user_impersonation** permission.
![user-impersonation](/images/azure-installation/user-impersonation.png)
6. Select **Add permissions**.

## 5. Collect Subscription ID and Set Role

To assign a role to the application, you’ll need the **Owner** or **User Access Administrator** role in Azure (the Contributor role will not work) or a custom role that grans write access for `Microsoft.Authorization`.

1. Navigate to **Home** > **Subscriptions** in Azure.
2. Copy the **Subscription ID** and return to the tab with Metricly open. Paste it into the appropriate field. Once it’s pasted, return to the Azure tab.
![copy-subscription-id](/images/azure-installation/copy-subscription-id.png)
3. Navigate to this subscription's **Access Control (IAM)** tab.
![access-control-tab](/images/azure-installation/access-control-tab.png)
4. Select **Add** > **Add role assignment**. A side panel appears.
![add-role-assignment](/images/azure-installation/add-role-assignment.png)
5. Complete the following fields:
 - **Role**: Reader
 - **Assign access to**: App service
 - **Subscription**: Select the same subscription from step 2.
 - **Select**: the Metricly app you created.
6. Select **Add**.

After permissions have been set, return to Metricly to include or exclude as many Azure element types as you want. **Azure VM and Azure Application Gateway are enabled by default**.

Optionally, filter elements.

## Use with Agents

If you install our Linux agent or Windows agent on an Azure VM, the VM’s power state (attribute `hostRunning` with a value of `true` or `false`) and tags are copied over to the corresponding Linux `SERVER` element / Windows `WINSRV` element. You can then use this information to create [policies][1].

[1]: /alerts-notificaitons/policies
