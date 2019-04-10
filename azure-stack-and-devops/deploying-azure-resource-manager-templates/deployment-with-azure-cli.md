# Deployment with Azure CLI

In addition to Azure PowerShell, Microsoft also offers the Azure CLI, which you can deploy to Windows-based operating systems and other non-Microsoft operating systems. For more information on how to install the Azure CLI, refer to the following Microsoft website: <https://aka.ms/moc-10995a-pg081>.

To use Azure CLI with Azure Stack, you must:

- Be signed into Azure through Azure CLI. This requires you to register Azure Stack with the Azure CLI.

- Configure the Azure CLI to use ARM.

- Connect to the correct subscription.

- Have the required permissions to deploy a template with the specified resources.

- Have a template file, either stored locally or on a publicly available web server.

- Store the values for any parameters in either a parameters JSON file or encode them as required by the Azure CLI.

Use the following high-level steps to deploy an Azure Resource Manager template with Azure CLI to a user subscription:

1. Run the following Windows PowerShell cmdlet to obtain the required Active Directory resource ID:

    ```PowerShell
    (Invoke-RestMethod -Uri https://management.local.azurestack.external/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
    ```

    The value returned will be in the format: `https://api.azurestack.local/<GUID>`
    &nbsp;

2. In the Azure CLI, run the following command, remembering to substitute the value obtained in the previous step:

    ```bash
    azure account env add AzureStack --resource-manager-endpoint-url "https://management.local.azurestack.external" --management-endpoint-url "https://management.local.azurestack.external" --active-directory-endpoint-url "https://login.windows.net" --portal-url "https://portal.local.azurestack.external" --gallery-endpoint-url "https://portal.local.azurestack.external/" --active-directory-resource-id "<Active directory resource ID>" --active-directory-graph-resource-id "https://graph.windows.net/"
    ```

3. Sign into Azure Stack through the Azure CLI:

    ```bash
    azure login -e AzureStack -u "<username>"
    ```

4. Enter the password when prompted. If you receive a failure notification regarding an untrusted certificate, enter the following command:

    ```bash
    set NODE_TLS_REJECT_UNAUTHORIZED=0
    ```

    Then attempt to sign in again.
    &nbsp;

5. To configure Azure CLI to use Azure Resource Manager, enter the following command:

    ```bash
    azure config mode arm
    ```

6. After you are connected, you can create a resource group using the following command:

    ```bash
    azure group create -n ExampleResourceGroup -l "local"
    ```

7. You can then deploy an Azure Resource Manager template by using the following command:

    ```bash
    azure group deployment create -f "c:\MyTemplates\example.json" -e "c:\MyTemplates\example.params.json" -g ExampleResourceGroup -n ExampleDeployment
    ```

For more details on how to deploy an Azure Resource Manager template with Azure CLI, refer to the following website: <https://aka.ms/moc-10995A-pg055>.

It should be noted that if you are using Azure CLI in AD FS mode with Azure Stack Development Kit, then only Service Principles are supported. You can obtain further information about Service Principles including how to create one for AD FS from the following website: <https://aka.ms/moc-10995a-pg082>.