---
title: 配置 Azure 机器学习的开发环境 | Microsoft 文档
description: 了解在使用 Azure 机器学习服务时如何配置开发环境。 本文档将学习如何使用 Conda 环境、创建配置文件和配置 Jupyter Notebooks、Azure Notebooks、IDE、代码编辑器和数据科学虚拟机。
services: machine-learning
author: rastala
ms.author: roastala
ms.service: machine-learning
ms.reviewer: larryfr
manager: cgronlun
ms.topic: conceptual
ms.date: 8/6/2018
ms.openlocfilehash: 7796accffb7041e567c5e18857d09e105b5268ce
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46961563"
---
# <a name="how-to-configure-a-development-environment-for-the-azure-machine-learning-service"></a>如何配置 Azure 机器学习服务的开发环境

了解如何使用 Azure 机器学习服务来配置开发环境。 你将了解如何创建将环境与 Azure 机器学习工作区相关联的配置文件。 另外，还将学习如何配置以下开发环境：

* 在你自己的计算机上的 Jupyter Notebooks
* Visual Studio Code
* 所选的代码编辑器

建议的方法是使用 Continuum Anaconda [conda 虚拟环境](https://conda.io/docs/user-guide/tasks/manage-environments.html)将工作环境隔离，以避免包之间的依赖项冲突。 本文介绍设置 conda 环境和将其用于 Azure 机器学习的步骤。


## <a name="prerequisites"></a>先决条件

* Azure 机器学习服务工作区。 要创建一个工作区，请使用[开始使用 Azure 机器学习服务](quickstart-get-started.md)文档中的步骤。

* [Continuum Anaconda](https://www.anaconda.com/download/) 或 [Miniconda](https://conda.io/miniconda.html) 包管理器。

 * 对于 Visual Studio Code 环境，[Python 扩展](https://code.visualstudio.com/docs/python/python-tutorial)。

## <a name="create-workspace-configuration-file"></a>创建工作区配置文件

工作区配置文件由 SDK 用于与 Azure 机器学习服务工作区通信。  可通过两种方式获取此文件：

* 完成[快速入门](quickstart-get-started.md)后，将为你在 Azure Notebooks 中创建 `config.json` 文件。  此文件含包含工作区的配置信息。  将其下载到与引用它的脚本或笔记本所在目录相同的目录中。

* 使用以下步骤自行创建配置文件：

    1. 在 [Azure 门户](https://portal.azure.com)中打开你的工作区。 复制“工作区名称”、“资源组”和“订阅 ID”。 这些值用于创建配置文件。

       门户的工作区仪表板仅在 Edge、Chrome 和 Firefox 浏览器上受支持。
    
        ![Azure 门户](./media/how-to-configure-environment/configure.png) 
    
    3. 在文本编辑器中，创建一个名为 config.json 的文件。  将以下内容添加到该文件，从门户中插入你的值：
    
        ```json
        {
        "subscription_id": "<subscription-id>",
        "resource_group": "<resource-group>",
        "workspace_name": "<workspace-name>"
        }
        ```
    
        >[!NOTE] 
        >稍后在代码中，你将读取含有 `ws = Workspace.from_config()` 的此文件
    
    4. 请确保将 config.json 保存到与引用它的脚本或笔记本相同的目录中。
    
## <a name="azure-notebooks-and-data-science-virtual-machine"></a>Azure Notebooks 和 Data Science Virtual Machine

对 Azure Notebooks 和 Azure Data Science Virtual Machine (DSVM) 进行了预配，以使用 Azure 机器学习服务。 在这些环境上预安装了所需的组件（如 Azure 机器学习 SDK）。

Azure Notebooks 是 Azure 云中的 Jupyter Notebook 服务。 Data Science Virtual Machine 是为数据科学工作预配置的 VM 映象。 VM 包括常用的工具、IDE 和包（如 Jupyter Notebooks、PyCharm 和 Tensorflow）。

你仍然需要工作区配置文件才能使用这些环境。

有关 Data Science Virtual Machine 的详细信息，请参阅 [Data Science Virtual Machine](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) 文档。

有关将 Azure Notebooks 与 Azure 机器学习服务结合使用的示例，请参阅[开始使用 Azure 机器学习服务](quickstart-get-started.md)文档。

## <a name="configure-jupyter-notebooks-on-your-own-computer"></a>在你自己的计算机上配置 Jupyter Notebooks

1. 打开命令提示符或 shell。

2. 若要创建 conda 环境，请使用以下命令：

    ```shell
    # create a new conda environment with Python 3.6, numpy and cython
    conda create -n myenv Python=3.6 cython numpy

    # activate the conda environment
    conda activate myenv

    # If you are running Mac OS you should run
    source activate myenv
    ```

    创建环境可能需要几分钟的时间才能完成，因为可能需要下载 Python 3.6 和其他组件。

3. 若要使用笔记本额外项安装 Azure 机器学习 SDK，请使用以下命令：

     ```shell
    pip install --upgrade azureml-sdk[notebooks,automl,contrib]
    ```

    安装 SDK 可能耗时几分钟。

4. 若要安装机器学习试验包，请使用以下命令，并将 `<new package>` 替换为你想要安装的包：

    ```shell
    conda install <new package>
    ```

5. 若要安装可感知 conda 的 Jupyter Notebooks 服务器并启用试验小组件（查看运行信息），请使用以下命令：

    ```shell
    # install Jupyter 
    conda install nb_conda

    # install experiment widget
    jupyter nbextension install --py --user azureml.train.widgets

    # enable experiment widget
    jupyter nbextension enable --py --user azureml.train.widgets
    ```

6. 若要启动 Jupyter Notebooks，请使用以下命令：

    ```shell
    jupyter notebook
    ```

7. 打开新的笔记本，然后选择“myenv”作为你的内核。 然后，通过在笔记本单元中运行以下命令来验证你已安装 Azure 机器学习 SDK：

    ```python
    import azureml.core
    azureml.core.VERSION
    ```

## <a name="configure-visual-studio-code"></a>配置 Visual Studio Code

1. 打开命令提示符或 shell。

2. 若要创建 conda 环境，请使用以下命令：

    ```shell
    # create a new conda environment with Python 3.6, numpy and cython
    conda create -n myenv Python=3.6 cython numpy

    # activate the conda environment
    conda activate myenv

    # If you are running Mac OS you should run
    source activate myenv
    ```

2. 若要安装 Azure 机器学习 SDK，请使用以下命令：
 
    ```shell
    pip install --upgrade azureml-sdk[automl,contrib]
    ```

4. 若要安装用于 AI 的 Visual Studio 代码工具，请参阅[用于 AI 的工具](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.vscode-ai)的 Visual Studio 市场条目。 

5. 若要安装机器学习试验包，请使用以下命令，并将 `<new package>` 替换为你想要安装的包：

    ```shell
    conda install <new package>
    ```

6. 启动 Visual Studio Code，然后使用 CTRL-SHIFT-P 来获取“命令面板”。 输入“Python: Select Interpreter”，然后选择你创建的 conda 环境。

    > [!NOTE]
    > Visual Studio Code 能够自动感知你的计算机上的 conda 环境。 有关详细信息，请参阅 [Visual Studio 代码文档](https://code.visualstudio.com/docs/python/environments#_conda-environments)。

7. 若要验证配置，请使用 Visual Studio Code 创建含有以下代码的新 Python 脚本文件，然后运行该文件：

    ```python
    import azureml.core
    azureml.core.VERSION
    ```

## <a name="configure-code-editor-of-your-choice"></a>配置所选的代码编辑器

若要将自定义代码编辑器与 Azure 机器学习 SDK 结合使用，请如上文中所述先创建 conda 环境。 然后，按照每个编辑器的说明操作，以使用 conda 环境。 例如，PyCharm 的说明位于 [https://www.jetbrains.com/help/pycharm/2018.2/conda-support-creating-conda-virtual-environment.html](https://www.jetbrains.com/help/pycharm/2018.2/conda-support-creating-conda-virtual-environment.html)。
 
## <a name="next-steps"></a>后续步骤

* [使用 MNIST 数据集对 Azure 机器学习的模型进行定型](tutorial-train-models-with-aml.md)
