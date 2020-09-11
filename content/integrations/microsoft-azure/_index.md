---
title: "Microsoft Azure"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations"]
author: Lawrence Lane
---

Microsoft Azure is a cloud computing platform, similar to Amazon Web Services. With the Azure integration in CloudWisdom, you can manage and optimize the cost of your entire cloud infrastructure. CloudWisdom requires Reader role permissions of your Azure environment, which can be granted using the Owner or User Access Administrator roles.

{{% notice tip %}}
If your Azure account is enrolled in an EA (Enterprise Administrator) setup, please ensure the "AO view charges" setting is enabled so assets within subscriptions have access to cost data. See [Azure's documentation](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/enterprise-mgmt-grp-troubleshoot-cost-view) for how to confirm it's enabled.
{{% /notice %}}

## Installation Methods
1. [CLI Method][1]
2. [Azure Portal Method][2]

## Optional Config
1. [Guest OS Diagnostic Metrics][3]


[1]:/integrations/microsoft-azure/azure-cli-installation
[2]:/integrations/microsoft-azure/azure-installation
[3]:/integrations/microsoft-azure/azure-enable-guest-os-diagnostic
