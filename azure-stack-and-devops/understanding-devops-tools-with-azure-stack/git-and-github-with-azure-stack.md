# Git and GitHub with Azure Stack

## Git

Git is an open-source version control system (VCS) that allows you to track changes in files. This enables multiple users to collaborate on projects and has become a popular VCS application. Linus Torvalds originally created Git in 2005 for the development of the Linux Kernel.

Unlike other VCS solutions, Git creates full copies of the repositories with full version tracking regardless of whether it can contact its primary Git server or not. When multiple developers work on a project together, this feature is extremely beneficial because when operations are performed, they are typically performed locally rather than calling back to the centralized repository.

You can use Git to branch code to allow developers to work on code without impacting the master copies and then merge their code into the master later. You can automate this process if required. In addition to branching, you can fork code where new projects are created from existing ones.

## GitHub

Microsoft uses GitHub extensively to store copies of the Azure documentation that is published on <https://aka.ms/moc-10995A-pg047>.

GitHub also stores the sample Azure Resource Manager templates from Microsoft for users to utilize, and it has become one of the best sources for Azure Resource Manager templates on the Internet. There is a large community of IT professionals who upload their templates for others to use.

When deploying Azure Resource Manager templates to Azure or Azure Stack, you can reference an Azure Resource Manager template stored on GitHub, without having to download the file to your local computer.

The PowerShell command below shows how to reference a template stored on GitHub and deploy to Azure or Azure Stack:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json
```