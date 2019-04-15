# Examples of ARM Template Deployment with Key Vault - SQL Database creation

The following section describes an example of SQL Database creation where you can use Key Vault in conjunction with ARM Templates:

When you create a SQL Database through the SQL Resource Provider (Microsoft.SQLAdapter) you must specify several different parameters. One of the required parameters is the password for the Database Owner account that is created for you during provisioning. The only time you will be able to see the password is when you enter it.

Using Azure Resource Manager Templates, it is possible to create a Key Vault and populate it during provisioning, as such the password entered could be stored securely in Azure Key Vault as the database is being created.

The ARM Template below creates the following 3 resources:

- SQL Database

- Azure Key Vault

- A new secret in the Key Vault

The password for the database is randomly generated by using several different ARM Template functions based on a variety of sources including the Resource Group ID and the Subscription ID.

```JSON
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "databaseName": {
            "type": "string",
            "metadata": {
                "description": "Name of the SQL database to be created."
            }
        },
        "databaseLoginName": {
            "type": "string",
            "metadata": {
                "description": "Name of the SQL login to be created for connecting to the new database."
            }
        },
        "databaseSizeMB": {
            "type": "int",
            "metadata": {
                "description": "Size in MB of the SQL database to be created."
            }
        }
    },
    "variables": {
        "sqlPassword": "[concat(uniquestring(parameters('databaseName'), resourceGroup().id, subscription().id), toUpper(resourceGroup().id))]",
        "skuName": "Basic",
        "skuTier": "Bronze",
        "skuFamily": "SQL 2014",
        "collation": "SQL_Latin1_General_CP1_CI_AS"
    },
    "resources": [
    {
        "type": "Microsoft.SQLAdapter/servers",
        "name": "[parameters('databaseName')]",
        "apiVersion": "2014-04-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
            "administratorLogin": "[parameters('databaseLoginName')]",
            "administratorLoginPassword": "[variables('sqlPassword')]",
            "SkuName": "[variables('skuName')]"
        },
        "resources": [
            {
            "type": "databases",
            "sku": {
                "name": "[variables('skuName')]",
                "tier": "[variables('skuTier')]",
                "family": "[variables('skuFamily')]"
            },
            "name": "[parameters('databaseName')]",
            "apiVersion": "2014-04-01-preview",
            "location": "[resourceGroup().location]",
            "properties": {
                "databaseName": "[parameters('databaseName')]",
                "collation": "[variables('collation')]",
                "maxSize": "[parameters('databaseSizeMB')]"
            },
            "dependsOn": [
                "[concat('Microsoft.SQLAdapter/servers/', parameters('databaseName'))]"
            ]
            }
        ]
    },
    {
        "type": "Microsoft.KeyVault/vaults",
        "name": "MASVault1",
        "apiVersion": "2015-06-01",
        "location": "[resourceGroup().location]",
        "properties": {
            "sku": {
                "family": "A",
                "name": "Standard"
            },
            "tenantId": "[subscription().tenantId]",
            "accessPolicies": [
            {
                "tenantId": "[subscription().tenantId]",
                "objectId": "9b65f3a5-8bc2-4bd8-8f94-bb2d583b4690",
                "permissions": {
                    "keys": [ "All" ],
                    "secrets": [ "All" ]
                }
            }
            ]
        },
        "dependsOn": [
        "[resourceId('Microsoft.SQLAdapter/servers', parameters('databaseName'))]"
        ]
    },
    {
        "type": "Microsoft.KeyVault/vaults/secrets",
        "name": "[concat('MASVault1/',parameters('databaseName'),'-pwd')]",
        "apiVersion": "2015-06-01",
        "properties": {
            "contentType": "text/plain",
            "value": "[variables('sqlPassword')]"
        },
        "dependsOn": [
            "[resourceId('Microsoft.KeyVault/vaults', 'MASVault1')]"
        ]
    }
    ]
}
```

At no time during the provisioning process does the user know the password that is created, as such the Key Vault could be configured in such a way that the provisioning user can set the secret but never get it. Other users may be able to get the secret, but not set it.