---
title: "Metrics"
date: 2018-12-11
draft: true
tags: ["java", "integrations", "metrics", "agents"]
author: Lawrence Lane
---

## Instrumenting Metric Values
1. First, set up the [Java Agent][1].
2. In the `zorka/scripts/` directory, create a **.bsh file** for the application you want to monitor.
3. Call **zorka.require** to load any extension scripts your application depends on.
4. Define the function(s) you want Zorka to monitor using the template below. The template will establish namespace by creating a function that returns a reference to its own instance and then defines a variable that holds an instance of the function.

```
__myapp() {

//function code
//goes here

returnthis;
}

myapp = __myapp();
```
5\. Within the function(s) you created in the previous, complete the following:

  - Define the JMX mbean that will host the method call statistics.

  ```
    _mbean="zorka:type=ZorkaStats,name=MyAppStats";
  ```
  - Create a configuration section that zorka can spy on.

  ```
    spy.add(spy.instrument(MyAppRequests"))
  ```
6\. Specify which method will be instrumented.

```
include(spy.byMethod("com.netuitive.agent.myappclass", "invoke")));
```
7\.  Navigate to the **zorka.properties** file, and add the file you created in step 2 to the list of loaded scripts.  
8. Update the **zorka.application** setting to your application’s name.

```
 zorka.application = my-app
```
9\. **Save** all edited files and restart the Java agent. You should find your JVM element in Metricly with general JVM system metrics and MyAppStats method call metrics.

## Config Options

### Add an Action on Method Entry


```
 .onEnter(spy.zorkaLog("INFO", "MyApp", "Request occurred."))
 ```
If you have multiple actions, separate them with a comma.

 ```
 .onEnter(
   spy.fetchArg("operator", 1),
   spy.zorkaLog("INFO", "MYAPP", "${operator}"))
 ```

### Declare Additional Metric Names

```
 spy.zorkaStats(mbsName, beanName, attrName, keyExpr, timeField, actions)
```
- `mbsName` is name of your mbean server (typically java or jboss).
- `beanName` is the name of the mbean used to host statistics in the file.
- `attrName` is the name of the attribute where the ZorkaStats object will be visible.
- `keyExpr` is the value used as a key in ZorkaStats.
- `timeField` indicates the field that stores method execution time (the defaults to T if not passed).
- `actions` determines what should be done when aggregating data.


[1]: /integrations/agents/java-agent
