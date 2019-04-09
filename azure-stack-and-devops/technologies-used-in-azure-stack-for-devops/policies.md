# Policies

Azure Resource Manager allows Cloud Administrators to create customized policies for controlling resources that are deployed in their subscriptions. Cloud Administrators can use these Policies to apply certain organization-level specific constraints such as naming conventions, limit the type and number of instances of resources that can be deployed, enforce the presence of tags, and other capabilities.

You define policies by using JSON, and you can apply these policies to either an entire subscription or resource group. While RBAC can define what users/groups are permitted to do, it does not enforce restrictions on them as policies can.

An example of a policy could be one that ensures that all virtual machines deployed are running Windows Server 2012 R2 or Windows Server 2016, or a certain variant of Linux. This can prevent the deployment of non-authorized versions of operating systems.

Policy implementation is the responsibility of the Cloud Administrator. For more information on Azure Resource Manager policies, refer to the following website: <https://aka.ms/moc-10995A-pg045>