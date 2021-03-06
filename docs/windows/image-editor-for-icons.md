---
title: 图标的图像编辑器（C++）
ms.date: 02/15/2019
f1_keywords:
- vc.editors.cursor.F1
- vc.editors.icon.F1
- vc.editors.cursor
- vc.editors.bitmap.F1
- vc.editors.bitmap
- vc.editors.dialog.GridSettings
- vc.editors.gridsettings
- vc.editors.bitmap
- vc.editors.icon
- vc.editors.texttool
- vc.editors.bitmap
- vc.editors.icon
helpviewer_keywords:
- editors, images
- resource editors [C++], graphics
- Image editor [C++]
- resource editors [C++], Image editor
- Image menu
- Grid Settings dialog box [C++]
- Graphics toolbar
- Image editor [C++], toolbar
- Image editor [C++], Option selector
- Properties window
- Option selector, Image editor
- toolbars [C++], showing
- toolbars [C++], hiding
- text, adding to an image
- Text Tool dialog box [C++]
- Text Tool Font dialog box [C++]
- fonts, changing on an image
- text, on images
- graphics editor [C++]
- Image editor [C++], panes
- Image editor [C++], magnification
- grids, pixel
- pixel grid, Image editor
- Image editor [C++], pixel grid
- Image editor [C++], grid settings
- grid settings, Image editor
ms.assetid: 586d2b8b-0348-4883-a85d-1ff0ddbf14dd
ms.openlocfilehash: 0f8fe228b804538b6a0d0377f05d79c34e787587
ms.sourcegitcommit: 389c559918d9bfaf303d262ee5430d787a662e92
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "69514216"
---
# <a name="image-editor-for-icons-c"></a>图标的图像编辑器（C++）

如果在**解决方案资源管理器**中选择图像文件（如 .ico、.bmp、.png），则图像将在 "**图像编辑器**" 中打开，其方式与在**代码编辑器**中打开代码文件的方式相同。 当 "**图像编辑器**" 选项卡处于活动状态时，将看到工具栏，其中包含用于创建和编辑图像的许多工具。 除了位图、图标和光标，还可以使用 **"图像" 菜单上**的命令和 "**图像编辑器**" 工具栏上的工具来编辑 GIF 或 JPEG 格式的图像。

图形资源是为应用程序定义的映像。 您可以使用形状绘制形状。 您可以选择图像的各个部分进行编辑、翻转或调整大小，也可以从图像的选定部分创建自定义画笔，并使用该画笔进行绘制。 您可以定义图像属性，以不同格式保存图像，并将图像从一种格式转换为另一种格式。

> [!NOTE]
> 使用**图像编辑器**，可以查看32位映像，但不能对其进行编辑。

还可以使用**图像编辑器**和[二进制编辑器](binary-editor.md)处理托管项目中的资源文件。 你要编辑的任何托管资源都必须是链接的资源。 Visual Studio 资源编辑器不支持编辑嵌入的资源。

除了创建新的图形资源之外，您还可以[导入现有的图像](../windows/how-to-copy-resources.md#import-and-export-resources)以进行编辑，然后将其添加到您的项目中。 你还可以打开和编辑不属于项目一部分的图像以进行[独立的图像编辑](../windows/editing-an-image-outside-of-a-project-image-editor-for-icons.md)。

有关**图像编辑器**的信息，请参阅如何[创建图标或其他图像](../windows/creating-an-icon-or-other-image-image-editor-for-icons.md)，如何[编辑图像](../windows/selecting-an-area-of-an-image-image-editor-for-icons.md)，如何[使用绘图工具](../windows/using-a-drawing-tool-image-editor-for-icons.md)，如何使用[颜色](../windows/working-with-color-image-editor-for-icons.md)和[加速键](../windows/accelerator-keys-image-editor-for-icons.md)。

> [!NOTE]
> 免费下载**Visual Studio 图像库**，其中包含许多可在应用程序中使用的动画、位图和图标。 有关如何下载库的详细信息，请参阅[Visual Studio 图像库](/visualstudio/designers/the-visual-studio-image-library)。

## <a name="image-menu"></a>“图像”菜单

"**图像**" 菜单（仅在**图像编辑器**处于活动状态时显示）、包含用于编辑图像的命令、管理调色板和设置 "**图像编辑器**" 窗口选项。 此外，使用图标和光标时，可以使用设备图像的命令。

|命令|描述|
|---|---|
|**反色**|反转颜色。|
|**水平翻转**|水平翻转图像或选定内容。|
|**垂直翻转**|垂直翻转图像或选定内容。|
|**旋转90度**|将图像或选定内容旋转 90 度。|
|**显示颜色窗口**|打开 "**颜色**" 窗口，您可以在其中选择要用于图像的颜色。|
|**将所选内容用作画笔**|使您能够从部分图像创建自定义画笔。<br/><br/>你的选择将成为一种自定义画笔，它在图像中分布所选内容中的颜色。 所选内容的副本沿着拖动路径为左。 拖动速度越慢，生成的副本就越多。|
|**复制和大纲选择**|创建当前选定内容的副本并绘制其轮廓。<br/><br/>如果当前选定内容中包含背景颜色，则在选择透明效果时，将排除该背景色。
|**调整颜色**|打开**自定义颜色选择器，该选择器**允许您自定义用于图像的颜色。|
|**加载调色板**|打开 "**加载**调色板" 对话框，您可以在其中加载以前保存到 pal 文件中的调色板颜色。|
|**保存调色板**|将调色板颜色保存到 pal 文件中。|
|**不透明绘图**|如果选择此选项，则使当前选定内容不透明。<br/><br/>如果清除此选项，则会使当前选择透明。|
|**工具栏编辑器**|打开 "[新建工具栏资源" 对话框](../windows/new-toolbar-resource-dialog-box.md)。|
|**网格设置**|打开 "**网格设置**" 对话框，您可以在其中指定图像的网格。|
|**新映像类型**|打开 "[新建\<设备 > 图像类型" 对话框](../windows/new-device-image-type-dialog-box-image-editor-for-icons.md)。<br/><br/>单个图标资源可以包含多个不同大小的图像，windows 可以根据显示方式使用相应的图标大小。 新设备类型不会修改图标的大小，而是在图标中创建新图像。 仅适用于图标和光标。|
|**当前图标/光标图像类型**|打开一个子菜单，其中列出了前九个可用的光标或图标图像。 子菜单上的最后一个命令将**打开 "** [打开\<设备 > 图像" 对话框](../windows/open-device-image-dialog-box-image-editor-for-icons.md)。|
|**删除图像类型**|删除所选的设备映像。|
|**工具**|启动一个子菜单，其中包含 "**图像编辑器**" 工具栏中的所有可用工具。|

