---
title: 为 AS2 消息解码 - Azure 逻辑应用 | Microsoft 文档
description: 使用 Azure 逻辑应用和 Enterprise Integration Pack 解码 AS 消息
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.date: 08/08/2018
ms.openlocfilehash: 06ffa6bddc1340ad548f9baf30eba65ba503bf73
ms.sourcegitcommit: 2ad510772e28f5eddd15ba265746c368356244ae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2018
ms.locfileid: "43128275"
---
# <a name="decode-as2-messages-with-azure-logic-apps-and-enterprise-integration-pack"></a>使用 Azure 逻辑应用和 Enterprise Integration Pack 解码 AS2 消息 

若要在传输消息时建立安全性和可靠性，请使用解码 AS2 消息连接器。 此连接器通过消息处置通知 (MDN) 提供数字签名、解密和确认等功能。

## <a name="before-you-start"></a>开始之前

需要具有以下各项：

* Azure 帐户；可以创建[免费帐户](https://azure.microsoft.com/free)
* 已定义的与 Azure 订阅关联的[集成帐户](logic-apps-enterprise-integration-create-integration-account.md)。 必须拥有集成帐户，才能使用解码 AS2 消息连接器。
* 已在集成帐户中至少定义了两个[合作伙伴](logic-apps-enterprise-integration-partners.md)
* 已在集成帐户中定义了 [AS2 协议](logic-apps-enterprise-integration-as2.md)

## <a name="decode-as2-messages"></a>为 AS2 消息解码

1. [创建逻辑应用](../logic-apps/quickstart-create-first-logic-app-workflow.md)。

2. 解码 AS2 消息连接器没有触发器，因此必须添加用于启动逻辑应用的触发器，如请求触发器。 在逻辑应用设计器中，添加触发器，然后将操作添加到逻辑应用。

3.  在搜索框中，输入“AS2”作为筛选器。 选择“AS2 - 解码 AS2 消息”。
   
    ![搜索“AS2”](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. 如果以前未创建与集成帐户的任何连接，系统会提示现在创建该连接。 为连接命名，并选择要连接的集成帐户。
   
    ![创建集成连接](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    带有星号的属性必填。

    | 属性 | 详细信息 |
    | --- | --- |
    | 连接名称 * |为连接输入任何名称。 |
    | 集成帐户 * |输入集成帐户的名称。 确保集成帐户和逻辑应用位于同一 Azure 位置。 |

5.  完成后，连接详细信息应如此示例所示。 若要完成连接创建，请选择“创建”。

    ![集成连接详细信息](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. 创建连接后，如此示例所示，从请求输出中选择“正文”和“标头”。
   
    ![已创建集成连接](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    例如：

    ![从请求输出中选择正文和标头](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 


## <a name="as2-decoder-details"></a>AS2 解码器详细信息

解码 AS2 连接器可执行以下任务： 

* 处理 AS2/HTTP 标头
* 验证签名（如果已配置）
* 对消息进行解密（如果已配置）
* 解压缩消息（如果已配置）
* 检查并禁止消息 ID 重复（如果已配置）
* 协调收到的 MDN 和原始的出站消息
* 更新并关联不可否认数据库中的记录
* 写入 AS2 状态报告的记录
* 输出有效负载内容采用了 base64 编码
* 根据 AS2 协议中的配置确定是否需要 MDN，以及 MDN 应该同步还是异步
* 生成同步或异步 MDN（基于协议的配置）
* 在 MDN 上设置关联令牌和属性


  > [!NOTE]
  > 如果使用 Azure Key Vault 进行证书管理，请确保配置密钥以允许**解密**操作。
  > 否则，AS2 解码将失败。
  >
  > ![KeyVault 解密](media/logic-apps-enterprise-integration-as2-decode/keyvault1.png)

## <a name="try-this-sample"></a>尝试此示例

若要尝试部署完全正常运行的逻辑应用和示例 AS2 方案，请参阅 [AS2 逻辑应用模板和方案](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)。

## <a name="view-the-swagger"></a>查看 Swagger
请参阅 [Swagger 详细信息](/connectors/as2/)。 

## <a name="next-steps"></a>后续步骤
[了解有关 Enterprise Integration Pack 的详细信息](logic-apps-enterprise-integration-overview.md) 

