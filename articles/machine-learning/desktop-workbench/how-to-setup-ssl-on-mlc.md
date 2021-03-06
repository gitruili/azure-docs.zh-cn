---
title: 在 Azure 机器学习计算 (MLC) 群集上启用 SSL | Microsoft Docs
description: 获取有关在 Azure 机器学习计算 (MLC) 群集上针对评分调用设置 SSL 的说明
services: machine-learning
author: SerinaKaye
ms.author: serinak
manager: hjerez
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 01/24/2018
ms.openlocfilehash: 982a6807ccaf393c3aea42f39f7e60bb7e0d3ac3
ms.sourcegitcommit: e8f443ac09eaa6ef1d56a60cd6ac7d351d9271b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2018
ms.locfileid: "35631860"
---
# <a name="enable-ssl-on-an-azure-machine-learning-compute-mlc-cluster"></a>在 Azure 机器学习计算 (MLC) 群集上启用 SSL 

这些说明可帮助你在机器学习计算 (MLC) 群集上针对评分调用设置 SSL。 

## <a name="prerequisites"></a>先决条件 

1. 选定在进行实时评分调用时要使用的 CNAME（DNS 名称）。

2. 使用该 CNAME 创建*无密码*证书。

3. 如果证书尚不是 PEM 格式，请使用 *openssl* 等工具将其转换为 PEM。

完成先决条件后，将获得两个文件：

* 一个证书文件，例如 `cert.pem`。 请确保该文件包含完整的证书链。
* 一个密钥文件，例如 `key.pem`



## <a name="set-up-an-ssl-certificate-on-a-new-acs-cluster"></a>在新的 ACS 群集上设置 SSL 证书

使用 Azure 机器学习 CLI，运行带 `-c` 开关的以下命令创建附加了 SSL 证书的 ACS 群集：

```
az ml env create -c -g <resource group name> -n <cluster name> --cert-cname <CNAME> --cert-pem <path to cert.pem file> --key-pem <path to key.pem file>
```


## <a name="set-up-an-ssl-certificate-on-an-existing-acs-cluster"></a>在现有 ACS 群集上设置 SSL 证书

如果针对的是未使用 SSL 的情况下创建的群集，则可以使用 Azure PowerShell cmdlet 添加证书。

需要提供密钥和原始 PEM 格式的证书。 可以将密钥和证书读取到 PowerShell 变量：

```
$keyValueInPemFormat = [IO.File]::ReadAllText('<path to key.pem file>')
$certValueInPemFormat = [IO.File]::ReadAllText('<path to cert.pem file>')
```
将证书添加到群集： 

```
Set-AzureRmMlOpCluster -ResourceGroupName my-rg -Name my-cluster -SslStatus Enabled -SslCertificate $certValueInPemFormat -SslKey $keyValueInPemFormat -SslCName foo.mycompany.com
```

## <a name="map-the-cname-and-the-ip-address"></a>映射 CNAME 和 IP 地址

在先决条件中选择的 CNAME 和实时前端 (FE) 的 IP 地址之间创建映射。 若要发现 FE 的 IP 地址，请运行以下命令。 输出会显示一个名为“publicIpAddress”的字段，其中包含实时群集前端的 IP 地址。 请参阅 DNS 提供程序的说明，从 CNAME 中使用的 FQDN 到公共 IP 地址建立一条记录。



## <a name="auto-detection-of-a-certificate"></a>自动检测证书 

使用“`az ml service create realtime`”命令创建实时 Web 服务时，Azure 机器学习会自动检测群集上设置的 SSL，并使用指定的证书自动设置评分 URL。 

若要查看证书状态，请运行以下命令。 请注意评分 URI 的“https”前缀和主机名中的 CNAME。 

``` 
az ml service show realtime -n <service name>
{
                "id" : "<your service id>",
                "name" : "<your service name >",
                "state" : "Succeeded",
                "createdAt" : "<datetime>”,
                "updatedAt" : "< datetime>",
                "scoringUri" : "https://<your CNAME>/api/v1/service/<service name>/score"
}
```
