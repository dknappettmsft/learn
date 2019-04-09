# Puppet with Azure Stack

Puppet is a configuration management application that is an alternative to PowerShell DSC. It uses the concept of a catalog to create configurations for servers in a similar manner to PowerShell DSC. You can create catalogs to deploy Windows and Linux features, and to install and configure software on both Windows and Linux operating systems.

Puppet requires the following key infrastructure components:

- **Puppet Master**: This is the core of the Puppet deployment, and is also known as the Puppet Server. The Puppet Master stores the system configuration and catalogs for use with target nodes. There is a web browser-based management console on the Puppet Master.

- **Puppet Agent**: This is installed on every target node that the Puppet Master is supposed to manage. The Puppet Agent is responsible for performing the configuration tasks defined in the module.

- **PuppetDB**: This is the database used by Puppet to store its catalogs. This is a PostgreSQL database.

You can deploy the Puppet Agent by using the VM Agent as an extension. During the deployment, you can specify the Puppet Master Server.