---
title: vector&lt;bool&gt;::reference::flip
ms.date: 11/04/2016
f1_keywords:
- vector/std::vector<bool>::reference::flip
helpviewer_keywords:
- reference::flip method
ms.assetid: ef940365-cbe4-4a87-a3e2-1f3cfa357e29
ms.openlocfilehash: 1743df7773d577e53f054fa4e403cf0d00da8ce7
ms.sourcegitcommit: 0dcab746c49f13946b0a7317fc9769130969e76d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68452173"
---
# <a name="vectorltboolgtreferenceflip"></a>vector&lt;bool&gt;::reference::flip

反转引用的 [vector\<bool>](../standard-library/vector-bool-class.md) 元素的布尔值。

## <a name="syntax"></a>语法

```cpp
void flip();
```

## <a name="example"></a>示例

```cpp
// vector_bool_ref_flip.cpp
// compile with: /EHsc /W4
#include <vector>
#include <iostream>

int main()
{
    using namespace std;
    cout << boolalpha;

    vector<bool> vb = { true, false, false, true, true };

    cout << "The vector is: " << endl << "    ";
    for (const auto& b : vb) {
        cout << b << " ";
    }
    cout << endl;

    vector<bool>::reference vbref = vb.front();
    vbref.flip();

    cout << "The vector with first element flipped is: " << endl << "    ";
    for (const auto& b : vb) {
        cout << b << " ";
    }
    cout << endl;
}
```

## <a name="output"></a>Output

```Output
The vector is:
    true false false true true
The vector with first element flipped is:
    false false false true true
```

## <a name="requirements"></a>要求

**标头：** \<vector>

**命名空间：** std

## <a name="see-also"></a>请参阅

[vector\<bool>::reference 类](../standard-library/vector-bool-reference-class.md)\
[C++ 标准库参考](../standard-library/cpp-standard-library-reference.md)
