# Trace Collector and Log Collection Tool

The Trace Collector collects Event Tracing for Windows (ETW) logs from all Azure Stack components and makes them available in a local file share. The Trace Collector is enabled by default after you install Azure Stack, which ensures that logs are collected at all times. The logs have a limit of five days and each log has a maximum file size of 200 MB. This helps maintain disk space used by the Trace Collector. For each component, a JSON configuration file is used to define the log collection parameters. These configuration files are stored in C:\TraceCollector\Configuration and you can edit them as required. For example, the following trace configuration file content provides Azure Stack with the log file information for the FabricRingServices Operations from the AzS-Xrp01 virtual machine.

```JSON
{
    "LogFile":
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

## Log Collection Tool

You can run the log collection tool at any time, use it to collect logs from all Azure Stack components, and store them in a location specified when running the tool. This feature is useful when you need to troubleshoot a problem immediately or when Microsoft requests these logs when a ticket is raised with Microsoft Support. To run the log collection tool, you perform the following steps on the Azure Stack host as a Cloud Operator.

1. Open a Windows PowerShell command prompt and navigate to:

        C:\CloudDeployment\AzureStackDiagnostics\Microsoft.AzureStack.Diagnostics.DataCollection

2. Run the following Windows PowerShell command to import the data collection module:

    ```PowerShell
    Import-Module .\Microsoft.AzureStack.Diagnostics.DataCollection.psd1
    ```

3. Run the following Windows PowerShell command to start log collection:

    ```PowerShell
    Get-AzureStackLogs -OutputPath C:\AzureStackLogs
    ```

You also can include filters, which can be useful when you need to target log collection to a specific role or within a specific time period. For example, using the -FilterByRole and -FromDate parameters, the following command collects logs for the VirtualMachines and BareMetal roles within the last eight hours.

```PowerShell
Get-AzureStackLogs -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)
```

For more information about Azure Stack Diagnostic Tools including other filters that can be used with them, refer to the following website: <https://aka.ms/moc-10995A-pg079>.

**Note:** that when collecting logs using Azure Stacks diagnostic tools, personal information might be included in the logs. For this reason, care should be taken when sharing the log information with other personnel.

**Note:** that in a production deployment of Azure Stack, access to infrastructure components is restricted. However, when troubleshooting Azure Stack, if access to some of its infrastructure components is necessary, Microsoft has provided the Emergency Console. However, this is only accessible though Microsoft Support and requires security codes to open.