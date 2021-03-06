---
title: 支持多字节字符集 (MBCS)
ms.date: 11/04/2016
helpviewer_keywords:
- MBCS [C++], about MBCS
- character sets [C++], multibyte
- multibyte characters [C++]
- MBCS [C++]
ms.assetid: b498733c-a1e1-45e3-8f26-d6da3cb5f2dd
ms.openlocfilehash: c21b5b1ff059f26558749e904894cb5d15572519
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62410559"
---
# <a name="support-for-multibyte-character-sets-mbcss"></a>支持多字节字符集 (MBCS)

多字节字符集 (MBCS) 是一种支持无法用单字节表示的字符集（如日语和中文）的旧方法。 如果要进行新的开发，则应对所有文本字符串（最终用户不会看到的系统字符串也许可以除外）使用 Unicode。 MBCS 是旧技术，不建议用于新开发。

最常见的 MBCS 实现是双字节字符集 (DBCS)。 通常，Visual C++（尤其是 MFC）对 DBCS 完全启用。

有关示例，请参阅 MFC 源代码文件。

对于在其语言使用大型字符集的市场中使用的平台，Unicode 的最佳备选方法是 MBCS。 MFC 通过使用可国际化的数据类型和 C 运行时函数来支持 MBCS。 应在你的代码中执行相同操作。

在 MBCS 下，字符以 1 或 2 字节进行编码。 在 2 字节字符中，第一个字节或前导字节会发出信号，表示它和下一个字节将被解释为一个字符。 第一个字节来自保留用作前导字节的代码范围。 哪个范围的字节可以是前导字节取决于正在使用的代码页。 例如，日语代码页 932 将 0x81 到 0x9F 的范围用作前导字节，而朝鲜语代码页 949 使用不同的范围。

请在 MBCS 编程中考虑以下各方面。

环境 MBCS 字符中的 MBCS 字符可以出现在如文件和目录名称的字符串。

### <a name="editing-operations"></a>编辑操作

MBCS 应用程序中的编辑操作应在字符上（而不是在字节上）执行。 将插入符号不应拆分一个字符，字符**向右箭头**密钥应移向右一个字符，依次类推。 **删除**应删除一个字符;**撤消**应将它重新插入。

### <a name="string-handling"></a>字符串处理

在使用 MBCS 的应用程序中，字符串处理会引起特殊问题。 在单一字符串中混合使用两种宽度的字符；因此，你必须记得检查前导字节。

### <a name="run-time-library-support"></a>运行时库支持

C 运行时库和 MFC 支持单字节、MBCS 和 Unicode 编程。 单字节字符串的处理与`str`系列的运行时函数，MBCS 字符串进行处理并且使用相应`_mbs`函数和 Unicode 字符串处理相对应的`wcs`函数。 MFC 类成员函数的实现使用可移植运行时函数，该函数在适当情况下映射到 `str` 系列的函数、MBCS 函数或 Unicode 函数，如“MBCS/Unicode 可移植性”中所述。

### <a name="mbcsunicode-portability"></a>MBCS/Unicode 可移植性

使用 tchar.h 头文件，可以构建单字节、 MBCS 和 Unicode 应用程序从相同的源。 Tchar.h 定义具有前缀的宏 *_tcs* ，它们分别映射到`str`， `_mbs`，或`wcs`函数，根据需要。 若要生成 MBCS，请定义符号`_MBCS`。 若要生成 Unicode，请定义符号`_UNICODE`。 默认情况下，`_UNICODE`为 MFC 应用程序定义。 有关详细信息，请参阅[tchar.h 中的一般文本映射](../text/generic-text-mappings-in-tchar-h.md)。

> [!NOTE]
>  如果同时定义行为是未定义`_UNICODE`和`_MBCS`。

Mbctype.h 和 Mbstring.h 头文件定义特定于 MBCS 的函数和宏，你可能在某些情况下需要它们。 例如，`_ismbblead` 告诉你字符串中的特定字节是否为前导字节。

国际可移植性，对程序进行编码与[Unicode](../text/support-for-unicode.md)或多字节字符集 (Mbcs)。

## <a name="what-do-you-want-to-do"></a>你希望做什么？

- [在我的程序中启用 MBCS](../text/international-enabling.md)

- [在我的程序中启用 Unicode 和 MBCS](../text/internationalization-strategies.md)

- [使用 MBCS 创建国际化的程序](../text/mbcs-programming-tips.md)

- [请参阅 MBCS 编程的摘要](../text/mbcs-programming-tips.md)

- [了解字节宽度可移植性的一般文本映射](../text/generic-text-mappings-in-tchar-h.md)

## <a name="see-also"></a>请参阅

[文本和字符串](../text/text-and-strings-in-visual-cpp.md)<br/>
[Visual C++ 中的 MBCS 支持](../text/mbcs-support-in-visual-cpp.md)
