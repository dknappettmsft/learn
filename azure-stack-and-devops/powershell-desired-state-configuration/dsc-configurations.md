# DSC Configurations

A DSC configuration uses a special DSC specific PowerShell keyword
called Configuration. The below example shows a basic DSC Configuration:

Example DSC Configuration:

```mof
Configuration ExampleConfiguration1 {
    Node "LON-IIS01" {
        WindowsFeature "IIS" {
            Ensure = Present
            Name = "Web-Server"
        }
    }
}
```

A DSC configuration is comprised of the following elements:

- **Configuration block:** This is the overall container of the script
    block and is defined with the Configuration keyword. The name of the
    Configuration is placed after the Configuration keyword.

- **Node block(s):** This element defines the configuration for a node
    (machine) with the matching name. You can use localhost to have it
    apply to any machine. If you give the Node element a
    ../../Linked\_Image\_Files value, it will only apply to a Node that
    matches the value. For example, if you use Node "LON-IIS01", then
    the configuration in the Node element will only apply to machines
    with the name LON-IIS01. You can define one or more Node elements in
    a DSC Configuration. You also can parameterize the Node value so
    that it can be passed to the Configuration when it is applied to a
    machine.

- **Resource(s):** Within each Node element, you must define the
    Resource you want to configure. For example, the WindowsFeature
    Resource can be used to ensure the File Server Windows role is
    installed on the server.

The preceding example shows the Configuration to be named
"ExampleConfiguration1", the Node is set to "LON-IIS01", and the
Resource is using the built-in WindowsFeature Resource to ensure that
the "Web-Server" Role/Feature is present on the machine.

Windows PowerShell compiles configurations into a Managed Object Format
(MOF) file. This is an industry-standard file that can be distributed to
any operating system that supports the format. You compile the MOF file
by running the name of the Configuration as a Windows PowerShell
command. You do this when parameters are passed to the configuration.
The resultant file is the name of the Node at which the MOF file is
targeted. Using the preceding example, the resultant MOF file would be
called "LON-IIS01.mof".

The contents of the MOF file are:

```mof
/*
@TargetNode='LON-IIS01'
@GeneratedBy=MSL
@GenerationDate=01/31/2017 15:04:57
@GenerationHost=MSL01
*/
instance of MSFT_RoleResource as $MSFT_RoleResource1ref
{
    ResourceID = "[WindowsFeature]IIS";
    Ensure = "Present";
    SourceInfo = "::5::9::WindowsFeature";
    Name = "Web-Server";
    ModuleName = "PSDesiredStateConfiguration";
    ModuleVersion = "1.0"; 
    ConfigurationName = "ExampleConfiguration1"; 
};
instance of OMI_ConfigurationDocument
{
    Version="2.0.0";
    MinimumCompatibleVersion = "1.0.0";
    CompatibleVersionAdditionalProperties= {"Omi_BaseResource:ConfigurationName"};
    Author="MSL";
    GenerationDate="03/31/2017 15:04:57";
    GenerationHost="MSL01";
    Name="ExampleConfiguration1";
};
```

You can deploy configurations by using one of the following two methods:

1. **Push:** The MOF file is pushed to the target node from another
    machine or on the local host itself with the Configuration being
    enacted locally. The Resources used by the Configuration must be
    present on the target node.

2. **Pull:** The LCM is configured to obtain a Configuration from a
    centralized location such as a web server or a Server Message Block
    (SMB) share.

DSC determines which method to use by querying the property of the
RefreshMode property in the Local Configuration Manager.