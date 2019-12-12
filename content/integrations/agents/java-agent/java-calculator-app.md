---
title: "Use Calculator App"
#date: 2018-12-11
draft: false
tags: ["#java", "#integrations", "#agents"]
author: Lawrence Lane
---
To to run the calculator app with the zorka agent, use the following command:

```
java -javaagent:/opt/netuitive-zorka-agent/netuitive.jar=/opt/netuitive-zorka-agent/ -jar /opt/zorka-core-test.jar
```

## Calculator.java Source

```
package com.netuitive.agent.test;

public class Calculator {

public Integer calculate(String operator, Integer first, Integer second) {

if (operator.equals(“+”)) {
return add(first, second);
} else if (operator.equals(“-“)) {
return minus(first, second);
} else if (operator.equals(“*”)) {
return multiply(first, second);
} else if (operator.equals(“/”)) {
return divide(first, second);
} else {
throw new IllegalArgumentException(“‘” + operator + “‘ is not supported, use one of [+|-|*|/] operators”);
}
}

private Integer add(Integer first, Integer second) {
return first + second;
}

private Integer minus(Integer first, Integer second) {
return first – second;
}

private Integer multiply(Integer first, Integer second) {
return first * second;
}

private Integer divide(Integer first, Integer second) {
return first / second;
}
}
```

## Example

Below is an example file called `calculator.bsh` that instruments metrics based on basic calculator operation method calls. When a user inputs an operator, the application will fetch the argument, calculate the result, and log the action into the Zorka Log file. Once the actions are submitted to the agent on the Java server, CloudWisdom will create a metric for each input into the ${operator} parameter (e.g., a metric for `+`, `-`, `*`, and `/`).

```
// Call zorka.require(...) to load additional scripts that this one depends on.
zorka.require("jvm.bsh");

// Simulate namespace.
__calculator() {

// Define JMX bean to host method call stats.
_mbean = “zorka:type=ZorkaStats,name=CalculatorStats”;

// Add the spy definition to instrument method “calculator”
// of “com.netuitive.agent.test.Calculator” class.
// The “calculate” method call statistics (calls, errors, time)
// are grouped/keyed by the method’s first argument (“operator”).
spy.add(spy.instrument(“CALCULATOR”)
.onEnter(
spy.fetchArg(“operator”, 1),
spy.zorkaLog(“INFO”, “CALCULATOR”, “${operator}”))
.onSubmit(
spy.zorkaStats(“java”, _mbean, “stats”, “${operator}”))
.include(spy.byMethod(“com.netuitive.agent.test.Calculator”, “calculate”))
);

return this;
}

calculator = __calculator();

```
