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
