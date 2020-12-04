---
title: "CloudWatch Agent"
#date: 2018-12-11
draft: false
tags: ["aws", "integrations", "agents" ]
author: Lawrence Lane
---

The CloudWatch Agent enables CloudWisdom to collect additional EC2 metrics, such as memory utilization, from AWS. Reports display cost vs. CPU utilization by default. We recommend installing the agent if you are interested in seeing cost vs. memory utilization.

{{% notice info %}}

The CloudWatch Agent configuration below adds a single memory metric to all instances it is installed on. This incurs an additional charge of **~$0.30/instance/month** to your CloudWatch bill. See [AWS Cloudwatch pricing](https://aws.amazon.com/cloudwatch/pricing/) for more information.

{{% /notice %}}


## How to Configure the CloudWatch Agent

Installing the CloudWatch agent can be done in a variety of ways, but each method requires the use of CloudWisdom's unique agent config file.

AWS offers [3 ways to install the CloudWatch Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-EC2-Instance.html):

- via the **Command Line**
- via **AWS Systems Manager**
- via **AWS CloudFormation**


We recommend using the CLI method. See below for steps to install the agent on Linux and Windows instances using this method.

### Linux Installation

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
9. Verify the agent is running: `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status`.
10. Complete! A new metric **cwagent.mem_used_percent** should appear in CloudWisdom on the respective EC2 element within approximately 10 minutes.

### Windows Installation

1. Log on to your instance.
2. **Download** the following file: https://s3.amazonaws.com/amazoncloudwatch-agent/windows/amd64/latest/amazon-cloudwatch-agent.msi.
3. Open Command Prompt, navigate to the directory containing the downloaded file, and enter the following to **install** the agent:
`msiexec /i amazon-cloudwatch-agent.msi`
4. Open a text editor, create a new file, and place the [Windows Agent Config File][3] contents in it.
5. Save the file with the name `amazon-cloudwatch-agent.json` to the following directory: `C:\ProgramData\Amazon\AmazonCloudWatchAgent`.
6. [Create an IAM role and attach it to the instance](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-iam-roles-for-cloudwatch-agent-commandline.html).
7. Open Windows PowerShell and run the following command to fetch the config and start the agent:
```
  & "C:\Program Files\Amazon\AmazonCloudWatchAgent\amazon-cloudwatch-agent-ctl.ps1" -a fetch-config -m ec2 -c file:"C:\ProgramData\Amazon\AmazonCloudWatchAgent\amazon-cloudwatch-agent.json" -s
```
8. Verify the agent is running: `& $Env:ProgramFiles\Amazon\AmazonCloudWatchAgent\amazon-cloudwatch-agent-ctl.ps1 -m ec2 -a status`.
9. If necessary, start the agent using this command: `& $Env:ProgramFiles\Amazon\AmazonCloudWatchAgent\amazon-cloudwatch-agent-ctl.ps1 -m ec2 -a start`.
10. Complete! A new metric **cwagent.memory % committed bytes in use** should appear in CloudWisdom on the respective EC2 element within approximately 10 minutes.

### Linux Agent Config File

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

### Windows Agent Config File

```
{
  "agent": {
    "metrics_collection_interval": 60,
    "logfile": "c:\\ProgramData\\Amazon\\AmazonCloudWatchAgent\\Logs\\amazon-cloudwatch-agent.log"
  },
  "metrics": {
    "metrics_collected": {
      "Memory": {
        "measurement": [
          "% Committed Bytes In Use"
        ],
        "metrics_collection_interval": 60
      }
    },
    "append_dimensions": {
      "InstanceId": "${aws:InstanceId}"
    }
  }
}
```

[2]: /integrations/agents/cloudwatch-agent/#linux-agent-config-file
[3]: /integrations/agents/cloudwatch-agent/#windows-agent-config-file
