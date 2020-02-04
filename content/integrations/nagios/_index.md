---
title: "Nagios"
#date: 2018-12-12
draft: false
tags: ["#nagios", "#integrations" ]
author: Lawrence Lane
---
Nagios is a comprehensive enterprise-class open source monitoring service. You can use our [Metricly Event Handler](https://github.com/netuitive/netuitive-event-handler) to send your Nagios events to CloudWisdom.

## Sending Nagios Events to CloudWisdom

1. Hover on your account name in the bottom left-hand corner and click **API Keys** from the drop-down menu.
2. Copy the **API Key** from the _Custom_ integration in the table.
3. Install the Metricly Event Handler.
4. Download the [Netuitive Event Handler](https://github.com/netuitive/netuitive-event-handler) to the `/bindirectory`.

```
sudo curl
http://repos.app.netuitive.com/cli-agent/netuitive-event-handler-linux -o "/bin/netuitive-event-handler"
```
5\. Ensure the file is executable (use the `chmod` command).

```
sudo chmod 755 /bin/netuitive-event-handler
```
6\. Create and configure the `/etc/netuitive/netuitive-event-handler.yaml` file using the API key you copied in step 2 and the URL to the events ingest API.

```
apikey: your-apikey
url: "https://api.app.netuitive.com/ingest/events"
```
7\. On your Nagios server, navigate to the **commands.cfg** file, located at `etc/nagios/objects/commands.cfg`.  
8\. In the **commands.cfg** file, create a _host_ and _service_ notification.

Host

```
define command{
  command_name	notify-host-by-netuitive-event
  command_line	/bin/netuitive-event-handler -s Nagios -e "$HOSTALIAS$" -t "Host
$HOSTALIAS$ is $HOSTSTATE$" -l
"$HOSTSTATE$"  -m "Host $HOSTALIAS$ is
$HOSTSTATE$ - Info: $HOSTOUTPUT$"
}
```

Service

```
define command{
  command_name	notify-service-by-netuitive-event
  command_line	/bin/netuitive-event-handler -s Nagios -e "$HOSTALIAS$" -t
"Service $SERVICEDESC$ is $SERVICESTATE$" -
l "$SERVICESTATE$"  -m "Service
$SERVICEDESC$ is $SERVICESTATE$ - Info:
$SERVICEOUTPUT$"
}
```

9\. Open the Nagios UI.  
10. Under the Shortcuts column, click **Hosts**.  
11. Select the **checkbox** next to your Nagios host server, and then click **Edit**.  
12. Under the Actions section of the menu on the right, click **Add Service Checks**.  
13. Input a Service Description.  
14. Click **Save service and let me edit it further**.
15. Once the service has been saved, click the **Advanced** tab.
16. In the **check_command** field, input the command you want Nagios to run to perform the service check.
17. In the **event_handler** field, input the following:

```
notify-service-by-netuitive-event
```
18\. In the **event_hander_enabled** field, input a `1` to enable the event handler.  
19\. Check **CloudWisdom** for your new Nagios events.
