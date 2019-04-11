# Virtual Machine Migration

One key differentiator between Azure Stack and Azure is the ability for virtual machines to be live migrated between Hyper-V hosts during host level maintenance. This ensures that tenant workloads and Azure Stack infrastructure workloads are not impacted during the maintenance operations on the Azure Stack fabric.

In Azure, several types of updates are performed ranging from non-service impacting updates to updates that require the Hyper-V host in Azure to be restarted. In the case of the latter, Azure powers down your virtual machine, performs the required maintenance, and restarts your virtual machine.

## Virtual Machine Agent

Module 5, "Microsoft Azure Stack and DevOps", describes the Virtual Machine Agent (VM Agent) with regards to the Configuration Management options. This topic discusses the VM Agent further to include other capabilities it offers.

The VM Agent is responsible for installing, configuring, and removing VM extensions from virtual machines. It is a secure, light-weight process. The VM Agent can communicate with Azure Stack through the Azure Virtual Filtering Platform (VFP) Switch Extension that resides within the Hyper-V virtual switch.

To list the available VM Extensions in Azure Stack, run the following Windows PowerShell command:

```PowerShell
Get-AzureRmVMImagePublisher -Location <Azure Stack Region> | Get-AzureRmVMExtensionImageType | Get-AzureRmVMExtensionImage | Select PublisherName,Type,Version | FT -AutoSize
```

We recommend that after you install the VM Agent, you do not uninstall it because this may lead to instability in communication between the Azure Stack fabric and the virtual machine. The agent will update itself when required and will not trigger a restart of the virtual machine.

**Note:** The VM Agent is an optional component for IaaS virtual machines. However, we highly recommended that you include this component. Because it is optional, you might decide that some of the images you offer to Tenants will not have the VM Agent installed.

**Note:** The VM Agent is available for both Windows and Linux-based operating systems.

The VM Agent is capable of extracting diagnostic information from the running operating system and outputting that, through the Azure Stack Fabric, to a Storage Account. The following table shows some example diagnostic information that can be collected.

|Operating System|Example Diagnostic Information|
|---------|---------|
|Windows|\Processor(_Total)% Processor Time, \Process(_Total)\Thread Count, \Memory\Available Bytes, \PhysicalDisk(_Total)\Disk Transfers/sec|
|Linux|CPU privileged time, Memory available, Disk transfers|

**Note:** This is just a subset of the possible diagnostic information that can be collected.

You can then use this information to analyze the performance of the virtual machines and this can be particularly beneficial where access to the virtual machine operating system is highly restricted.