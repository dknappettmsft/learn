# Objects as Variables

Within an Azure Resource Manager template, you can create an object as a variable, and then reference the variable as an entire object to retrieve specific properties of the object. This can be useful when you want to create a common object such as an object containing tags.

The example below shows three parameters:

- departmentRef

- deploymentEnv

- supportTeam

Each of these parameters are used in tags on resources within the template. They are combined in the variable element to create an object called tagArray, which is then used within the resources section.

```JSON
"parameters": {
    "departmentRef": {
        "type": "string",
        "metadata": {
            "description": "Which department is this for?"
        }
    },
    "deploymentEnv": {
        "type": "string",
        "allowedValues": [
            "Development",
            "Testing",
            "Production"
        ],
        "metadata": {
            "description": "What type of deployment are you undertaking?"
        }
    },
    "supportTeam": {
        "type": "string",
        "metadata": {
            "description": "Who is supporting this application?"
        }
    },
    "variables": {
        "tagArray": {
            "DepartmentReference": "[parameters('departmentRef')]",
            "Environment": "[parameters('deploymentEnv')]",
            "SupportTeam": "[parameters('supportTeam')]"
        }
    },
    "resources": [
        {
            ...
            "tags": "[ variables('tagArray') ]",
            ...
        } ...
```

This allows you to reuse the entire tagArray object where required. If you wanted to use the tagArray as a base object, and then have additional tags per resource, the use of the tagArray variable would be different.

To reference a property of an object like the DepartmentReference from the tagArray variable you need to use object orientated notation. The example below shows the tags element within a Resource using this notation:

## Dot Notation for Accessing Object Properties in an ARM Template

```JSON
"parameters": {
    "departmentRef": {
        "type": "string",
        "metadata": {
            "description": "Which department is this for?"
        }
    },
    "deploymentEnv": {
        "type": "string",
        "allowedValues": [
            "Development",
            "Testing",
            "Production"
        ],
        "metadata": {
            "description": "What type of deployment are you undertaking?"
        }
    },
    "supportTeam": {
        "type": "string",
        "metadata": {
            "description": "Who is supporting this application?"
        }
    },
    "deploymentVersion": {
        "type": "string",
        "metadata": {
            "description": "Which version are you deploying?"
        }
    }
},
"variables": {
    "tagArray": {
        "DepartmentReference": "[parameters('departmentRef')]",
        "Environment": "[parameters('deploymentEnv')]",
        "SupportTeam": "[parameters('supportTeam')]"
    }
}
"resources": [
    {
        ...
        "tags": {
            "DeploymentVersion": "[parameters('deploymentVersion')]",
            "DepartmentReference": "[variables('tagArray').DepartmentReference]",
            "Environment": "[variables('tagArray').Environment]",
            "SupportTeam": "[variables('tagArray').SupportTeam]",
            "AnotherTag" : "ValueHere"
        },
        ...
    } ...
```

As you can see in the previous example, the range of possibilities with ARM template functions is quite extensive.