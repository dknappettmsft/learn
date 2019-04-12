# VM Creation

When creating a Virtual Machine, you are required to provide a username and password (for Windows Server) for a local user that is to be local administrator on the Virtual Machine during its provisioning. It is possible to use secrets within a Key Vault to answer both questions, so the provisioning user does not know the username or password.
To utilize secrets in Azure Key Vault as parameters for an ARM Template deployment, they must be referenced in a parameters file and that file passed to ARM during provisioning.
Below is an example parameters file that obtains the adminUsername and adminPassword from a Key Vault:

```JSON
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "reference": {
                "keyVault": {
                    "id": "/subscriptions/683b75d2-eb2f-41c0-bd58-98791d060b8c/resourceGroups/RG-Local-KeyVaults/providers/Microsoft.KeyVault/vaults/VMPasswords"
                },
                "secretName": "defaultAdminUsername"
            }
        },
        "adminPassword": {
            "reference": {
                "keyVault": {
                    "id": "/subscriptions/683b75d2-eb2f-41c0-bd58-98791d060b8c/resourceGroups/RG-Local-KeyVaults/providers/Microsoft.KeyVault/vaults/VMPasswords"
                },
                "secretName": "defaultAdminPassword"
            }
        },
        "vmName": {
            "value": "AZMEM0001"
        },
        "windowsOSVersion": {
            "value": "2016-Datacenter"
        }
    }
}
```

The template below can use the parameters file above to provide values for the following parameters using values from an Azure Key Vault:

- adminUsername

- adminPassword

The other values can be changed in the parameters file as required.

```JSON
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "vmName": {
            "type": "string",
            "minLength": 10,
            "maxLength": 15,
            "metadata": {
                "description": "The name of the virtual machine."
            }
        },
        "adminUsername": {
            "type": "securestring",
            "minLength": 1,
            "metadata": {
                "description": "Username for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "windowsOSVersion": {
            "type": "string",
            "defaultValue": "2016-Datacenter",
            "allowedValues": [
                "2016-Datacenter"
            ],
            "metadata": {
                "description": "The Windows version for the VM."
            }
        }
    },
    "variables": {
        "imagePublisher": "MicrosoftWindowsServer",
        "imageOffer": "WindowsServer",
        "OSDiskName": "osdiskforwindowssimple",
        "nicName": "[concat(parameters('vmName'),'-nic')]",
        "subnetName": "MemSrvrSubnet",
        "subnetPrefix": "10.0.0.0/24",
        "vhdStorageType": "Standard_LRS",
        "publicIPAddressName": "[concat(parameters('vmName'),'-pip')]",
        "publicIPAddressType": "Dynamic",
        "vhdStorageContainerName": "vhds",
        "vmName": "[parameters('vmName')]",
        "vmSize": "Standard_A2",
        "virtualNetworkName": "VN-local",
        "vnetResourceGroup": "RG-VNet",
        "vnetId": "[resourceId(variables('vnetResourceGroup'), 'Microsoft.Network/virtualNetworks', variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetId'), '/subnets/', variables('subnetName'))]",
        "vhdStorageAccountName": "[concat('vhdstorage', uniqueString(resourceGroup().id))]",
        "diagnosticsStorageAccountName": "[variables('vhdStorageAccountName')]",
        "wadmetricsresourceid": "[resourceId('Microsoft.Compute/virtualMachines', variables('vmName'))]"
    },
    "resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('vhdStorageAccountName')]",
        "apiVersion": "2015-06-15",
        "location": "[resourceGroup().location]",
        "tags": {
            "displayName": "StorageAccount"
        },
        "properties": {
            "accountType": "[variables('vhdStorageType')]"
        }
    },
    {
        "apiVersion": "2015-06-15",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[variables('nicName')]",
        "location": "[resourceGroup().location]",
        "tags": {
            "displayName": "NetworkInterface"
        },
        "properties": {
            "ipConfigurations": [
                {
                    "name": "ipconfig1",
                    "properties": {
                        "privateIPAddress": "10.0.1.4",
                        "privateIPAllocationMethod": "../../Linked_Image_Files",
                        "privateIPAddressVersion": "IPv4",
                        "subnet": {
                            "id": "[variables('subnetRef')]"
                        }
                    }
                }
            ]
        }
    },
    {
        "apiVersion": "2015-06-15",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[variables('vmName')]",
        "location": "[resourceGroup().location]",
        "tags": {
            "displayName": "VirtualMachine"
        },
        "dependsOn": [
            "[resourceId('Microsoft.Storage/storageAccounts/', variables('vhdStorageAccountName'))]",
            "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[variables('vmSize')]"
            },
            "osProfile": {
                "computerName": "[variables('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "imageReference": {
                    "publisher": "[variables('imagePublisher')]",
                    "offer": "[variables('imageOffer')]",
                    "sku": "[parameters('windowsOSVersion')]",
                    "version": "latest"
                },
                "osDisk": {
                    "name": "osdisk",
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts', variables('vhdStorageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vhdStorageContainerName'), '/', variables('OSDiskName'), '.vhd')]"
                    },
                    "caching": "ReadWrite",
                    "createOption": "FromImage"
                }
            },
            "networkProfile": {
                "networkInterfaces": [
                    {
                        "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('nicName'))]"
                    }
                ]
            }
        }
    }
    ]
}
```

The above example will create a Virtual Machine with the name AZMEM0001 with some parameter values obtained from a Key Vault.