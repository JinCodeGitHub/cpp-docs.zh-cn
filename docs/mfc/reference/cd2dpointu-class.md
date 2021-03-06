---
title: CD2DPointU 类
ms.date: 08/29/2019
f1_keywords:
- CD2DPointU
- AFXRENDERTARGET/CD2DPointU
- AFXRENDERTARGET/CD2DPointU::CD2DPointU
helpviewer_keywords:
- CD2DPointU [MFC], CD2DPointU
ms.assetid: 04733f96-b6de-4a89-82e3-caad1e8087a9
ms.openlocfilehash: 6289d33aa0672d1ee423d91b11527dccfc868da7
ms.sourcegitcommit: e10a5feea193c249ddc5a6faba48e7c6d8784e73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70177174"
---
# <a name="cd2dpointu-class"></a>CD2DPointU 类

`D2D1_POINT_2U`的包装器。

## <a name="syntax"></a>语法

```
class CD2DPointU : public D2D1_POINT_2U;
```

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|名称|描述|
|----------|-----------------|
|[CD2DPointU::CD2DPointU](#cd2dpointu)|已重载。 构造 from 对象`D2D1_POINT_2U`对象。 `CD2DPointU`|

### <a name="public-operators"></a>公共运算符

|名称|描述|
|----------|-----------------|
|[CD2DPointU:: operator CPoint](#operator_cpoint)|转换`CD2DPointU` 为`CPoint`对象。|

## <a name="inheritance-hierarchy"></a>继承层次结构

`D2D1_POINT_2U`

`CD2DPointU`

## <a name="requirements"></a>要求

**标头:** afxrendertarget

##  <a name="cd2dpointu"></a>CD2DPointU:: CD2DPointU

从 CPoint 对象构造 CD2DPointU 对象。

```
CD2DPointU(const CPoint& pt);
CD2DPointU(const D2D1_POINT_2U& pt);
CD2DPointU(const D2D1_POINT_2U* pt);
CD2DPointU(UINT32 uX = 0, UINT32 uY = 0);
```

### <a name="parameters"></a>参数

*pt*<br/>
源点

*uX*<br/>
源 X

*uY*<br/>
源 Y

##  <a name="operator_cpoint"></a>CD2DPointU:: operator CPoint

将 CD2DPointU 转换为 CPoint 对象。

```
operator CPoint();
```

### <a name="return-value"></a>返回值

D2D 点的当前值。

## <a name="see-also"></a>请参阅

[类](../../mfc/reference/mfc-classes.md)
