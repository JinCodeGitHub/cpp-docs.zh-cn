---
title: _filelength、_filelengthi64
ms.date: 11/04/2016
api_name:
- _filelengthi64
- _filelength
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
- api-ms-win-crt-stdio-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _filelength
- _filelengthi64
- filelengthi64
helpviewer_keywords:
- filelengthi64 function
- lengths, file
- filelength function
- _filelength function
- files [C++], length
- _filelengthi64 function
ms.assetid: 3ab83d5a-543c-4079-b9d9-0abfc7da0275
ms.openlocfilehash: d7cf7f5bea5ed8964ec1a714a2a70d289daf085f
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2019
ms.locfileid: "70957220"
---
# <a name="_filelength-_filelengthi64"></a>_filelength、_filelengthi64

获取文件的长度。

## <a name="syntax"></a>语法

```C
long _filelength(
   int fd
);
__int64 _filelengthi64(
   int fd
);
```

### <a name="parameters"></a>参数

*fd*<br/>
以文件说明符为目标。

## <a name="return-value"></a>返回值

**_Filelength**和 **_filelengthi64**都返回与*fd*关联的目标文件的文件长度（以字节为单位）。 如果*fd*是无效的文件描述符，则此函数将调用无效参数处理程序，如[参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则这两个函数都将返回-1L 以指示错误，并将**errno**设置为**ebadf (** 。

## <a name="requirements"></a>要求

|函数|必需的标头|
|--------------|---------------------|
|**_filelength**|\<io.h>|
|**_filelengthi64**|\<io.h>|

有关更多兼容性信息，请参阅 [兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

请参见 [_chsize](chsize.md) 的示例。

## <a name="see-also"></a>请参阅

[文件处理](../../c-runtime-library/file-handling.md)<br/>
[_chsize](chsize.md)<br/>
[_fileno](fileno.md)<br/>
[_fstat、_fstat32、_fstat64、_fstati64、_fstat32i64、_fstat64i32](fstat-fstat32-fstat64-fstati64-fstat32i64-fstat64i32.md)<br/>
[_stat、_wstat 函数](stat-functions.md)<br/>
