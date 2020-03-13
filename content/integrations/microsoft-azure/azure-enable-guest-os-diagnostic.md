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
4. Under _Configure metrics_, select the checkbox next to **Basic metrics**. CloudWisdom will now receive the basic VM metrics.

## Enabling basic metrics on a new VM
1. In Azure, navigate to **Virtual machines**.
2. At the top of the _Virtual machines_ window, click **Add**.
3. Select the type and create the instance.
4. In Step 3, under _Management_, enable **Guest OS diagnostics**. Choose one of the existing Diagnostic storage accounts or create a new one. Note: additional charges may apply by Azure.
5. Finish creating the VM. The basic metrics are now available in CloudWisdom (just give it a few minutes to appear).
