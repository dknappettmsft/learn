# SDN Control

For an SDN to function, it requires a centralized management function to inform components of the tenant-defined networks and where the tenant-defined resources are located. In the first release of SDN, Microsoft used System Center Virtual Machine Manager (SCVMM) for the centralized management function. The primary consumer of this SDN was the Windows Azure Pack, although other applications could use the SCVMM APIs to create and manage the tenant networks.

SCVMM would inform the Hyper-V hosts through Windows Management Instrumentation (WMI) and Windows PowerShell, which were part of the SDN infrastructure, where the tenant workloads were located. If a Tenant workload was migrated for any reason, such as Dynamic Optimization of virtual machines, host-level maintenance, or other reasons, SCVMM would update the Hyper-V hosts.

With Windows Server 2016, Microsoft has moved to using the Virtual Extensible LAN (VXLAN) protocol for network encapsulation. You can still use NVGRE if required. However, the default protocol now is VXLAN. In Windows Server 2016, Microsoft has created a new Windows Server role called the Network Controller, which was discussed in Module 3, “Deploying Microsoft Azure Stack”. This new role is responsible for the centralized management function in the new HNV stack and when used with VXLAN, this role is known as HNVv2. You can use this role to centrally configure virtual network devices, such as routers, switches, and gateways, in your datacenter.

Within Azure Stack, the network resource provider is responsible for instructing all changes to all SDNs, whether they are the infrastructure networks or the tenant networks. The Network resource provider sits between the Azure Resource Manager layer and the network controller.

Microsoft has replaced the filter driver in Windows Server 2016 with the Azure Virtual Filtering Platform (VFP) Switch Extension from Microsoft Azure. This has allowed Microsoft to incorporate a great deal more functionality into HNVv2. Microsoft has also made a significant investment in Network Function Virtualization.

By using Network Function Virtualization, you can deploy network functions such as firewalls, load balancers, and other network infrastructure within a SDN. For example, you can deploy Layer 7 load balancers from companies such as F5 and Kemp Technologies. Several other load balancers are also available.

The fabric of Azure Stack contains a single IP address that virtual machines can use to access the Internet from their virtual network. This is an outbound connection only. For inbound access to a virtual machine, you must create a public IP address and assign it to either a network adapter on the virtual machine or an external load balancer. You then configure the external load balancer to allow access. The Azure Stack owner provides this default Internet access.

You can override the default routing within an Azure Stack SDN by using user-defined routing, which is covered later in this lesson.

- An SDN environment typically includes the following three areas:

- Management Plane. This is responsible for the following tasks:

- Exposing a management interface for consumption by tenants and administrators.

- Authorizing activity prior to instructing the control plane.

- Communicating the tenants’ requirements to the Control Plane.

- Control Plane: This is responsible for the following tasks:

- Creating the policies for the tenant-based SDN instance.

- Keeping track of where the tenant workloads are running.

- Managing updates to SDN hosts, and other network infrastructure, to ensure their route tables are up-to-date.

- Facilitating the connection between a SDN network and other network infrastructure such as gateways.

- Data Plane: This is responsible for the following tasks:

- Encapsulating tenant traffic in the SDN network protocol such as VXLAN or NVGRE.

- Sending encapsulated traffic between SDN hosts and breakout infrastructure such as gateways.

- Gateways are responsible for the decapsulation of outbound tenant traffic destined for resources outside of the tenants’ SDN and encapsulation of inbound traffic to a tenant workload

Each of these planes is critical to the deployment of an SDN environment. The following table shows where each plane resides within the Azure Stack fabric.

|Plane|Azure Stack Component|
|---------|---------|
|Management Plane|Azure Resource Manager, Network Resource Provider|
|Control Plane|Network Controller|
|Data Plane|Hyper-V Servers, Gateway Virtual Machines|