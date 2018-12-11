---
title: "Salt"
date: 2018-12-11
draft: true
tags: ["salt", "integrations", "configuration management"]
author: Lawrence Lane
---

Salt (or SaltStack) is configuration management software that’s designed to automate infrastructure setup. Metricly’s formula will help get our Linux agent running on all of your minions quickly, so you can start seeing basic host data (as well as collector information if you so choose) for your whole environment using a single command.

## Configuration
1. Add the `netuitive-agent-formula` to a directory on your Salt master.  
```
mkdir -p /metricly/formulas
cd /metricly/formulas
git clone https://github.com/netuitive/netuitive-agent-formula.git
```
2. Add the new directory to `file_roots`:

 ```
 file_roots:
   base:
     - /srv/salt
     - /metricly/formulas/netuitive-agent-formula
 ```

3. Restart the Salt Master.
4. Include the formula in an existing state tree or from a top file. Read more about this as well as about using formulas [here](https://docs.saltstack.com/en/latest/topics/development/conventions/formulas.html#usage).
5. Copy the contents of our [example salt pillar](https://github.com/netuitive/netuitive-agent-formula/blob/master/pillar.example) and merge it into your pillar file.
6. Edit the default pillar settings as necessary, ensuring you maintain proper nesting and formatting.
7. Replace the `api_key` value with the Linux integration API key from Metricly. To find this API key, point to the user account menu in the top right-hand corner of Metricly and select Integrations. Your Linux API key is found next to the integration listed as _INFRASTRUCTURE_.
8. Run the **init.sls** script.
9. Apply the formula to all of your salt minions.  
```
sudo salt '*' state.apply netuitive-agent
```
 - The pillar applies to your minions universally. If you want a minion to use a different version of a collector from a separate pillar file, you’ll need to specify which minion in your `top.sls` file. If you update the pillar file, you’ll need to reapply the pillar to your minions.
