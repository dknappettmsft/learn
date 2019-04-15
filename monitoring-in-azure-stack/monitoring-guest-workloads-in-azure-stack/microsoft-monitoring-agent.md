# Microsoft Monitoring Agent

Although, Operations Manager can provide agentless monitoring, many of its key monitoring features require you to deploy an agent to be deployed to the monitored computer. This provides several benefits such as:

- Scripts can be run locally to collect monitored data.

- Monitored data is filtered by the agent before it is sent over the network back to Operations Manager.

- Monitors and Rules are copied to the agent so they can run locally reducing network overhead.

- Agent action accounts can be used to provide a level of security when monitoring data on sensitive computers.

You can install the Microsoft Monitoring Agent manually or by using the Operations Manager console. Using the console is the preferred method because you can deploy the agent to multiple computers at the same time, which is useful when there are a large number of computers that you need to manage. You can use a Lightweight Directory Access Protocol (LDAP) query to select multiple computers on which the agent should be deployed.