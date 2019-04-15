# Azure Stack Virtual Machine Start Up Order

Use the following order when starting virtual machines in the Azure Stack environment:

1. AzS -DC01

2. AzS-ERCS01

3. AzS -BGPNAT01

4. AzS -NC01

5. AzS -SLB01

6. AzS -Gwy01

7. AzS -ASql01

8. AzS -ADFS01

9. AzS -CA01

10. AzS -ACS01

11. AzS -Xrp01

12. AzS -WASP01

13. AzS -WAS01

During the startup procedure, it is important that a pause of at least 60 seconds is added between the startup of each virtual machine. For example, start AzS-DC01, then wait 60 seconds, then start AzS-ERCS01 and so on. This is to ensure that each virtual machine has started and its services are running before the next virtual machine (which might depend on services from the previous virtual machine) is started. As noted earlier, AzS-DC01 is the first virtual machine to be started because all other virtual machines rely on it for their service accounts.

**Note:** The virtual machines listed in the preceding sections represent the Azure Stack Development Kit deployment. In a production implementation of Azure Stack, the AzS-BGPNAT01 virtual machine is not included.