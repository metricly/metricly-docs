---
title: "SSO"
#date: 2018-12-11
draft: false
tags: ["#sso", "#integrations", "#authentication", "#okta"]
author: Lawrence Lane
---

## 1. Generate a Certificate in Metricly

1. Navigate to **Account Profile** > **SSO**.
2. Click **Generate**.
![generate](/images/_index/generate.png)
3. Copy the generated certificate and use it to create a `.cert` file.
4. Click **Continue**. Keep this tab open and open a new tab; you must now go to your SSO provider and upload the certificate. Each provider will be slightly different.

## 2. Link to your SSO Provider & Download Certificate (Public Key)

1. Log into **Okta** as an administrator and navigate to _Applications_.
2. Click **Add Application**.
3. Click **Create New App**.
4. Select **Web** in the _Platform_ dropdown and then choose **SAML 2.0**;  click **Create**.
5. Type an `App name` and upload a logo (if desired). Leave the App visibility options as they are.
6. Click **Next**.
7. For the Single sign on URL, use `https://app.metricly.com/saml/SSO` and leave **Use this for Recipient URL and Destination URL** checkmarked.
8. For the **Audience URI (SP Entity ID)**, use `netuitive-api`.
9. For **Name ID format**, select **EmailAddress**. Leave Application username as the default, and click **Show Advanced Settings**.
10. Under the Advanced Settings:
  - Select **Encrypted** for **Assertion Encryption.**
  - Upload the certificate you received in Step 1 for the Encryption Certificate setting.
  - Change **Authentication** context class to **X.509 Certificate**.
11. Under the **Attribute Statements** section:
  - In the first default blank attribute, type `firstName` in the **Name field** and `user.firstName` into the **Value field**.
  - Click **Add Another**.
  - In the first default blank attribute, type `lastName` in the **Name field** and `user.lastName` into the **Value field**.
  - Click **Add Another**.
  - In the first default blank attribute, type `email` in the **Name field** and `user.email` into the **Value field**.
  - Click **Add Another**.
  - In the first default blank attribute, type `role` in the **Name field** and `user.role` into the **Value field**  `user.role` must be entered manually and does not appear in the dropdown.
    - Metricly requires administrator access for creating and editing data. To grant administrator privileges enter `user.isMemberOfGroupName("OurAdminGroup") ? 'Administrator' : null` as your role value and replace _OurAdminGroup_ with your group for Metricly Administrators.
    ![add-attributes](/images/_index/add-attributes.png)
12. Click **Next**.
13. Click **Finish**.
14. Click **View Setup Instructions** in your app.
15. Click **Download Certificate** (this is your public key)
16. **Copy** and **save** the metadata as an `XML file`. This is under _Optional_ in Okta.
![optional-metadata](/images/_index/optional-metadata.png)

{{% notice tip %}}
Add your tenant name to the **Default Relay State** field if you do not want to enter it when logging into Metricly from Okta. Your tenant name is the company name you used when you signed up for a Metricly account. Contact support if you do not know your tenant name.
![default-relay-state](/images/_index/default-relay-state.png)
{{% /notice %}}

## 3. Finish SSO Set-up in Metricly

1. Upload the certificate (public key) from Okta.
2. Upload the `metadata.xml` file from Okta.
![upload-metadata-xml](/images/_index/upload-metadata-xml.png)
2. When finished, it should look like this:
![setup-complete](/images/_index/setup-complete.png)

- **login URL:**
`https://app.metricly.com/#/login?sso=true`

- **login URL (tenant name pre populated):**
`https://app.metricly.com/#/login?sso=true&tenantName=Your+Tenant+Name`
