---
title: 将 Power BI Desktop 文件导入到 Azure Analysis Services 中 | Microsoft Docs
description: 介绍了如何使用 Azure 门户导入 Power BI Desktop 文件 (pbix)。
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 08/16/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: a2855ca5dbb76d3fcc30c4b1007c20bb48c91c9b
ms.sourcegitcommit: f057c10ae4f26a768e97f2cb3f3faca9ed23ff1b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2018
ms.locfileid: "42141448"
---
# <a name="import-a-power-bi-desktop-file"></a>导入 Power BI Desktop 文件

可以将 Power BI Desktop 文件 (pbix) 中的数据模型导入到 Azure Analysis Services 中。 将导入模型元数据、缓存的数据以及数据源连接。 不会导入报表和可视化效果。 从 Power BI Desktop 中导入的数据模型的兼容级别为 1400。

**限制**   

- 从 pbix 文件中进行导入使用门户中的 Web 设计器功能，该功能处于**预览版**。 功能较为有限。 对于更高级的模型开发和测试，最好使用 Visual Studio (SSDT) 和 SQL Server Management Studio (SSMS)。
- 必须具有服务器管理员权限才能从 pbix 文件中进行导入。
- pbix 模型只能连接到“Azure SQL 数据库”和“Azure SQL 数据仓库”数据源。
- pbix 模型不能具有实时连接或 DirectQuery 连接。 
- 如果 pbix 数据模型包含 Analysis Services 不支持的元数据，导入可能会失败。


## <a name="to-import-from-pbix"></a>从 pbix 中导入

1. 在服务器的“概述” > “Web 设计器”中，单击“打开”。

    ![在 Azure 门户中创建模型](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. 在“Web 设计器” > “模型”中，单击“+ 添加”。

    ![在 Azure 门户中创建模型](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. 在“新建模型”中，键入模型名称，然后选择 Power BI Desktop 文件。

    ![Azure 门户中的“新建模型”对话框](./media/analysis-services-import-pbix/aas-import-pbix-new-model.png)

4. 在“导入”中，找到并选择你的文件。

     ![Azure 门户中的“连接”对话框](./media/analysis-services-import-pbix/aas-import-pbix-select-file.png)

## <a name="change-credentials"></a>更改凭据

从 pbix 文件中导入数据模型时，默认情况下，用来连接数据源的凭据设置为 ServiceAccount。 从 pbix 中导入模型后，可以使用以下方法来更改凭据：

- 使用 2018 年 7 月版（版本 17.8.1）或更高版本的 SSMS 来编辑凭据。 这是最简单的方法。
- 对 [DataSources 对象](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl)使用 TMSL [Alter 命令](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl)来修改连接字符串属性。 
- 在 Visual Studio 中打开模型，编辑数据源连接的凭据，然后重新部署该模型。

使用 SSMS 更改凭据 

1. 在 SSMS 中，展开数据库 >“连接”。 
2. 右键单击数据库连接，然后单击“刷新凭据”。 

    ![刷新凭据](./media/analysis-services-import-pbix/aas-import-pbix-creds.png)

3. 在凭据对话框中，选择凭据类型，然后输入凭据。 对于 SQL 身份验证，请选择“数据库”。 对于组织帐户 (OAuth)，请选择“Microsoft 帐户”。
    ![编辑凭据](./media/analysis-services-import-pbix/aas-import-pbix-edit-creds.png)

2018 年 7 月版的 Power BI Desktop 包括了用于更改数据源权限的一项新功能。 在“主页”选项卡上，单击“编辑查询”  > “数据源设置”。 选择数据源连接，然后单击“编辑权限”。


## <a name="see-also"></a>另请参阅

[在 Azure 门户中创建模型](analysis-services-create-model-portal.md)   
[连接到 Azure Analysis Services](analysis-services-connect.md)  
