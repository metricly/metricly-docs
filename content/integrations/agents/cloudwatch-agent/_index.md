---
title: "CloudWatch Agent"
#date: 2018-12-11
draft: false
tags: ["#aws", "#integrations", "#agents" ]
author: Lawrence Lane
---

Use the CloudWatch agent to run faster EC2 Recommendation Reports at scale. This is especially useful for clients with larger environments. Using the CloudWatch Agent enables CloudWisdom to directly pull EC2 utilization data, such as memory utilization, directly from AWS.

{{% notice info %}}

The CloudWatch Agent adds a single memory metric to all instances it is installed on. This  incurs an additional charge of **~$0.30/instance/month** on your CloudWatch bill. See [AWS Cloudwatch pricing](https://aws.amazon.com/cloudwatch/pricing/) for more information.

{{% /notice %}}


## Configure

Installing the CloudWatch agent can be done in a variety of ways, but each method requires the use of CloudWisdom's unique agent config file (found in Section 2).

### 1. Choose an Installation Method

AWS offers [3 ways to install the CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance.html):

- via the **Command Line**
- via **AWS Systems Manager**
- via **AWS CloudFormation**

CloudWisdom recommends that you follow the [Command Line installation method](/integrations/agents/cloudwatch-agent/#command-line-steps).

### 2. Create a Config File

CloudWisdom uses a minimal config file template to add a single memory metric to your instances.

1. Use the following JSON to create an agent config file:

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
2\. Save the file as `cwconf.json`.

### 3. Complete Installation

Use the `cwconf.json` file when following the steps of your preferred installation method. For example, if using the AWS CloudFormation method, upload the config file within the AWS Console while creating your stack.

![aws-cloudf-upload-configfile](/images/_index/aws-cloudf-upload-configfile.png)


{{% notice tip %}}

**AWS Systems Manager Method**: You must assign the AWS default _CloudWatchAgentAdmin IAM Role_ to an instance before using the saved `cwconf.json` file uploaded to the Systems Manager Parameter Store.

{{% /notice %}}

---

### Command Line Steps

1. SSH into your instance.
2. Run `wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb` to download the agent.
3. Run `sudo dpkg -i -E ./amazon-cloudwatch-agent.deb` to install the agent.
4. Start the wizard using `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard`.
5. Complete the wizard. Don't worry about answering each question correctly, as the config.json file this wizard creates will be overwitten with our custom file.
6. Run `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:config.json -s`. You may get a parsing error.
7. Run all of the following:
 - `sudo mkdir /usr/share/collectd`
 - `cd /usr/share/collectd`
 - `sudo touch types.db`
8. Reboot the instance.
