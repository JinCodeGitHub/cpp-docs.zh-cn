---
title: C 杂注
ms.date: 01/29/2018
helpviewer_keywords:
- pragmas, C/C++
ms.assetid: 3d6d36b4-d565-4632-a4cd-e39aeaded5ad
ms.openlocfilehash: f0517e83c36f97af35dab7d4be85be5aee1b01af
ms.sourcegitcommit: 6052185696adca270bc9bdbec45a626dd89cdcdd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50650668"
---
# <a name="c-pragmas"></a>C 杂注

**Microsoft 专用**

“杂注”指示编译器在编译时执行特定操作。 杂注随编译器的不同而不同。 例如，可以使用 optimize 杂注来设置要在程序中执行的优化。 Microsoft C 杂注为：

|||||
|-|-|-|-|
|**alloc_text**|**data_seg**|**inline_recursion**|**setlocale**|
|**auto_inline**|**函数**|**intrinsic**|**warning**|
|**check_stack**|**hdrstop**|**message**||
|**code_seg**|**include_alias**|**optimize**||
|**comment**|**inline_depth**|**pack**||

有关 Microsoft C 编译器杂注的说明，请参阅 [Pragma 指令和 __Pragma 关键字](../preprocessor/pragma-directives-and-the-pragma-keyword.md)。

**结束 Microsoft 专用**

## <a name="see-also"></a>请参阅

[源文件和源程序](../c-language/source-files-and-source-programs.md)
