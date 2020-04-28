---
title: "Enable Guest OS Diagnostic Metrics"
#date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#optional config"]
author: Lawrence Lane
---

Azure Virtual Machines have a subset of core metrics by default. However, guest OS diagnostic metrics are needed for CloudWisdom's Azure cost reports. To enable guest OS diagnostic metrics, you’ll need to follow the steps below.

## Enable Guest OS Diagnostic Metrics on an Existing VM
1. In Azure, navigate to **Virtual machines**.
2. Select a virtual machine. Another window with options will open.
3. Select **Diagnostic settings** under *Monitoring*.
4. Choose one of the existing Diagnostic storage accounts or create a new one. Note: Additional charges in Azure may apply.
5. Select the **Enable guest-level monitoring** button.


{{% notice info %}}
This operation can take a few minutes to complete.
{{% /notice %}}

## Enable Guest OS Diagnostic Metrics on a New VM
1. In Azure, navigate to **Virtual machines**.
2. At the top of the _Virtual machines_ window, click **Add**.
3. Complete steps 1-3 (*Basics*, *Disks*, *Networking*)
4. In step 4, under _Management_, set **OS guest diagnostics** to "On". Choose one of the existing Diagnostic storage accounts or create a new one. Note: Additional charges in Azure may apply.
5. Finish creating the VM.
