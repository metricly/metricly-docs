---
title: "Custom MBeans"
#date: 2018-12-11
draft: false
tags: ["#java", "#integrations", "#agents"]
author: Lawrence Lane
---
The Java agent can collect metrics from custom mbeans. We have provided a sample spring boot application that creates 2 custom mbeans with test attributes [here](https://github.com/netuitive/zorka-custom-mbean-examples/blob/master/multiple-mbeans-example/src/main/java/com/netuitive/Application.java).

## Multiple Custom MBean Diagram
![multi diagram](/images/java-custom-mbeans/multi-diagram.png)

## For a Single Custom MBean
1. Navigate to the **zorka.properties** file in your Java agent directory.
2. Near the bottom of the file, set the attribute **netuitive.api.custom.stats.mbean** to the custom mbean you defined in your application

```
#custom mbean to collect metrics from
netuitive.api.custom.stats.mbean = com.netuitive.mbean:type=Test,name=CustomTestMBean
```
3. **Save** the file.

## For Multiple MBeans

We’ve provided a [sample .bsh script](https://github.com/netuitive/zorka-custom-mbean-examples/blob/master/multiple-mbeans-example/netuitive-zorka-1.0.17/scripts/custom-mbean.bsh) that creates getter objects for each of the mbeans in the sample multiple mbean [spring boot application file](https://github.com/netuitive/zorka-custom-mbean-examples/blob/master/multiple-mbeans-example/src/main/java/com/netuitive/Application.java).

1. Create a **.bsh script** that contains getter objects for each of your custom mbean values. In the same script, create a rollup mbean and add the getter objects you created in step 1 as attributes of the rollup mbean.
2. Navigate to the **zorka.properties** file in your Java agent directory.
3. Add the script you created in step 1 to the scripts setting.

```
#Default collection of jvm metrics
scripts = jvm.bsh, custom-mbean.bsh
```
4. Near the bottom of the file, set the attribute **netuitive.api.custom.stats.mbean** to the new rollup mbean you created in step 2.
```
#custom mbean to collect metrics from
netuitive.api.custom.stats.mbean
= com.netuitive.mbean:type=Test,name=RollupTestMBean
```
5. **Save** the file.

{{% notice tip %}}
Leave the netuitive.api.custom.stats.mbean.attr.includeattribute blank to include all metrics.
{{% /notice %}}
