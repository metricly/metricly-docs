---
title: "Sudden Change Detection"
#date: 2018-04-12
draft: false
categories:
tags: ["#getting started", "#analytics", "#metrics"]
author: Lawrence Lane
---
Sudden Change is a time-series metric used to analyze trends of historical data and make predictions based on past behavior.

 This process finds an expected average of activity by **generating data points every 5 minutes** in a sliding, one-hour window of time. It then uses this data to make predictions on the next interval.

When the future point is actualized and falls _outside_ the expected prediction range, that interval is defined as a sudden change alert. You can configure the scope of this metric’s prediction range by adjusting the acceptable percentage change of the future interval; doing so increases or decreases the sensitivity of your policy and affects the frequency of any associated alerts.

![Sudden Change Example](/images/sudden-change-detection/sudden-change-example.png)

Sudden Change is useful for trend analysis on hourly min/max rollup data, like disk space usage or number of page hits. A best practice to consider when setting up a Sudden Change condition is to understand the average behavior of a metric beforehand. If the behavior is naturally prone to fluctuate, use a higher percentage. This widens the predictability scope, avoiding unnecessary policy activity and alerts.

## Sudden Change Example 1

You are monitoring the response time for a transaction. The conditions for the policy are looking for increases in response time of more than 50%, with a duration of 2 hours. An alert is generated after the response time has exceeded the average by 50% for that specified duration.

## Configuring The Sudden Change Condition
Complete the following steps to configure a new policy using the Sudden Change condition:

1. Navigate to **Alerts** > **+ Add New Policy**.
2. Under the **Conditions** tab, select **Add Condition** > **Add Metric Condition**.
3. In the Deviation(s) section, check **Sudden Change**.
 - Select **Increase/Decrease by More Than**.
 - Enter a `percentage value`.

![Conifgure Sudden Change](/images/sudden-change-detection/conifgure-sudden-change.png)

## Sudden Change Example 2

The following graph depicts a policy with a sudden change deviation condition on a certain metric. In this example, an alert triggers due to a sudden change alert (in red) on the 25th data point.

![Sudden Change Example 2](/images/sudden-change-detection/sudden-change-example-2.png)

- **Black Dots**: Each black point represents 1 of the 24 previous 5-minute values (PT5M) of a metric
- **Black Line**: A best-fit regression line through the black points
- **Blue Line**: The projected trend of the 25th data point, based off of the historical data shown
- **Blue Dot**: The predicted value of the 25th data point
- **Red Line**: Breadth of sudden change, deviating from the expected projection in blue
- **Red Dot**: 25th data point’s actual observed value

{{% notice note %}}
This graph is for functionality demonstration and not found in the product. In CloudWisdom, a red dot appears on the Metric Explorer graph where the sudden change alert occurred.
{{% /notice %}}

## How a Percent Drop is Measured
A percent drop, or step change, is computed as:

``| (projected value) - (observed value) | / | (projected value) |``

The sudden change algorithm returns this value for use by a condition in a policy. If the value exceeds the threshold in the policy condition, then the condition is true. If all the other conditions in the policy (if any) are also true, then an alert is emitted.

## Confidence Validation

Before reporting back the above value as a potential change, the algorithm performs several checks.

One of these checks is designed to determine if the regression model is a good enough fit for us to have any confidence in it’s projected value. Another check is used to add confidence that the observed value is sufficiently different from the projected value to be truly “anomalous”. Additional checks deal with detecting the trend in values leading up to the observed value. For example, if the trend was already negative and the actual observed value is just continuation of that trend, then no drop will be reported. The algorithm also requires data points to be consistently available and not be sparse.

In the above example, it is possible that some of these checks may have failed. In that case, the algorithm reports back that there was no drop.

## Best Practices
When configuring a condition for sudden change deviation, we recommend setting a **duration of no longer than 5 minutes**. This is due to the nature of the alert you are trying to capture: a single, sudden change in activity. Expecting a secondary sudden change in a longer duration of time may cause your policy to never activate, meaning you could miss otherwise genuine alerts.
