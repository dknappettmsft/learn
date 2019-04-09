# Role Based Access Control (RBAC)

RBAC allows for the granular control of actions over resources. It is natively integrated into the management platform and applies the access control to all services in a resource group. You must understand two main components when you work with RBAC:

- **Role definition:** This defines a set of permissions that you can undertake. You create role definitions at the subscription level and you can reuse them.

- **Role assignment:** This associates a role definition with an identity, be that a user or a group, for a specific scope. You can scope to a subscription, a resource group, or resource. Role assignments are inherited by lower scopes. For example, if you assign a role definition to a resource group, all the resources within the resource group inherit that role definition.

Azure Resource Manager provides several predefined role definitions. Some are defined at the subscription level, while others are assigned at the resource group or resource level. The following table shows the subscription-level role definitions.

|Role Name|Description|
|---------|---------|
|Owner|This role has total control over everything in the subscription, including access control.|
|Contributor|This role has total control over everything in the subscription, except access control.|
|Reader|This role permits view permissions over everything in the subscription. However, this role cannot make any changes.|
|User Access Administrator|This role can manage access to Azure resources.|

Each resource provider offers resource-specific roles. The following table lists some common examples.

|Role Name|Description|
|---------|---------|
|Virtual Machine Contributor|This role can manage virtual machines (at the Azure level) but does not have access to them. The role does have permission to manage the virtual network or storage account(s) used by Virtual Machines.|
|Network Contributor|This role can manage network-level resources such as subnet and internal load balancers. This role cannot grant access to network resources.|
|Storage Account Contributor|This role can manage storage accounts and their contents. For example, it can create containers in a storage account and delete contents from storage accounts. However, it cannot grant access to storage accounts.|

You can create your own role definitions in Azure Resource Manager based on the actions exposed by each resource provider. You can assign more than one role definition to an Azure Active Directory (Azure AD) identity.

Designing RBAC for subscriptions, resource groups, and resources is the responsibility of the Cloud Administrator. For more information, refer to the following website: <https://aka.ms/moc-10995A-pg044>.