# Distributed Firewall

The distributed firewall is a component of the Network Controller. It is responsible for applying traffic filters to subnets and virtual network adapters in a software-defined networking environment. In Azure Stack, the distributed firewall is surfaced through Network Security Groups (NSGs) for the tenants to control traffic within their networks. You can use a distributed firewall to prevent unwanted traffic from reaching a tenant workload and to ensure the workload remains unaware of the connection attempt. For example, you can use a distributed firewall to prevent unsolicited network traffic from outside of the tenant’s virtual network from reaching an Active Directory domain controller.

The policies are distributed from the Network Controller to the Hyper-V hosts and the policies are applied at the virtual port-level within the Hyper-V virtual switch. The policy follows the virtual machine from host to host because the Hyper-V virtual switch is responsible for managing the traffic to the virtual machine.

Tenants define NSGs in Azure Stack. The following table shows an example of a NSG:

|Priority|Name|Source|Destination|Service|Action|
|---------|---------|---------|---------|---------|---------|
|200|SMB-In|10.10.0.0/16|192.168.1.0/24|Custom (TCP/445)|Allow|
|210|RDP-In|10.10.10.0/24|192.168.1.0/24|RDP (TCP/3389)|Allow|
|220|FTP-In|Any|192.168.1.0/24|FTP (TCP/21)|Deny|

The preceding example NSG would allow the following traffic:

- Server Message Block (SMB) (TCP port 445) traffic from any IP address that falls within the 10.10.0.0/16 subnet to a destination IP address in the 192.168.1.0/24 subnet.

- RDP (TCP port 3389 by default) traffic from any IP address that falls within the 10.10.10.0/24 subnet to a destination IP address in the 192.168.1.0/24 subnet.

This NSG would deny the following traffic:

- FTP (TCP port 21) traffic from any IP address to a destination IP address in the 192.168.1.0/24 subnet

The preceding example NSG can be created by using an Azure Resource Manager template. The following snippet shows how to define the SMB-In rule:

```JSON
{
    "name": "SMB-In",
    "properties": {
        "protocol": "TCP",
        "sourcePortRange": "*",
        "destinationPortRange": "445",
        "sourceAddressPrefix": "10.10.0.0/16",
        "destinationAddressPrefix": "192.168.1.0/24",
        "access": "Allow",
        "priority": 250,
        "direction": "Inbound"
    }
}
```