---
title: "Manual Install"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux",]
author: Lawrence Lane
#pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 3
---
## Via RPM  
```
rpm --import https://repos.app.netuitive.com/RPM-GPG-KEY-netuitive
rpm -ivh https://repos.app.netuitive.com/rpm/noarch/netuitive-repo-1-0.2.noarch.rpm
yum -y install netuitive-agent
```

## Via DEB
```
curl -s https://repos.app.netuitive.com/netuitive.gpg | apt-key add
apt-get install -y apt-transport-https
echo "deb https://repos.app.netuitive.com/deb/ stable main" > /etc/apt/sources.list.d/netuitive.list
apt-get -y update
apt-get install -y netuitive-agent
```
