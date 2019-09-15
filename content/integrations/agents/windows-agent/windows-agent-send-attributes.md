---
title: "Send Tags & Attributes"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", "#install", "#tags", "#attributes", "#elements"]
author: Lawrence Lane
---

You can send tags and attributes through the Windows Agent by updating files in from the `/CollectedWin/config` folder.

## Sending Tags

1. Navigate to the `/CollectdWin/config/ReadWindowsTags.config` file.
2. Update the **`<Tags>`** section.

```
<ReadWindowsTags>
  <Tags>
    <!-- Example
    <Tag Name="tag1" Value="value1"/>
    -->
  </Tags>
</ReadWindowsTags>

```
3\. **Save** your file.

## Sending Attributes

1. Navigate to the `/CollectdWim/config/ReadWindowsAttributes.config` file.
2. Update the **`<EnvironmentVariables>`** section.
  - **EnvironmentVariable Name="static_display_name_here"**: replace `static_display_name_here` with the key for your attribute. This string shows up in Metricly next to the attribute's value.
    - **Value="ATTRIBUTE_NAME"**: replace  `ATTRIBUTE_NAME` with the exact environment variable name you wish to send.
3. **Save** your file.

### Attribute Example
```
<EnvironmentVariable Name="processor_architecture" Value="PROCESSOR_ARCHITECTURE"/>
```

{{% notice tip %}}
You must choose an environment variable listed by the host when running `set` from the command prompt, e.g. `PROCESSOR_ARCHITECTURE`:
![send-attributes-cmd](/images/windows-agent-send-attributes/send-attributes-cmd.png)
{{% /notice %}}
