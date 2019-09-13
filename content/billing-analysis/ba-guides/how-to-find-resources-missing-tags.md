---
title: "Find Resources Missing Tags"
#date: 2019-07-29
draft: false
categories:
tags: ["#tools", "#aws services", "#cost", "#getting started", "#guides"]
author: Lawrence Lane
weight: 3
---

You already have a tagging strategy in place and you've mastered exploring your costs by services, attributes, and tags. So what's next?

Another great way to discover savings opportunities (or simply gain more context for your bill) is to examine what _hasn't_ been tagged. The easiest way to find resources that are missing tags is to use the Billing Analysis tool.

## Prerequisites

This guide assumes you have already created User-Defined Cost Allocation Tags from your AWS Console. If you have not, follow the steps below to do so for your AWS resources.

### Promote Resource Tags to Cost Allocation Tags

There are two kinds of Cost Allocation tags
- AWS-Generated Cost Allocation Tags
- User-Defined Cost Allocation Tags

#### 1. Activate AWS-Generated Tags
This creates a `resource created by` tag automatically on all resources.

1. Log in to your **AWS Console**.
2. Navigate to **Billing** > **Cost Allocation Tags**.
3. Select **Activate** under AWS-Generated Cost Allocation Tags.
![activate-cost-allocation-tags](/images/how-to-find-uncategorized-costs/activate-cost-allocation-tags.png)

#### 2. Create User-Defined Cost Allocation Tags

User-Defined cost allocation tags, once created, appear in **Billing** > **Cost Allocation Tags**. You must use the AWS Tag Editor to create these tags.

1. Log in to your **AWS Console**.
2. Navigate to **Resource Groups** > **Tag Editor** > **Manage Tags**.
![tag-editor-manage-tags](/images/how-to-find-uncategorized-costs/tag-editor-manage-tags.png)
3. Create your `Key-Value` tags and assign them to your resources.

Now you are ready to use Cost Allocation Tags to analyze your bill in Metricly.

## Two ways to find resources that are missing tags

### 1. Group costs by tag

1. Log in to Metricly and navigate to **Cost Management** > **Billing Analysis**.
2. Select the time frame you wish to analyze.
  - A larger time frame may help you discover the most significant resources missing tags.
3. Select **Configure**. A modal appears.
4. Choose the **Stacked View** visualization.
5. Choose a `tag value` from **Options** > **Group By**. In this example, we are grouping by the `app` tag.
6. Notice the bar missing a label. This bar represents all of your spend missing this tag.
![spend-without-app-tag](/images/how-to-find-uncategorized-costs/spend-without-app-tag.png)
7. Add a **Stacked By** value, such as `service`, to gain more insight into your untagged resource spend.
![untagged-costs-stacked-by-service](/images/how-to-find-uncategorized-costs/untagged-costs-stacked-by-service.png)
8. Notice now the untagged spend is divided by each service. You can use these insights to further explore your costs.
 - Change the **Stacked By** value to `Region` to get an idea of where your missing resources are located
 - Change the **Stacked By** value to `Usage Type` for a specific, granular list of costs such as EBS volume usage.

Use this information to triangulate resources you are paying for that may have gone unlabeled. Keeping untagged resources to a minimum is a great way to prevent cost creep!

### 2. Filter billing data by not specified tag

You can also jump straight to untagged resources by filtering by **Tags** > ` * Not Specified *`.

1. Log in to Metricly and navigate to **Cost Management** > **Billing Analysis**.
2. Select the time frame you wish to analyze.
  - A larger time frame may help you discover the most significant resources missing tags.
3. Select **Configure**. A modal appears.
4. Choose the **Stacked View** visalization.
5. Filter by **Tag** > `* Not Specified *`. This automatically selects all costs which are not tagged.
![tag-not-specified-filter](/images/how-to-find-uncategorized-costs/tag-not-specified-filter.png)
6. Now you can group by other dimensions to quickly analyze all untagged spend.
7. Change the **Grouped By** value to `Operations`.
8. Change the **Stacked By** value to `Usage Type`.
9. Now, all untagged operations are broken down by usage type. Hover over a bar to see each operation's amount of spend by usage type.
![untagged-spend-grouped-by-operations](/images/how-to-find-uncategorized-costs/untagged-spend-grouped-by-operations.png)
