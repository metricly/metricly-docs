---
title: "Puppet"
#date: 2018-12-12
draft: false
tags: ["#puppet", "#integrations" ]
author: Lawrence Lane
---

This guide covers how to add the puppet module to your puppet master. The puppet module installs and configures the [netuitive-agent][1] and [CollectdWin][2].

## Installation

**Options**

- Clone the [puppet_metricly_agents](https://github.com/metricly/puppet_metricly_agents) repo on Github
- Download the package via [puppetforge](https://forge.puppet.com/metricly/puppet_metricly_agents).

### 1. Update Init.pp File

1. Navigate to `puppet_metricly_agents/manifests/init.pp`.
2. Find the **`puppet_metricly_agents`** class.
3. Add your Linux and Windows integration API keys found in the Metricly app to the class, replacing `undef`:
![api-key](/images/_index/api-key.png)

  ```
  class puppet_metricly_agents(
    $net_api_key_linux = undef,
    $net_api_key_win   = undef,
    ) {

  ```
4. **Save** the file.

### 2. Update Linux.pp

Update the Linux.pp file with the Linux agent version you are going to use. If you use both Redhat and Debian, both need to be updated with the linux agent version.

#### Redhat

1. Navigate to `puppet_metricly_agents/manifests/linux.pp`.
2. Find the `puppet_metricly_agents::linux` class.
3. Find `package` belonging to `$::osfamily == 'redhat'`.

```
class puppet_metricly_agents::linux {
  $net_api_key_linux = $puppet_metricly_agents::net_api_key_linux
  if $::osfamily == 'redhat' {
    exec { 'install netuitive-agent repo yum':

  creates => '/etc/yum.repos.d/netuitive.repo',
  command => 'rpm --import https://repos.app.netuitive.com/RPM-GPG-KEY-netuitive && rpm -ivh https://repos.app.netuitive.com/rpm/noarch/netuitive-repo-1-0.2.noarch.rpm',
  path    => '/usr/bin',
    }
    package { 'netuitive-agent':
      ensure => '{agentversion}', #replace {agentversion} with an agent version e.g. 0.7.6-188.el6
      before => Service['netuitive-agent'],
    }
}
```
4. Replace` {agentversion}` with an agent version (e.g. **0.7.6-188.el6**). See [RPM Linux Agent versions](https://repos.app.netuitive.com/rpm/x86_64/) for more info.
5. **Save** the file.

#### Debian

1. Navigate to `puppet_metricly_agents/manifests/linux.pp`.
2. Find the `puppet_metricly_agents::linux` class.
3. Find `package` belonging to `$::osfamily == 'debian'`.
4. Replace` {agentversion}` with an agent version (e.g. **0.7.6-188**) See [DEB Linux Agent versions](https://repos.app.netuitive.com/deb/dists/stable/main/binary-amd64/) for more info.
5. **Save** the file.

### 3. Update Windows.pp

1. Navigate to `puppet_metricly_agents/manifests/windows.pp`.
2. Find the `puppet_metricly_agents::windows` class.
3. Replace `{agentversion}` with an agent version (e.g **0.10.6.75**) See [Windows Agent versions](https://repos.app.netuitive.com/windows-agent/index.html) for more info.

```
package { 'CollectdWinService (64 bit)':
   ensure          => '{agentversion}', #replace {agentversion} with an agent version e.g 0.10.6.75
   source          => 'C:/Temp/CollectdWin-x64.msi',
   install_options => ['/quiet', "NETUITIVE_API_KEY=${net_api_key_win}",],
```
4. **Save** the file.
5. Download and install the [MSI package](https://repos.app.netuitive.com/windows-agent/index.html) to the `/modules/puppet_metricly_agents/files/` folder

[1]: https://docs.metricly.com/integrations/agents/linux-agent/
[2]: https://docs.metricly.com/integrations/agents/windows-agent/

You have finished installing the puppet module and agents.
