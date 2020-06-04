---
title: "CloudWatch Agent"
#date: 2018-12-11
draft: false
tags: ["#aws", "#integrations", "#agents" ]
author: Lawrence Lane
---

The CloudWatch Agent enables CloudWisdom to collect additional EC2 metrics, such as memory utilization, from AWS. Reports display cost vs. CPU utilization by default. We recommend installing the agent if you are interested in seeing cost vs. memory utilzation.

{{% notice info %}}

The CloudWatch Agent configuration below adds a single memory metric to all instances it is installed on. This incurs an additional charge of **~$0.30/instance/month** to your CloudWatch bill. See [AWS Cloudwatch pricing](https://aws.amazon.com/cloudwatch/pricing/) for more information.

{{% /notice %}}


## How to Configure the CloudWatch Agent

Installing the CloudWatch agent can be done in a variety of ways, but each method requires the use of CloudWisdom's unique [agent config file][1].

AWS offers [3 ways to install the CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance.html):

- via the **Command Line**
- via **AWS Systems Manager**
- via **AWS CloudFormation**


Virtana recommends using the CLI method. The following steps work for **Linux** instances:

1. SSH into your instance.
2. Run `wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm` or `wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb` depending on your distro to **download** the agent.
3. Run `sudo rpm -i amazon-cloudwatch-agent.rpm` or `sudo dpkg -i -E ./amazon-cloudwatch-agent.deb` to **install** the agent.
4. Navigate to the **bin** directory of the agent: `cd /opt/aws/amazon-cloudwatch-agent/bin`.
5. Create a file `config.json` and place the [Linux Agent Config File][2] contents in it and save it.
6. [Create an IAM role and attach it to the instance](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-iam-roles-for-cloudwatch-agent-commandline.html).
7. Run the following command to initialize the agent configuration:
```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:config.json -s
```
   - You may get a parsing error. Here is the workaround:
     - `sudo mkdir /usr/share/collectd`
     - `cd /usr/share/collectd`
     - `sudo touch types.db`

8. Start the agent: `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a start`.
9. Verify it is running: `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status`.
10. Complete! A new metric **cwagent.mem_used_percent** should appear in CloudWisdom on the respective EC2 element within approximately 10 minutes.

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
