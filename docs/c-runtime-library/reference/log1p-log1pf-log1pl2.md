---
title: log1p、log1pf、log1pl2
ms.date: 04/05/2018
api_name:
- log1p
- log1pf
- log1pl
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-math-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- log1p
- log1pf
- log1pl
- math/log1p
- math/log1pf
- math/log1pl
helpviewer_keywords:
- log1p function
- log1pf function
- log1pl function
ms.assetid: a40d965d-b4f6-42f4-ba27-2395546f7c12
ms.openlocfilehash: aad6675a832e1715c505026fe11ffe77f1f6d275
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2019
ms.locfileid: "70953220"
---
# <a name="log1p-log1pf-log1pl"></a>log1p、log1pf、log1pl

计算 1 加上指定值的自然对数。

## <a name="syntax"></a>语法

```C
double log1p(
   double x
);

float log1p(
   float x
); //C++ only

long double log1p(
   long double x
); //C++ only

float log1pf(
   float x
);

long double log1pl(
   long double x
);
```

### <a name="parameters"></a>参数

*x*<br/>
浮点型参数。

## <a name="return-value"></a>返回值

如果成功，则返回（*x* + 1）的自然（以*e*为底）对数。

否则，可能返回以下值之一：

|输入|结果|SEH 异常|errno|
|-----------|------------|-------------------|-----------|
|+inf|+inf|||
|非规格化数|与输入相同|UNDERFLOW||
|±0|与输入相同|||
|-1|-inf|DIVBYZERO|ERANGE|
|< -1|nan|INVALID|EDOM|
|-inf|nan|INVALID|EDOM|
|±SNaN|与输入相同|INVALID||
|± QNaN，不定|与输入相同|||

如果*x* =-1，则**errno**值设置为 ERANGE。 如果*x* <-1，则将**errno**值设置为**EDOM** 。

## <a name="remarks"></a>备注

当 x 接近0时， **log1p**函数可能更准确。 `log(x + 1)`

由于C++允许重载，因此可以调用**log1p**的重载，该重载采用和返回**float**和**long** **double**类型。 在 C 程序中， **log1p**始终采用并返回**双精度型**。

如果*x*是自然数，则此函数返回（*x* -1）的阶乘的对数。

## <a name="requirements"></a>要求

|函数|C 标头|C++ 标头|
|--------------|--------------|------------------|
|**log1p**、 **log1pf**、 **log1pl**|\<math.h>|\<cmath>|

有关其他兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="see-also"></a>请参阅

[按字母顺序的函数参考](crt-alphabetical-function-reference.md)<br/>
[log2、log2f、log2l](log2-log2f-log2l.md)<br/>
[log、logf、log10、log10f](log-logf-log10-log10f.md)<br/>
