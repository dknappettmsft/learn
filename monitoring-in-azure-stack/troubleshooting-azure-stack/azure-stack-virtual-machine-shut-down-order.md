# Azure Stack Virtual Machine Shut Down Order

Use the following order when shutting down virtual machines in the Azure Stack environment:

1. AzS-WAS01

2. AzS-WASP01

3. AzS-Xrp01

4. AzS-ACS01

5. AzS-CA01

6. AzS-ADFS01

7. AzS-ASql01

8. AzS-Gwy01

9. AzS-SLB01

10. AzS-NC01

11. AzS-BGPNAT01

12. AzS-ERCS01

13. AzS-DC01

Notice that AzS-DC01 is the final virtual machine to be shut down. This is to ensure that authentication for service accounts is maintained during the shutdown process. Virtual Machines can fail to respond during shutdown if the guest operating system has lost connectivity to the domain controller.

## Gracefully Shutting Down the Azure Stack Environment

In scenarios where you are required to shut down the Azure Stack host computer, including all infrastructure virtual machines, Microsoft have provided the Stop-AzureStack Windows PowerShell Cmdlet. This Cmdlet can be used to gracefully shut down all Azure Stack virtual machines and then the physical host computer. The Cmdlet can only be run from the AzS-ERCS01 virtual machine however. To gracefully shutdown the Azure Stack environment including all virtual machines and the physical host computer you perform the following steps:

1. From Hyper-V Manager on the host computer, sign-in to the AzS-ERCS01 virtual machine using an account that is an administrator in Azure Stack.

2. In the Command prompt window, type Start PowerShell to open a Windows PowerShell session.

3. Type Stop-AzureStack and press enter.

The Azure Stack virtual machines will then be gracefully shut down, and then the physical host is shut down.