"**网格设置**" 对话框允许您为图像指定网格设置，并在编辑后的图像上显示网格线。 线条对于编辑图像非常有用，但并不作为图像本身的一部分进行保存。

|属性|描述|
|---|---|
|**像素网格**|选中时，会在**图像编辑器**中的每个像素周围显示网格。<br/><br/>网格仅以4×和更高的分辨率显示。|
|**磁贴网格**|选中时，会在**图像编辑器**中围绕像素块显示网格，由网格间距值指定。|
|**Width**|指定每个图块的宽度。<br/><br/>当绘制的位图包含多个按固定间隔排列的图像时，此属性很有用。|
|**Height**|指定每个图块的高度。<br/><br/>当绘制的位图包含多个按固定间隔排列的图像时，此属性很有用。|

## <a name="toolbar"></a>Toolbar

"**图像编辑器**" 工具栏包含用于绘制、绘制、输入文本、擦除和操作视图的工具。 它还包含选项选择器，你可以使用该选择器来选择使用每个工具的选项。 例如，可以从各种画笔宽度、放大因子和线条样式中进行选择。

"**图像编辑器**" 工具栏上提供的所有工具也可通过菜单**图像** > **工具**获得。 若要使用 "**图像编辑器**" 工具栏和**选项**选择器，请选择所需的工具或选项。

![图像编辑器工具栏](../mfc/media/vcimageeditortoolbar.gif "vcImageEditorToolbar")<br/>
**图像编辑器**工具栏

> [!TIP]
> 当你将光标悬停在工具栏按钮上时，将显示工具提示。 这些提示可帮助您识别每个按钮的功能。

由于[键盘](../windows/accelerator-keys-image-editor-for-icons.md)上提供了许多绘图工具，因此隐藏 "**图像编辑器**" 工具栏有时会很有用。

- 若要显示或隐藏 "**图像编辑器**" 工具栏，请前往菜单**视图** > **工具栏**，然后选择 "**图像编辑器**"。

> [!NOTE]
> 当当前项目或解决方案中的图像文件未在**图像编辑器**中打开时，此工具栏中的元素将显示为不可用。

### <a name="option-selector"></a>选项选择器

使用**选项**选择器，可以指定线条的宽度、画笔笔划等。 **选项**选择器按钮上的图标根据您选择的工具而更改。

!["&#45;图像编辑器" 工具栏上的绘图形状选择器](../mfc/media/vcimageeditortoolbaroptionselector.gif "vcImageEditorToolbarOptionSelector")<br/>
"**图像编辑器**" 工具栏上的**选项**选择器

### <a name="text-tool"></a>文本工具

使用 "**文本工具**" 对话框可以将文本添加到光标、位图或图标资源。

若要访问此对话框，请打开 "**图像编辑器**" 并中转到 "菜单**图像** > **工具**"，然后选择 "**文本工具**" 命令。

> [!TIP]
> 您可以右键单击 "**文本工具**" 对话框以访问包含标准 Windows 命令列表的默认快捷菜单。

打开 "**文本工具字体**" 对话框以更改光标字体的字体、样式或大小。 将更改应用到**文本**区域中显示的文本。

若要访问此对话框，请在 "**文本工具**" 对话框中选择 "**字体**" 按钮。 可用的属性包括：

