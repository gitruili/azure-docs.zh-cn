---
title: Azure 事件网格订阅事件架构
description: 介绍为 Azure 事件网格的订阅事件提供的属性
services: event-grid
author: tfitzmac
ms.service: event-grid
ms.topic: reference
ms.date: 08/17/2018
ms.author: tomfitz
ms.openlocfilehash: 18f2a64a4354fbd99f1a471c21cc35cbf5df6619
ms.sourcegitcommit: f057c10ae4f26a768e97f2cb3f3faca9ed23ff1b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2018
ms.locfileid: "42140220"
---
# <a name="azure-event-grid-event-schema-for-subscriptions"></a>Azure 事件网格用于订阅的事件架构

本文提供 Azure 订阅事件的属性和架构。 有关事件架构的简介，请参阅 [Azure 事件网格事件架构](event-schema.md)。

Azure 订阅和资源组发出相同的事件类型。 这些事件类型与资源中的更改相关。 主要区别是资源组针对资源组中的资源发出事件，Azure 订阅针对跨订阅的资源发出事件。

已为发送到 `management.azure.com` 的 PUT、PATCH 和 DELETE 操作创建资源事件。 POST 和 GET 操作不会创建事件。 发送到数据面板的操作（如 `myaccount.blob.core.windows.net`）不会创建事件。

当订阅 Azure 订阅的事件时，终结点接收该订阅的所有事件。 事件可能包括要查看的事件（例如更新虚拟机），以及可能不重要的事件（例如在部署历史记录中编写新条目）。 可以接收终结点上的所有事件并编写处理待处理事件的代码，也可以在创建事件订阅时设置筛选器。

若要以编程方式处理事件，可通过查看 `operationName` 值对事件进行排序。 例如，事件终结点可能只处理值等于 `Microsoft.Compute/virtualMachines/write` 或 `Microsoft.Storage/storageAccounts/write` 的操作的事件。

事件主题是作为操作目标的资源的资源 ID。 若要筛选资源的事件，请在创建事件订阅时提供该资源 ID。 若要按资源类型筛选，请使用以下格式的值：`/subscriptions/<subscription-id>/resourcegroups/<resource-group>/providers/Microsoft.Compute/virtualMachines`

