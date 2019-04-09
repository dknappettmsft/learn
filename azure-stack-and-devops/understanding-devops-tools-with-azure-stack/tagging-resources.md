# Tagging Resources

Within Azure Resource Manager, you can apply arbitrary tags to resources and resource groups as required. Tags are based on a Key/Value pair concept and are optional. However, they are considered critical for workload identification and classification. The following table provides a list of suggested tags that you can use with Azure Resource Manager Resources:

|Tag Name|Example Value|Description|
|---------|---------|---------|
|Environment|Production|This tag describes the environment in which the resource resides. It can help identify resources that might have been provisioned to an incorrect subscription, region, or resource group.|
|SLA|Tier 1|This helps identify critical workloads in a subscription.|
|CostCenter|A1234|When the Azure Stack billing routines are executed, this tag can help you, or the users, perform chargeback/show back to the correct department within an organization.|
|DateCreated|2017-01-15|Obtaining the date that a resource was created in Azure Resource Manager can be difficult. Therefore, adding a tag for this can be beneficial, especially for life-cycle management. We highly recommend that you use a standardized date pattern regardless of the common date pattern in a geographical location.|
|MaintenanceWindow|Standard|This tag dictates the maintenance window used by the resource. For example, the Standard value could signify that maintenance could be undertaken between midnight and 4:00 am every Saturday.|
|DataProfile|Level 1|This tag could signify the type of data this resource deals with. For example, Level 1 could mean highly regulated data, and therefore, you could use a monitoring process to ensure the correct level of RBAC has been applied to the resource.|

These are just some examples of scenarios where you can use tagging. The primary goal of tags is to help you understand what a resource is and how you can logically organize and classify it. You should be aware of the following restrictions on using tags:

- A resource, or resource group, has a maximum of 15 tags

- Each tag name is limited to 512 characters

- A tag value is limited to 256 characters

- Tags applied at the resource group-level are not inherited by resources that are contained within the resource group.

After you have applied tags, you can obtain all resources (including resource groups) within a subscription that has the same tag. This can be useful in organizing resources and ensuring billing is applied correctly.

Within an Azure Resource Manager Policy, you can establish a baseline for tags in a subscription. This can prevent resources and resource groups from being created without the appropriate tag being present. For example, if you stipulate in your subscription policy that the DataProfile tag is present on every resource and it is omitted from a deployment, the deployment will fail.

The snippet from an ARM Policy shows this:

```JSON
    {
        "if": {
        "not" : {
            "field" : "tags",
            "containsKey" : "DataProfile"
        }
    },
    "then" : {
        "effect" : "deny"
        }
    }
```

When using tags, it is possible to include a space within the Key value. However, we do not recommend including one. We recommend using Pascal casing, where each word used starts with a capital letter but does not contain spaces, such as DataProfile and CostCenter. For more information, refer to the following website: <https://aka.ms/moc-10995A-pg049>.