---
title: Azure 事件网格 SDK
description: 介绍 Azure 事件网格的 SDK。 这些 SDK 提供管理、发布和使用功能。
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: reference
ms.date: 06/29/2018
ms.author: tomfitz
ms.openlocfilehash: 3c085074863aa166a5766116b6c63b7dc341ad96
ms.sourcegitcommit: 5892c4e1fe65282929230abadf617c0be8953fd9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37130829"
---
# <a name="event-grid-sdks-for-management-and-publishing"></a>用于管理和发布的事件网格 SDK

使用事件网格提供的 SDK 可以编程方式管理资源和发布事件。

## <a name="management-sdks"></a>管理 SDK

使用管理 SDK 可以创建、更新和删除事件网格主题和订阅。 目前有以下 SDK 可用：

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.Management.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://search.maven.org/#search%7Cga%7C1%7Cazure-mgmt-eventgrid)
* [Node](https://www.npmjs.com/package/azure-arm-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-mgmt-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_mgmt_event_grid)

## <a name="data-plane-sdks"></a>数据平面 SDK

使用数据平面 SDK，可以通过处理身份验证、形成事件并以异步方式发布到指定终结点来将事件发布到主题。 还可以通过这些 SDK 使用第一方事件。 目前有以下 SDK 可用：

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventgrid)
* [Node](https://www.npmjs.com/package/azure-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_event_grid)

## <a name="next-steps"></a>后续步骤

* 有关示例应用程序，请参阅[事件网格代码示例](https://azure.microsoft.com/resources/samples/?sort=0&service=event-grid)。
* 有关事件网格的介绍，请参阅[什么是事件网格？](overview.md)
* 有关 Azure CLI 中的事件网格命令，请参阅 [Azure CLI](/cli/azure/eventgrid)。
* 有关 PowerShell 中的事件网格命令，请参阅 [PowerShell](/powershell/module/azurerm.eventgrid)。
