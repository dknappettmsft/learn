# Azure Automation and Backup

You can use automation in OMS to automate manual tasks such as collecting log data or enforcing configurations on physical or virtual machines. Because Azure Automation uses Windows PowerShell scripting or Windows PowerShell workflows, it can easily be integrated with other OMS services such as Log Analytics or Azure Backup. This makes automation of tasks possible in these services as well. Azure Automation uses Runbooks to automate manual processes and share variables between Runbooks making them reusable in many different scenarios.

You can run runbooks in the cloud and can access any resources available to them in the cloud. Moreover, you can install Runbook Hybrid Workers that you can use to access resources in your datacenter. Runbooks are also useful when you apply a configuration to physical or virtual machines. For example, Azure Automation includes a Windows PowerShell Desired State Configuration (DSC) Pull server hosted in the cloud that agents can connect to for configuration information.

## Azure Backup

Azure Backup provides data protection and recovery for both the physical and virtual environment. It also includes support for application workloads such as SQL Server and SharePoint. Azure Backup stores protected data in a vault that is replicated throughout the current region in which it is located. You can also enable cross-region replication for further resiliency if required. You can run Azure Backup in three different scenarios as described in the following section:

- **Azure Backup Agent and Windows machines:** You can back up data from a Windows server or client directly to the Azure Backup vault by using the Azure Backup Agent.

- **System Center Data Protection Manager (DPM) or Microsoft Azure Backup Server:** You protect data locally by using DPM or Azure Backup Server and then replicate the data to the Azure Backup vault. Support for workloads such as SQL Server and SharePoint is included. In addition, virtual machines running on Microsoft Hyper-V or VMware are also supported.

- **Azure Virtual Machine Extensions:** Provides data protection for virtual machines running in Azure. Data is replicated from Azure virtual machines to the Azure Backup Vault.