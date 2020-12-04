---
title: "Inventory"
#date: 2018-04-12
draft: false
categories:
tags: ["#getting started", "#metrics", "#elements", "#inventory page"]
author: Lawrence Lane
type: docs
---

Your inventory is the elements that make up your environment, from your java virtual machines to your Amazon EC2s. CloudWisdom’s Inventory Explorer allows you to view and search the elements in your inventory.

## About Elements
The physical or logical components that CloudWisdom monitors are called elements. An element can be a physical entity, such as a server or network element, a virtual entity, such as a transaction, or a business entity, such as a company traded on the stock market. Elements are the base component that CloudWisdom uses to analyze metrics and determine the status of your environment.

All elements share the following characteristics:

- A unique name and identifier in CloudWisdom.
- Descriptive attributes, or characteristics, assigned by an integration.
- Events that are triggered when the conditions in policies are met.
- A tag or tags used to label and organize elements.
- An element type, usually assigned by an integration.

### Attributes

An attribute is a property or characteristic that describes an element. Having attributes gives you access to more statistical data that can be used to troubleshoot issues. Most elements receive attributes from their integration.

{{% notice info %}}
For example, with attribute information, you can see the number and type of CPU running on a server element, while also viewing an event that was generated based on that element’s CPU value.
{{% /notice %}}

### Element Types

Each element has a type that determines how it is processed and represented by CloudWisdom. Element type is also used as a filter in list pages in the UI. The types of elements in your environment will vary based on the integration that you use<superscript>1</superscript>.

| Integration      | Element Type in CloudWisdom       |
|------------------|-----------------------------------|
| AWS              | ASG (Auto Scaling Group)          |
| AWS              | Custom Cloudwatch Metrics         |
| AWS              | DynamoDB                          |
| AWS              | EBS (Elastic Block Store)         |
| AWS              | ECS (EC2 Container Service)       |
| AWS              | EC2 (Elastic Compute Cloud)       |
| AWS              | Elasticache Elasticache           |
| AWS              | ELB (Elastic load balance         |
| AWS              | EMR (Elastic Map Reduce)          |
| AWS              | Kinesis (Stream)                  |
| AWS              | Lambda                            |
| AWS              | RDS (Relational Database Service) |
| AWS              | Redshift                          |
| AWS              | SQS (Simple Queue Service)        |
| Browser          | BROWSER                           |
| Custom           | N/A                               |
| Docker           | Docker Container                  |
| Java             | JVM                               |
| Java             | CLUSTER                           |
| Linux (Metricly) | SERVER                            |
| Ruby             | RUBY                              |
| Windows          | WINSRV                            |
| Collectd         | SERVER                            |
| Diamond          | SERVER                            |
| StatsD           | StatsD                            |
