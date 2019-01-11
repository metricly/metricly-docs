---
title: "Regex Guide"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#events", "#policies", "#conditions", "#regex"]
author: Lawrence Lane
alwaysopen: false
---
## Use Regex to Match Metric Conditions
Regex uses all metrics that contain your input value. Typing `aws.elb.httpcode.*` would match both `aws.elb.httpcode_backend_2xx`, as well as `netuitive.aws.elb.httpcodebackenderrorpercent`.

- Exclude computed metrics using a ^ before the start of a metric name.
- Use Metric Tags to select a tag to further filter your condition.

{{% notice tip %}}
We recommend testing any regular expressions that you create at https://regexr.com.
{{% /notice %}}

### Match String
Match the start and end of the string contained between ``^`` and ``$``.

- **Tag Key**: ``^Metricly$``
- **Tag Value**: ``^true$``

Matches the key-value pair Metricly = true

### Match Multiple Variables
Match multiple values separated by ``|`` between ``( )``.

- **Tag Key**: ``^Name$``
- **Tag Value**: ``(my-server-one|my-server-two|my-server-three)``

Matches  any of the following key-value pairs:  

- `Name = my-server-one`
- `Name = my-server-two`  
- `Name = my-server-three`  

### Match Wildcard
Match any character(s) using ., which acts as a wildcard.

- **Tag Key**: ``^Name$``
- **Tag Value**: ``.Prod-app-1``

Matches any value (e.g., `Name = myProd-app-1`, `Name = yourProd-app-1`) as long as `Prod-app-1` followed:

### Escape Special Regex Characters
Escape special regex characters ``. * /`` using a `.`

- **Tag Key**: `^Name$`
- **Tag Value**: `my.server.one`

Matches the key-value pair `Name = my.server.one`.

{{% notice tip %}}
For a list of special regex characters you may have to escape, consult this page.
{{% /notice %}}

### Match Entire Directory

Match an entire website’s directory using ``.*``

```
Qhttps://www.metricly.comE.*
```
- Matches anything that comes after `www.metricly.com`
- The **Q** and **E**  force the URL to be matched literally

### Match Part of Directory
Make the URL more specific to match everything from a particular part of the directory.

```
Qhttps://help.metricly.com/Content/Reports/E.*
```
Matches anything in the  `https://help.metricly.com/Content/Reports/directory`
- **Match**: `https://help.metricly.com/Content/Reports/Cost/report_pic.png`
- **Not a Match**: `https://help.metricly.com/Content/home.htm`

### Match Multiple Containers
Match multiple containers between ``( )`` and separated by ``|``. The following would match any of the following container IDs and exclude them from collection: `abcdef123456`, `123456abcdef`, `ghijkl789012`.

```
metrics_blacklist = containers. (abcdef123456|123456abcdef|ghijkl789012)..*
```

### Filter Exclusions
Use a negative lookahead (``?!``) to specify a group that cannot match after the main expression--if something matches, the result is discarded. The following would match anything but the `_all`, `datastore`, and `docsindices` and exclude them from collection.

```
metrics_blacklist = elasticsearch .indices.(?!_all$|datastore$|docs$)
```

### Add Filter
Add another index to a negative lookahead by placing the index name between ``|`` and ``$``.

```
(?!_all$|datastore$|docs$|myimportantindexname$)
```
