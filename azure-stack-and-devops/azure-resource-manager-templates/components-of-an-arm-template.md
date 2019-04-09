# Components of an ARM Template

An ARM Template is composed of 3-6 elements that can be seen below:

```JSON
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": { },
    "variables": { },
    "resources": [ ],
    "outputs": { }
}
```

The following table describes each element:

|Element Name|Required|Description|
|---------|---------|---------|
|$schema|Yes|This role has total control over everything in the subscription, including access control.|
|contentVersion|Yes|This role has total control over everything in the subscription, except access control.|
|parameters|No|This role permits view permissions over everything in the subscription. However, this role cannot make any changes.|
|variables|No|This role can manage access to Azure resources.|
|resources|Yes|This role can manage access to Azure resources.|
|outputs|No|This role can manage access to Azure resources.|

The base syntax of the Azure Resource Manager template is JSON but you can extend the functionality to include Azure Resource Manager specific expressions and functions. For example, you could use the concat function to concatenate two strings together. The source strings could be parameters, variables, resource identifiers – anything that can be referenced inside the JSON template. The next lesson covers ARM functions in details.