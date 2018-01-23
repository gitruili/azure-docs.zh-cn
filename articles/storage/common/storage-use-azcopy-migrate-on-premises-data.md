---
title: "使用 AzCopy 将本地数据迁移到 Azure 存储 | Microsoft 文档"
description: "使用 AzCopy 将数据迁移或复制到 blob、表和文件内容或从其中迁移或复制出数据。 轻松将本地存储中的数据迁移到 Azure 存储中。"
services: storage
author: ruthogunnnaike
manager: jeconnoc
ms.service: storage
ms.tgt_pltfrm: na
ms.devlang: azcopy
ms.topic: tutorial
ms.date: 12/14/2017
ms.author: v-ruogun
ms.openlocfilehash: 3dbfb935ac0b134e127a5dccb7bc76716c688e8a
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
#  <a name="migrate-on-premises-data-to-cloud-storage-by-using-azcopy"></a>使用 AzCopy 将本地数据迁移到云存储

AzCopy 是一个命令行工具，借助该工具，可使用简单命令将数据复制到 Azure Blob 存储、Azure 文件和 Azure 表存储或从其中复制出数据。 这些命令旨在实现最佳性能。 可在文件系统和存储帐户之间或在存储帐户之间复制数据。  

有两种版本的 AzCopy 可供下载：

* [AzCopy on Linux](storage-use-azcopy.md) 使用 .NET 核心 Framework 生成。 它面向 Linux 平台，提供 POSIX 样式命令行选项。 
* [AzCopy on Windows](../storage-use-azcopy.md) 使用 .NET Framework 生成。 它提供 Windows 样式命令行选项。 
 
本教程介绍如何执行下列操作：

> [!div class="checklist"]
> * 创建存储帐户。 
> * 使用 AzCopy 上传所有数据。
> * 修改用于测试目的的数据。
> * 创建一个计划任务或 cron 作业，以标识要上传的新文件。

## <a name="prerequisites"></a>系统必备

