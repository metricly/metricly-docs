---
title: "Uninstall Agent"
#date: 2018-12-11
draft: false
tags: ["java", "integrations", "agents"]
author: Lawrence Lane
---
## How to Uninstall
1. Remove any JVM startup references to the Netuitive Java Agent.

```
java -javaagent:/opt/netuitive-zorka/netuitive.jar=/opt/netuitive-zorka -jar zorka-core-test.jar -- service

```
2. Delete all Netuitive Java Agent (**netuitive-zorka-{version}**) files.

{{% notice tip %}}
If you instrumented metrics using the jvm.bsh script, you will need to remove the references to the script as well.
{{% /notice %}}
