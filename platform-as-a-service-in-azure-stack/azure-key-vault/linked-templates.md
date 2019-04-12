# Linked Templates

The alternative method of utilizing Key Vault during Azure Resource Manager template deployment is using linked templates. The linked template is referenced within the parent template and the parameter values required for the linked template are passed from the parent template to the linked template. This method allows dynamic referencing of secrets.

The following is an extract from an Azure Resource Manager template that shows you how to dynamically reference a Key Vault and a secret within, where the name of the Key Vault and the secret being referenced are taken from parameters in the parent template:

Extract of an ARM Template for Dynamic Reference

```JSON
"resources":
    [
        {
            "apiVersion": "2015-01-01",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "properties": {
                "mode": "incremental",
                "templateLink": {
                    "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
                "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminPassword": {
                        "reference": {
                            "keyVault": {
                                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
                            },
                            "secretName": "[parameters('secretName')]"
                        }
                    }
                }
            }
        }
    ]
```