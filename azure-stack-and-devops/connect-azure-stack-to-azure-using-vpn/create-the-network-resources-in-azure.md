# Create the Network Resources in Azure

First you create the network resources for Azure. The following instructions show how to create the resources by using the Azure portal: <https://portal.azure.com>.

## Create the virtual network and VM subnet

1. Sign in to the Azure portal using your Azure account.

2. In the user portal, select **New**.

3. Go to **Marketplace**, and then select **Networking**.

4. Select **Virtual network**.

5. Use the information from the network configuration table to identify the values for Azure **Name**, **Address space**, **Subnet name**, and **Subnet address range**.

6. For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.

7. Select the **Location** of your VNet. If you\'re using the example values, select **East US** or use another location if you prefer.

8. Select **Pin to dashboard**.

9. Select **Create**.

## Create the Gateway Subnet

1. Open the Virtual network resource you created (**AzureVNet**) from the dashboard.

2. On the **Settings** section, select **Subnets**.

3. Select **Gateway subnet** to add a gateway subnet to the virtual network.

4. The name of the subnet is set to **GatewaySubnet** by default. Gateway subnets are special and must have this specific name to function properly.

5. In the **Address range** field, verify the address is **10.100.0.0/24**.

6. Select **OK** to create the gateway subnet.

## Create the virtual network gateway

1. In the Azure portal, select **New**.

2. Go to **Marketplace**, and then select **Networking**.

3. From the list of network resources, select **Virtual network gateway**.

4. In **Name**, type **Azure-GW**.

5. To choose a virtual network, select **Virtual network**. Then select **AzureVnet** from the list.

6. Select **Public IP address**. When the **Choose public IP address** section opens, select **Create new**.

7. In **Name**, type **Azure-GW-PiP**, and then select **OK**.

8. By default, for **VPN type**, **Route-based** is selected. Keep the **Route-based** VPN type.

9. Verify that **Subscription** and **Location** are correct. You can pin the resource to the dashboard. Select **Create**.

## Create the local network gateway resource

1. In the Azure portal, select **New**.

2. Go to **Marketplace**, and then select **Networking**.

3. From the list of resources, select Local network gateway.

4. In **Name**, type **Azs-GW**.

5. In **IP address**, type the public IP address for your Azure Stack Virtual Network Gateway that is listed earlier in the network configuration table.

6. In **Address Space**, from Azure Stack, type the **10.0.10.0/23** address space for **AzureVNet**.

7. Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.

## Create the connection

1. In the user portal, select **New**.

2. Go to **Marketplace**, and then select **Networking**.

3. From the list of resources, select **Connection**.

4. On the **Basic** settings section, for the **Connection type**, choose **Site-to-site (IPSec)**.

5. Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.

6. On the **Settings** section, select **Virtual network gateway**, and then select **Azure-GW**.

7. Select **Local network gateway**, and then select **Azs-GW**.

8. In **Connection name**, type **Azure-Azs**.

9. In **Shared key (PSK)**, type **12345**. If you choose a different value, remember that it must match the value for the shared key that you create on the other end of the connection. Select **OK**.

10. Review the **Summary** section, and then select **OK**.

## Create a virtual machine

Create a virtual machine in Azure now and put it on your VM subnet in
your virtual network.

1. In the Azure portal, select **New**.

2. Go to **Marketplace**, and then select **Compute**.

3. In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval image**.

4. On the **Basics** section, for **Name**, type **AzureVM**.

5. Type a valid username and password. You use this account to sign in to the virtual machine after it\'s created.

6. Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.

7. On the **Size** section, select a virtual machine size for this instance, and then select **Select**.

8. On the **Settings** section, you can accept the defaults. Make sure that the **AzureVNet** virtual network is selected, and verify that the subnet is set to **10.0.20.0/24**. Select **OK**.

9. Review the settings on the **Summary** section, and then select **OK**.