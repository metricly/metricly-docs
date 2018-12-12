---
title: "Standard Install"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux",]
author: Lawrence Lane
pre: "<i class='fa fa-download'></i> &nbsp;"
weight: 1
---
This integration’s package (computed metrics, dashboards, and policies that will give you important events and alerts) will be automatically enabled and provisioned to your account as soon as Metricly receives data from the integration. The PACKAGES button on the integration setup page will become active once data is received, so you’ll be able to disable and re-enable the package at will.

## 1. Copy Install Command From Linux Integration Setup Page

1. From the top navigation menu, select **Integrations**.
2. Select the **Linux** card. The name should be already populated, and Data Collection should be enabled.
3. Highlight the one-line install command from the instructions and copy them. A unique API key for your account has already been generated and included in the command line.
![Linux Install Command](/images/LINUX-standard-install/linux-install-command.png)

If you’d prefer to specify the element name, copy the following instead:

```
sudo N_APIKEY=your-apikey N_HOSTNAME=your-element-name bash -c "$(curl -Ls http://repos.app.netuitive.com/linux.sh)"
```

`your-apikey` is the API key generated from the integration and `your-element-name` can be any element name you wish (it must be unique from your other elements).

## 2. Install Linux Agent
1. Paste the command from step 1.3 into your command line. This  installs the agent and adds your account’s unique API key to the configuration file.

{{% alert = "info"%}}If you install our Linux agent on an AWS EC2 or Azure VM, the EC2’s / VM’s power state (it will come in as the attribute hostRunning with a value of `true` or `false`) and tags are copied over to the corresponding Linux SERVER element. You can then use this information to create policies. {{% /alert %}}

## 3. Edit Linux Agent Config File
1. Navigate to the Linux Agent configuration file found at ``/opt/netuitive-agent/conf/netuitive-agent.conf``.
2. Ensure the API key provided in step 1 is input in the `netuitive-agent.conf` file. The section below is only a portion of the config file. [Go here to view the full config file][1].
```
[[NetuitiveHandler]]
    ### MetriclyCloud URL to post the metrics
    url = https://api.app.metricly.com/ingest/infrastructure

    ## Metricly Datasource api key
    api_key = <datasource api key>

    ### Uncomment to add tags (optional)
    # tags = tag1:tag1val, tag2:tag2val

    ### Uncomment to add relations
    # relations = element1, element2

    # How many samples to store before sending to Metricly
    batch = 100

    # how many batches to store before trimming
    max_backlog_multiplier = 5

    # Trim down how many batches
    trim_backlog_multiplier = 4

    # local statsd server
    [[[statsd]]]
    enabled = False
```
3. **Save** the configuration file.
4. **Restart** the Linux Agent service to begin monitoring your data with Metricly.

### Config Options
- **Option 1**:  Substitute tags value with desired tags and uncomment the line to pass in tags for your element.
- **Option 2**:  Substitute relations value with desired element relationships; must include the fully qualified name of the elements. Uncomment the line to pass in relationships for your element.
- **Option 3**: Adjust  default collectors (CPU, DiskSpace, DiskUsage, Heartbeat, LoadAverage, Memory, VMStat, Network) using the configuration options found here.  


[1]:https://raw.githubusercontent.com/netuitive/omnibus-netuitive-agent/master/netuitive/conf/netuitive-agent.conf
