---
title: 编译器错误 C3499
ms.date: 11/04/2016
f1_keywords:
- C3499
helpviewer_keywords:
- C3499
ms.assetid: 6717de5c-ae0f-4024-bdf2-b5598009e7b6
ms.openlocfilehash: e50aaeac4a9f02cf3e67c25a08afdc2df0f1c62f
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74738006"
---
# <a name="compiler-error-c3499"></a>编译器错误 C3499

已指定返回类型为 void 的 lambda 无法返回值

当将 `void` 指定为返回类型的 lambda 表达式返回值时，编译器产生此错误；或者当 lambda 表达式包含多条语句并返回一个值，但是未指定其返回类型时也会产生此错误。

### <a name="to-correct-this-error"></a>更正此错误

- 请勿从 lambda 表达式返回值，或

- 提供 lambda 表达式的返回类型，或

- 将构成 lambda 表达式主体的语句合并成一条语句。

## <a name="example"></a>示例

以下示例将生成 C3499，因为 lambda 表达式的主体包含多条语句并返回一个值，但 lambda 表达式未指定返回类型：

```cpp
// C3499a.cpp

int main()
{
   [](int x) { int n = x * 2; return n; } (5); // C3499
}
```

## <a name="example"></a>示例

以下示例演示 C3499 的两个可能的解决方法。 第一个解决方法是提供 lambda 表达式的返回类型。 第二个解决方法是将构成 lambda 表达式主体的语句合并成一条语句。

```cpp
// C3499b.cpp

int main()
{
   // Possible resolution 1:
   // Provide the return type of the lambda expression.
   [](int x) -> int { int n = x * 2; return n; } (5);

   // Possible resolution 2:
   // Combine the statements that make up the body of
   // the lambda expression into a single statement.
   [](int x) { return x * 2; } (5);
}
```

## <a name="see-also"></a>另请参阅

[Lambda 表达式](../../cpp/lambda-expressions-in-cpp.md)
