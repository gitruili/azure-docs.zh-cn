---
title: 快速入门 - 通过成本分析了解 Azure 成本 | Microsoft Docs
description: 本快速入门可帮助你通过成本分析了解和分析 Azure 组织成本。
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 09/14/2018
ms.topic: quickstart
ms.service: cost-management
manager: dougeby
ms.custom: ''
ms.openlocfilehash: 0e94392b882d111d925c864feb9aaeb54bae4e2a
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46980400"
---
# <a name="quickstart-explore-and-analyze-costs-with-cost-analysis"></a>快速入门：通过成本分析了解和分析成本

需要知道你组织中哪些方面产生了成本，然后才能正确地控制和优化 Azure 成本。 这还有助于了解你服务的成本及其支持哪些环境和系统。 要准确地了解组织的支出模式，必须了解成本的方方面面。 在强制实施成本控制机制（如预算）时可使用支出模式。

在本快速入门中，你将通过成本分析了解和分析组织成本。 可以按组织查看合计成本，了解哪些方面持续产生成本并确定支出趋势。 可以查看一段时间的累计成本，根据预算预估每月、每季度甚至每年的成本趋势。 预算可帮助你遵守财务约束。 并且预算用于查看每日或每月成本，以隔离异常支出行为。 你还可下载当前报表的数据进行深入分析或在外部系统中使用。

此快速入门介绍如何：

- 通过成本分析查看成本
- 自定义成本视图
- 下载成本分析数据


## <a name="prerequisites"></a>先决条件

所有企业协议 (EA) 客户均可使用成本分析。 必须至少具有下列某一作用域的读权限，才可查看成本数据。

- Azure EA 计费帐户（注册）
- Azure EA 订阅
- Azure EA 订阅资源组

## <a name="sign-in-to-azure"></a>登录 Azure

- 通过 http://portal.azure.com 登录到 Azure 门户。

## <a name="review-costs-in-cost-analysis"></a>通过成本分析查看成本

要通过成本分析查看你的成本，请打开 Azure 门户，然后导航到“成本管理 + 计费”&gt;“计费帐户”，选择“EA 计费帐户”，再在“成本管理”下选择“成本分析”。

初始成本分析视图包括以下方面：

总计 - 显示当月的总成本。

预算 - 显示所选范围的计划支出限额（如可用）。

累计成本 - 显示从本月初算起的累计每日支出总额。 为计费帐户或订阅[创建预算](tutorial-acm-create-budgets.md)后，可快速查看对预算而言的支出趋势。 将鼠标悬停某个日期上以查看该天的累计成本。

透视图（圆环图）– 提供动态透视，按一组常见标准属性分解总成本。 它们显示当月累计的最高成本至最低成本。 通过选择不同的透视，可以随时更改透视图。 成本按以下类别分类：服务（计量类别）、位置（区域）和子范围（默认）。 例如，注册帐户在计费帐户之下，资源组在订阅之下，资源在资源组之下。

![成本分析的初始视图](./media/quick-acm-cost-analysis/cost-analysis-01.png)

## <a name="customize-cost-views"></a>自定义成本视图

通过默认视图，可快速解答常见问题，例如：

- 我支出了多少？
- 在预算范围内吗？

但是，在很多情况下需要更深入的分析。 在页面顶部通过数据选择进行自定义。

默认情况下，成本分析显示当前月份的数据。 使用日期选择器可快速切换到：上个月、本月、本季度、本年度或所选的自定义日期范围。 要分析最近的 Azure 发票并轻松进行对账，最快速的方式是选择上个月。 当前季度和年度选项有助于跟踪针长期预算的成本。 也可以选择不同的日期范围。 例如，可以选择一天、过去七天或当前月之前一年的任何时间。

![日期选择器](./media/quick-acm-cost-analysis/date-selector.png)

默认情况下，成本分析显示“累计”成本。 累计成本显示包括前几天在内的每日费用总额，显示每日应计成本不断变化的情况。 此视图已进行优化，可显示对预算而言所选日期范围的支出趋势。

此外，还有每日视图显示每日成本。 每日视图不会显示增长趋势。 该视图旨在显示异常，如每日的成本峰值或 dip。 如果选择了预算，则每日视图还会显示每日预算的估算值。 如果你的每日成本不断高于估算的每日预算，则可能会超出每月预算。 估算的每日预算只是一种可在较浅显的层面上帮助你直观查看预算的方式。 如果每日成本出现波动，则与每月预算比较，估算的每日预算不太准确。

![每日视图](./media/quick-acm-cost-analysis/daily-view.png)

可通过“分组依据”选择分组类别，从而更改顶部“总计”面积图中显示的数据。 通过分组，可以快速查看支出是如何按资源类型进行分类的。 下面是 Azure 服务成本的上月视图。

![分组的每日汇总视图](./media/quick-acm-cost-analysis/grouped-daily-accum-view.png)

顶部“总计”视图下的透视图显示不同分组和筛选类别的视图。 选择任一组类别后，“总计”视图的完整数据集位于视图的底部。 下面是一个资源组的示例。

![当前视图的完整数据](./media/quick-acm-cost-analysis/full-data-set.png)

上图显示了资源组名称。 资源的查看标记不适用于任何成本分析视图、筛选或分组。

## <a name="download-cost-analysis-data"></a>下载成本分析数据

可以从“成本分析”下载信息，为 Azure 门户中当前显示的所有数据生成一个 CSV 文件。 应用的任何筛选或分组均包含在文件中。 顶部“总计”视图中灰显的基础数据也会包含在 CSV 文件中。

## <a name="next-steps"></a>后续步骤

转到第一个教程，了解如何创建并管理预算。

> [!div class="nextstepaction"]
> [创建并管理预算](tutorial-acm-create-budgets.md)
