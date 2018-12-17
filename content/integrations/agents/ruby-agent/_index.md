---
title: "Ruby Agent"
#date: 2018-12-12
draft: false
tags: ["ruby", "integrations", "agents" ]
author: Lawrence Lane
---
The Ruby Agent comprises three Ruby gems--[netuitived](https://rubygems.org/gems/netuitived), [netuitive_ruby_api](https://rubygems.org/gems/netuitive_ruby_api), and [netuitive_rails_agent](https://rubygems.org/gems/netuitive_rails_agent)--that work in tandem to monitor the performance of your Ruby applications.

- **netuitived**: allows metrics to be exported to the Metricly API.
- **netuitive_ruby_api**: allows for easy integration with `netuitived`.
- **netuitive_rails_agent**: provides default Ruby on Rails metrics and sends them to  `netuitived` using `netuitive_ruby_api`.

The Ruby Agent can also be tuned to help application performance and used to read garbage collection metrics. The flow-chart below details the flow of data from your application to Metricly.

![old diagram](/images/_index/old-diagram.png)

## Configure

### 1. Copy API Key From Ruby Integration
1. From the top navigation menu, select **Integrations**.
2. Select the **Ruby** card. The name should be already populated, and Data Collection should be enabled. A unique API key for your account has already been generated.
3. Copy the **API Key**.

### 2. Install Gems
1. Install the **netuitived gem** using the below command:

```
gem install netuitived
```
2\. Run the start script once the gem has been installed:

```
netuitived start
```

3\. Enter the desired element name into the prompt, then type into the prompt the unique API key generated for your account that you copied in step 1.

  - Optionally, edit the** netuitived config/agent.yml** file if you wish to update the caching interval, use environment variables, change the host location instead of using the default, or want to adjust the logging configuration options.

4\. Add the following line to the **Gemfile** in your rails application:

```
gem 'netuitive_rails_agent'
```

6\. Inside your rails application project directory, run the following code snippet to install both the **netuitive_rails_agent** and **netuitive_ruby_api gems**:

```
bundle install
```

7\. **Restart** your rails application and begin monitoring your data with Metricly.
