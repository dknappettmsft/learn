# Validating Azure Resource Manager Templates

Prior to deploying an Azure Resource Manager template, you can validate the template by using Azure PowerShell, Visual Studio, or the Azure CLI. By validating your template prior to its deployment, you can avoid deployment failures due to poorly formed JSON or the template being non-compliant with the ARM template schema.

When validating an Azure Resource Manager template, you can specify the parameters that would be passed to the deployment, which could be through a local or remote parameters file or as inline parameters.