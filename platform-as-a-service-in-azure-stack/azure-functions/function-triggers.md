# Function Triggers

There are several different ways of triggering a function:

- **Blob Trigger:** The function is triggered when you add a blob to a specific storage account in a container. This could be useful for triggering a process when a customer uploads a file to a storage account.

- **Event Hub Trigger:** This can respond to events that are delivered an Azure Event Hub. This trigger is ideal for usage with Internet of Things (IoT) scenarios, where a process must be executed when an IoT-based device posts a message to an Azure Event Hub.

- **Generic Webhook:** This can execute the function when it receives a Webhook-based invocation.

- **GitHub Webhook:** GitHub can send a Webhook when an event occurs on a repository. For example, if a Fork is created on a GitHub, the GitHub workflow could call this Webhook to execute your function.

- **HTTP Trigger:** A special URI is created that triggers the function when a HTTP request is sent. You can add variables to the query string if executing a GET that can be parsed by the function with actions undertaken based on the values.

- **Queue Trigger:** This can respond to a message within an Azure Storage account queue. As messages arrive, the function is triggered to notify another application of the message or to perform a process on the message itself.

- **Service Bus Queue Trigger:** This is similar in principal to a Queue Trigger. However, it is based on Azure Service Bus.

- **Service Bus Topic Trigger:** This is based on a subscription to a topic with Azure Service Bus.

- **Timer Trigger:** This executes the function based on the timer interval.

As you can see from the preceding list, there are several ways in which a function can be triggered. Some of these from within an Azure Stack environment, and others from sources external to Azure Stack such as GitHub and Azure Event Hubs.

**Note:** Because Azure Stack Functions are executed within the App Service resource provider, you must install the App Service resource provider.