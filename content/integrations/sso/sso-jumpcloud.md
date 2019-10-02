---
title: "JumpCloud SSO"
#date: 2018-12-11
draft: false
tags: ["#sso", "#integrations", "#authentication", "#jumpcloud"]
author: Lawrence Lane
weight: 2
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

Keep this tab open and open a new tab; you must now login to JumpCloud and upload the certificate.

## 2. Create New Application in JumpCloud
1. Log into **JumpCloud** as an administrator.
{{% notice tip %}}
 Login page _must_ say **JumpCloud Administrator Login** and _not_  **JumpCloud User Login**.
{{% /notice %}}
2. Navigate to **Applications** > **+** (New Application). A slide-out panel appears.
![jc-new-application](/images/sso-jumpcloud/jc-new-application.png)
3. Search for `SAML` and select **Custom SAML App** > **Configure**.
4. Input the following values:
  - **DISPLAY LABEL**: `Your SSO Label` ("A name of your choosing to identify this configuration.)
  - **IDP ENTITY ID**: `jumpcloud-metricly`
  - **SP ENTITY ID**: `netuitive-api`
  - **ACS URL**: `https://app.metricly.com/saml/SSO`
  - **SP CERTIFICATE**:  Upload the .`cert` file from section 1.
  - **SAMLSUBJECT NAMEID**: `email`
  - **SAMLSUBJECT NAMEID FORMAT**: `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`
5. Create **USER ATTRIBUTES** for the following:
  - **email**: `email`
  - **firstName**: `firstname`
  - **lastName**: `lastname`
  - **role**: `Read Only`
6. Add your tenant name to the **Default Relay State** field if you do not want to enter it when logging into Metricly from JumpCloud. Your tenant name is the company name you used when you signed up for a Metricly account. Contact support if you do not know your tenant name.
![jc-relay-state](/images/sso-jumpcloud/jc-relay-state.png)
7. **Save** your new SSO application.

  {{% notice tip %}}
Be careful not to accidentally create your **USER ATTRIBUTES** (green) under **CONSTANT ATTRIBUTES** (red).
![jc-user-attributes-tip](/images/sso-jumpcloud/jc-user-attributes-tip.png)
{{% /notice %}}

Now you are ready to download your certificate and metadata to be uploaded to Metricly.

### Download IDP Certificate & Export Metadata
1. Expand the **IDP Certificate Valid** menu on the left of the app.
2. Select **Download certificate**
![jumpcloud-download-certificate](/images/sso-jumpcloud/jumpcloud-download-certificate.png)
3. Scroll to the bottom of the app's settings and select **export metadata**.
![jumpcloud-export-metadata](/images/sso-jumpcloud/jumpcloud-export-metadata.png)

You are now ready to import your JumpCloud certificate and metadata to Metricly.

## 3. Finish SSO Set-up in Metricly

1. Navigate to **Account Profile** > **SSO**.
2. Upload the **IDP Certificate** file from JumpCloud.
2. Upload the **Metadata.xml** file from JumpCloud.
![upload-metadata-xml](/images/_index/upload-metadata-xml.png)
2. When finished, it should look like this:
![metricly-sso-complete](/images/sso-azure/metricly-sso-complete.png)


## Login URLs

- **login URL:** `https://app.metricly.com/#/login?sso=true`
- **login URL (tenant name pre populated):** `https://app.metricly.com/#/login?sso=true&tenantName=Your+Tenant+Name`
