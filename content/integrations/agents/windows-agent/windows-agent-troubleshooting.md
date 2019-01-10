---
title: "Troubleshooting"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", ]
author: Lawrence Lane
---

- Logs are written to **C:\ProgramData\CollectdWin\CollectdWin.log** by default.
- Errors are written to the **Event Log**.

To adjust the log file level, edit the line below near the end of the CollectdWinService.exe.config:

1. Navigate to `C:\Program Files\CollectdWin\config` or `C:\Program Files (x86)\CollectdWin\config`.
2. Edit`<logger name="*" writeTo="default" minlevel="[Trace/Debug/Info/Warn/Error/Fatal]" />`.
3. **Save** file.

## Windows Server 2003
If you are monitoring a Windows Server 2003 instance and are having trouble seeing data in Metricly, you may need to install a hotfix from Microsoft. In August 2016, AWS disabled an SSL cipher in their standard ELB policy that was the last supported SSL cipher that comes with Windows Server 2003 by default. Microsoft has created a hotfix (Windows Server 2003 R2 32Bit and 64Bit) to add more modern ciphers to your OS, which will fix the issue. The hotfix can be found [here](https://support.microsoft.com/en-gb/kb/948963).

{{% notice info %}}
Versions of the Windows Agent later than v0.7.4.55 do not support Windows Server 2003.
{{% /notice %}}
