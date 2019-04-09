# Variables

You can use the Variables element of the Azure Resource Manager template to specify and construct values that will be used throughout your template. You can hard-code variables into your template, create them from parameters by using the Azure Resource Manager template functions, or use a mixture of the two methods. We recommend that you use variables wherever possible to aid in the change management of a template.

The following JSON file shows the structure of the variable element and an example variable.

```JSON
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": {
        <variable-complex-type-value>
    }
}
```

Note that variables do not have specific data types.