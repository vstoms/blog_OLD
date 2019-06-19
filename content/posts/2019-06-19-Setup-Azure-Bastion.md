---
template: post
title: Microsoft Azure Bastion
slug: /posts/2019/setup-azure-bastion
draft: false
date: 2019-06-19T17:14:23.724Z
description: >-
  What is and how to set up Azure Bastion.
category: blog
tags:
  - Azure
  - Bastion
---
![logo](/media/Bastion/logo_bastion.png)

Microsoft has recently announced the preview of Azure Bastion. And I will show you how to set this up.

__Word of caution: per 19.06.19 Azure Bastion is still under preview.__

### What is Bastion

Azure Bastion is a new managed PaaS service that provides seamless RDP and SSH connectivity to your virtual machines over the Secure Sockets Layer (SSL). This is completed without any exposure of the public IPs on your virtual machines.

Azure Bastion provisions directly in your Azure Virtual Network, providing bastion host or jump server as-a-service and integrated connectivity to all virtual machines in your virtual networking using RDP/SSH directly from and through your browser and the Azure portal experience.

This can be executed with just two clicks and without the need to worry about managing network security policies.

### Architecture

![Architecture](/media/Bastion/2.png)

* RDP and SSH from the Azure portal: Initiate RDP and SSH sessions directly in the Azure portal with a single-click seamless experience.
* Remote session over SSL and firewall traversal for RDP/SSH: HTML5 based web clients are automatically streamed to your local device providing the RDP/SSH session over SSL on port 443. This allows easy and securely traversal of corporate firewalls.
* No public IP required on Azure Virtual Machines: Azure Bastion opens the RDP/SSH connection to your Azure virtual machine using a private IP, limiting exposure of your infrastructure to the public Internet.
* Simplified secure rules management: Simple one-time configuration of Network Security Groups (NSGs) to allow RDP/SSH from only Azure Bastion.
* Increased protection against port scanning: The limited exposure of virtual machines to the public Internet will help protect against threats, such as external port scanning.
* Hardening in one place to protect against zero-day exploits: Azure Bastion is a managed service maintained by Microsoft. It’s continuously hardened by automatically patching and keeping up to date against known vulnerabilities.

### Create an Azure Bastion host

Once you provision the Azure Bastion service in your virtual network, the seamless RDP/SSH experience is available to all your VMs in the same virtual network.
This deployment is per virtual network, not per subscription/account or virtual machine.

The public preview is limited to the following Azure public regions:

* West US
* East US
* West Europe
* South Central US
* Australia East
* Japan East

Make sure that you are signed into your Azure account and are using the subscription that you want to onboard for this preview. Use the following example to enroll:

```powershell
Register-AzureRmProviderFeature -FeatureName AllowBastionHost -ProviderNamespace Microsoft.Network
```

Reregister your subscription once again with the Microsoft.Network provider namespace.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

Use the following command to verify that the AllowBastionHost feature is registered with your subscription:

```powershell
Get-AzureRmProviderFeature -ProviderNamespace Microsoft.Network
```

1. Next we need to create the bastion host, use the [Azure portal - preview](http://aka.ms/BastionHost)
2. On the __New page__, in the Search the Marketplace field, type Bastion, then click Enter to get to the search results.
3. From the results, click __Bastion (preview).__ Make sure the publisher is Microsoft and the category is Networking.
4. On the __Bastion (preview)__ page, click Create to open the Create a bastion page.
5. On the Create a __bastion page__, configure a new Bastion resource. Specify the configuration settings for your Bastion resource.

![Azure Portal](/media/Bastion/1.png)

The virtual network in which the Bastion resource will be created in. You can create a new virtual network in the portal during this process, in case you don’t have or don’t want to use an existing virtual network. If you are using an existing virtual network, make sure the existing virtual network has enough free address space to accommodate the Bastion subnet requirements.

The subnet in your virtual network to which the new Bastion host resource will be deployed. You must create a subnet using the name value __AzureBastionSubnet__. This value lets Azure know which subnet to deploy the Bastion resources to. This is different than a Gateway subnet. Microsoft highly recommend that you use at least a /27 or larger subnet (/27, /26, and so on). Create the __AzureBastionSubnet__ without any Network Security Groups, route tables, or delegations.

### Connect to a Windows virtual machine

In order to make a connection, the following roles are required:

* Reader role on the virtual machine
* Reader role on the NIC with private IP of the virtual machine
* Reader role on the Azure Bastion resource.

In the [Azure portal - preview](http://aka.ms/BastionHost), navigate to the virtual machine that you want to connect to, then click Connect. The VM should be a Windows virtual machine when using an RDP connection.

![Azure Portal](/media/Bastion/3.png)

After you click Connect, a side bar appears that has three tabs – RDP, SSH, and Bastion. If Bastion was provisioned for the virtual network, the Bastion tab is active by default. If you didn't provision Bastion for the virtual network, you can click the link to configure Bastion

![Azure Portal](/media/Bastion/4.png)

On the Bastion tab, the username and password for your virtual machine, then click Connect. The RDP connection to this virtual machine via Bastion will open directly in the Azure portal (over HTML5) using port 443 and the Bastion service.

![Azure Portal](/media/Bastion/5.png)