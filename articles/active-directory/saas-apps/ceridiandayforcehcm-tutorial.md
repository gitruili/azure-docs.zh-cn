---
title: 教程：Azure Active Directory 与 Ceridian Dayforce HCM 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 Ceridian Dayforce HCM 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 47ed72667b46edb06a7d07cbc971810cb97e6f90
ms.sourcegitcommit: 16ddc345abd6e10a7a3714f12780958f60d339b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36211605"
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a>教程：Azure Active Directory 与 Ceridian Dayforce HCM 集成

本教程介绍如何将 Ceridian Dayforce HCM 与 Azure Active Directory (Azure AD) 集成。

将 Ceridian Dayforce HCM 与 Azure AD 集成具有以下优势：

- 可在 Azure AD 中控制谁有权访问 Ceridian Dayforce HCM。
- 可以让用户使用其 Azure AD 帐户自动登录到 Ceridian Dayforce HCM（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Ceridian Dayforce HCM 的集成，需要具有以下项：

- Azure AD 订阅
- 已启用 Ceridian Dayforce HCM 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Ceridian Dayforce HCM
2. 配置和测试 Azure AD 单一登录

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a>从库中添加 Ceridian Dayforce HCM
要配置 Ceridian Dayforce HCM 与 Azure AD 的集成，需要从库中将 Ceridian Dayforce HCM 添加到托管 SaaS 应用列表。

**若要从库中添加 Ceridian Dayforce HCM，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]
    
3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

