---
title: 自定义生成步骤属性 (Linux C++)
ms.date: 06/07/2019
ms.assetid: 77a9c1fb-7c41-4a9b-9418-18ac17ce4e74
ms.openlocfilehash: e09af7642171d0d73d2b06c048067bbe61290ddc
ms.sourcegitcommit: 8adabe177d557c74566c13145196c11cef5d10d4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66821411"
---
# <a name="custom-build-step-properties-linux-c"></a>自定义生成步骤属性 (Linux C++)

::: moniker range="vs-2015"

Linux 支持在 Visual Studio 2017 及更高版本中提供。

::: moniker-end

::: moniker range=">=vs-2017"

Property | 说明
--- | ---
命令行 | 将由自定义生成步骤执行的命令。
说明 | 自定义生成步骤运行时显示的消息。
输出 | 自定义生成步骤生成的输出文件。 需要该设置，以使增量生成正确执行。
附加依赖项 | 用于自定义生成步骤的任何其他输入文件的以分号分隔的列表。
在以下操作之后执行和在以下操作之前执行 | 这些选项定义相对于列出的目标，何时在生成过程中运行自定义生成步骤。 最常列出的目标是 BuildGenerateSources、BuildCompile 和 BuildLink，因为它们代表生成过程中的主要步骤。 其他经常列出的目标是 Midl、CLCompile 和链接。
将输出视为内容 | 该选项只对于 Microsoft 应用商店或 Windows Phone 应用有意义，这些应用将所有内容文件包含在 .appx 包中。

::: moniker-end