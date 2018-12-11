---
title: "ASG Recommendations"
date: 2018-12-03
draft: true
categories:
tags: ["reports", "asg" ]
author: Lawrence Lane
---

The Auto Scaling Group (ASG) Recommendations report provides a summary of the EC2 instance hours managed by all of your Auto Scaling Groups over the past few weeks. The data is summarized by hour and day for the preceding one-to-four weeks depending on how long Metricly has been monitoring the ASG.
![asg report breakdown](/images/reports-asg-recommendations/asg-report-breakdown.png)

1. **Total Instance Count graph**: This graph depicts the average total number of instances managed by all of your ASG(s) by hour and day. It also shows the maximum and minimum total instance counts observed by hour and day.
2. **Auto Scaling Groups table**: This table summarizes the observed EC2 instance counts managed by your ASGs, including Estimated Cost, Minimum Instances Seen, Minimum Instances Allowed, Maximum Instances Seen, Maximum Instances Allowed, Instance Hours, whether the Recommended Instance Count Metric is enabled, Instance Type, Region, whether the ASG is using Spot Instances, the Platform on each ASG, and the type of Tenancy. Use the filters at the top of the page to filter the elements displayed in the table/graph.
3. **Element Usage Summary**: The number on the left is the number of ASGs monitored by Metricly for which there is sufficient data to produce the report. Some ASGs that are monitored by Metricly may be missing from the report if there is less than a week of data available for them. The number on the right is the total average EC2-instance hours across all of your ASGs.

{{% notice tip %}}
The maximum number of instance hours in a week for a single EC2 instance is 168. So an ASG with 2 instances active for an entire week will contribute 336 instance-hours to the total.
{{% /notice %}}


## Tuning your ASGs
By analyzing the instance count and the CPU utilization across managed instances over several weeks, the ASG Recommendations report can provide simple recommendations to help you right-size each ASG to match the observed and expected load. You can use the ASG Recommendations report to try out different settings, from aggressively minimized to more conservative instance counts to see how this might affect the overall utilization and EC2 costs.

### Opening the Tuning Settings

1. Navigate to **Reports** > **ASG**.
2. In the **Auto Scaling Groups table**, click one of the Element names. A menu will appear.
3. Click **Tune Auto Scaling Group**. You can now tune the ASG as you wish using the settings in the left menu.

Refer to the image above when reading the following sections.

![asg full breakdown](/images/reports-asg-recommendations/asg-full-breakdown.png)

#### (1) Historical Charts
These charts let you visualize the historical behavior of the ASG. The Historical Instance Count chart displays the average instance count (and max/min instance count range) for the ASG over the last one-to-four weeks (depending on the available data). The Historical Utilization chart displays the average utilization across the EC2 instances managed by the selected ASG over the same period.


#### (2) Projected Charts
The Tuned Instance Count chart shows the recommended instance count for the ASG by hour of day as determined from the historical utilization, historical instance count, and the selected tuning settings (see below). The Projected Tuned Utilization chart shows the expected average CPU utilization across the instances managed by the ASG based upon the recommended hourly instance counts.


#### (3) Tuning Settings
You can try different tuning settings to do a what-if analysis on the ASG. The tuning settings directly control the Tuned Instance Count and Projected Tuned Utilization charts. The settings are:

  - **Utilization Statistic**: The utilization statistic used to tune the instance count. Using the maximum utilization is the most conservative, as the target should never exceed the value. The other settings here are increasingly more aggressive the further the setting is away from the maximum average utilization, e.g., 80th Percentile signifies that the utilization should exceed the target utilization 20% of the time.
  - **Target Utilization**: The target average utilization across the EC2 instances manged by the ASG. A higher target will result in smaller number of instances with a higher average utilization.
  - **Maximum Scale-In Rate**: Controls the rate at which the instance count can reduce. A higher scale-in rate results in a tighter profile and a lower overall instance count. For example, if your usage profile is fixed in time it may be acceptable to scale-in abruptly when a period of heavy load stops. Conversely, if your usage profile is more fluid, it may be more appropriate to slowly decrease the number of instances in case of lag in the load.
  - **Scale-out Early**: If the utilization is expected to rise in the next hour, the setting increases the instance count early to allow for provisioning time and variances in the time of utilization increase.
  - **Minimum Instance Count**: This is a hard lower limit on the number of instances the ASG should maintain at all times. If you allow the ASG to scale-in to zero instances, an additional _Zero Utilization Threshold_ setting is enabled.
  - **Update frequency**: This setting controls how often the instance count should update. The default is hourly, which gives the optimal tuning results. The weekly setting calculates the peak instance count needed and uses this value for the entire week. The daily setting calculates the peak instance count needed each day and uses this for the entire day.

