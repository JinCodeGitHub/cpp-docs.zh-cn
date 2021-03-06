---
title: 创建自己的对话框类
ms.date: 09/06/2019
helpviewer_keywords:
- dialog boxes [MFC], creating
- MFC dialog boxes [MFC], creating
- files [MFC], creating
- dialog classes [MFC], Add Class Wizard
- dialog classes [MFC], creating
ms.assetid: d5321741-da41-47a8-bb1c-6a0e8b28c4c1
ms.openlocfilehash: b8275754d46e9d76933624af55335e956736319a
ms.sourcegitcommit: 1e6386be9084f70def7b3b8b4bab319a117102b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2019
ms.locfileid: "71685645"
---
# <a name="creating-your-dialog-class"></a>创建自己的对话框类

对于程序中的每个对话框，创建一个与对话框资源一起使用的新对话框类。

[添加类](../ide/adding-a-class-visual-cpp.md)说明了如何创建新的对话框类。 使用[类向导](reference/mfc-class-wizard.md)创建对话框类时，它会将以下项写入指定的 .h 和 .cpp 文件中：

在 .h 文件中：

- 对话框类的类声明。 该类派生自[CDialog](../mfc/reference/cdialog-class.md)。

在 .cpp 文件中：

- 类的消息映射。

- 对话框的标准构造函数。

- [DoDataExchange](../mfc/reference/cwnd-class.md#dodataexchange)成员函数的重写。 编辑此函数。 它用于对话框数据交换和验证功能，如稍后在[对话框数据交换和验证](../mfc/dialog-data-exchange-and-validation.md)中所述。

## <a name="see-also"></a>请参阅

[使用代码向导创建对话框类](../mfc/creating-a-dialog-class-with-code-wizards.md)<br/>
[使用 MFC 中的对话框](../mfc/life-cycle-of-a-dialog-box.md)
