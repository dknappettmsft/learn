# Parameters File

As detailed in Module 5, "Azure Stack and DevOps", you can use a parameters file to pass values to an Azure Resource Manager Template during deployment. When referencing a secret in a Key Vault in a parameters file, you must use a specific syntax.

The following is the structure of a single parameters file:

```JSON
"{parameter-name}": {
    "reference": {
    "keyVault": {
        "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
    },
    "secretName": "{secret-name}"
    }
} 
```

As you can see in the preceding syntax, the Key Vault could be in a different subscription and/or resource group than the one in which the template is being deployed.

The following example shows a full parameters file where one parameter value is being referenced from a Key Vault and another is a value:

## Full Example of Parameters File

```JSON
{
   "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
   "contentVersion": "1.0.0.0",
   "parameters": {
       "sqlsvrAdminLoginPassword": {
            "reference": {
                "keyVault": {
                    "id": "/subscriptions/683b75d2-eb2f-41c0-bd58-98791d060b8c/resourceGroups/RG-Local-KeyVaults/providers/Microsoft.KeyVault/vaults/SQLPwds"
                },
                "secretName": "defaultAdminPassword"
            }
        },
        "sqlsvrAdminLoginPassword": {
            "value": "sqlAdmin"
        },
    }
}
```

This type of reference is known as a ../../Linked_Image_Files ID reference because you cannot change the secret name that is being referenced at deployment time without changing the parameters file.