---
title: "Troubleshooting"
#date: 2018-12-11
draft: false
tags: ["windows", "integrations", ]
author: Lawrence Lane
---

- Logs are written to **C:\ProgramData\CollectdWin\CollectdWin.log** by default.
- Errors are written to the **Event Log**.

To adjust the log file level, edit the line below near the end of the CollectdWinService.exe.config:

1. Navigate to `C:\Program Files\CollectdWin\config` or `C:\Program Files (x86)\CollectdWin\config`.
2. Edit`<logger name="*" writeTo="default" minlevel="[Trace/Debug/Info/Warn/Error/Fatal]" />`.
3. **Save** file.

## Windows Server 2003
If you are monitoring a Windows Server 2003 instance and are having trouble seeing data in CloudWisdom, you may need to install a hotfix from Microsoft. In August 2016, AWS disabled an SSL cipher in their standard ELB policy that was the last supported SSL cipher that comes with Windows Server 2003 by default. Microsoft has created a hotfix (Windows Server 2003 R2 32Bit and 64Bit) to add more modern ciphers to your OS, which will fix the issue. The hotfix can be found [here](https://support.microsoft.com/en-gb/kb/948963).

{{% notice info %}}
Versions of the Windows Agent later than v0.7.4.55 do not support Windows Server 2003.
{{% /notice %}}

## Proxy Troubleshooting
### Determining if you have a proxy enabled
1. Open Internet Explorer.
2. Click the **Tools** icon, and then click **Internet Options**.
3. On the Connections tab, click **LAN** settings.
If any of the checkboxes are selected and the appropriate information is filled out, you may need to configure proxy settings to enable data being posted by the agent on your server.

![LAN settings](/images/windows-agent-proxy/lan-settings.png)


### Configuring the proxy
1. Add the following to the end of the **CollectdWinService.exe.config**  file after the _<startup>_ section and before the closing _</configuration>_ tag:

```
<system.net>
<defaultProxy enabled="true" useDefaultCredentials="true">
<proxy/>
</defaultProxy>
</system.net>
```

2\. Replace the **<proxy />** element with one of the options below (corresponding to which option was selected in Internet Explorer).

#### Proxy Options

More information about proxy settings can be found in the [MSDN](https://msdn.microsoft.com/en-us/library/sa91de1e(v=vs.110).aspx).

##### **No Proxy**

![no proxy](/images/windows-agent-proxy/no-proxy.png)

##### **Automatically Detect Settings**
If the Automatically detect settings checkbox was selected, use the following proxy element:
![auto detect settings](/images/windows-agent-proxy/auto-detect-settings.png)

```
<system.net>
 <defaultProxy enabled="true" useDefaultCredentials="true">
   <proxy autoDetect="true" />
 </defaultProxy>
</system.net>
```

##### **Use automatic configuration script**
If the Use automatic configuration script checkbox was selected, use the following proxy element:

![auto config script](/images/windows-agent-proxy/auto-config-script.png)

```
<system.net>
      <defaultProxy enabled="true" useDefaultCredentials="true">
        <proxy scriptLocation="http://www.test.com:1234/sampleScript" />
      </defaultProxy>
    </system.net>
```
Replace `SCRIPT_URI` with the content of the Address text box in the LAN settings window.


##### **Use a proxy server for your LAN**
If the Use a proxy server for your LAN checkbox was selected and the address and port are specified, use the following proxy element:

![proxy for LAN](/images/windows-agent-proxy/proxy-for-lan.png)

```
<system.net>
    <defaultProxy enabled="true" useDefaultCredentials="true">
      <proxy proxyAddress="http://proxyhost:8088" />
    </defaultProxy>
  </system.net>
```

Replace `URI_STRING` with the address and port settings used (e.g., `http://proxyhost:8088`). If the address and port are not specified, then the proxy is manually configured on the Advanced screen. Enter the proxy element as above but using the address and port given for the HTTPS protocol.

![proxy for lan 2](/images/windows-agent-proxy/proxy-for-lan-2.png)
