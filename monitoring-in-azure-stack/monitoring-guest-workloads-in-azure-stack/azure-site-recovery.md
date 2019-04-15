# Azure Site Recovery

You can use Azure Site Recovery to replicate on-premises physical or virtual machines running Windows or Linux. Azure Site Recovery includes support for both Hyper-V and VMware virtual machines. You can replicate data from your on-premises datacenter to Azure or to a secondary site. Orchestration is built in with Azure Site Recovery, which means that the management of replication, failover, and recovery is included. For example, should a virtual machine or service fail in your datacenter, you can use Azure Site Recovery to fail over to the replicated resource in either Azure or your secondary site. You also can manage failback when the local resources are back online. Azure Site Recovery works in the following three scenarios:

- **Hyper-V Virtual Machine Replication:** When Virtual Machine Manager (VMM) is used to manage Hyper-V virtual machines, you can use Azure Site Recovery to replicate them to Azure or to a secondary datacenter. If you do not use VMM to manage your virtual machines, you can use Azure Site Recovery to replicate them to Azure only.

- **VMware Virtual Machine Replication:** You can perform the replication of virtual machines by VMware to a secondary site that is also running VMware. You also can replicate to Azure.

- **Physical Windows and Linux machines:** You can replicate physical machines running either Windows or Linux to a secondary site or to Azure.

In addition to the services described before, Microsoft and its partners have created a number of management solutions that use some or all of the services described in this topic. For example, the Update Management solution from Microsoft uses the Log Analytics service to collect update information on Windows and Linux machines. This solution provides a dashboard that displays installed updates on these machines. You can then use Azure automation to automate the update installation process to ensure machines are compliant with your update policy.

**Note:** You also can integrate Operations Management Suite with Operations Manager, which will be described further in the final topic in this lesson.  For more information about Operations Management Suite, refer to the following website: <https://aka.ms/moc-10995A-pg075>.