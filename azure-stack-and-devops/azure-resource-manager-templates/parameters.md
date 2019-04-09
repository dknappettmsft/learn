# Parameters

These are the inputs that you need to specify for the template to be deployed. By specifying these parameters, you can customize deployments as required. After you have specified a parameter, you can use it throughout your ARM template. For example, if you parameterize a prefix for virtual machines and you deploy four virtual machines with your template, you can use the parameter in all the four resources. You can have optional parameters by specifying a default value.

Each parameter is composed of 2-9 elements. These can be seen below:

```JSON
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": "<minimum-value-for-int>",
        "maxValue": "<maximum-value-for-int>",
        "minLength": "<minimum-length-for-string-or-array>",
        "maxLength": "<maximum-length-for-string-or-array-parameters>",
        "metadata": {
            "description": "<description-of-the parameter>"
        }
    }
}
```

The following table below describes each element:

|Element Name|Required|Description|
|---------|---------|---------|
|parameterName|Yes|The name of the parameter.|
|type|Yes|The data type of the parameter.|
|defaultValue|No|The default value of the parameter, which is used if no value is passed.|
|allowedValues|No|This is an array of values and the parameter value must match one of these values.|
|minValue|No|The minimum value for an integer parameter.|
|maxValue|No|The maximum value for an integer parameter.|
|minLength|No|The minimum length for a string, secureString, or array parameter type.|
|maxLength|No|The maximum length for a string, secureString, or array parameter type.|
|description|No|A description of the parameter. This is displayed in the portal in the custom template interface.|

There are only seven allowed data types for a parameter:

1. string

2. secureString

3. int

4. bool

5. object

6. secureObject

7. array

When using these data types, any sensitive data such as passwords, keys, or other sensitive information that should not be recorded should use the appropriate secureString or secureObject data type. The values passed to parameters are stored in the deployment history. Therefore, if there are any security considerations, you should use secureString and secureObject.

The following code is an example of a parameters element in an Azure Resource Manager template:

```JSON
"parameters": {
    "Username": {
        "type": "string",
        "defaultValue": "MyAdminUser",
        "metadata": {
            "description": "What do you want to name the Administrator account?"
        }
    },
    "Password": {
        "type": "secureString",
        "metadata": {
            "description": "What password do you want to use for the Administrator account?"
        }
    },
    "VMSize": {
        "type": "string",
        "defaultValue": "A1",
        "allowedValues": [
            "A0",
            "A1",
            "A2"
        ],
        "metadata": {
            "description": "What size VMs would you like to create?"
        }
    },
    "NumberToCreate": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1,
        "maxValue": 5,
        "metadata": {
            "description": "How many VMs would you like to create?"
        }
    }
}
```