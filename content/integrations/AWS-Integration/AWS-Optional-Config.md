---
title: "Optional Config"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#optional config", "#elements"]
author: Lawrence Lane
weight: 5
---
## Change Element Display Names
You can change how certain elements’ names are displayed in the application to help distinguish between each instance, e.g., you have 15 EC2 instances with the same name and want to know the difference between each.  

1. Under the Include Types list, expand the desired type.  
2. Beneath the Tag Key field, click **Advanced**. A menu expands.  
![Element Name](/images/AWS-Optional-Config/element-name.png)
3. Hover next to Element Name; an edit icon will appear. Click the icon.  
4. Type the desired name into the field.  
5. Select an element to use as a preview for your new element name using the Element To Preview drop-down menu.  
6. Next to the Element Name field, click **Preview** to view your new template using the selected element.  
7.  If you’re satisfied with the name, press **Enter** on your keyboard while in the Element Name field to lock in the name.  

Exit the integration setup page and wait until the next analytics cycle (5 minutes) to see your changes.  

## Collection Frequency

The default collection frequency for CloudWatch metrics is every 5 minutes. If you need to reduce this frequency, return to your AWS integration card settings in **Integrations** > **AWS**.  You can also access a full list of your integrations by navigating to your User **Profile** > **Integrations** > Select an AWS Integration.

1. Navigate to your AWS integration.
2. Select the **60 Minutes** button under _Collection Frequency_.
![collection-frequency](/images/AWS-Optional-Config/collection-frequency.png)
3. **Save**. 

This can be undone by selecting the **5 Minutes**  _Collection Frequency_ option and saving the integration.

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

## Filter AWS Elements
You can filter what AWS elements are included in Metricly’s monitoring by using regex to match key-value pairs (ASG, EC2, EBS, ELB, RDS, Redshift, Elasticache, EMR), Namespace names (Custom Cloudwatch Metric), queue names (SQS), table names (DynamoDB), cluster names (ECS), function names (Lambda), or stream names (Kinesis). Metricly offers opt-in (include) or opt-out (exclude) element filtering. For more information about tagging elements in AWS, see the following AWS documentation.

### Using opt-in filtering
**For key-value pairs (ASG, EC2, EBS, ELB, RDS, Redshift, Elasticache, EMR elements, ALB):**  

1. In your AWS account, create or choose an existing tag (key-value pair). Then, assign the tag to the AWS elements you want Metricly to monitor.
2. On the AWS Integration Setup page, expand  the element types you want to filter. Key-value pair fields display.
![Opt-In Filtering](/images/AWS-Optional-Config/opt-in-filtering.png)
3. Select the **Filtering** checkbox.
4. Select **Include**. Type the proper Regex to match the tag(s) you created in your AWS account for each element type you want to filter.
5. Click **Save**.

**For names (Custom Cloudwatch, SQS, DynamoDB, Kinesis, ECS, Lambda elements, ALB):**
1. Prepate the queue, table, or stream name(s) for the AWS element(s) you want to monitor.
2. On the AWS Integration Setup page, expand  the element types you want to filter. Name fields display.
![SQS filtering](/images/AWS-Optional-Config/sqs-filtering.png)
3. Select the **Filtering** checkbox.
4. Select **Include**. Type the name of the table, queue, or stream for each element type you want to filter.
5. Click **Save**.

{{% alert theme="info" %}} Say you want to filter out all Custom Cloudwatch Namespaces except for customnamespace1 and customnamespace2. You would put the following in the field: (customnamespace1|customnamespace2) {{% /alert %}}

#### Regex Examples
The filtering fields append a ``.*`` to the front and back of each value input into the fields. For example, if you input ``.Prod-app1``, it will be interpreted as ``.*.Prod-app1.*.`` We recommend testing any regular expressions that you create here.

 - Match the start and end of the string contained between ``^`` and ``$``. The following would match the key-value pair `Metricly = true`.
 - Match multiple values separated by ``|`` between ``( )``. The following would match any of the following key-value pairs: `Name = my-server-one, Name = my-server-two, Name = my-server-three`.
 - Match any character(s) using `.`, which acts as a wildcard. The following would match any value (e.g., `Name = myProd-app-1, Name = yourProd-app-1`) as long as Prod-app-1 followed.
 - Escape special regex characters ` . *  /` using a ``/``. The following would match the key-value pair `Name = my.server.one`. For a list of special regex characters you may have to escape, consult this page.
