# Linking Templates

You can link an Azure Resource Manager template to another ARM template. Therefore, you can independently create templates, link them together in a master deployment, and allow for teams to generate their own templates and combine them together.

To create a link between two templates, you link it at the resource-level, within the properties element. Within the properties element, you create a property called templateLink.

Below is the structure of a resource with a linked template:

```JSON
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
                "StorageAccountName":{"value": "[parameters('StorageAccountName')]"}
            }
        }
    }
]
```

The preceding example links to a template called newStorageAccount.json and passes a parameter from the current template to the child template.