# Variable Manipulation

Some of the strings in your template might be supplied during deployment time as parameters or maybe variables within your template. There may be situations where you need to combine a parameter with some variable content to create a unique value for your deployment.

Within the String functions available is the concat function. The syntax for this is shown below:

```JSON
concat (string1, string2, string3, …)
```

To reference a parameter that is passed during deployment time you need to use the parameters function. The syntax for which is shown below:

```JSON
parameters(‘<parameter name>’)
```

The ARM template snippet below shows a parameter called vmPrefix and two variables vm1Name and vm2Name. The snippet shows how to use the concat function with the parameter function to create a unique variable content:

```JSON
"parameters": {
    "vmPrefix": {
        "type": "string",
        "metadata": {
            "description": "What prefix name do you want to give your VMs?"
        }
    }
},
"variables": {
    "vm1Name": "[concat(parameters('vmPrefix'),'01')]",
    "vm2Name": "[concat(parameters('vmPrefix'),'02')]"
}
```

To reference a variable in an ARM Template you use the variables function. The syntax for this is shown below:

```JSON
variables(‘<variable name’)
```