# Installation of the MySQL  Resource Provider

To install the MySQL resource provider, you must obtain the latest copy of the installation media from Microsoft and any additional scripts provided by Microsoft. You can obtain these from the following website: <https://aka.ms/moc-10995A-sql>.

With the Azure Stack Development Kit, the installation must be performed on the Hyper-V host.

The example code shows you how to start the installation process for the MySQL Resource Provider. You should start this from the same location as the DeploySQLProvider.ps1 PowerShell script:

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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)
$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)
# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
# Change directory to the folder where you extracted the installation files 
# and adjust the endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath```
```

The installation process will download the appropriate versions of the required MySQL Server software. Depending upon which version of the PowerShell for Azure Stack you have installed you might be prompted to update the required Azure PowerShell modules during the installation. The installation process typically takes approximately 90 minutes to complete dependent upon the hardware.

The following table lists the details of the default Azure Stack resources that the resource provider installation creates:

|Azure Stack Resource|Details|
|---------|---------|
|Resource group|MySQLRG|
|Virtual machine|MySQLRP|
|Network interface|MySQLRP-NIC|
|Network security group|MySQLRP-NSG|
|Public IP address|MySQLVM-PublicIP|
|Virtual network|MySQLVM-VNET|
|Storage Accounts|masa and Systemmysqlst|
|Resource providers|Microsoft.MySQLAdapter, Microsoft.MySQLAdapter.Admin, Microsoft.MySQLAdapterForAdmin|

After the installation is complete, the resource provider is available for configuration through the Azure Stack Portal under the Resource Providers section. As with the SQL resource provider, you must then use the Administrator Portal to configure the provider with the details of a hosting MySQL Server that will be used for capacity when provisioning MySQL databases.

**Note:** Prior to the GA release of the Azure Stack Development Kit, both the SQL and MySQL resource providers also created an instance of SQL and MySQL respectively. In the GA release however, this does not occur. For this reason, you must add a hosting server to each provider that will be used as capacity when provisioning databases in Azure Stack. This is covered in greater detail later in this lesson.