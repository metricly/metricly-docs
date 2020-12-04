---
title: "Tomcat"
#date: 2018-12-11
draft: false
tags: ["tomcat", "integrations",]
author: Lawrence Lane
---

Tomcat (also known as Apache Tomcat or Tomcat Server) is an open source Java Servlet Container. You can use CloudWisdom’s Java agent to collect information on your Tomcat Server.

## Prerequisites
- [Java Agent][1]

## Configure

1. Navigate to the **zorka.properties** file.
2. Comment out the **Default collection** scripts section.

```
# Default collection of jvm metrics
# scripts = jvm.bsh
```

3\. Uncomment the **Apache Tomcat** scripts section.

```
# Example: Apache Tomcat configuration with CAS server
scripts = jvm.bsh, zabbix.bsh, apache/tomcat.bsh, apps/cas.bsh
```

5\.Configure Tomcat to load the Java agent. This is often configured via the **setenv.sh** or **tomcat.conf** files.  
6. **Restart** your app server.


[1]: /integrations/agents/java-agent