要完成本教程，请下载最新版本的 AzCopy on [Linux](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux#download-and-install-azcopy) 或 AzCopy on [Windows](http://aka.ms/downloadazcopy)。 

[!INCLUDE [storage-quickstart-tutorial-create-account-portal](../../../includes/storage-quickstart-tutorial-create-account-portal.md)]

>[!NOTE]
>如果希望能够将 blob 从辅助区域下载到本地存储或反向操作，可将“复制”设置为“读取-访问-异地冗余存储”。 选择此选项会创建一个[异地冗余存储](https://docs.microsoft.com/azure/storage/common/storage-redundancy#geo-redundant-storage)帐户。 
>
>

## <a name="create-a-container"></a>创建容器

始终将 Blob 上传到容器中。 可使用容器整理 blob 组，就像在计算机的文件夹中整理文件一样。 

按照这些步骤创建容器：

1. 选择主页上的“存储帐户”按钮，然后选择创建的存储帐户。
2. 选择“服务”下的“Blob”，然后选择“容器”。 

   ![创建容器](media/storage-azcopy-migrate-on-premises-data/CreateContainer.png)
 
容器名必须以字母或数字开头。 名称中只能包含字母、数字和连字符 (-)。 有关命名 Blob 和容器的更多规则，请参阅[命名和引用容器、Blob 和元数据](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)。

## <a name="upload-all-files-in-a-folder-to-blob-storage"></a>将文件夹中的所有文件上传到 Blob 存储

可使用 AzCopy 将文件夹中的所有文件上传到 [Windows](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy#upload-blobs-to-blob-storage) 或 [Linux](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux#blob-download) 上的 Blob 存储中。 若要上传文件夹中的所有 Blob，请输入以下 AzCopy 命令：

# <a name="linuxtablinux"></a>[Linux](#tab/linux)
    azcopy \
        --source /mnt/myfolder \
        --destination https://myaccount.blob.core.windows.net/mycontainer \
        --dest-key <key> \
        --recursive

# <a name="windowstabwindows"></a>[Windows](#tab/windows)
    AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey: key /S
---

将 `<key>` 和 `key` 替换为帐户密钥。 在 Azure 门户中，可通过选择存储帐户中“设置”下的“访问密钥”来检索账户密钥。 选择一个密钥，将其粘贴到 AzCopy 命令中。 如果指定的目标容器不存在，AzCopy 将创建它并将文件上传到其中。 将源路径更新为数据目录，并将目标 URL 中的 myaccount 替换为存储帐户名称。

若要将指定目录的内容以递归方式上传到 Blob 存储，请指定 `--recursive` (Linux) 或 `/S` (Windows) 选项。 当使用这些选项之一运行 AzCopy 时，会同时上传所有子文件夹及其中文件。

## <a name="upload-modified-files-to-blob-storage"></a>将修改的文件上传到 Blob 存储
可基于文件的上次修改时间，使用 AzCopy [上传文件](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy#other-azcopy-features)。 若要尝试此操作，可在源目录中修改文件或创建新文件，用于测试目的。 如果仅上传更新的或新文件，请将 `--exclude-older` (Linux) 或 `/XO` (Windows) 参数添加到 AzCopy 命令。

如果只想复制目标中不存在的源资源，在 AzCopy 命令中同时指定 `--exclude-older` 和 `--exclude-newer` (Linux) 或 `/XO` 和 `/XN` (Windows) 参数。 AzCopy 仅上传更新的数据（基于时间戳）。
 
# <a name="linuxtablinux"></a>[Linux](#tab/linux)
    azcopy \
    --source /mnt/myfolder \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive \
    --exclude-older

# <a name="windowstabwindows"></a>[Windows](#tab/windows)
    AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey: key /S /XO
---

## <a name="create-a-scheduled-task-or-cron-job"></a>创建计划任务或 cron 作业 
可创建用于运行 AzCopy 命令脚本的计划任务或 cron 作业。 此脚本标识新的本地数据，并按特定时间间隔将其上传到云存储。 

将 AzCopy 命令复制到文本编辑器。 将 AzCopy 命令的参数值更新为合适的值。 将文件另存为适用于 AzCopy 的 `script.sh` (Linux) 或 `script.bat` (Windows)。 

# <a name="linuxtablinux"></a>[Linux](#tab/linux)
    azcopy --source /mnt/myfiles --destination https://myaccount.blob.core.windows.net/mycontainer --dest-key <key> --recursive --exclude-older --exclude-newer --verbose >> Path/to/logfolder/`date +\%Y\%m\%d\%H\%M\%S`-cron.log

# <a name="windowstabwindows"></a>[Windows](#tab/windows)
    cd C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy
    AzCopy /Source: C:\myfolder  /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey: key /V /XO /XN >C:\Path\to\logfolder\azcopy%date:~-4,4%%date:~-7,2%%date:~-10,2%%time:~-11,2%%time:~-8,2%%time:~-5,2%.log
---

使用详细 `--verbose` (Linux) 或 `/V` (Windows) 选项运行 AzCopy。 输出会重定向到日志文件。 

在本教程中，[Schtasks](https://msdn.microsoft.com/library/windows/desktop/bb736357(v=vs.85).aspx) 用于在 Windows 上创建计划任务。 [Crontab](http://crontab.org/) 命令用于在 Linux 上创建 cron 作业。 
 使用 Schtasks，管理员能够在本地或远程计算机上创建、删除、查询、更改、运行和结束计划的任务。 使用 Cron，Linux 和 Unix 用户能够使用 [cron 表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression)在指定日期和时间运行命令或脚本。


# <a name="linuxtablinux"></a>[Linux](#tab/linux)
若要在 Linux 上创建 cron 作业，请在终端上输入以下命令： 

```bash
crontab -e 
*/5 * * * * sh /path/to/script.sh 
```

在命令中指定 cron 表达式 `*/5 * * * * ` 可指示 shell 脚本 `script.sh` 应每隔五分钟运行一次。 可计划让脚本在每日、每月或每年的特定时间运行。 若要了解有关设置作业执行日期和时间的详细信息，请参阅 [cron 表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression)。 

# <a name="windowstabwindows"></a>[Windows](#tab/windows)
若要在 Windows 上创建计划任务，请在命令提示符下或在 PowerShell 中输入以下命令：

```cmd 
schtasks /CREATE /SC minute /MO 5 /TN "AzCopy Script" /TR C:\Users\username\Documents\script.bat
```

命令使用：
- `/SC` 参数指定分钟计划。
- `/MO` 参数指定五分钟的间隔。
- `/TN` 参数指定任务名称。
- `/TR` 参数指定 `script.bat` 文件的路径。 

若要了解有关在 Windows 上创建计划的任务的详细信息，请参阅 [Schtasks](https://technet.microsoft.com/library/cc772785(v=ws.10).aspx#BKMK_minutes)。

---
 
若要验证计划的任务或 cron 作业运行正常，在 `myfolder` 目录中创建新文件。 等待五分钟以确认已将新文件上传到存储帐户。 转到日志目录，以查看计划任务或 cron 作业的输出日志。 

若要详细了解如何在本地和 Azure 存储之间移动数据，请参阅[将数据移到 Azure 存储及从其中移出数据](https://docs.microsoft.com/azure/storage/common/storage-moving-data?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。  

## <a name="next-steps"></a>后续步骤
有关 Azure 存储和 AzCopy 的详细信息，请参阅以下资源：

* [Azure 存储简介](../storage-introduction.md)
* [使用 AzCopy on Windows 传输数据](storage-use-azcopy.md) 
* [使用 AzCopy on Linux 传输数据](storage-use-azcopy-linux.md) 
* [创建存储帐户](../storage-create-storage-account.md)
* [使用存储资源管理器管理 Blob](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs)  






 
 
