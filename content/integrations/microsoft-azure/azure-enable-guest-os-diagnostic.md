---
title: "Enable Guest OS Diagnostic Metrics"
#date: 2018-12-11
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#microsoft", "#azure", "#integrations", "#optional config"]
author: Lawrence Lane
---

Azure Virtual Machines will share boot diagnostic metrics by default, which are a small subset of core metrics. To enable Guest OS diagnostic (basic) metrics that provide more information about your machine, you’ll need to follow these steps (depending on your situation):

## Enable Basic Metrics on Existing VM
1. In Azure, navigate to **Virtual machines**.
2. Select a virtual machine. Another window with options will open.
3. Select **Diagnostic settings**.
4. Choose one of the existing Diagnostic storage accounts or create a new one. Note: Additional charges in Azure may apply.
5. Click the **Enable guest-level monitoring** button
6. Under _Metrics_, ensure **Basic** is selected and all the metrics underneath are checked. 
7. Click the **Save** button. 

CloudWisdom will begin showing basic VM metrics after a few minutes.

## Enabling basic metrics on a new VM
1. In Azure, navigate to **Virtual machines**.
2. At the top of the _Virtual machines_ window, click **Add**.
3. Select the type and create the instance.
4. In Step 4, under _Management_, set **OS guest diagnostics** to "On". Choose one of the existing Diagnostic storage accounts or create a new one. Note: Additional charges in Azure may apply.
5. Finish creating the VM. 

CloudWisdom will begin showing basic VM metrics after a few minutes.
