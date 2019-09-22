---
title: "Upgrade Agent"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", "#install"]
author: Lawrence Lane
---
To upgrade the Windows agent, follow the installation steps listed on the main Windows Integration page using the version of the agent you wish to upgrade to. The latest versions of the agent can be downloaded from the [agent repo](https://repos.app.netuitive.com/windows-agent/index.html) and details of the releases can be found on the [Github project page](https://github.com/Netuitive/netuitive-windows-agent).

{{% notice info %}}
Installing a new version of the agent will overwrite changes you have made to existing agent configuration files located in `C:\Program Files\CollectdWin\config` or `C:\Program Files (x86)\CollectdWin\config` depending on your environment. To preserve those changes, it is recommended you create backups of the files prior to upgrading.
{{% /notice%}}

## Check Version

You may need the verify the version of the Windows agent you’re currently using.

1. Open the [Element Detail panel][1] for a WINSRV element.
2. Navigate to **Attributes** (squared in green).
3. Verify that the **agent** (squared in blue) contains the correct version number.

![step 2-3](/images/windows-agent-check-version/step-2-3.png)


[1] :/capacity-monitoring/inventory
