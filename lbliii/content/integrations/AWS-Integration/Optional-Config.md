---
title: "Optional Config"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started"]
tags: ["aws", "optional config"]
author: Lawrence Lane
---
## Change Element Display Names
You can change how certain elements’ names are displayed in the application to help distinguish between each instance, e.g., you have 15 EC2 instances with the same name and want to know the difference between each.  

1. Under the Include Types list, expand the desired type.  
2. Beneath the Tag Key field, click **Advanced**. A menu expands.  
![Element Name](/images/Optional-Config/element-name.png)
3. Hover next to Element Name; an edit icon will appear. Click the icon.  
4. Type the desired name into the field.  
5. Select an element to use as a preview for your new element name using the Element To Preview drop-down menu.  
6. Next to the Element Name field, click **Preview** to view your new template using the selected element.  
7.  If you’re satisfied with the name, press **Enter** on your keyboard while in the Element Name field to lock in the name.  

Exit the integration setup page and wait until the next analytics cycle (5 minutes) to see your changes.  

### Naming Tips
When choosing a name, replace the following with underscores:  

**(space) ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _  { | } ~**   

  - `example.io/service-name` should be ``${tags.example_io_service_name}``. Variables are compatible, but note that values in key.value pairs are case sensitive. Spaces and dots in any returned value are replaced with underscores.

  - An element name of ``${meta.originalName}`` would resolve to whatever name comes in with the original element payload before it would be replaced with the optional element name template.  

The element name template preview in the UI will resolve this field to [original name] as a placeholder because Metricly only knows what the current name is, not what the incoming name might be.

  - An AWS EC2 with element name of ``${tags.Name} - (AZ:${attributes.availabilityZone})`` would utilize each EC2 instance’s Name (from the tag value) and availability zone (from the attribute).
  - An element name of ``${tags.InternalName} (${tags.Name})`` will give you something like `MyServer (ip-10.101.3.99)`
  - An element name of ``${tags.Name} (${attributes.availabilityZone})`` would return something like `ServerX (eu-west-1c)``


### Example: Adding the Private IP Address to an Element Name
Adding the private IP address to your element names enables your team to immediately begin troubleshooting problematic instances.  
```
<#if tags.Name??>${tags.Name}<#elseif tags.aws_autoscaling_groupName??>${tags.aws_autoscaling_groupName}<#else>${meta.originalName}</#if><#if attributes.privateIpAddress??> (${attributes.privateIpAddress})</#if>
```
