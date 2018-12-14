---
title: "Docker Install"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux", "docker"]
author: Lawrence Lane
pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 2
---
## 1. Copy API Key From Docker Integration
1. From the Metricly top navigation menu, select Integrations.  
2. Click the Docker card.  
3. Ensure Data Collection is enabled. A unique API key for your account has already been generated.  
4. Highlight the one-line install command from the instructions and copy them. A unique API key for your account has already been generated and included in the command line.  
![Docker API Key](/images/LINUX-docker-install/docker-api-key.png)

The command runs a container named `netuitive-agent` in the background and publishes the port values to the host. It then sets the environment variable `DOCKER_HOSTNAME` and `APIKEY` to the described values. Lastly, a volume is mounted so the agent has access to the Docker API.

### Command Line Alternative

You can also copy the line below and paste it into your command line. Ensure you replace ``<my-api-key>`` with your API key from Metricly and ``<my-docker-host>`` with the desired hostname. Additional environment variables are located in the drop-down below if you’d like to include more or edit existing ones.

```
docker run -d -p 8125:8125/udp --name netuitive-agent -e DOCKER_HOSTNAME="<my-docker-host>" -e APIKEY="<my-api-key>" -v /proc:/host_proc:ro -v /var/run/docker.sock:/var/run/docker.sock:ro netuitive/docker-agent
```

### Environment Variables

| Variable         | Description                                                                            | Example                                                                         |
|------------------|----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| LOGLEVEL         | Changes the log level of the agent.                                                    | ``-e LOGLEVEL=DEBUG`` would set the agent tolog at DEBUG level.                     |
| INTERVAL         | Sets the interval in seconds at which the agent collectors run.                        | ``-e INTERVAL=120`` would set collection attwo-minute intervals.                    |
| DOCKER_HOSTNAME  | Sets the host name of the docker host.                                                 | ``-e DOCKER_HOSTNAME="my-docker-host"``  would set the host name to my-docker-host. |
| APIKEY           | Sets the API key used send data to Metricly.                                           | ``-e APIKEY=myapikey`` would set the API keyto myapikey.                            |
| USE_LOCAL_CONFIG | Tells the agent to ignore any environment variables set and to usea local config file. | ``-e USE_LOCAL_CONFIG=true`` would enable this feature.                              |
| LPRT             | Tells the Netuitive StatsD agent whatUDP port to listen on. 8125 is the default.       |                                                                                 |
| FORWARD          | Enables forwarding from the `netuitive-statsd` server to anotherStatsD server.           |                                                                                 |
| FIP              | Tells the Netuitive StatsD agent what IP address to forward to.                        |                                                                                 |
| FPRT             | Tells the Netuitive StatsD agent what port to forward to. 8125 isthe default           |                                                                                 |

## 2. Install Linux Agent Docker Container
Paste the command from 1.3 into your command line. Replace my-docker-host in the command with the name of the docker host. The command will install the agent and add your account’s unique API key to the configuration file.
 - **Optional**: Navigate to the Linux agent configuration file at ``/opt/netuitive-agent/conf/netuitive-agent.conf`` and add a metrics blacklist or whitelist under the ``[[NetuitiveDockerCollector]]`` section to reduce the number of metrics you receive.

### Regex Examples
- Escape special regex characters `` . * / `` using a ``/``. The following would match `containers.*.blkio.` metrics and exclude them from collection.   
`metrics_blacklist = containers\..*\.blkio\..*`
- Match multiple containers between ( ) and separated by |. The following would match any of the following container IDs and exclude them from collection: `abcdef123456`, `123456abcdef`, `ghijkl789012`.  
`metrics_blacklist = containers\.(abcdef123456|123456abcdef|ghijkl789012)\..*`
