---
title: "Element Display Name"
#date: 2018-04-12
draft: false
categories:
tags: ["#integrations",  "#elements", "#inventory page"]
author: Lawrence Lane
---

You can change the display name of certain elements to help distinguish between each instance. Elements must have existing tags and attributes assigned in order to modify their display name in the UI.


## How to Update Element Display Names Using Tags & Attributes

1. Navigate to **Integrations** > select an integration (Linux Agent, Windows Agent, etc).
2. Select **Advanced**; a menu expands.
![expand-adv-tab](/images/inventory-element-display-name/expand-adv-tab.png)
3. Select the **Element Name** field to edit it.
4. Type the desired name into the field.
  - ``${meta.originalName}`` resolves to the name included with the original element payload _before_ being replaced with the optional element name template. The Element Preview in the UI resolves this field to `[original name]` as a placeholder because CloudWisdom only knows what the current name is, not what the incoming name might be.
  - ``${tags.Name} (${attributes.privateIp})`` returns something like `MyServer (ip-10.101.3.99)`
  - ``${tags.Name} (${attributes.availabilityZone})`` returns something like `ServerX (eu-west-1c)`
5. Select an element to use as a preview for your new element name using the Element To Preview drop-down menu.
6. Next to the Element Name field, select **Preview** to view your new template using the selected element.
7. If you’re satisfied with the name, press **Enter** on your keyboard while in the Element Name field to lock in the name. Exit the integration setup page and wait until the next analytics cycle (5 minutes) to see your changes.

### Metadata Variable Templates

- **Element FQN**: `${meta.fqn}` | e.g., _720523155433:ec2:us-east-1:i-20c9ae302d2e7b45e_
- **Element Location**: `${meta.location}` | e.g., _us-east-1_
- **Element Type**: `${meta.type}` | e.g., _EC2_
- **Tenant ID**: `${meta.tenantId}` | e.g., _38907e4c-392a-9f9a-b682-7h938e43dt73_
- **Element ID** `${meta.id}`| e.g., _1f71ab78-80a9-3f9b-941f-07cbe8fe4703_

{{% notice tip %}}

Not all element types have location metadata. Consider the type of element you are working with when customizing display names.

{{% /notice %}}

### Example: Adding the Private IP Address to an Element Name
Adding the private IP address to your element names enables your team to immediately begin troubleshooting problematic instances.

```
<#if tags.Name??>${tags.Name}<#elseif tags.aws_autoscaling_groupName??>${tags.aws_autoscaling_groupName}<#else>${meta.originalName}</#if><#if attributes.privateIp??> (${attributes.privateIp})</#if>
{noformat}
```
