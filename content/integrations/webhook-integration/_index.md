---
title: "Webhook Integration"
#date: 2018-12-11
draft: false
tags: ["#webhook", "#integrations",]
author: Lawrence Lane
---
Webhooks are an HTTP/HTTPS callback request sent to a desired URL in response to some event, which could be pushing code to a repository or a comment being posted in an online community. A Webhook integration can be used to generate external events in Metricly’s Event Explorer, meaning you could create policies based on the content of those messages.

## Configure

1. From the top navigation menu, select **Integrations**.
2. Select the **Webhook** card. The name should be already populated, and Data Collection should be enabled.
3. Copy the **API key**.  
4. Select an element from your inventory to associate the Webhook events with.
5. Post to Metricly’s API using the URL included in the instructions.

Metricly recommends using your Webhook external events as a basis for a policy using external event conditions. 