|属性|描述|
|---|---|
|**字体**|列出可用字体。|
|**字形**|列出指定字体的可用样式。|
|**Size**|列出指定字体的可用点大小。|
|示例|显示使用指定字体设置显示文本的示例。|
|**脚本**|列出指定字体的可用语言脚本。<br/><br/>选择其他语言脚本时，可以使用该语言的字符集创建多语言文档。|

#### <a name="to-change-the-font-of-text-on-an-image"></a>更改图像上文本的字体

下面的示例演示如何向 Windows 应用程序中的图标添加文本以及如何操作文本字体。

1. 创建C++ Windows 窗体应用程序。 有关详细信息，请参阅[如何：创建 Windows 窗体应用](/previous-versions/visualstudio/visual-studio-2008/s69bf10x(v%3dvs.90))程序。 默认情况下，会将一个*app.config*文件添加到项目。

1. 在**解决方案资源管理器**中，双击文件*app.config*。 **图像编辑器**将打开。

1. 中转到菜单**图像** > **工具**并选择**文本工具**。

1. 在 "**文本工具**" 对话框中， *C++* 键入空文本区域。 此文本将显示在**图像编辑器**的*app.config*的左上角的可调整大小的框中。

1. 在 "**图像编辑器**" 中，将 "可调整大小" 框拖到*app.config*的中心，以提高文本的可读性。

1. 在 "**文本工具**" 对话框中，选择 "**字体**" 按钮。

1. 在 "**文本工具字体**" 对话框中：

   - 从 "**字体**" 列表框中列出的可用字体列表中选择 "**新罗马时间**"。

   - 从 "**字体样式**" 列表框中列出的可用字体样式列表中选择 "**粗体**"。

   - 从 "**大小**" 列表框中列出的可用点大小列表中选择**10** 。

   - 选择 **“确定”** 。 "**文本工具字体**" 对话框将关闭，新的字体设置将应用于文本。

1. 选择 "**文本工具**" 对话框上的 "**关闭**"。 文本周围的可调整大小的框将从**图像编辑器**中消失。

文本区域显示作为资源的一部分显示的文本。 此区域最初为空。

> [!NOTE]
> 如果设置了**透明背景**，则只会在图像中放置文本。 如果设置了不**透明背景**，则使用背景色填充的边框将置于文本后面。

## <a name="window-panes"></a>窗口窗格

"**图像编辑器**" 窗口显示图像的两个视图，其中分隔条用于分隔两个窗格。 你可以将拆分条从一端拖动到另一端来更改窗格的相对大小。 活动窗格将显示选择边框。

一个视图是实际大小，另一个视图按默认放大系数6放大。 这两个窗格中的视图会自动更新，在一个窗格中所做的任何更改会立即显示在另一个窗格中。 通过这两个窗格，您可以轻松地处理图像的放大视图，在这种情况下，您可以区分单个像素，同时可以在图像的实际大小视图上观察工作效果。

左窗格使用所需的空间（最多一半的**图像**窗口）来显示图像的默认1:1 放大视图。 右窗格显示默认的6:1 放大倍数图像。 您可以使用 "**图像编辑器**" 工具栏上的**放大**工具或使用快捷键来更改每个窗格中的放大倍数。

您可以放大 "**图像编辑器**" 窗口的小窗格，并使用两个窗格来显示大图像的不同区域。 在窗格中选择以将其选中。

您可以通过将指针放在拆分栏上并向右或向左移动拆分栏来更改窗格的相对大小。 如果只想使用一个窗格，则拆分栏可以全部移动到任何一侧。

如果 "**图像编辑器**" 窗格的放大系数为4或更大，则可以显示一个像素网格，用于分隔图像中的各个像素。

### <a name="to-change-the-magnification-factor"></a>更改放大因子

默认情况下，**图像编辑器**将在左窗格中按实际大小显示视图，并在右窗格中按实际大小显示视图。 放大因子（在工作区底部的状态栏中显示）是图像的实际大小和显示大小之间的比率。 默认系数为6，范围为1到10。

1. 选择要更改其放大因子的 "**图像编辑器**" 窗格。

1. 在 "**图像编辑器**" 工具栏上，选择 "**放大**" 工具右侧的箭头，然后从子菜单中选择放大因子：**1x**、 **2x**、 **6 倍**或**8x**。

   > [!NOTE]
   > 若要**选择放大系数**之外的放大因子，请使用快捷键。

### <a name="to-display-or-hide-the-pixel-grid"></a>显示或隐藏像素网格

对于放大系数为4或更大的所有 "**图像编辑器**" 窗格，可以显示一个网格，用于分隔图像中的各个像素。

1. 中转到菜单**图像** > **网格设置**。

1. 选中 "**像素网格**" 复选框可显示网格，或者清除该复选框以隐藏网格。

## <a name="requirements"></a>要求

None

## <a name="see-also"></a>请参阅

[资源编辑器](../windows/resource-editors.md)<br/>
[图标](/windows/win32/menurc/icons)