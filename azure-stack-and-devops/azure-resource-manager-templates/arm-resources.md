# ARM Resources

This element declares the resources that you want to provision as part of the template. The structure of the resources element is based on a JSON array, which is declared with "[ ]".

Below is the base structure of the Resources element. Each Resource declared uses this syntax:

```JSON
"resources": [
    {
        "apiVersion": "<api-version-of-resource>",
        "type": "<resource-provider-namespace/resource-type-name>",
        "name": "<name-of-the-resource>",
        "location": "<location-of-resource>",
        "tags": "<name-value-pairs-for-resource-tagging>",
        "comments": "<your-reference-notes>",
        "dependsOn": [
            "<array-of-related-resource-names>"
        ],
        "properties": "<settings-for-the-resource>",
        "copy": {
            "name": "<name-of-copy-loop>",
            "count": "<number-of-iterations>"
        }
        "resources": [
            "<array-of-child-resources>"
        ]
    }
]
```

The following table describes each element:

|Element Name|Required|Description|
|---------|---------|---------|
|apiVersion|Yes|The name of the parameter.|
|type|Yes|The data type of the parameter.|
|name|Yes|The default value of the parameter, which is used if no value is passed.|
|location|Varies|This is an array of values and the parameter value must match one of these values.|
|tags|No|The minimum value for an integer parameter.|
|comments|No|The maximum value for an integer parameter.|
|dependsOn|No|The minimum length for a string, secureString, or array parameter type.|
|properties|No|The maximum length for a string, secureString, or array parameter type.|
|copy|No|A description of the parameter. This is displayed in the portal in the custom template interface.|
|resources|No|A description of the parameter. This is displayed in the portal in the custom template interface.|

The sample below shows how a Virtual Network Resource could be defined:

```JSON
"resources": [
    {
        "type": "Microsoft.Network/virtualNetworks",
        "comments": "Main virtual network",
        "name": "TestVNet1",
        "apiVersion": "2016-03-30",
        "location": "local",
        "properties": {
            "addressSpace": {
                "addressPrefixes": [ "10.11.0.0/16" ]
            },
            "dhcpOptions": {
                "dnsServers": [ "208.67.220.220", "208.67.222.222" ]
            },
            "subnets": [
                {
                    "name": "GatewaySubnet",
                    "properties": {
                        "addressPrefix": "10.11.0.0/25",
                    }
                },
                {
                    "name": "WebServers",
                    "properties": {
                        "addressPrefix": "10.11.1.0/24",
                    }
                },
            ]
        }
    }
]
```