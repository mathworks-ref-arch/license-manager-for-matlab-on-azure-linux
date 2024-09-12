# Network License Manager for MATLAB on Microsoft Azure (Linux VM)

This repository shows how to automate the process of starting a Network License Manager for MATLAB&reg;, running on a Linux&reg; virtual machine, using your Azure&reg; account. The cloud resources are created using Azure Resource Manager (ARM) templates. For information about the architecture of this solution, see [Learn About Architecture](#learn-about-architecture).

# Requirements

You need:

- An Azure&reg; account.

- A valid MathWorks&reg; license. For more information on configuring your license for cloud use, see [License Requirements for MATLAB on Cloud Platforms](https://www.mathworks.com/help/licensingoncloud/matlab-on-the-cloud.html).

- To be an administrator of the network license you want to use.

# Costs
You are responsible for the cost of the Azure services used when you create cloud resources using this guide. Resource settings such as instance type affect the cost of deployment. For cost estimates, see the pricing pages for each Azure service you will be using. Prices are subject to change.


# Deployment Steps

To view instructions for deploying the Network License Manager for MATLAB reference architecture, select a MATLAB release:

| Linux | Windows |
| ----- | ------- |
| [R2024b](releases/R2024b/README.md) | [R2024b](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2024b/README.md) |
| [R2024a](releases/R2024a/README.md) | [R2024a](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2024a/README.md) |
|                                     | [R2023b](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2023b/README.md) |
|                                     | [R2023a](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2023a/README.md) |
|                                     | [R2022b](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2022b/README.md) |
|                                     | [R2022a](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2022a/README.md) |
|                                     | [R2021b](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2021b/README.md) |
|                                     | [R2021a](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2021a/README.md) |
|                                     | [R2020b](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2020b/README.md) |
|                                     | [R2020a](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2020a/README.md) |
|                                     | [R2019b](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2019b/README.md) |
|                                     | [R2019a\_and\_older](https://github.com/mathworks-ref-arch/license-manager-for-matlab-on-azure/blob/master/releases/R2019a_and_older/README.md) |

## Learn About Architecture

The network license manager and its resources are created using [ARM templates](https://docs.microsoft.com/en-gb/azure/azure-resource-manager/resource-group-overview). The architecture is illustrated in Figure 2. For more information about each resource, see the [Azure template reference](https://docs.microsoft.com/en-us/azure/templates/).

![Server Architecture](img/FlexServer_in_Azure_architecture.png?raw=true)

*Figure 2: Network License Manager Architecture*

The following resources are created.

### Networking resources
* Virtual Network (Microsoft.Network/virtualNetworks) The Virtual Network includes the following components:
    * Subnet (Microsoft.Network/virtualNetworks/subnets)
    * Network Security Group (Microsoft.Network/networkSecurityGroups) : Ingress rules from client IP address:
        * Allow 3389: Required for Remote Desktop Protocol to connect to the network license manager server.
        * Allow 22: Required for SSH into the network license manager server.
        * Allow 443: Required for communication between client and network license manager for MATLAB Dashboard server.
        * Allow 27000-27010: Required for communication from MATLAB and MATLAB workers to the network license manager for MATLAB.
        * Allow all internal traffic: Open access to network traffic between all cluster nodes internally.
* Network interface (Microsoft.Network/networkInterfaces)
* Public IP Address (Microsoft.Network/publicIPAddresses)

### Instances
* Network license manager instance (Microsoft.Compute/virtualMachines): A Compute instance for the license server.
  * Custom Script Extension (Microsoft.Compute/virtualMachines/extensions): An extension which configures this instance at deployment time to start the network license manager for MATLAB Dashboard web server.

# Technical Support
To request assistance or additional features, contact [MathWorks Technical Support](https://www.mathworks.com/support/contact_us.html).

----

Copyright 2024 The MathWorks, Inc.

----
