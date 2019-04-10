# Deployment with Visual Studio

In addition to Azure PowerShell and Azure CLI, you can deploy Azure Resource Manager templates by using Visual Studio. You can connect Visual Studio directly to Azure Stack in the same manner as Azure.

Visual Studio must be connected to Azure Stack before you can deploy a template to Azure Stack. Use the following high-level steps to do deploy Azure Resource Manager templates by using Visual Studio:

1. Launch Visual Studio Community Edition.

2. In the Cloud Explorer pane, select Add an account.

3. Sign in with your Azure AD credentials.

4. Because your account already has access to an Azure Stack environment, you will be connected to it.

5. You will see the subscriptions you have access to beneath your Azure AD username.

After you have connected Visual Studio to Azure Stack, you can deploy Azure Resource Manager templates directly from Visual Studio. Use the following high-level steps to achieve this:

1. After your Azure Resource Manager template is ready to be deployed, select the template in Solution Explorer.

2. Click Deploy.

3. If required, change the selected account to your Azure AD account associated with Azure Stack.

4. Elect the subscription and resource group.

5. Edit any parameters required by the template, and then click OK.

6. The output pane will show whether the deployment has been accepted by Azure Stack for deployment.

For more details on how to deploy an Azure Resource Manager template with Visual Studio, refer to the following website: <https://aka.ms/moc-10995A-pg056>.