---
title: 编译器警告（等级 4）C4213
ms.date: 11/04/2016
f1_keywords:
- C4213
helpviewer_keywords:
- C4213
ms.assetid: 59fc3f61-ebd2-499e-99d7-f57bec11eda1
ms.openlocfilehash: 318b228a1af17543062943a336ccccd06bc6ae46
ms.sourcegitcommit: 3ee06ec53153cf21910fc8cfef78a4f25f9633f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2019
ms.locfileid: "74541813"
---
# <a name="compiler-warning-level-4-c4213"></a>编译器警告（等级 4）C4213

使用了非标准扩展：左值上的强制转换

使用默认的 Microsoft 扩展（/Ze），可以在赋值语句的左侧使用强制转换。

## <a name="example"></a>示例

```c
// C4213.c
// compile with: /W4
void *a;
void f()
{
   int   i[3];
   a = &i;
   *(( int * )a )++ = 3;  // C4213
}

int main()
{
}
```

此类转换在 ANSI 兼容性（[/za](../../build/reference/za-ze-disable-language-extensions.md)）下无效。