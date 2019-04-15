# Requirements for the Backup Controller

For the Backup Controller to function, it requires access to an external file share. This is a location in the organization’s datacenter, where the exported data is stored. The exported data is compressed and encrypted automatically. This file share is then included in the organization’s backup policy and backed up regularly using the organizations preferred backup solution.

Note that the Backup Controller takes full backups each time the backup process runs. Incremental backups are not provided. For this reason, the Backup Controller also performs the purging of backups older than a specific number of days. It is therefore critical that organizations use their own backup solution to ensure regular backups are taken of the file share used by the Backup Controller. This is especially important because by design, the data retention of backups is not configurable and nor are the inner mechanisms of Backup Controller exposed.

## Disk Space Requirements

At the time of writing it is expected that a minimum of 8 gigabytes (GB) of disk space is made available for the backup file share used by the Backup Controller. However, for future releases of Azure Stack it is estimated that approximately a 1 terabyte (TB) share will be required, but this might change with deduplication enabled.

Finally, note that you cannot use the normal backup solutions, which organizations use for their daily backup process, to back up the Azure Stack infrastructure directly. You can only use these solutions to back up the file share used by the Backup Controller.