#### (4) Tuning Model
The _Aggressive_ and _Conservative_ options apply default presets to the tuning settings. The Aggressive profile aims for a high utilization and low instance count. The Conservative profile aims for a lower utilization with allowances for scaling out early. Note that the aggressive profile is not the most aggressive nor is the conservative profile the most conservative combination of settings. The individual tuning options can be refined after choosing a preset. Changing any of the tuning settings will automatically change the tuning model to Custom.


#### (5) Estimated Cost / Projected Savings
This section shows the estimated historical cost over the observed period. Click the expand icon  to show additional data about the instance and observed period. To the right of the _Estimated Historical cost_ is the Projected savings (percent change) and cost if you were to implement the Tuning Settings on the left. Clicking the expand icon  on the _Estimated Historical Cost_ drop-down will also show additional information about the projection.


#### (6) Recommended Instance Count
Click **Activate** to enable the _Recommended Instance Count metric_.

##### Enabling the Recommended Instance Count metric
After reviewing tuning settings and choosing a recommended instance count profile that you are happy with, you can enable the instance count profile as a metric on the ASG available for use in dashboards, policies, etc.

1. Adjust the tuning settings and/or choose a preset as necessary.
2. Click **Activate Settings** (or _Update Settings_ if you’ve already activated settings but made additional changes). It may take a few minutes, but the Recommended Instance Count metric will now be available on the selected ASG element.

{{% notice tip %}}
You can disable the metric by clicking **Deactivate Settings**.
{{% /notice %}}

## Tips
### Creating a Recommended Instance-related policy
You can use the Recommended Instance Count in a policy to adjust an ASG instance to the desired value.

1. Enable the Recommended Instance Count metric (if it’s not enabled already). It may take a few minutes to appear, but the Recommended Instance Count metric (metricly.aws.autoscaling.recommendedinstances) is now available on the selected element.
2. Navigate to the Policies page, and click **New Policy**.
3. Set the scope of the policy to the desired ASG instance(s).
4. Click the **Conditions** tab. For the condition, set the Metric field to `metricly.aws.autoscaling.grouptotalinstances`.
![step 4](/images/reports-asg-recommendations/step-4.png)
5. Select the Metric Threshold checkbox under Deviation(s), set the drop-down to Not Equal To, and set the metric field to metricly.aws.autoscaling.recommendedinstances.
![step 5](/images/reports-asg-recommendations/step-5.png)
6. Click the **Actions** tab. Select a category and add a desired notification so you’ll be notified whenever the metric `metricly.aws.autoscaling.grouptotalinstances` has a different value than `metricly.aws.autoscaling.recommendedinstances`.

You can now use this notification in a script to adjust your instance count as performance needs fluctuate.

### General Tips
- If you currently have a fixed instance count for your ASG and cannot scale every hour, consider setting the Update Frequency to daily or weekly—this can often still provide considerable savings.
- Change the Utilization Metric setting to see the statistic within the minimum/maximum range in the historical utilization chart. For instance, if the 95th percentile utilization is much lower than the maximum utilization it demonstrates greater volatility.
- If the Utilization Metric is set to 80th percentile, then we expect the projected CPU utilization to exceed the target 20% of the time. If the Target Utilization is high, it is possible that the projected CPU utilization will exceed 100%. This indicates that the settings are incompatible, and it is recommend that you use a higher utilization statistic, such as the 95th percentile or maximum.
- The report can sometimes recommend an increase in the instance count. This typically occurs if the historical utilization is higher than the target utilization. This is not a problem but simply indicates that you may want to increase the instance count in your ASG to meet your utilization goal.
- You can zoom in on any of the graphs by clicking and dragging across a section of the graph (similarly to zooming in on the Event Explorer graph).
