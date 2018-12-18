---
title: "Windows Agent"
#date: 2018-12-11
draft: false
tags: ["windows", "integrations", "agents"]
author: Lawrence Lane
---

The Metricly Windows Agent is a Microsoft Windows service that collects, aggregates, and publishes windows performance counters and attributes. Microsoft SQL Server, IIS, and .NET metrics are native to our Windows Agent. Only one Windows integration in your account is necessary to receive all Windows-related metrics.

## Configure
Installation is as easy as [executing an MSI installer](https://repos.app.netuitive.com/windows-agent/index.html) and configuring the service. The agent is pre-configured to send the most important performance metrics, windows events, and system attributes to Metricly. It can also be configured to send additional or different data if required

### 1. Copy the API key
1. In Metricly, click **Integrations** on the top-nav bar.
2. Search for and click the **Windows Server** card. The name should be already populated, and Data Collection should be enabled. A unique API key for your account has already been generated.
3. Copy the **API key**.

### 2. Install the Windows Agent
If you install our Windows agent on an AWS EC2 or Azure VM, the EC2’s / VM’s power state (it will come in as the attribute `hostRunning` with a value of true or false) and tags are copied over to the corresponding Windows WINSRV element. You can then use this information to create policies.

1. Download the latest [Windows agent](https://repos.app.netuitive.com/windows-agent/index.html). Ensure you download the correct version for your environment.
2. Open a command line interface and change to the directory you downloaded the Windows agent to.
3. Run the following command:

```
msiexec /quiet /package CollectdWin-x64.msi NETUITIVE_API_KEY=my_api_key
```
- **my_api_key** is the unique API key generated for your account that you copied in step 1.

### 3. Set up a proxy (Optional)
Optionally, if you have a web proxy in your environment, you may need to configure the agent to use it.

### 4. Start the agent
1. Open the **Windows Service Control Manager**.
2. Select the **CollectdWinService**.
3. Start the service.

If the service is already running, you’ll need to restart it for any configuration changes to take effect.
