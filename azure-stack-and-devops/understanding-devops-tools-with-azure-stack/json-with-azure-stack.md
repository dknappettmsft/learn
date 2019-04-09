# JSON with Azure Stack

JavaScript Object Notation (JSON) is an extremely lightweight way of storing information in structured manner with Property Value data. For example, the JSON document below describes a person and their address:

```JSON
{
    "givenName" : "Jon",
    "lastName" : "Doe",
    "address" : {
        "line1" : "21 Unknown Street",
        "city:" : "Seattle",
        "state" : "WA",
        "zipCode" : "12345"
    }
}
```

As you can see in the preceding example, the code is in a human readable format. You can attach additional items such as a reference to a schema to ensure the JSON document meets the required structure.

Ajax-based websites use JSON to interchange structured data in a lightweight fashion. However, it has also lead to the rise of NoSQL-based databases. Because you can structure the format of a JSON document as required, it allows for a great deal of flexibility.

Within an ARM Template, you cannot add JavaScript comments as shown in the following example:

```JSON
...
},
// This is the Resources section
"resources": [
{
    "name": "[variables('storageAccountName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "[variables('location')]",
...
```

Because you cannot add comments into ARM templates directly, we recommend that you to keep documentation about the template, along with the template, in your code repository.