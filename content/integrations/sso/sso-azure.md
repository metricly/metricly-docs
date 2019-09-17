---
title: "Azure SSO"
#date: 2018-12-11
draft: false
tags: ["#sso", "#integrations", "#authentication", "#azure"]
author: Lawrence Lane
weight: 1
---

{{% alert success %}}
Single Sign-On (SSO) is a **paid-only feature**. Wish to upgrade? Contact your [Sales Representative](mailto:sales@metricly.com).
{{% /alert %}}

## 1. Generate a Certificate in Metricly

1. Navigate to **Account Profile** > **SSO**.
2. Select **Generate**.
![generate](/images/_index/generate.png)
3. Copy the generated certificate and use it to create a `.cert` file.
4. Select **Continue**.

Keep this tab open and open a new tab; you must now login to Azure and upload the certificate.

## 2. Create New Application in Azure

1. Log into **Azure** as an administrator.
2. Navigate to **Azure Active Directory** > **Enterprise Applications**.
![azure-enterprise-applications](/images/sso-azure/azure-enterprise-applications.png)
3. Select **+ New Application**.
![azure-new-application](/images/sso-azure/azure-new-application.png)
4. Select **Non-Gallery Application** and name your SSO application.
![azure-non-gallery-application](/images/sso-azure/azure-non-gallery-application.png)
5. `Name` your SSO application and select **Add**.
![azure-name-add-application](/images/sso-azure/azure-name-add-application.png)
6. Select **Configure single sign-on (required)**.
![azure-configure-sso-required](/images/sso-azure/azure-configure-sso-required.png)
7. Select **SAML** for the single sing-on method.
![azure-saml-method](/images/sso-azure/azure-saml-method.png)

You are now ready to define your new SSO application's SAML and user settings. If you need to return to these settings in the future, follow this path: **Azure Active Directory** > **Enterprise applications** > `Your Application Name` > **Single sign-on** > **SAML-based Sign-on**.

### Upload Certificate From Metricly To Azure SAML SSO Application

1. Select **Upload metadata file**.
![azure-upload-cert](/images/sso-azure/azure-upload-cert.png)
2. Upload the `.cert` file created in Metricly from the first step.

### Define Azure SAML SSO Configuration

1. Select **Edit** on the Basic SAML Configuration card. A slide-out panel appears.
![azure-edit-basic-saml](/images/sso-azure/azure-edit-basic-saml.png)
2. Input the following values:
  - **Identifier (Entity ID)**: `netuitive-api`
  - **Reply URL (Assertion Consumer Service URL)**: `https://app.metricly.com/saml/SSO`
  - **Sign on URL**: `https://app.metricly.com/saml/SSO`
  - **Relay State**: `Your Tenant Name` (optional)

  {{% notice tip %}}
  Add your tenant name to the **Relay State** field if you do not want to enter it when logging into Metricly from Azure. Your tenant name is the company name you used when you signed up for a Metricly account. Contact support if you do not know your tenant name.
  {{% /notice %}}

### Define User Attributes & Claims
1. Select **Edit** on the User Attributes & Claims card.
2. Select **+ Add new claim**.
![azure-add-new-claims](/images/sso-azure/azure-add-new-claims.png)
3. Add the following claims:
  - **email**: `user.mail`
  - **firstName**: `user.givenname`
  - **lastName**: `user.surname`
  - **role**:  `"Read Only"`

  {{% notice tip %}}
  The **role** claim attribute can also be set to `"Administrator"`, however this makes all SSO users administrators in Metrcly. We recommend updating your administrator accounts individually and leaving the default role to `Read Only`.
  {{% /notice %}}

### Define & Download SAML Signing Certificate

1. Select **Edit** on the SAML Signing Certificate card.
2. Select the following dropdowns:
  - **Singing Option**: `Sign SAML Assertion`
  - **Signing Algorithm**: `SHA-256`
3. Download the **Certificate (Base64)**.
4. Download the **Federation Metadata XML**.
![azure-download-cert](/images/sso-azure/azure-download-cert.png)

These files must be uploaded to Metricly.

## 3. Finish SSO Set-up in Metricly

1. Navigate to **Account Profile** > **SSO**.
2. Upload the **Certificate (Base64)** file from JumpCloud.
2. Upload the **Federation Metadata.xml** file from JumpCloud.
![upload-metadata-xml](/images/_index/upload-metadata-xml.png)
2. When finished, it should look like this:
![metricly-sso-complete](/images/sso-azure/metricly-sso-complete.png)

## Login URLs

- **login URL:** `https://app.metricly.com/#/login?sso=true`
- **login URL (tenant name pre populated):** `https://app.metricly.com/#/login?sso=true&tenantName=Your+Tenant+Name`
