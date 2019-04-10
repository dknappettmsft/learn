# Azure Resource Manager Template Deployment Types

It is important to understand that when you deploy an Azure Resource Manager template to a resource group, you have two choices for the deployment type:

1. **Incremental:** In this mode, the deployment will not delete any existing resources in the resource group into which the resource is being deployed. If there are matching resources in the resource group that are defined in the Azure Resource Manager template, then the template will use the existing resource. For example, if you are provisioning a storage account as part of your template and a matching storage account already exists, then the template will use that existing storage account.

2. **Complete:** In this mode, the deployment uses the Azure Resource Manager template as the template for the desired state of the resource group. This mode will remove any existing resource that is in the target resource group and provision the resources defined in the template. However, if a resource already exists in the resource group that matches the required configuration of a resource in the template, this resource will not be deleted. Any resources in the resource group that are not defined in the template will be deleted.

By default, Azure Resource Manager deploys templates in the Incremental mode. If you want to deploy a template in the Complete mode, then you must specify it at the point of deployment.

The code sample below shows how to use the Mode Parameter to do a Complete  PowerShell based ARM Template Deployment:

```PowerShell
New-AzureRmResourceGroupDeployment -Mode Complete
```