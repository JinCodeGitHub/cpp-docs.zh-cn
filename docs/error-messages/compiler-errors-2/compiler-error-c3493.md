---
title: 编译器错误 C3493
ms.date: 11/04/2016
f1_keywords:
- C3493
helpviewer_keywords:
- C3493
ms.assetid: 734b4257-12a3-436f-8488-c8c55ec81634
ms.openlocfilehash: 178d1221886dc62edd9785d211e2189fa50962f4
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74738292"
---
# <a name="compiler-error-c3493"></a>编译器错误 C3493

无法隐式捕获“var”，因为尚未指定默认捕获模式

空 lambda 表达式捕获 `[]`指定 lambda 表达式不显式或隐式捕获任何变量。

### <a name="to-correct-this-error"></a>更正此错误

- 提供默认捕获模式，或

- 显式捕获一个或多个变量。

## <a name="example"></a>示例

下面的示例生成 C3493，因为它将修改外部变量，但指定空的 capture 子句：

```cpp
// C3493a.cpp

int main()
{
   int m = 55;
   [](int n) { m = n; }(99); // C3493
}
```

## <a name="example"></a>示例

下面的示例通过将“按引用”指定为默认捕获模式来解决 C3493。

```cpp
// C3493b.cpp

int main()
{
   int m = 55;
   [&](int n) { m = n; }(99);
}
```

## <a name="see-also"></a>另请参阅

[Lambda 表达式](../../cpp/lambda-expressions-in-cpp.md)
