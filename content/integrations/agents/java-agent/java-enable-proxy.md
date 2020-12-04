---
title: "Enable Proxy"
#date: 2018-12-11
draft: false
tags: ["java", "integrations", "agents"]
author: Lawrence Lane
---
## Enable a Proxy
1. Navigate to the `zorka.properties` file.
2. Find the proxy section:  

```
netuitive.api.proxy = no
netuitive.api.proxy.address = http://<proxy host>:<proxy port>
```
3\. Change the `netuitive.api.proxy` line to yes.  
4. Add the correct proxy host and port to the `netuitive.api.proxy.address` line.
