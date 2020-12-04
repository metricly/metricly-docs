---
title: "Elastic Beanstalk"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux", "elastic beanstalk"]
author: Lawrence Lane
#pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 4
---
Using an existing application file, you can deploy the Netuitive agent to a self-contained EC2 instance complete with a load balancer and everything else it needs to run. The Elastic Beanstalk instance can also scale by itself.[Check out our Elastic Beanstalk repo here](https://github.com/Netuitive/netuitive-agent-elasticbeanstalk/).

1. Before creating your Elastic Beanstalk instance, find or create a folder called .ebextensions in your application’s directory.
2. Copy the netuitive.config file to your .ebextensions folder.
3. Replace the sample API key at the top of the `netuitive.config` file `N_APIKEY=<datasource api key>` as well as in the configuration portion of the file `api_key = <datasource api key>` with the Linux integration API key in your account.
4. Either use the new application files to create a new Beanstalk environment or to update a current application version by replacing it.   

**Locating Your API key:**  
To find your API Key, navigate to the **user account** and select **Integrations**.   

Your Linux API key is found next to the integration listed as _INFRASTRUCTURE_. The default config file included in the `netuitive.config` file does not include any additional collector files yet (e.g, Flume, Elasticsearch, Kafka, etc.). The collector files can be added to and modified directly on each EC2, but those changes may not be persisted if your Beanstalk application is rebuilt.
