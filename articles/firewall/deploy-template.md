---
title: 使用模板部署 Azure 防火墙
description: 使用模板部署 Azure 防火墙
services: firewall
author: vhorne
manager: jpconnock
ms.service: firewall
ms.topic: article
ms.date: 7/11/2018
ms.author: victorh
ms.openlocfilehash: d32e6e29c287d140c28206743e36dc025b26158b
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46991328"
---
# <a name="deploy-azure-firewall-using-a-template"></a>使用模板部署 Azure 防火墙

此模板创建防火墙和测试网络环境。 网络有一个 VNet，其中包含三个子网：*AzureFirewallSubnet*、*ServersSubnet* 和 *JumpboxSubnet*。 ServersSubnet 和 JumpboxSubnet 每个中都有一个 2 核 Windows Server。

防火墙在 AzureFirewallSubnet 中并配置有一个应用程序规则集合，其中包含允许访问 www.microsoft.com 的单个规则。

创建了用户定义的一个路由，它引导来自 ServersSubnet 的网络流量穿过应用了防火墙规则的防火墙。

如果没有 Azure 订阅，请在开始之前创建一个[免费帐户](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。

## <a name="template-location"></a>模板位置

该模板位于：

[https://github.com/Azure/azure-quickstart-templates/tree/master/101-azurefirewall-sandbox](https://github.com/Azure/azure-quickstart-templates/tree/master/101-azurefirewall-sandbox)

阅读简介，并准备好部署后，单击“部署到 Azure”。

## <a name="clean-up-resources"></a>清理资源

首先，探究随防火墙创建的资源，当不再需要这些资源时，可以使用 [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) 命令来删除资源组、防火墙和所有相关资源。

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="next-steps"></a>后续步骤

接下来，可以监视 Azure 防火墙日志：

- [教程：监视 Azure 防火墙日志](./tutorial-diagnostics.md)

