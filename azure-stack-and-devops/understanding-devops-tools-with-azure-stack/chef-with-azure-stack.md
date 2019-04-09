# Chef with Azure Stack

Chef is a configuration management and systems automation tool that is an alternative to PowerShell DSC. It uses the concept of a Cookbook to create a configuration policy for servers in a similar manner to PowerShell DSC. You can create Cookbooks to deploy Windows features, Linux features and to install and configure software on both Windows and Linux operating systems.

Chef requires the following key infrastructure components:

- **Chef Server**: This is a central repository for storing system configuration and cookbooks for use with target nodes. There is a web browser-based management console on the Chef Server.

- **Chef Client**: This is installed on every target node that the Chef Server is supposed to manage. It is responsible for performing the configuration tasks defined in the Cookbook.

- **Workstation**: Cookbooks are created, tested, and maintained in the workstations and you use a workstation to upload the cookbooks to the Chef Server.

- **Chef Automate**: This is a platform that stores the actions and run history of cookbooks and nodes. It offers real-time reporting and notifications for the automation activities performed with Chef and a code-testing pipeline.

The Chef Supermarket is an additional component of Chef that you can use. . This is an open-source repository of community generated cookbooks that are available for Chef users to use within their environment or to use as a base and to tailor to their requirements.

You can deploy the Chef Client by using the VM Agent as an extension. During the deployment, you can specify the following parameters:

- Chef Server URL*

- Chef Node Name*

- Run List

- Validation Client Name*

- Validation Key*

- Client Configuration File

- SL Verification Mode

- Chef Environment

- Encrypted Database Secret

- Chef Server SSL Certificate