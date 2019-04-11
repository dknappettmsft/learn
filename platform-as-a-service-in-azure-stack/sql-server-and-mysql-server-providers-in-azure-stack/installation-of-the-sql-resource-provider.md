# Installation of the SQL Resource Provider

To install the SQL resource provider, you must obtain the latest copy of the installation media from Microsoft and any additional scripts provided by Microsoft. You can obtain these from the following website: <https://aka.ms/moc-10995A-az10>.

With the Azure Stack Development Kit, the installation must be performed on the Hyper-V host.

The example code shows you how to start the installation process for the SQL resource provider. You can start this from the same location as the DeploySQLProvider.ps1 PowerShell script:

```PowerShell
# Install the AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force
# Installs and imports the API Version Profile required by Azure Stack into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force
# Download the Azure Stack Tools from GitHub and set the environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force
# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 
# For AAD, use the following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin
# For ADFS, replace the previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin
$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)
$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)
# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
# Change directory to the folder where you extracted the installation files 
# and adjust the endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
```

The installation process typically takes approximately 90 minutes to complete depending upon the hardware.

The following table lists the details of the default Azure Stack resources that are created by the SQL Server resource provider installation:

|Azure Stack Resource|Details|
|---------|---------|
|Resource group|SqlRPRG|
|Virtual machine|SQLVM|
|Network interface|SQLVM-NIC|
|Network security group|SQLVM-NSG|
|Public IP address|SQLVM-PublicIP|
|Virtual network|SQLVM-VNET|
|Storage Accounts|masa and 0000sqlvm|
|Resource providers|Microsoft.SQLAdapter, Microsoft.SQLAdapter.Admin, Microsoft.SQLAdapterForAdmin|

After the installation is complete, the resource provider is available for configuration through the Azure Stack Administrator Portal under the Resource Providers section. You must then use the Administrator Portal to configure the provider with the details of a hosting Microsoft SQL Server that will be used for capacity when provisioning SQL Server databases.