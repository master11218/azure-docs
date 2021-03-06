---
title: Upgrade the configuration of an Azure Service Fabric cluster | Microsoft Docs
description: Learn how to upgrade the configuration that runs a Service Fabric cluster in Azure using a Resource Manager template.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: chackdan
editor: ''

ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/09/2018
ms.author: dekapur

---
# Upgrade the configuration of a cluster in Azure 

This article describes how to customize the various fabric settings for your Service Fabric cluster. For clusters hosted in Azure, you can customize settings through the [Azure portal](https://portal.azure.com) or by using an Azure Resource Manager template.

> [!NOTE]
> Not all settings are available in the portal, and it is a [best practice to customize it using an Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-best-practices-infrastructure-as-code); Portal is for Service Fabric Dev\Test scenario's only.
> 

## Customize cluster settings using Resource Manager templates
Azure clusters can be configured through the JSON Resource Manager template. To learn more about the different settings, see [Configuration settings for clusters](service-fabric-cluster-fabric-settings.md). As an example, the steps below show how to add a new setting *MaxDiskQuotaInMB* to the *Diagnostics* section using Azure Resource Explorer.

1. Go to https://resources.azure.com
2. Navigate to your subscription by expanding **subscriptions** -> **\<Your Subscription>** -> **resourceGroups** -> **\<Your Resource Group>** -> **providers** -> **Microsoft.ServiceFabric** -> **clusters** -> **\<Your Cluster Name>**
3. In the top right corner, select **Read/Write.**
4. Select **Edit** and update the `fabricSettings` JSON element and add a new element:

```json
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

You can also customize cluster settings in one of the following ways with Azure Resource Manager:

- Use the [Azure portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-export-template) to export and update the Resource Manger template.
- Use [PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-export-template-powershell) to export and update the Resource Manager template.
- Use the [Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-export-template-cli) to export and update the Resource Manager template.
- Use the Azure RM PowerShell [Set-AzureRmServiceFabricSetting](https://docs.microsoft.com/powershell/module/azurerm.servicefabric/Set-AzureRmServiceFabricSetting) and [Remove-AzureRmServiceFabricSetting](https://docs.microsoft.com/powershell/module/azurerm.servicefabric/Remove-AzureRmServiceFabricSetting) commands to modify the setting directly.
- Use the Azure CLI [az sf cluster setting](https://docs.microsoft.com/cli/azure/sf/cluster/setting) commands to modify the setting directly.

## Next steps
* Learn about the [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).
* Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).
