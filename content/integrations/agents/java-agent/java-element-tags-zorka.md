---
title: "Send Tags Via Zorka"
#date: 2018-12-11
draft: false
tags: ["java", "integrations", "agents"]
author: Lawrence Lane
---
## Send Element Tags via Zorka Agent
1. Navigate to the **zorka.properties** file in your Java agent directory.
2. Near the bottom of the file, uncomment the `#netuitive.api.tags` list and add tags following the below format:

```
  netuitive.api.tags = name:value, second:value
```
3\. **Save** the file.
