---
title: 快速入门：提取手写文本 - SDK、C# - 计算机视觉
titleSuffix: Azure Cognitive Services
description: 本快速入门将在认知服务中使用计算机视觉 Windows C# 客户端库从图像中提取手写文本。
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: computer-vision
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: v-deken
ms.openlocfilehash: 14778c6b51fa0c68ffeec41dc282de8e1bb246b0
ms.sourcegitcommit: 3d0295a939c07bf9f0b38ebd37ac8461af8d461f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43840948"
---
# <a name="quickstart-extract-handwritten-text---sdk-c35---computer-vision"></a>快速入门：提取手写文本 - SDK、C&#35; - 计算机视觉

本快速入门将使用计算机视觉 Windows 客户端库从图像中提取手写文本。

## <a name="prerequisites"></a>先决条件

* 若要使用计算机视觉，需要订阅密钥；请参阅[获取订阅密钥](../Vision-API-How-to-Topics/HowToSubscribe.md)。
* 任何版本的 [Visual Studio 2015 或 2017](https://www.visualstudio.com/downloads/)。
* [Microsoft.Azure.CognitiveServices.Vision.ComputerVision](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.ComputerVision) 客户端库 NuGet 包。 不需下载程序包。 下面提供了安装说明。

## <a name="recognizetextasync-method"></a>RecognizeTextAsync 方法

`RecognizeTextAsync` 和 `RecognizeTextInStreamAsync` 方法分别为远程图像和本地图像包装[识别文本 API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200)。 `GetTextOperationResultAsync` 方法包装[获取识别文本操作结果 API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2cf1154055056008f201)。  可以使用这些方法检测图像中的手写文本，并将识别的字符提取到可供计算机使用的字符流中。

若要运行此示例，请执行以下步骤：

1. 在 Visual Studio 中创建新的 Visual C# 控制台应用。
1. 安装计算机视觉客户端库 NuGet 包。
    1. 在菜单上，单击“工具”，然后依次选择“NuGet 包管理器”、“管理解决方案的 NuGet 包”。
    1. 单击“浏览”选项卡，在“搜索”框中键入“Microsoft.Azure.CognitiveServices.Vision.ComputerVision”。
    1. 选择显示的 **Microsoft.Azure.CognitiveServices.Vision.ComputerVision**，单击项目名称旁边的复选框，然后单击“安装”。
1. 将 `Program.cs` 替换为以下代码。
1. 将 `<Subscription Key>` 替换为有效订阅密钥。
1. 如有必要，请将 `computerVision.AzureRegion = AzureRegions.Westcentralus` 更改为获得订阅密钥的位置。
1. 将 `<LocalImage>` 替换为本地图像的路径和文件名。
1. （可选）将 `remoteImageUrl` 设置为另一图像。
1. 运行该程序。

```csharp
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision;
using Microsoft.Azure.CognitiveServices.Vision.ComputerVision.Models;

using System;
using System.IO;
using System.Threading.Tasks;

namespace ImageHandText
{
    class Program
    {
        // subscriptionKey = "0123456789abcdef0123456789ABCDEF"
        private const string subscriptionKey = "<SubscriptionKey>";

        // localImagePath = @"C:\Documents\LocalImage.jpg"
        private const string localImagePath = @"<LocalImage>";

        private const string remoteImageUrl =
            "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/" +
            "Cursive_Writing_on_Notebook_paper.jpg/" +
            "800px-Cursive_Writing_on_Notebook_paper.jpg";

        private const int numberOfCharsInOperationId = 36;

        static void Main(string[] args)
        {
            ComputerVisionAPI computerVision = new ComputerVisionAPI(
                new ApiKeyServiceClientCredentials(subscriptionKey),
                new System.Net.Http.DelegatingHandler[] { });

            // You must use the same region as you used to get your subscription
            // keys. For example, if you got your subscription keys from westus,
            // replace "Westcentralus" with "Westus".
            //
            // Free trial subscription keys are generated in the westcentralus
            // region. If you use a free trial subscription key, you shouldn't
            // need to change the region.

            // Specify the Azure region
            computerVision.AzureRegion = AzureRegions.Westcentralus;

            Console.WriteLine("Images being analyzed ...");
            var t1 = ExtractRemoteHandTextAsync(computerVision, remoteImageUrl);
            var t2 = ExtractLocalHandTextAsync(computerVision, localImagePath);

            Task.WhenAll(t1, t2).Wait(5000);
            Console.WriteLine("Press any key to exit");
            Console.ReadLine();
        }

        // Recognize text from a remote image
        private static async Task ExtractRemoteHandTextAsync(
            ComputerVisionAPI computerVision, string imageUrl)
        {
            if (!Uri.IsWellFormedUriString(imageUrl, UriKind.Absolute))
            {
                Console.WriteLine(
                    "\nInvalid remoteImageUrl:\n{0} \n", imageUrl);
                return;
            }

            // Start the async process to recognize the text
            RecognizeTextHeaders textHeaders = await computerVision.RecognizeTextAsync(
                    imageUrl, TextRecognitionMode.Handwritten);

            await GetTextAsync(computerVision, textHeaders.OperationLocation);
        }

        // Recognize text from a local image
        private static async Task ExtractLocalHandTextAsync(
            ComputerVisionAPI computerVision, string imagePath)
        {
            if (!File.Exists(imagePath))
            {
                Console.WriteLine(
                    "\nUnable to open or read localImagePath:\n{0} \n", imagePath);
                return;
            }

            using (Stream imageStream = File.OpenRead(imagePath))
            {
                // Start the async process to recognize the text
                RecognizeTextInStreamHeaders textHeaders =
                    await computerVision.RecognizeTextInStreamAsync(
                        imageStream, TextRecognitionMode.Handwritten);

                await GetTextAsync(computerVision, textHeaders.OperationLocation);
            }
        }

        // Retrieve the recognized text
        private static async Task GetTextAsync(
            ComputerVisionAPI computerVision, string operationLocation)
        {
            // Retrieve the URI where the recognized text will be
            // stored from the Operation-Location header
            string operationId = operationLocation.Substring(
                operationLocation.Length - numberOfCharsInOperationId);

            Console.WriteLine("\nCalling GetHandwritingRecognitionOperationResultAsync()");
            TextOperationResult result =
                await computerVision.GetTextOperationResultAsync(operationId);

            // Wait for the operation to complete
            int i = 0;
            int maxRetries = 10;
            while ((result.Status == TextOperationStatusCodes.Running ||
                    result.Status == TextOperationStatusCodes.NotStarted) && i++ < maxRetries)
            {
                Console.WriteLine(
                    "Server status: {0}, waiting {1} seconds...", result.Status, i);
                await Task.Delay(1000);

                result = await computerVision.GetTextOperationResultAsync(operationId);
            }

            // Display the results
            Console.WriteLine();
            var lines = result.RecognitionResult.Lines;
            foreach(Line line in lines)
            {
                Console.WriteLine(line.Text);
            }
            Console.WriteLine();
        }
    }
}
```

## <a name="recognizetextasync-response"></a>RecognizeTextAsync 响应

成功的响应会显示每个图像的各行已识别文本。

如需原始 JSON 输出的示例，请参阅 [API 快速入门：使用 C# 提取手写文本](../QuickStarts/CSharp-hand-text.md#recognize-text-response)。

```cmd
Calling GetHandwritingRecognitionOperationResultAsync()

Calling GetHandwritingRecognitionOperationResultAsync()
Server status: Running, waiting 1 seconds...
Server status: Running, waiting 1 seconds...

dog
The quick brown fox jumps over the lazy
Pack my box with five dozen liquor jugs
```

## <a name="next-steps"></a>后续步骤

探索用于分析图像、检测名人和特征点，创建缩略图以及提取打印文本和手写文本的计算机视觉 API。

> [!div class="nextstepaction"]
> [探索计算机视觉 API](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44)
