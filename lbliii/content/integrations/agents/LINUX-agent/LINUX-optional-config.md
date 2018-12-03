---
title: "Optional Config"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux", "elements", "FQNs" ]
author: Lawrence Lane
weight: 8
---

## Changing Element Display Names
You can change the display name of certain elements to help distinguish between each instance.

1. Navigate to **Integrations** > **Linux Integration**.
2. Click **Advanced**; a menu expands.
![Linux Element Display Names](/images/LINUX-optional-config/linux-element-display-names.png)
3. Click the **Element Name** field to edit it.
4. Type the desired name into the field.
  - An element name of ``${meta.originalName}`` would resolve to whatever name comes in with the original element payload before it would be replaced with the optional element name template.
  - The element name template preview in the UI will resolve this field to [original name] as a placeholder because Metricly only knows what the current name is, not what the incoming name might be.
  - An element name of ``${tags.InternalName} (${tags.Name})`` will give you something like `MyServer (ip-10.101.3.99)`
  - An element name of ``${tags.Name} (${attributes.availabilityZone)`` would return something like `ServerX (eu-west-1c)`
5. Select an element to use as a preview for your new element name using the Element To Preview drop-down menu.
6. Next to the Element Name field, click **Preview** to view your new template using the selected element.
7. If you’re satisfied with the name, press **Enter** on your keyboard while in the Element Name field to lock in the name. Exit the integration setup page and wait until the next analytics cycle (5 minutes) to see your changes.

### Example: Adding the Private IP Address to an Element Name
Adding the private IP address to your element names enables your team to immediately begin troubleshooting problematic instances.

```
<#if tags.Name??>${tags.Name}<#elseif tags.aws_autoscaling_groupName??>${tags.aws_autoscaling_groupName}<#else>${meta.originalName}</#if><#if attributes.privateIp??> (${attributes.privateIp})</#if>
{noformat}
```
## Write Metric FQNs to Local File
If you want to keep a local file with a list of metric FQNs (fully qualified names), you can do so by updating the below lines in your `netuitive-agent.conf` file, under the ``[[NetuitiveHandler]]``. By default, this ability is set to False. When set to True, this file updates with any new FQNs as long as the agent is running.

If the agent is started and `write_metric_fqns` is set to `True`, the file is overwritten; it remains unchanged if set to False before starting the agent.

**To Enable:**  

1. Open your `netuitive-agent.conf` file.  
2. Change `write_metric_fqns = False` to `True`.  
3. Confirm your desired path (`metric_fqns_path`) for the file.  
4. **Save**.  

## Update the Hostname Manually
If you’re having issues with the default naming method or the hostname isn’t what you desire, you can manually set the hostname via the agent’s configuration file located at ``/opt/netuitive-agent/conf/netuitive-agent.conf``. Consult the table below for more information.

| Method                            | Description                                                                                                                                                                                                                                                                | Usage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Hard-coded                        | Force a hard-coded desired hostname.                                                                                                                                                                                                                                       | Uncomment the hostname setting. ``# hostname = my_custom_hostname Replace my_custom_hostname`` with your desired hostname, keeping in mind that periods are common separators.                                                                                                                                                                                                                                                                                                                         |
| smart                             | The agent will initially try to use the short FQDN (fully qualifieddomain name). If the short FQDN is “localhost”, the agent will use the value returned by the hostname -s command.                                                                                       | Because smart is the default naming method, do not make changes to this section of the configuration file to continue using it.                                                                                                                                                                                                                                                                                                                                                                               |
| fqdn (fully qualifed domain name) | Comprises three separate methods:fqdn_short, which is similar to the value returned by the hostname -scommand. fqdn, which is the fullhostname value. fqdn_rev, which is the full hostname value but reversed, e.g., com.example.www.                                      | Uncomment the hostname_method setting. ``# hostname_method = smart`` Replace smart with the desired fqdn setting.  `hostname_method = fqdn_rev`                                                                                                                                                                                                                                                                                                                                                |
| uname                             | Comprises two methods:uname_short, which is similar to the value returned by the `uname -n (network node hostname)` command but only the first portion. `uname_rev`, which is the value returned by the `uname -r (kernel release)` command but reversed, e.g., com.example.www. | Uncomment the hostname_method setting. Replace smart with the desired uname setting. `hostname_method = uname_short`                                                                                                                                                                                                                                                                                                                                                                                 |
| hostname                          | Comprises three separate methods:hostname_short, which is the value returned by the hostname -scommand. hostname, which is the full hostname value. hostname_rev, which is the full hostname value but reversed, e.g., com.example.www.                                    | Uncomment the hostname_method setting.  ``# hostname_method = smart`` Replace smart with the desired hostnamesetting. `hostname_method = hostname`                                                                                                                                                                                                                                                                                                                                             |
| shell                             | Uses the string set in the hard-coded hostname variable as ashell command. The agent will use its output (with spaces trimmed from both ends) as the hostname.                                                                                                             | Uncomment the hostname setting. ``# hostname = my_custom_hostname`` Replace my_custom_hostname with your desired shell command. For example, with the following shell command you can use the AWS metadata endpoint to retrieve the instanceId and ensure uniqueness. `hostname = curl -sS "http://169.254.169.254/latest/meta-data/instance-id"` | xargs echo "$HOSTNAME -" Uncomment the hostname_method setting. ``# hostname_method = smart` Replace smart with shell. |
