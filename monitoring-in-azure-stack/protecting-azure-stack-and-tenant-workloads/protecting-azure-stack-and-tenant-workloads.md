# Protecting Azure Stack and Tenant Workloads

As mentioned in previous modules, Azure Stack includes a number of infrastructure components that are used to provision and manage the resources required to facilitate tenant workloads. Protecting these infrastructure components from corruption or data loss is critical to the functionality of Azure Stack. Additionally, when tenants provision workloads using Azure Stack, they also need to ensure they are protected accordingly.

In this final lesson, you will learn how to back up the Azure Stack infrastructure and how you can use other backup tools to protect this data. You will also learn what tools are available to back up tenant workloads that have been provisioned in Azure Stack.

After completing this section you will be able to:

- Understand how Azure Stack infrastructure is protected.

- Protect the tenant workloads provisioned in Azure Stack.

## Protecting Azure Stacks infrastructure Components

One of the key roles in the Azure Stack architecture is the Backup Controller. This role provides an automatic backup of the Azure Stacks core components, which are the components required to ensure that Azure Stack can function. It is important to note that this does not include any tenant-related data such as tenant workloads or data provisioned in tenant subscriptions. The final topic covers how to protect this data.

The Backup Controller role performs the backup of the Azure Stack infrastructure periodically. At the time of writing, there is no method of initiating a backup manually. However, an API will be included in a later revision of Azure Stack. Additionally, at the time of writing, the frequency schedule of backups has not been disclosed.

The following components and services (or rather the data that these services rely upon) are included as part of the backup performed by the Backup Controller:

- Azure Resource Manager

- Key Vault

- Compute Resource Provider

- Network Resource Provider

- Storage Resource Provider

- Subscriptions

- Offers

- Plans

The preceding list is not exhaustive but as mentioned previously, all data relevant to ensuring Azure Stack can function is backed up by the Backup Controller.