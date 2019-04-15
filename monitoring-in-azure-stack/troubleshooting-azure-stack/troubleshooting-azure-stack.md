# Troubleshooting Azure Stack

With any application, troubleshooting is an important aspect that you must master. Azure Stack incorporates a number of different components, which includes not just its infrastructure components and the role services they host, but also the Azure Stack software itself. Therefore, it is important that you understand the various troubleshooting tools available for you should an issue arise with Azure Stack or any of its infrastructure components.

In this lesson, you will learn about the startup and shutdown sequence of the Azure Stack infrastructure components. You will then see how to use the Heath Service Log to troubleshoot issues in Azure Stack. Then, you will learn some of the key Windows Event Log entries you should be aware of that relate to problems in Azure Stack. Finally, you will learn how integration between Operations Manager and Operations Management Suite can help troubleshoot an Azure Stack implementation.

After completing this section you will be able to:

- Understand the virtual machine startup and shutdown order for the Azure Stack infrastructure.

- Use the Health Service Log to troubleshoot problems in Azure Stack.

- Use the Windows Event Log to troubleshoot problems in Azure Stack.

- Use Azure Stack Diagnostic Tools to help troubleshoot problems in Azure Stack.

## Virtual Machine Startup and Shutdown Order in Azure Stack

As you are aware, there are several infrastructure components that Azure Stack is comprised of, such as the virtual machines that host its server roles and features. When you shut down a Hyper-V host in Azure Stack, its virtual machines are migrated (if possible) and then shut down automatically. This is the default behavior in Hyper-V, but you can change it by editing the virtual machine settings. However, note that in a production environment of Azure Stack, you cannot edit virtual machine settings.

Similarly, when you start a Hyper-V host, you can configure its virtual machines to start automatically. However, by default, no action is taken on virtual machines when a Hyper-V host is started.

![Virtual Machine Startup and Shutdown Order in Azure Stack](media/virtual-machine-startup-and-shutdown-order-in-azure-stack.png)

You should configure the virtual machine automatic start and stop settings in Hyper-V with the following settings except for the domain controller virtual machine AzS-DC01:

- Automatic Start Action: None.

- Automatic Stop Action: Shut down the guest operating system.

**Note:** For the AzS-DC01 virtual machine, you should configure its Automatic Start Action in Hyper-V with either the Automatically start if it was running when the service stopped or the Always start the virtual machine automatically setting. This is because the Domain Controller hosted on AzS-DC01 should always be the first virtual machine to be started because it provides authentication for all service accounts configured in Azure Stack.

It is important that the startup and shutdown process for Azure Stack virtual machines is performed in a specific order. If they are not, services might fail to respond or stop because dependent services running on other virtual machines might not have started in time. This can also result in errors occurring in the Azure Stack Portal.

For this reason, you should perform the shutdown and startup order described in the following sections when you restart Hyper-V hosts Azure Stack or when you perform maintenance.