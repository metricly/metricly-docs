---
title: "Tags & Attributes"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", "#install", "#tags", "#attributes", "#elements"]
author: Lawrence Lane
---

You can send tags and attributes through the Windows Agent by updating files in from the `/CollectedWin/config` folder.

## Sending Tags

1. Navigate to the `/CollectdWin/config/ReadWindowsTags.config` file.
2. Update the **`<Tags>`** section.
  - **Tag Name ="tag1"**: replace `tag1` with the static key for this tag.
  - **Value="value1"**: replace `value1` with the host's tag value.
3. **Save** your file.

### Tag Example

```
<ReadWindowsTags>
  <Tags>
    <!-- Example
    <Tag Name="candle" Value="fresh-linen"/>
    <Tag Name="spice" Value="ginger"/>
    -->
  </Tags>
</ReadWindowsTags>
```

## Sending Attributes

1. Navigate to the `/CollectdWim/config/ReadWindowsAttributes.config` file.
2. Update the **`<EnvironmentVariables>`** section.
  - **EnvironmentVariable Name="static_display_name_here"**: replace `static_display_name_here` with the key for your attribute. This string shows up in Metricly next to the attribute's value.
    - **Value="ATTRIBUTE_NAME"**: replace  `ATTRIBUTE_NAME` with the exact environment variable name you wish to send.
3. **Save** your file.

### Attribute Example
```
<ReadWindowsAttributes ReadEC2InstanceMetadata="true">
  <EnvironmentVariables>
    <EnvironmentVariable Name="processor_architecture" Value="PROCESSOR_ARCHITECTURE"/>
    <EnvironmentVariable Name="number_of_processors" Value="NUMBER_OF_PROCESSORS"/>
  </EnvironmentVariables>
</ReadWindowsAttributes>
```

{{% notice tip %}}
You must choose an environment variable listed by the host when running `set` from the command prompt, e.g. `PROCESSOR_ARCHITECTURE`:
![send-attributes-cmd](/images/windows-agent-send-attributes/send-attributes-cmd.png)
{{% /notice %}}