有关示例脚本和教程的列表，请参阅 [Azure 订阅事件源](event-sources.md#azure-subscriptions)。

## <a name="available-event-types"></a>可用事件类型

Azure 订阅从 Azure 资源管理器发出管理事件，例如，在创建 VM 或删除存储帐户时。

| 事件类型 | Description |
| ---------- | ----------- |
| Microsoft.Resources.ResourceWriteSuccess | 当资源创建或更新操作成功时引发。 |
| Microsoft.Resources.ResourceWriteFailure | 当资源创建或更新操作失败时引发。 |
| Microsoft.Resources.ResourceWriteCancel | 当资源创建或更新操作取消时引发。 |
| Microsoft.Resources.ResourceDeleteSuccess | 当资源删除操作成功时引发。 |
| Microsoft.Resources.ResourceDeleteFailure | 当资源删除操作失败时引发。 |
| Microsoft.Resources.ResourceDeleteCancel | 当资源删除操作取消时引发。 取消模板部署时会发生此事件。 |

## <a name="example-event"></a>示例事件

以下示例展示了 ResourceWriteSuccess 事件的架构。 具有不同 `eventType` 值的 ResourceWriteFailure 和 ResourceWriteCancel 事件会使用相同的模式。

```json
[{
  "subject": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
  "eventType": "Microsoft.Resources.ResourceWriteSuccess",
  "eventTime": "2018-07-19T18:38:04.6117357Z",
  "id": "4db48cba-50a2-455a-93b4-de41a3b5b7f6",
  "data": {
    "authorization": {
      "scope": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
      "action": "Microsoft.Storage/storageAccounts/write",
      "evidence": {
        "role": "Subscription Admin"
      }
    },
    "claims": {
      "aud": "{audience-claim}",
      "iss": "{issuer-claim}",
      "iat": "{issued-at-claim}",
      "nbf": "{not-before-claim}",
      "exp": "{expiration-claim}",
      "_claim_names": "{\"groups\":\"src1\"}",
      "_claim_sources": "{\"src1\":{\"endpoint\":\"{URI}\"}}",
      "http://schemas.microsoft.com/claims/authnclassreference": "1",
      "aio": "{token}",
      "http://schemas.microsoft.com/claims/authnmethodsreferences": "rsa,mfa",
      "appid": "{ID}",
      "appidacr": "2",
      "http://schemas.microsoft.com/2012/01/devicecontext/claims/identifier": "{ID}",
      "e_exp": "{expiration}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "{last-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "{first-name}",
      "ipaddr": "{IP-address}",
      "name": "{full-name}",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "{ID}",
      "onprem_sid": "{ID}",
      "puid": "{ID}",
      "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "{ID}",
      "http://schemas.microsoft.com/identity/claims/tenantid": "{ID}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": "{user-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "{user-name}",
      "uti": "{ID}",
      "ver": "1.0"
    },
    "correlationId": "{ID}",
    "resourceProvider": "Microsoft.Storage",
    "resourceUri": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
    "operationName": "Microsoft.Storage/storageAccounts/write",
    "status": "Succeeded",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}"
  },
  "dataVersion": "2",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}"
}]
```

以下示例展示了 ResourceDeleteSuccess 事件的架构。 具有不同 `eventType` 值的 ResourceDeleteFailure 和 ResourceDeleteCancel 事件会使用相同的模式。

```json
[{
  "subject": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
  "eventType": "Microsoft.Resources.ResourceDeleteSuccess",
  "eventTime": "2018-07-19T19:24:12.763881Z",
  "id": "19a69642-1aad-4a96-a5ab-8d05494513ce",
  "data": {
    "authorization": {
      "scope": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
      "action": "Microsoft.Storage/storageAccounts/delete",
      "evidence": {
        "role": "Subscription Admin"
      }
    },
    "claims": {
      "aud": "{audience-claim}",
      "iss": "{issuer-claim}",
      "iat": "{issued-at-claim}",
      "nbf": "{not-before-claim}",
      "exp": "{expiration-claim}",
      "_claim_names": "{\"groups\":\"src1\"}",
      "_claim_sources": "{\"src1\":{\"endpoint\":\"{URI}\"}}",
      "http://schemas.microsoft.com/claims/authnclassreference": "1",
      "aio": "{token}",
      "http://schemas.microsoft.com/claims/authnmethodsreferences": "rsa,mfa",
      "appid": "{ID}",
      "appidacr": "2",
      "http://schemas.microsoft.com/2012/01/devicecontext/claims/identifier": "{ID}",
      "e_exp": "262800",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "{last-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "{first-name}",
      "ipaddr": "{IP-address}",
      "name": "{full-name}",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "{ID}",
      "onprem_sid": "{ID}",
      "puid": "{ID}",
      "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "{ID}",
      "http://schemas.microsoft.com/identity/claims/tenantid": "{ID}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": "{user-name}",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "{user-name}",
      "uti": "{ID}",
      "ver": "1.0"
    },
    "correlationId": "{ID}",
    "httpRequest": {
      "clientRequestId": "{ID}",
      "clientIpAddress": "{IP-address}",
      "method": "DELETE",
      "url": "https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2018-02-01"
    },
    "resourceProvider": "Microsoft.Storage",
    "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}",
    "operationName": "Microsoft.Storage/storageAccounts/delete",
    "status": "Succeeded",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}"
  },
  "dataVersion": "2",
  "metadataVersion": "1",
  "topic": "/subscriptions/{subscription-id}"
}]
```

## <a name="event-properties"></a>事件属性

事件具有以下顶级数据：

| 属性 | Type | Description |
| -------- | ---- | ----------- |
| 主题 | 字符串 | 事件源的完整资源路径。 此字段不可写入。 事件网格提供此值。 |
| subject | 字符串 | 事件主题的发布者定义路径。 |
| eventType | 字符串 | 此事件源的一个注册事件类型。 |
| EventTime | 字符串 | 基于提供程序 UTC 时间的事件生成时间。 |
| id | 字符串 | 事件的唯一标识符。 |
| 数据 | 对象 | 订阅事件数据。 |
| dataVersion | 字符串 | 数据对象的架构版本。 发布者定义架构版本。 |
| metadataVersion | 字符串 | 事件元数据的架构版本。 事件网格定义顶级属性的架构。 事件网格提供此值。 |

数据对象具有以下属性：

| 属性 | Type | Description |
| -------- | ---- | ----------- |
| authorization | 对象 | 操作请求的授权。 |
| 声明 | 对象 | 声明的属性。 有关详细信息，请参阅 [JWT 规范](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)。 |
| correlationId | 字符串 | 用于故障排除的操作 ID。 |
| httpRequest | 对象 | 操作的详细信息。 仅在更新现有资源或删除资源时才包含此对象。 |
| resourceProvider | 字符串 | 执行该操作的资源提供程序。 |
| resourceUri | 字符串 | 操作中资源的 URI。 |
| operationName | 字符串 | 执行的操作。 |
| status | 字符串 | 操作状态。 |
| subscriptionId | 字符串 | 资源的订阅 ID。 |
| tenantId | 字符串 | 资源的租户 ID。 |

## <a name="next-steps"></a>后续步骤

* 有关 Azure 事件网格的简介，请参阅[什么是事件网格？](overview.md)。
* 有关创建 Azure 事件网格订阅的详细信息，请参阅[事件网格订阅架构](subscription-creation-schema.md)。
