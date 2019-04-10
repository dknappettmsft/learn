# Deployment with Azure PowerShell

To use Azure PowerShell to deploy an Azure Resource Manager template, you must:

- Be logged into Azure through Azure PowerShell.

- Connect to the correct subscription.

- Have the required permissions to deploy a template with the specified resources.

- Have a template file, either stored locally or on a publicly available web server.

- Have the values for any parameters stored in either a parameters JSON file or as a Windows PowerShell hashtable object.

The following high-level steps show you how to deploy an Azure Resource Manager template with Azure PowerShell:

1. Sign into Azure by using the Add-AzureRmAccount cmdlet with the required parameters to connect to Azure Stack.

2. Use the Select-AzureRmSubscription cmdlet and provide the required parameter. Typically, this is the subscription ID.

3. Create a new resource group using the New-AzureRmResourceGroup cmdlet and provide the required parameters.

4. Start a deployment by using the New-AzureRmResourceGroupDeployment cmdlet, and provide the Azure Stack region, the name of the resource group to be deployed into, the ARM template location as either a file or a URI, the parameters as either a file, a URI, or a Windows PowerShell hashtable.

For more details on how to deploy an Azure Resource Manager template with Azure PowerShell, refer to the following website: <https://aka.ms/moc-10995A-pg054>.