4. 在搜索框中，键入 **Ceridian Dayforce HCM**，从结果面板中选择“Ceridian Dayforce HCM”，然后单击“添加”按钮添加该应用程序。

    ![结果列表中的 Ceridian Dayforce HCM](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，基于一个名为“Britta Simon”的测试用户配置和测试 Ceridian Dayforce HCM 的 Azure AD 单一登录。

为使单一登录能正常工作，Azure AD 需要知道与 Azure AD 用户相对应的 Ceridian Dayforce HCM 用户。 换句话说，需要建立 Azure AD 用户与 Ceridian Dayforce HCM 中相关用户之间的关联关系。

可通过将 Azure AD 中“用户名”的值指定为 Ceridian Dayforce HCM 中“用户名”的值来建立此关联关系。

若要配置和测试 Ceridian Dayforce HCM 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. **[创建 Ceridian Dayforce HCM 测试用户](#create-a-ceridian-dayforce-hcm-test-user)** - 在 Ceridian Dayforce HCM 中创建 Britta Simon 的对应用户，并将其链接到该用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Ceridian Dayforce HCM 应用程序中配置单一登录。

**若要配置 Ceridian Dayforce HCM 的 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户的 **Ceridian Dayforce HCM** 应用程序集成页中，单击“单一登录”。

    ![配置单一登录链接][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![“单一登录”对话框](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. 在“Ceridian Dayforce HCM 域和 URL”部分中，执行以下步骤：

    ![配置单一登录](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    a. 在“登录 URL”文本框中，键入用户用于登录 Ceridian Dayforce HCM 应用程序的 URL。
    
    | 环境 | 代码 |
    | :-- | :-- |
    | 生产 | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | 测试 | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    b. 在“标识符”文本框中，使用以下模式键入 URL：
    
    | 环境 | 代码 |
    | :-- | :-- |
    | 生产 | `https://ncpingfederate.dayforcehcm.com/sp` |
    | 测试 | `https://fs-test.dayforcehcm.com/sp` |
    
    c. 在“回复 URL”文本框中，键入 Azure AD 用来发布响应的 URL。
    
    | 环境 | 代码 |
    | :-- | :-- |
    | 生产 | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | 测试 | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > 这些不是实际值。 请使用实际的“标识符”、“回复 URL”和“登录 URL”更新这些值。 请联系 [Ceridian Dayforce HCM 客户端支持团队](https://www.ceridian.com/contact-us/index.html)获取这些值。

4. 在“SAML 签名证书”部分中，单击“元数据 XML”，并在计算机上保存元数据文件。

    ![证书下载链接](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. Ceridian Dayforce HCM 应用程序需要采用特定格式的 SAML 断言。 先联系 [Ceridian Dayforce HCM 支持团队](https://www.ceridian.com/contact-us/index.html)，确定正确的用户标识符。 Microsoft 建议将“name”属性用作用户标识符。 可以在应用程序集成页的“用户属性”部分管理这些属性的值。 以下屏幕截图显示一个示例。  

    ![配置单一登录](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. 在“单一登录”对话框的“用户属性”部分中，按上图所示配置 SAML 令牌属性，并执行以下步骤：
    
    | 属性名称  | 属性值 |
    | --------------- | -------------------- |    
    | 名称  | user.extensionattribute2 |    

    a. 单击“添加属性”，打开“添加属性”对话框。

    ![配置单一登录](./media/ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![配置单一登录](./media/ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    b. 在“名称”文本框中，键入为该行显示的属性名称。

    c. 在“值”列表中，选择要用于实现的用户属性。
    例如，如果想要使用 EmployeeID 作为唯一用户标识符并且已在 ExtensionAttribute2 中存储属性值，则选择“user.extensionattribute2”。
    
    d. 单击“确定” 。

7. 单击“保存”按钮。

    ![配置单一登录“保存”按钮](./media/ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. 在“Ceridian Dayforce HCM 配置”部分中，单击“配置 Ceridian Dayforce HCM”打开“配置登录”窗口。 从“快速参考”部分中复制“注销 URL”、“SAML 实体 ID”和“SAML 单一登录服务 URL”。

    ![Ceridian Dayforce HCM 配置](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. 若要在 **Ceridian Dayforce HCM** 端配置单一登录，需要将下载的**元数据 XML**、**注销 URL、SAML 实体 ID 和 SAML 单一登录服务 URL** 发送给 [Ceridian Dayforce HCM 支持团队](https://www.ceridian.com/contact-us/index.html)。

> [!TIP]
> 之后在设置应用时，就可以在 [Azure 门户](https://portal.azure.com)中阅读这些说明的简明版本了！  从“Active Directory”>“企业应用程序”部分添加此应用后，只需单击“单一登录”选项卡，即可通过底部的“配置”部分访问嵌入式文档。 可在此处阅读有关嵌入式文档功能的详细信息：[ Azure AD 嵌入式文档]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

   ![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。

    ![“用户和组”以及“所有用户”链接](./media/ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。

    ![“添加”按钮](./media/ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. 在“用户”对话框中，执行以下步骤：

    ![“用户”对话框](./media/ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    a. 在“姓名”框中，键入“BrittaSimon”。

    b. 在“用户名”框中，键入用户 Britta Simon 的电子邮件地址。

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a>创建 Ceridian Dayforce HCM 测试用户

本部分的目的是在 Ceridian Dayforce HCM 中创建名为 Britta Simon 的用户。 请联系 [Ceridian Dayforce HCM 支持团队](https://www.ceridian.com/contact-us/index.html)，将用户添加到 Ceridian Dayforce HCM 应用程序中。 

### <a name="assigning-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Ceridian Dayforce HCM 的权限，允许她使用 Azure 单一登录。

![分配用户][200] 

**要将 Britta Simon 分配到 Ceridian Dayforce HCM，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

2. 在应用程序列表中，选择“Ceridian Dayforce HCM”。

    ![配置单一登录](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. 在左侧菜单中，单击“用户和组”。

    ![分配用户][202] 

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![分配用户][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Ceridian Dayforce HCM 的权限，允许她使用 Azure 单一登录。

![分配用户角色][200] 

**要将 Britta Simon 分配到 Ceridian Dayforce HCM，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

2. 在应用程序列表中，选择“Ceridian Dayforce HCM”。

    ![应用程序列表中的 Ceridian Dayforce HCM 链接](./media/ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202]

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="test-single-sign-on"></a>测试单一登录

本部分旨在使用“访问面板”测试 Azure AD 单一登录配置。  
当在访问面板中单击 Ceridian Dayforce HCM 磁贴时，应当会自动登录到 Ceridian Dayforce HCM 应用程序。 

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/ceridiandayforcehcm-tutorial/tutorial_general_203.png
