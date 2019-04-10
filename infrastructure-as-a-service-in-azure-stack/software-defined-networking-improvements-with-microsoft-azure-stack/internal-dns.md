# Internal DNS (iDNS) for Software Defined Networking

By using HNVv2, you can provide Domain Name System (DNS) services to virtual machines hosted in Azure Stack. Tenants are not required to host their own DNS servers. Typically, virtual machines and applications, must be able to perform DNS lookups for resources within their own networks and for Internet-based resources. You can do this by using the Internal DNS (iDNS) feature in Windows Server 2016.

The tenant virtual machines cannot directly access the iDNS service., The iDNS service uses an iDNS proxy to filter requests to the DNS server. Therefore, the underlying DNS server is not vulnerable to attacks from malicious tenants.

The following list describes key features of the iDNS service:

- It is a shared DNS name resolution service for your tenant workloads.

- It is an authoritative DNS registration and name resolution service for tenants.

- It offers recursive DNS name resolution for Internet domains from tenant workloads.

- Tenants are not required to deploy a DNS service within their networks.

- It is a highly available solution through Active Directory integration.

For Azure Stack virtual machines, iDNS integration is enabled by default. The “DnsProxy” Windows Service is deployed on every Hyper-V host that is part of the Azure Stack deployment.

The following Windows PowerShell command shows you how to obtain the currently configured DNS forwarder for the DnsProxy Windows Service. This command is run on the host computer.

```PowerShell
Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\DnsProxy\Parameters
```

The Azure Stack installation and management process performs the configuration of the DnsProxy service.