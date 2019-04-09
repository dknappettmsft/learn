# Resource Groups

When you define your resource group, you should be aware of the
following considerations:

- The resources within a resource group should share the same
    lifecycle. You should deploy, update, and delete them at the same
    time. If one of the resources, such as a virtual network, has a
    different lifecycle, it should be in a separate resource group.

- A resource, such as a virtual machine, can only reside in a single
    resource group.

- You can add or remove resources from a resource group when required.

- You can move resources between resource groups. However, there are
    some resources that you cannot move. Some examples include:

- Virtual private network (VPN) gateway

- Recovery Services Vault (only applies to Azure)

- Virtual machines with a certificate stored in Key Vault (only
    applies to Azure)

- A resource group can contain resources that are in different
    regions.

- You can use resource groups to scope administrative access through
    the implementation of RBAC.

- A resource in one resource group can interact with resources in
    other resource groups. For example, a virtual network can be one
    resource group and the virtual machines that are deployed into that
    virtual network are associated with another resource group.

Although a resource group can have resources that reside in different
regions, the resource group itself as a logical entity, must reside in a
single region. This is because the resource group contains metadata
about all the resources it contains and by defining the resource group
location you are defining where the metadata is stored.