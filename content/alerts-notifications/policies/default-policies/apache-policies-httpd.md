---
title: "Apache HTTPD Policies"
date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "apache", "httpd"]
author: Lawrence Lane
---

| Linux Apache HTTPD – Depressed Traffic Volume | 30 min | httpd.<host>.ReqPerSec has a lower baseline deviation  | WARNING | The number of requests per second has been lower than expected for at least the past 30 minutes.  |
|-----------------------------------------------|--------|--------------------------------------------------------|---------|---------------------------------------------------------------------------------------------------|
| Linux Apache HTTPD – Elevated Traffic Volume  | 30 min | httpd.<host>.ReqPerSec has an upper baseline deviation | WARNING | The number of requests per second has been higher than expected for at least the past 30 minutes. |
