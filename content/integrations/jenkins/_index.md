---
title: "Jenkins"
#date: 2018-12-11
draft: false
tags: [ "integrations",]
author: Lawrence Lane
---
Jenkins is  an open source automation server which enables developers around the world to build, test, and deploy their software.

## 1. Download the Metricly Plugin file for Jenkins

1. Go to the [Jenkins Metricly Plugin](https://github.com/metricly/jenkins-metricly-plugin/releases/latest) release page.
2. Download the **jenkins-metricly-plugin.hpi** file.
![jenkins-metricly-hpi-file](/images/_index/jenkins-metricly-hpi-file.png)


## 2. Upload .hpi file to Jenkins

1. Open Jenkins as an Administrator.
2. Navigate to **Manage Jenkins**.
![manage-jenkins](/images/_index/manage-jenkins.png)
3. Select **Manage Plugins**.
![jenkins-manage-plugins](/images/_index/jenkins-manage-plugins.png)
4. Select the **Advanced** tab.
![jenkins-adv-tab](/images/_index/jenkins-adv-tab.png)
5. Under Upload Plugin, select **Choose File** > **jenkins-metricly-plugin.hpi**.
6. Select **Upload**.
7. Enable the **Restart** checkbox.
![restart-jenkins](/images/_index/restart-jenkins.png)


## 3. Edit Global Settings

1. Navigate to **Manage Jenkins**.
2. Select **Configure System**.
![jenkins-configure-system](/images/_index/jenkins-configure-system.png)
3. Scroll to **Metricly Plugin**.
4. Add the following configuration:
 - **Custom API Key**:  Input your Metricly CUSTOM integration API key [Found here](https://us.cloudwisdom.virtana.com/#/profile/integrations).
 - **Hostname**: Element name for all metrics from this Jenkins installation (default: `Jenkins`).
 - **API Location**: Metricly API location (default: `https://api.us.cloudwisdom.virtana.com/`).
5. **Save**.

### Advanced Global Settings

You can also configure **Job Name Black/Whitelist RegEx** from this menu.

1. Select **Advanced**.  
![jenkins-metricly-plug-adv](/images/_index/jenkins-metricly-plug-adv.png)
2. Complete the following fields:
 - **Job Name Whitelist RegEx**: Only jobs matching this RegEx submit statistics to CloudWisdom when field is not empty.
 - **Job Name Blacklist RegEx**: Jobs matching this RegEx do not submit statistics to CloudWisdom --- **even when they match the whitelist** --- if included in this field.
3. **Save**.
