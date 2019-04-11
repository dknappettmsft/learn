# Accessing Virtual Machine Operating Systems

Azure Stack does not provide any method of directly accessing the Console session of the virtual machine. You can enable a feature called Boot Diagnostics, which shows two outputs:

1. Screenshot of the virtual machine. This shows you the state of the virtual machine. For example, it can show you the virtual machine sign-in screen. This can help you identify if the virtual machine has booted correctly.

2. Console output. For Linux virtual machines, this can show you the output of the Console Log and gives you the option to download the log file.

To obtain access to a virtual machine operating system, you can use one of the following two methods:

1. **Public IP address on a network interface:** This option involves adding a public IP address to a network interface. After you add the IP address to the network interface, it is available for connections. This option can present security challenges because the virtual machine relies upon two layers of security:

    - **NSG:** The NSG attached to either the subnet or the Network Interface can prevent unauthorized access based on the rules configured.

    - **Operating system firewall:** If the operating system inside the virtual machine has the firewall software enabled, it can prevent unauthorized access.
\
**Note:** The Azure Stack fabric will not intervene outside of the NSG. For example, it will not protect against Distributed Denial of Service (DDoS) attacks.
&nbsp;

2. **VPN connection to the virtual network:** This could be a point-to-site connection that allows a single client device, such as Windows 10 client, a remote connection to the virtual network, or a site-to-site connection. From this connection, it is possible to obtain access to the operating system through the associated internal IP address.

For Windows-based virtual machines, Microsoft offers native Remote Desktop Protocol (RDP) connections for remote administration. All virtual machines have RDP enabled by default. However, as the Cloud Operator of Azure Stack, you could offer a marketplace item where RDP is not enabled if required. Linux-based virtual machines offer Secure Shell (SSH) access with either a password or SSH Keys. We recommend using SSH Keys where possible.

As with Azure, tenants can upload their own images for use with Azure Stack. Tenants are responsible for ensuring the image is compatible with Azure Stack, whereas the Azure Stack administrator is responsible for ensuring the Marketplace images are compatible, especially if they are offering custom images to tenants.