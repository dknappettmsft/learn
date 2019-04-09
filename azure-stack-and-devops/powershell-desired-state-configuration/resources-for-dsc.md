# Resources for DSC

To implement the required configuration, a DSC Configuration requires certain resources. Windows PowerShell provides several built-in resources for you to use.

These can be viewed with the following PowerShell cmdlet:

```PowerShell
Get-DscResource
```

You can create your own DSC resources to perform required tasks. We recommend that you look at the PowerShell Gallery, which is located at <https://aka.ms/moc-10995A-pg046> to see if any suitable resources already exist. This repository hosts many different resources that you can download and utilize in your configurations. You can also modify these resources to fit your requirements.

It is important to know that, by default, you need to use the System account to perform DSC resource actions. However, with Windows PowerShell 5.0 and later, you can perform resource-level actions by using a specified user account.

Each resource can have its own set of properties that you can parameterize in the Configuration and pass to the resource for its use. For example, you could have a property that specifies a custom installation path for a piece of software and the resource would then be able to use that path.

Every Resource must implement the following three functions:

1. **Get-TargetResource:** This function accepts all the parameters for the resource and then checks if the parameters match the configuration. The function returns a hashtable of the parameters with the values that they are determined to be. For example, in the WindowsFeature Resource, you specify the Name parameter to be “Web-Server” and the Ensure parameter to be “Present”. The output of this function returns a hashtable with a Key/Value pair of “Name=Web-Server” and a Key/Value pair of “Ensure=Present”, if the feature is a present, or “Ensure=Absent”, if the feature is not installed.\
\
\
Example hashtable output:

    ```mof
    @{
        Name = "Web-Server"
        Ensure = "Present"
    }
    ```

2. **Set-TargetResource:** This function accepts all the parameters for
    the resource and performs the required steps, as defined in the
    function, to apply the required configuration. This function might
    be called multiple times. Therefore, it might be necessary to test
    each section of the configuration. For example if you install SQL
    Server 2012, you need to install the Microsoft .NET Framework 3.5 on
    the server. However, you should test if it is already installed and
    then proceed with the SQL Server installation.

3. **Test-TargetResource:** This function accepts all the parameters
    for the resource and then checks if the configuration is applied
    correctly or not. It returns a True/False value based on the
    configuration test.

The DSC engine uses these three functions to determine if the required
configuration is already in place which is undertaken by the Lifecycle
Management (LCM).