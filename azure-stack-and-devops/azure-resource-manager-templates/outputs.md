# Outputs

Outputs from an Azure Resource Manager template are optional. However, any output that is defined must return a value. The values that are returned from an ARM template do require you to declare a data type. There are only seven allowed data types for an output:

1. string

2. secureString

3. int

4. bool

5. object

6. secureObject

7. array

These are the same data types as described in the Parameters section before.

Below is the structure of the Output element:

```JSON
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

The following table describes each element:

|Element Name|Required|Description|
|---------|---------|---------|
|outputName|Yes|The name of the output value. This must be a valid JavaScript identifier.|
|type|Yes|This is the data type for the output. It must be one of the seven valid data types.|
|value|Yes|The value of the output. You can use Azure Resource Manager functions within the value to create or reference the required value. An example of the output could be the URI of a newly created resource.|