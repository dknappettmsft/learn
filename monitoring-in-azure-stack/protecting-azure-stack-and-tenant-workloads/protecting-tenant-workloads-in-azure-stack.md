# Protecting Tenant Workloads in Azure Stack

You have a number of options for providing protection to the tenant workloads. For example, tenants might already own their own backup and recovery solution such as Data Protection Manager (DPM). You can install DPM in a virtualized environment. Therefore, tenants can provision a virtual machine and use DPM to protect their workloads such as SQL Server, SharePoint Server, and relevant file data. Some of the key features that DPM provides include:

- **Disk-to-disk backup:** DPM backs up data to a storage pool, which you can then use to recover data when required.

- **Disk-to-tape backup:** For offline storage, DPM can back up data to tape, which you can then move off-site.

- **Disk-to-Azure backup:** DPM can back up data to Azure. This can remove the requirement of utilizing tape-based media for offsite storage because the data is backed up to the cloud.

- **Application-aware backups:** The intelligent protection agent of DMP ensures all relevant data for an application is included in the backup. For example, when providing protection for SQL Server, DPM detects when a new database has been added to an SQL Server, and automatically starts protecting it.

- **Flexible recovery options:** You can use DPM to recover data to its original location or to another location. For example, when recovering a SQL Server database, you can recover to the original SQL Server or to another SQL Server, or a network location. This can be useful when you need to review recovered data before it is moved back into a production environment. Additionally, you can use DPM to protect itself. You can provision a secondary DPM server that backs up data on the primary DPM server. If the primary DPM server is unavailable, you can use the secondary DPM server to recover data to the primary DPM server and/or back to its source location.

- **Online and performant backups:** DPM uses the Volume Shadow Copy Service (VSS), which allows you to take backups while the data or application is online. This means applications or computers do not need to be shut down while you take a backup. Furthermore, after you take an initial replica is taken of the data to be protected, only block-level changes to the data is copied during subsequent backups. This provides a number of benefits such as reducing backup time, disk space, and network bandwidth utilization.

The preceding features represent only a small number of DPM capabilities. For more information about DPM, including the workloads that it provides protection for, refer to the following website: <https://aka.ms/moc-10995a-pg085>.

**Note:** DPM also provides protection for Hyper-V virtual machines. However, you cannot use this feature with the virtual machines provisioned in Azure Stack, or for Azure Stack infrastructure virtual machines.

If tenants do not use their own backup solution, they can use the Azure Backup Server to provide protection for their workloads. Azure Backup Server provides intelligent protection of the workloads mentioned before by backing up data to Azure. Azure Backup Server uses part of the same code that was used to develop DPM. Therefore, many of the features found in DPM are also available in Azure Backup Server, with the exception of tape-based backup. In addition to the benefit of backup data being secured offsite, Azure Backup Server provides the following benefits:

- **Pay-as-you-go storage:** Storage in Azure Backup Server uses a pay-as-you-go model, meaning you only pay for storage that you actually use in Azure. There is no cost for local storage that you use when providing protection. This can reduce the Total Cost of Ownership (TCO) of the backup solution because you do not need to provision storage that is not used for any period of time. This also reduces the administrative overhead when managing storage because you do not need to add additional storage when required. Azure Backup Server manages this automatically.

- **High-availability and scaling:** Because data in Azure Backup Server is hosted in the Microsoft cloud environment, scaling and high-availability for protected data is provided automatically. Additionally, Azure manages the maintenance and monitoring of protected data. This means you do not have to use another solution to monitor the backup solution. If required, you can also enable alerting to notify you when backup events occur.

- **Storage replication:** Depending on the data being protected in Azure, you might wish to increase the level of protection by replicating it to other Azure regions. For example, when using the Locally Redundant Storage (LRS) option, data is replicated three times within the same region. This provides protection against local hardware failure in the same region. When using the Geo-Redundant Storage (GRS) option, data is replicated to another Azure region miles away from the source region. This provides protection against a complete region outage in Azure.

For more information about Azure Backup Server, including all its features and capabilities, refer to the following website: <https://aka.ms/moc-10995a-pg086>.

Note: Similar to the case of DPM with Azure Stack's infrastructure and tenant workloads, you cannot use Azure Backup Server to provide protection for virtual machines in this scenario.