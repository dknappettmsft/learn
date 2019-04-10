# EvOps from GridPro Software

GridPro Software is an independent software vendor (ISV) based in Sweden. They have several products related to IT Service Management that integrate with Microsoft technology:

- **WebFront for Service Manager:** This is a HTML5-based analyst portal for Microsoft System Center Service Manager. This product is capable of performing many of the functions associated with the standard Service Manager Console from Microsoft. However, because it is HMTL5-based, it is more flexible. You can access this application from any HTML5-based web browser and the application adjusts itself to the platform. For example, if you access the application from a tablet, the application will scale and orientate itself appropriately.

- **SMA Connector:** This is a connector for System Center Service Manager to enable communication with Service Management  Automation (SMA). This enables Service Manager to start and monitor runbooks based in SMA and not just System Center Orchestrator.

- **Request Management:** This is a resource provider for the Windows Azure Pack. This enables you to present Service Request Offerings to users in the WAP User Portal and to create the SRO in System Center Service Manager. In this scenario, you can use an Service Request Offerings to create a complex deployment or to request a new user account to be created.

In addition to the above software, GridPro has created EvOps for Azure Stack. There are three main components in EvOps:

1. **Service Catalog:** You can use the Service Catalog to create new Marketplace items within Azure Stack for deployment of Azure Stack resources. You could also create non-Azure Stack items such as a Service Request to request a new laptop or onboard a new employee. The items are templated within the Marketplace with predefined workflows that can include approval steps, deployment tasks, and other activities. A key feature here is the ability to integrate with external sources to perform validation of input. For example, you could verify that the name of a virtual machine does not already exist in AD DS prior to the deployment.

2. **Customer Support:** This component offers Support as a Service within the Azure Stack portal. Users can raise incidents through the EvOps resource provider regarding Azure Stack resources and potentially other resources too. This supports the delegated provider model within Azure Stack. Therefore, delegated providers can have an Azure Stack-based support service too. The Customer Support component also integrates with third-party Service Desk solutions such as Microsoft System Center Service Manager, BMC Remedy, Service Now, and others.

3. **Event Workflow:** This monitors Azure Stack for various events and can trigger predefined actions.

When you create items for the Service Catalog, you can create wizard-driven deployments, similar to normal Marketplace items, which you can define. You can define the behavior of the user experience (UX) directly within the EvOps resource provider. You can map the answers given by users to parameters in your workflow behind the Marketplace item. These parameters could be in a JSON template or in a API call to another system.

You do not need to deploy additional infrastructure for the EvOps resource provider. For example, there are no requirements for additional virtual machines because it uses the existing infrastructure within Azure Stack.

For more information about the EvOps Resource Provider from GridPro Software, refer to the following website: <https://aka.ms/moc-10995A-pg041>.