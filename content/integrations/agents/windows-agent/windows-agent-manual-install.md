---
title: "Manual Install"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", "#install"]
author: Lawrence Lane
---

## Manually Install the Windows Agent
1. Download the latest [Windows Agent](https://repos.app.metricly.com/windows-agent/index.html). Ensure you download the correct version for your environment.
2. Run the setup wizard and follow the instructions to install it.
3. Navigate to the** WriteNetuitive.config** file (`C:\Program Files\CollectdWin\config` or `C:\Program Files (x86)\CollectdWin\config` depending on your environment.
4. Open the file and locate the line `<WriteNetuitiveURL="https://api.app.metricly.com/ingest/windows/{apikey}" />`.
5. Replace **{apikey}** in the URL with the API key generated in step 1.
6. **Save** the file and **restart** the agent.

## Manually Update Host Name

1. After downloading the Windows agent, open the **CollectdWin.config** file.
2. At the top of the file, update the Hostname setting to the desired value.

```
<GeneralSettings Interval="60" Timeout="120"
StoreRates="false" Hostname="" />
```

3\. **Save** the file.
4. Restart the **CollectdWin** service (if currently running).