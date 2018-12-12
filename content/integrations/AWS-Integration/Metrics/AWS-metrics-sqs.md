---
title: "SQS Metrics"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "sqs"]
author: Lawrence Lane
---


## Collected
| Friendly Name                              | Fully Qualified Name (FQN)                    | AWS Metric                            | Statistic | Units   | BASE |
|--------------------------------------------|-----------------------------------------------|---------------------------------------|-----------|---------|------|
| Approximate Age of Oldest Message          | aws.sqs.approximateageofoldestmessage         | ApproximateAgeOfOldestMessage         | average   | seconds | yes  |
| Approximate Number of Messages Delayed     | aws.sqs.approximatenumberofmessagesdelayed    | ApproximateNumberOfMessagesDelayed    | sum       | Count   | yes  |
| Approximate Number of Messages Not Visible | aws.sqs.approximatenumberofmessagesnotvisible | ApproximateNumberOfMessagesNotVisible | sum       | Count   | yes  |
| Approximate Number of Messages Visible     | aws.sqs.approximatenumberofmessagesvisible    | ApproximateNumberOfMessagesVisible    | sum       | Count   | yes  |
| Number of Empty Receives                   | aws.sqs.numberofemptyreceives                 | NumberOfEmptyReceives                 | sum       | Count   | yes  |
| Number of Messages Deleted                 | aws.sqs.numberofmessagesdeleted               | NumberOfMessagesDeleted               | sum       | Count   | yes  |
| Number of Messages Received                | aws.sqs.numberofmessagesreceived              | NumberOfMessagesReceived              | sum       | Count   | yes  |
| Number of Messages Sent                    | aws.sqs.numberofmessagessent                  | NumberOfMessagesSent                  | sum       | Count   | yes  |
| Sent Message Size                          | aws.sqs.sentmessagesize                       | SentMessageSize                       | average   | Bytes   | yes  |
