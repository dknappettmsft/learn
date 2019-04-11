# Pagefile

Microsoft Azure virtual machines are provisioned with a temporary drive, which is assigned to the D drive automatically. This drive is deleted when the virtual machine is deallocated from the Hyper-V server and, therefore, it is not used for any data that needs preserving.

The consistency of behavior between Azure Stack and Azure ensures that virtual machines deployed in Azure Stack also have the temporary drive attached, which is sized as per the virtual machine size. For example, a D3v2 virtual machine will have a temporary drive of 200 GB attached. When the virtual machine is deallocated from the Hyper-V server, this drive is deleted, exactly as it is deleted in Azure.