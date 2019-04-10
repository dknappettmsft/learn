# Microsoft Azure Consistency

Azure offers the following two types of storage accounts:

- **Standard:** These storage accounts are backed by a hard-disk drive (HDD) disk and Azure places certain limitations on them, such as only offering 60MB/sec throughput to a single page blob. A single page blob (VHD file) cannot exceed 500 input/output operations per second (IOPS).

- **Premium:** These storage accounts are solid–state drive (SSD) storage and have different limitations compared to the standard type. The core limitation change is the number of IOPS available per disk (depending upon the size of the disk) and the MB/sec throughput available to a single page blob.

Azure offers the following four types of data replication option:

- **Local redundant storage (LRS):** In Azure, Microsoft make three synchronous copies of data because it is written across the Azure datacenter where the storage account is located. LRS is the only option available for Premium storage accounts.

- **Geo-redundant storage (GRS):** In addition to LRS, three asynchronous copies of the data are stored in the paired Azure region, making it six copies of the data in total.

- **Zone-redundant storage (ZRS):** This sits in-between LRS and GRS storage by offering more copies stored in the local Azure region but split across local datacenters or regions.

- **Read-access geo-redundant storage (RA-GRS):** This offers the same number of copies of data as GRS. However, the secondary copy of the data is accessible in the read-only format.

At General Availability (GA), Azure Stack provides of the Azure Stack equivalent of Standard and Premium-based LRS as the option for storage. The Quality of Service (QoS) for the storage is only be applied at the Hyper-V level on a page blob (VHD). Therefore, the number of IOPS is capped on each VHD.

The Storage resource provider exposes the Standard and Premium storage accounts at the API level. However, there is no Storage QoS available outside of the IOPS control on the VHD files as described before.

To enforce the limitations of a Standard storage account, Microsoft uses the Storage QoS, which is part of the software-defined storage capabilities within Windows Server 2016. The Storage resource provider creates the required Storage QoS policies.