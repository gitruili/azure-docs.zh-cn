---
title: Azure 容器实例配额和区域可用性
description: Azure 容器实例服务的默认配额和区域可用性
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 02/27/2018
ms.author: marsma
ms.openlocfilehash: 1bc890abc8b406ae75f292f37775e4cb62cf0473
ms.sourcegitcommit: 7827d434ae8e904af9b573fb7c4f4799137f9d9b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39115269"
---
# <a name="quotas-and-region-availability-for-azure-container-instances"></a>Azure 容器实例的配额和区域可用性

所有 Azure 服务都包括某些针对资源和功能的默认限制和配额。 以下部分详述了多个 Azure 容器实例 (ACI) 资源的默认资源限制，以及 Azure 区域中 ACI 服务的可用性。

## <a name="service-quotas-and-limits"></a>服务配额和限制

[!INCLUDE [container-instances-limits](../../includes/container-instances-limits.md)]

## <a name="region-availability"></a>上市区域

Azure 容器实例在具有指定 CPU 和内存限制的以下区域中可用。

| 位置 | OS | CPU | 内存 (GB) |
| -------- | -- | :---: | :-----------: |
| 美国西部、美国东部、西欧、北欧 | Linux | 4 | 14 |
| 美国西部 2 区、东南亚 | Linux | 2 | 7 |
| 澳大利亚东部、美国东部 2、美国中部 | Linux | 1 | 1.5 |
| 美国西部、美国东部、西欧、北欧 | Windows | 4 | 14 |
| 美国西部 2 区、东南亚 | Windows | 2 | 3.5 |

在这些资源限制内创建的容器实例受部署区域内可用性的限制。 某个区域负载较重时，部署实例时可能会失败。 若要减少此类部署失败，请尝试部署具有较低 CPU 和内存设置的实例，或稍后尝试部署。

如果需要其他区域，或者需要提高 CPU/内存限制，请告知我们的团队，网址为：[aka.ms/aci/feedback](https://aka.ms/aci/feedback)。

有关容器实例部署故障排除的详细信息，请参阅[排查 Azure 容器实例的部署问题](container-instances-troubleshooting.md)。

## <a name="next-steps"></a>后续步骤

某些默认限制和配额可以提高。 若要请求增加一个或多个资源（如果支持此功能），请提交 [Azure 支持请求][azure-support]（选择“配额”作为“问题类型”）。

<!-- LINKS - External -->
[azure-support]: https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest
