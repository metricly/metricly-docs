---
title: "CloudWatch Agent"
#date: 2018-12-11
draft: false
tags: ["#aws", "#integrations", "#agents" ]
author: Lawrence Lane
---

The CloudWatch Agent enables CloudWisdom to collect additional EC2 metrics, such as memory utilization, from AWS. Reports display cost vs. cpu utilization by default. We recommend installing the agent if you are interested in seeing cost vs. memory utilzation.

{{% notice info %}}

The CloudWatch Agent configuration below adds a single memory metric to all instances it is installed on. This incurs an additional charge of **~$0.30/instance/month** to your CloudWatch bill. See [AWS Cloudwatch pricing](https://aws.amazon.com/cloudwatch/pricing/) for more information.

{{% /notice %}}


## How to Configure the CloudWatch Agent

Installing the CloudWatch agent can be done in a variety of ways, but each method requires the use of CloudWisdom's unique [agent config file][1].

AWS offers [3 ways to install the CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance.html):

- via the **Command Line**
- via **AWS Systems Manager**
- via **AWS CloudFormation**


Virtana recommends using the CLI method. The following steps work for **Linux (Ubuntu)** instances:

1. SSH into your instance.
2. Run the following to download the agent:
```
  wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
```

3. Run `sudo dpkg -i -E ./amazon-cloudwatch-agent.deb` to install the agent.
4. Start the wizard using `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard`.
5. Complete the wizard. Don't worry about the answers as we will use the CloudWisdom agent config file.
6. Navigate to the /bin folder: `cd /opt/aws/amazon-cloudwatch-agent/bin`.
7. Overwrite the config.json file with the [following][2].
8. [Create an IAM role and attach it to the instance](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-iam-roles-for-cloudwatch-agent-commandline.html).
9. Run the following to start the agent:
```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config
-m ec2 -c file:config.json -s
```
   - You may get a Parsing error. Here is the workaround:
     - `sudo mkdir /usr/share/collectd`
     - `cd /usr/share/collectd`
     - `sudo touch types.db`

10. Metrics appear in CloudWisdom within approximately 10 min of finishing setup.


### Linux Agent Config File

 CloudWisdom uses a minimal config file template to add a single memory metric to your instances. Save the following JSON as a config.json file:

```
{
    "agent": {
        "metrics_collection_interval": 60,
        "run_as_user": "root"
    },
    "metrics": {
        "append_dimensions": {
            "InstanceId": "${aws:InstanceId}"
        },
        "metrics_collected": {
            "collectd": {
                "metrics_aggregation_interval": 60
            },
            "mem": {
                "measurement": [
                    "mem_used_percent"
                ],
                "metrics_collection_interval": 60
            },
            "statsd": {
                "metrics_aggregation_interval": 60,
                "metrics_collection_interval": 60,
                "service_address": ":8125"
            }
        }
    }
}

```

[1]: /integrations/agents/cloudwatch-agent/#linux-agent-config-file
[2]: /integrations/agents/cloudwatch-agent/#linux-agent-config-file
