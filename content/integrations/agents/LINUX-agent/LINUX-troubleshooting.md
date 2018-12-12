---
title: "Troubleshooting"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux", "logs", "metadata"]
author: Lawrence Lane
pre: "<i class='fa fa-bug'></i> &nbsp;"
weight: 11
---
##  Set Logs to Debugging Mode
To set the Linux Agent logs to Debugging Mode, update the `netuitive-agent.conf` file.

1. Navigate to the `netuitive-agent.conf` file.
2. `Update level = INFO` to `level = DEBUG`.
3. **Save** and **restart** your agent.

```
# to increase verbosity, set DEBUG
level = DEBUG
handlers = rotated_file
propagate = 1
```

## Need Help?
### 1. Save as Zip File

Copy `/opt/netuitive-agent/bin/get-support` and paste it into your command line interface to zip up your agent configurations, logs, and system metadata. The file will be stored in `/opt/netuitive-agent/`

**Success Message:**
```
Collecting logs and configuration....
creating file....
Please open a support case and upload
/opt/netuitive-agent/support-YYYYMMDD_173454
with a detailed description of the issue.
Thank you
```

### 2. Send Zip to Support

 Open a support ticket by emailing `support@metricly.com` with the file attached and a subject / message body describing the issue(s) you experienced.
