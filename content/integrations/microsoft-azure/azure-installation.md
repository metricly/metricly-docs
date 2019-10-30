---
title: "Azure Installation"
#date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#installation"]
author: Lawrence Lane
---
## 1. Create a Microsoft Azure Integration Card
1. From the top navigation menu, select **Integrations**.
2. Click the **Microsoft Azure** card.
3. In a separate, new tab, open the [Azure portal](https://portal.azure.com/).

{{% notice info %}}
The following instructions were created using the Azure portal not the classic portal. Instructions vary depending on which portal you’re using.
{{% /notice %}}

## 2. Create an Active Directory Application in Azure
1. Once in the Azure portal, click **Azure Active Directory** from the left side menu.
2. Click the **App registrations** widget.
3. Click **Add** at the top. A _Create_ window will open.
4. Type the name of the application. We recommend Azure / CloudWisdom Integration, or something similar.
4. Ensure the Application Type is **Web app / API**.
5. Input `https://us.cloudwisdom.virtana.com` for the **Sign-on URL**.
6. Click **Create** at the bottom of the window.

## 3. Get the Application ID, Application Key, & Tenant ID
1. Select your new application from the _App registrations_ list. The application’s Essentials and Settings windows open.
2. Copy the **Application ID** (also known as the **Client ID**) and return to the tab with CloudWisdom open. Paste it into the _Client ID_ field. Once it’s pasted, return to the Azure tab.
3. From the _Settings_ window, click **Keys**.
4. In the _Keys_ window, add a `description` for the key.
5. Select a duration for the key.
6. Click **Save** at the top of the Keys window.
7. Copy the Key’s Value and return to the tab with CloudWisdom open. Paste it into the **Access Key** field. Once it’s pasted, return to the Azure tab.
8. Return to the App registrations window and click **Endpoints**.
9. From the list of endpoints, you’ll notice your `Tenant ID` in each of the URLs. Copy the `Tenant ID` from one of the endpoints and return to the tab with CloudWisdom open. Paste it into the **Tenant ID** field. Once it’s pasted, return to the Azure tab.

## 4. Set Delegated Permissions
1. Open the application’s settings window and click **Required permissions**.
2. Click **Add** at the top of the _Required permissions_ window.
3. In the _Add API access_ window, click **step 1. Click Windows Azure Service Management API**, then click **Select** at the bottom of the _Select an API_ window.
4. Click step **2** and select the **Delegated Permissions** checkbox, then click **Select** at the bottom of the _Enable Access_ window.
{{% notice tip %}}
After selecting the Delegated Permissionscheckbox, you may have to clear and then select the Access Azure Service Management as organization users (preview) checkbox again to activate the Select button.
{{% /notice %}}
5. Click **Done** in the _Add API access_ window.

## 5. Collect Subscription ID and Set Role

To assign a role to the application, you’ll need the Owner or User Access Administrator role in Azure (the Contributor role will not work) or a custom role that grans write access for Microsoft.Authorization. You can check your permissions for the subscription by opening the user account menu (top right-hand corner), clicking My permissions, and then selecting the relevant subscription from the drop-down menu. If you don’t have the correct permissions, contact your subscription administrator.

1. Navigate to **Subscriptions** in Azure.
{{% notice tip %}}
If you don’t see Subscriptions in your side menu, click **More services** and search for `Subscriptions` using the filter.
{{% /notice %}}
2. Copy the **Subscription ID** and return to the tab with CloudWisdom open. Paste it into the appropriate field. Once it’s pasted, return to the Azure tab.
3. Click the appropriate subscription.
4. Click **Access Control (IAM)**.
5. Click **Add**.
6. Select Reader for the role.
7. Search for the application you created in Step 1, and select it. Click **Select** at the bottom of the window.

After permissions have been set, return to CloudWisdom to include or exclude as many Azure element types as you want. **Azure VM and Azure Application Gateway are enabled by default**.

Optionally, filter elements.

## Use with Agents

If you install our Linux agent or Windows agent on an Azure VM, the VM’s power state (attribute `hostRunning` with a value of `true` or `false`) and tags are copied over to the corresponding Linux `SERVER` element / Windows `WINSRV` element. You can then use this information to create [policies][1].

[1]: /alerts-notificaitons/policies
