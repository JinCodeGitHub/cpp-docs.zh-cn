---
title: basic_filebuf 类
ms.date: 11/04/2016
f1_keywords:
- fstream/std::basic_filebuf
- fstream/std::basic_filebuf::char_type
- fstream/std::basic_filebuf::int_type
- fstream/std::basic_filebuf::off_type
- fstream/std::basic_filebuf::pos_type
- fstream/std::basic_filebuf::traits_type
- fstream/std::basic_filebuf::close
- fstream/std::basic_filebuf::is_open
- fstream/std::basic_filebuf::open
- fstream/std::basic_filebuf::overflow
- fstream/std::basic_filebuf::pbackfail
- fstream/std::basic_filebuf::seekoff
- fstream/std::basic_filebuf::seekpos
- fstream/std::basic_filebuf::setbuf
- fstream/std::basic_filebuf::Swap
- fstream/std::basic_filebuf::sync
- fstream/std::basic_filebuf::uflow
- fstream/std::basic_filebuf::underflow
helpviewer_keywords:
- std::basic_filebuf [C++]
- std::basic_filebuf [C++], char_type
- std::basic_filebuf [C++], int_type
- std::basic_filebuf [C++], off_type
- std::basic_filebuf [C++], pos_type
- std::basic_filebuf [C++], traits_type
- std::basic_filebuf [C++], close
- std::basic_filebuf [C++], is_open
- std::basic_filebuf [C++], open
- std::basic_filebuf [C++], overflow
- std::basic_filebuf [C++], pbackfail
- std::basic_filebuf [C++], seekoff
- std::basic_filebuf [C++], seekpos
- std::basic_filebuf [C++], setbuf
- std::basic_filebuf [C++], Swap
- std::basic_filebuf [C++], sync
- std::basic_filebuf [C++], uflow
- std::basic_filebuf [C++], underflow
ms.assetid: 3196ba5c-bf38-41bd-9a95-70323ddfca1a
ms.openlocfilehash: 16d485320eb3970bd5c1e4a7a7fabb0602149e6f
ms.sourcegitcommit: ea9d78dbb93bf3f8841dde93dbc12bd66f6f32ff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72778552"
---
# <a name="basic_filebuf-class"></a>basic_filebuf 类

描述一个流缓冲区，该缓冲区控制*Char_T*类型的元素（其字符特征由类*Tr*确定）与外部文件中存储的元素序列之间的传输。

## <a name="syntax"></a>语法

```cpp
template <class Char_T, class Tr = char_traits<Char_T>>
class basic_filebuf : public basic_streambuf<Char_T, Tr>
```

### <a name="parameters"></a>参数

*Char_T* \
文件缓冲区的基本元素。

*Tr* \
文件缓冲区的基本元素的特征（通常为 `char_traits<Char_T>`）。

## <a name="remarks"></a>备注

类模板描述了一个流缓冲区，该缓冲区控制*Char_T*类型的元素（其字符特征由类*Tr*确定）与外部文件中存储的元素序列之间的传输。

> [!NOTE]
> @No__t_0 类型的对象是使用__char \*__ 类型的内部缓冲区创建的，而不考虑类型参数*Char_T*指定的 `char_type`。 这意味着 Unicode 字符串（包含**wchar_t**个字符）将在写入内部缓冲区之前转换为 ANSI 字符串 **（包含字符**）。 若要在缓冲区中存储 Unicode 字符串，请创建一个类型为**wchar_t**的新缓冲区，并使用[`basic_streambuf::pubsetbuf`](../standard-library/basic-streambuf-class.md#pubsetbuf) `()` 方法对其进行设置。 若要查看演示此行为的示例，请参阅下面的内容。

类的对象 `basic_filebuf<Char_T, Tr>` 存储文件指针，它指定用于控制与打开的文件关联的流的 `FILE` 对象。 另外，它还存储指向两个文件转换方面的指针，以供受保护的成员函数 [overflow](#overflow) 和 [underflow](#underflow) 使用。 有关详细信息，请参阅 [`basic_filebuf::open`](#open)。

## <a name="example"></a>示例

下面的示例演示如何通过调用 `pubsetbuf()` 方法来强制 `basic_filebuf<wchar_t>` 类型的对象将 Unicode 字符存储在其内部缓冲区中。

```cpp
// unicode_basic_filebuf.cpp
// compile with: /EHsc

#include <iostream>
#include <string>
#include <fstream>
#include <iomanip>
#include <memory.h>
#include <string.h>

#define IBUFSIZE 16

using namespace std;

void hexdump(const string& filename);

int main()
{
    wchar_t* wszHello = L"Hello World";
    wchar_t wBuffer[128];

    basic_filebuf<wchar_t> wOutFile;

    // Open a file, wcHello.txt, then write to it, then dump the
    // file's contents in hex
    wOutFile.open("wcHello.txt",
        ios_base::out | ios_base::trunc | ios_base::binary);
    if(!wOutFile.is_open())
    {
        cout << "Error Opening wcHello.txt\n";
        return -1;
    }
    wOutFile.sputn(wszHello, (streamsize)wcslen(wszHello));
    wOutFile.close();
    cout << "Hex Dump of wcHello.txt - note that output is ANSI chars:\n";
    hexdump(string("wcHello.txt"));

    // Open a file, wwHello.txt, then set the internal buffer of
    // the basic_filebuf object to be of type wchar_t, then write
    // to the file and dump the file's contents in hex
    wOutFile.open("wwHello.txt",
        ios_base::out | ios_base::trunc | ios_base::binary);
    if(!wOutFile.is_open())
    {
        cout << "Error Opening wwHello.txt\n";
        return -1;
    }
    wOutFile.pubsetbuf(wBuffer, (streamsize)128);
    wOutFile.sputn(wszHello, (streamsize)wcslen(wszHello));
    wOutFile.close();
    cout << "\nHex Dump of wwHello.txt - note that output is wchar_t chars:\n";
    hexdump(string("wwHello.txt"));

    return 0;
}

// dump contents of filename to stdout in hex
void hexdump(const string& filename)
{
    fstream ifile(filename.c_str(),
        ios_base::in | ios_base::binary);
    char *ibuff = new char[IBUFSIZE];
    char *obuff = new char[(IBUFSIZE*2)+1];
    int i;

    if(!ifile.is_open())
    {
        cout << "Cannot Open " << filename.c_str()
             << " for reading\n";
        return;
    }
    if(!ibuff || !obuff)
    {
        cout << "Cannot Allocate buffers\n";
        ifile.close();
        return;
    }

    while(!ifile.eof())
    {
        memset(obuff,0,(IBUFSIZE*2)+1);
        memset(ibuff,0,IBUFSIZE);
        ifile.read(ibuff,IBUFSIZE);

        // corner case where file is exactly a multiple of
        // 16 bytes in length
        if(ibuff[0] == 0 && ifile.eof())
            break;

        for(i = 0; i < IBUFSIZE; i++)
        {
            if(ibuff[i] >= ' ')
                obuff[i] = ibuff[i];
            else
                obuff[i] = '.';

            cout << setfill('0') << setw(2) << hex
                 << (int)ibuff[i] << ' ';
        }
        cout << "  " << obuff << endl;
    }
    ifile.close();
}
```

```Output
Hex Dump of wcHello.txt - note that output is ANSI chars:
48 65 6c 6c 6f 20 57 6f 72 6c 64 00 00 00 00 00   Hello World.....

Hex Dump of wwHello.txt - note that output is wchar_t chars:
48 00 65 00 6c 00 6c 00 6f 00 20 00 57 00 6f 00   H.e.l.l.o. .W.o.
72 00 6c 00 64 00 00 00 00 00 00 00 00 00 00 00   r.l.d...........
```

### <a name="constructors"></a>构造函数

|构造函数|描述|
|-|-|
|[basic_filebuf](#basic_filebuf)|构造 `basic_filebuf` 类型的对象。|

### <a name="typedefs"></a>Typedef

|类型名称|描述|
|-|-|
|[char_type](#char_type)|将类型名与 `Char_T` 模板参数关联。|
|[int_type](#int_type)|使 `basic_filebuf` 范围中的此类型等效于 `Tr` 范围中具有相同名称的类型。|
|[off_type](#off_type)|使 `basic_filebuf` 范围中的此类型等效于 `Tr` 范围中具有相同名称的类型。|
|[pos_type](#pos_type)|使 `basic_filebuf` 范围中的此类型等效于 `Tr` 范围中具有相同名称的类型。|
|[traits_type](#traits_type)|将类型名与 `Tr` 模板参数关联。|

### <a name="member-functions"></a>成员函数

|成员函数|描述|
|-|-|
|[close](#close)|关闭文件。|
|[is_open](#is_open)|指示文件是否打开。|
|[open](#open)|打开文件。|
|[overflow](#overflow)|将新字符插入到已满缓冲区时可以调用的受保护虚函数。|
|[pbackfail](#pbackfail)|受保护虚拟成员函数尝试将元素放回到输入流中，随后使它成为当前元素（由下一个指针指向）。|
|[seekoff](#seekoff)|受保护虚拟成员函数尝试更改受控制流的当前位置。|
|[seekpos](#seekpos)|受保护虚拟成员函数尝试更改受控制流的当前位置。|
|[setbuf](#setbuf)|受保护虚拟成员函数执行特定于每个派生流缓冲区的操作。|
|[Swap](#swap)|为提供的 `basic_filebuf` 参数的内容交换此 `basic_filebuf` 的内容。|
|[sync](#sync)|受保护虚函数尝试将受控制流与任何关联的外部流同步。|
|[uflow](../standard-library/basic-streambuf-class.md#uflow)|受保护虚函数从输入流中提取当前元素。|
|[underflow](#underflow)|受保护虚函数从输入流中提取当前元素。|

## <a name="requirements"></a>要求

**标头：** \<fstream>

**命名空间:** std

## <a name="basic_filebuf"></a>  basic_filebuf::basic_filebuf

构造 `basic_filebuf` 类型的对象。

```cpp
basic_filebuf();

basic_filebuf(basic_filebuf&& right);
```

### <a name="remarks"></a>备注

第一个构造函数将 null 指针存储在控制输入缓冲区和输出缓冲区的所有指针中。 同时它还将 null 指针存储在文件指针中。

第二个构造函数使用*右侧*的内容初始化对象，该对象被视为右值引用。

## <a name="char_type"></a>  basic_filebuf::char_type

将类型名与 `Char_T` 模板参数关联。

```cpp
typedef Char_T char_type;
```

## <a name="close"></a>  basic_filebuf::close

关闭文件。

```cpp
basic_filebuf<Char_T, Tr> *close();
```

### <a name="return-value"></a>返回值

如果文件指针为 null 指针，则该成员函数返回 null 指针。

### <a name="remarks"></a>备注

`close` 调用 `fclose(fp)`。 如果该函数返回一个非零值，则该函数返回 null 指针。 否则，它将返回 **this** 以指示已成功关闭文件。

对于宽流，如果自打开流以来或自上次调用 `streampos` 后发生任何插入操作，则该函数将调用[`overflow`](#overflow)。 它还会插入还原初始转换状态所需的任何序列，方法是使用文件转换方面 `fac` 按需调用 `fac.unshift`。 **Char**类型的每个生成的元素 `byte` 都将写入文件指针所指定的关联流 `fp` 就像通过对窗体 `fputc(byte, fp)` 的连续调用一样。 如果对 `fac.unshift` 或任何写入操作失败，则该函数不会成功。

### <a name="example"></a>示例

下面的示例假定当前目录中有两个文件： *basic_filebuf_close* （内容为 "测试"）和*iotest* （内容为 "ssss"）。

```cpp
// basic_filebuf_close.cpp
// compile with: /EHsc
#include <fstream>
#include <iostream>

int main() {
   using namespace std;
   ifstream file;
   basic_ifstream <wchar_t> wfile;
   char c;
   // Open and close with a basic_filebuf
   file.rdbuf()->open( "basic_filebuf_close.txt", ios::in );
   file >> c;
   cout << c << endl;
   file.rdbuf( )->close( );

   // Open/close directly
   file.open( "iotest.txt" );
   file >> c;
   cout << c << endl;
   file.close( );

   // open a file with a wide character name
   wfile.open( L"iotest.txt" );

   // Open and close a nonexistent with a basic_filebuf
   file.rdbuf()->open( "ziotest.txt", ios::in );
   cout << file.fail() << endl;
   file.rdbuf( )->close( );

   // Open/close directly
   file.open( "ziotest.txt" );
   cout << file.fail() << endl;
   file.close( );
}
```

```Output
t
s
0
1
```

## <a name="int_type"></a>  basic_filebuf::int_type

在 `basic_filebuf` 作用域内使此类型等效于 `Tr` 作用域中具有相同名称的类型。

```cpp
typedef typename traits_type::int_type int_type;
```

## <a name="is_open"></a>  basic_filebuf::is_open

指示文件是否打开。

```cpp
bool is_open() const;
```

### <a name="return-value"></a>返回值

如果文件指针不是 null 指针，**则为 true** 。

### <a name="example"></a>示例

```cpp
// basic_filebuf_is_open.cpp
// compile with: /EHsc
#include <fstream>
#include <iostream>

int main( )
{
   using namespace std;
   ifstream file;
   cout << boolalpha << file.rdbuf( )->is_open( ) << endl;

   file.open( "basic_filebuf_is_open.cpp" );
   cout << file.rdbuf( )->is_open( ) << endl;
}
```

```Output
false
true
```

## <a name="off_type"></a>  basic_filebuf::off_type

在 `basic_filebuf` 作用域内使此类型等效于 `Tr` 作用域中具有相同名称的类型。

```cpp
typedef typename traits_type::off_type off_type;
```

## <a name="open"></a>  basic_filebuf::open

打开文件。

```cpp
basic_filebuf<Char_T, Tr> *open(
    const char* filename,
    ios_base::openmode mode,
    int protection = (int)ios_base::_Openprot);

basic_filebuf<Char_T, Tr> *open(
    const char* filename,
    ios_base::openmode mode);

basic_filebuf<Char_T, Tr> *open(
    const wchar_t* filename,
    ios_base::openmode mode,
    int protection = (int)ios_base::_Openprot);

basic_filebuf<Char_T, Tr> *open(
    const wchar_t* filename,
    ios_base::openmode mode);
```

### <a name="parameters"></a>参数

*文件名*\
要打开的文件的名称。

*模式*\
[@No__t_1](../standard-library/ios-base-class.md#openmode)中的一个枚举。

*保护*\
默认的文件打开保护，等效于[_fsopen、_wfsopen](../c-runtime-library/reference/fsopen-wfsopen.md)中的*shflag*参数。

### <a name="return-value"></a>返回值

如果文件指针为 null 指针，则该函数返回 null 指针。 否则，返回 **this**。

### <a name="remarks"></a>备注

成员函数通过调用[`fopen`](../c-runtime-library/reference/fopen-wfopen.md) `(filename, strmode)` 来打开名称*文件名*为的文件。 `strmode` 通过 `mode & ~(`[ `ate`](../standard-library/ios-base-class.md#openmode) ` | `[ `binary`](../standard-library/ios-base-class.md#openmode) `)` 确定：

- `ios_base::in` 变成 `"r"` （打开现有文件以进行读取）。

- [ios_base：： out](../standard-library/ios-base-class.md#fmtflags)或 `ios_base::out | ios_base::trunc` 变成 `"w"` （截断现有文件或创建以进行写入）。

- `ios_base::out | app` 将变成 `"a"` （打开现有文件以追加所有写入）。

- `ios_base::in | ios_base::out` 变成 `"r+"` （打开现有文件以进行读取和写入）。

- `ios_base::in | ios_base::out | ios_base::trunc` 将变成 `"w+"` （截断现有文件或创建以进行读写）。

- `ios_base::in | ios_base::out | ios_base::app` 将变成 `"a+"` （打开现有文件以进行读取，并追加所有写入）。

如果 `mode & ios_base::binary` 为非零值，则函数会将 `b` 追加到 `strmode`，以打开二进制流而不是文本流。 然后，它将 `fopen` 返回的值存储 `fp` 的文件指针中。 如果 `mode & ios_base::ate` 为非零值，并且文件指针不是 null 指针，则该函数将调用 `fseek(fp, 0, SEEK_END)` 将流定位到文件末尾。 如果该定位操作失败，该函数将调用[`close`](#close) `(fp)` 并将 null 指针存储在文件指针中。

如果文件指针不是 null 指针，该函数将确定文件转换方面： `use_facet<codecvt<Char_T, char, traits_type::`[ `state_type`](../standard-library/char-traits-struct.md#state_type) `> >(`[ `getloc`](../standard-library/basic-streambuf-class.md#getloc) `)`，以供[下溢](#underflow)和[溢出](#overflow)使用。

如果文件指针为 null 指针，则该函数返回 null 指针。 否则，返回 **this**。

### <a name="example"></a>示例

有关使用 `open` 的示例，请参阅[`basic_filebuf::close`](#close) 。

## <a name="op_eq"></a>  basic_filebuf::operator=

分配此流缓冲区对象的内容。 这是涉及不会留下副本的右值的移动赋值。

```cpp
basic_filebuf& operator=(basic_filebuf&& right);
```

### <a name="parameters"></a>参数

*right* \
对 [basic_filebuf](../standard-library/basic-filebuf-class.md) 对象的右值引用。

### <a name="return-value"></a>返回值

返回 __* this__。

### <a name="remarks"></a>备注

成员运算符使用*right*的内容替换对象的内容，并将其视为右值引用。 有关详细信息，请参阅[右值引用声明符： & &](../cpp/rvalue-reference-declarator-amp-amp.md)。

## <a name="overflow"></a>  basic_filebuf::overflow

当新字符插入到已满缓冲区时调用。

```cpp
virtual int_type overflow(int_type _Meta = traits_type::eof);
```

### <a name="parameters"></a>参数

*_Meta* \
要插入到缓冲区或 `traits_type::eof` 中的字符。

### <a name="return-value"></a>返回值

如果该函数不能成功，它将返回 `traits_type::eof`。 否则，它将返回 `traits_type::`[ `not_eof`](../standard-library/char-traits-struct.md#not_eof) `(_Meta)`。

### <a name="remarks"></a>备注

如果 `_Meta != traits_type::`[ `eof`](../standard-library/char-traits-struct.md#eof)，受保护的虚拟成员函数尝试将元素 `ch = traits_type::`[ `to_char_type`](../standard-library/char-traits-struct.md#to_char_type) `(_Meta)` 插入到输出缓冲区。 它可以用多种方法执行此操作：

- 如果写入位置可用，它可将元素存储到写入位置并递增输出缓冲区的下一个指针。

- 它可以通过为输出缓冲区分配新的或额外的存储空间，提供写入位置。

- 它可以在输出缓冲区中转换任何挂起的输出，然后在 `ch` 的情况下，使用文件转换方面 `fac` 根据需要调用 `fac.out`。 *Char*类型的每个生成的元素 `ch` 都将写入文件指针所指定的关联流 `fp` 就像通过对窗体 `fputc(ch, fp)` 的连续调用一样。 如果任何转换或写入失败，该函数不会成功。

## <a name="pbackfail"></a>  basic_filebuf::pbackfail

尝试将元素放回到输入流中，随后使它成为当前元素（由下一个指针指向）。

```cpp
virtual int_type pbackfail(int_type _Meta = traits_type::eof);
```

### <a name="parameters"></a>参数

*_Meta* \
要插入到缓冲区的字符或 `traits_type::eof`。

### <a name="return-value"></a>返回值

如果该函数不能成功，它将返回 `traits_type::eof`。 否则，它将返回 `traits_type::`[ `not_eof`](../standard-library/char-traits-struct.md#not_eof) `(_Meta)`。

### <a name="remarks"></a>备注

受保护虚拟成员函数将元素放回到输入缓冲区中，随后使它成为当前元素（由下一个指针指向）。 如果 `_Meta == traits_type::`[ `eof`](../standard-library/char-traits-struct.md#eof)，要推送回的元素在当前元素之前实际上已是流中的一个元素。 否则，该元素将被 `ch = traits_type::`[ `to_char_type`](../standard-library/char-traits-struct.md#to_char_type) `(_Meta)` 替换。 该函数可以用多种方法放回元素：

- 如果 `putback` 位置可用，且存储在该位置的元素等于 `ch`，则它可以递减输入缓冲区的下一个指针。

- 如果函数可以使 `putback` 位置可用，则可以执行此操作，将下一个指针设置为指向该位置的点，并将 `ch` 存储在该位置。

- 如果函数可以将某个元素推送回输入流，则它可以执行此操作，例如通过对**char**类型的元素调用 `ungetc`。

## <a name="pos_type"></a>  basic_filebuf::pos_type

在 `basic_filebuf` 作用域内使此类型等效于 `Tr` 作用域中具有相同名称的类型。

```cpp
typedef typename traits_type::pos_type pos_type;
```

## <a name="seekoff"></a>  basic_filebuf::seekoff

尝试更改受控制流的当前位置。

```cpp
virtual pos_type seekoff(
    off_type _Off,
    ios_base::seekdir _Way,
    ios_base::openmode _Which = ios_base::in | ios_base::out);
```

### <a name="parameters"></a>参数

*_Off* \
要查找的相对于 *_Way*的位置。

*_Way* \
偏移操作的起点。 请参阅 [seekdir](../standard-library/ios-base-class.md#seekdir)，查看可能的值。

*_Which* \
指定指针位置的模式。 默认值允许修改读取和写入位置。

### <a name="return-value"></a>返回值

返回新位置或无效的流位置。

### <a name="remarks"></a>备注

受保护的虚拟成员函数尝试更改受控流的当前位置。 对于类[`basic_filebuf`](../standard-library/basic-filebuf-class.md) `<Char_T, Tr>` 的对象，流位置可由 `fpos_t` 类型的对象表示，该对象存储偏移量以及分析宽流所需的任何状态信息。 偏移量为零表示流的第一个元素。 （类型[`pos_type`](../standard-library/basic-streambuf-class.md#pos_type)的对象至少存储 `fpos_t` 对象。）

对于打开供读取和写入的文件，输入流和输出流串联放置。 若要在插入和提取之间切换，必须调用[`pubseekoff`](../standard-library/basic-streambuf-class.md#pubseekoff)或[`pubseekpos`](../standard-library/basic-streambuf-class.md#pubseekpos)。 调用 `pubseekoff`（因而调用 `seekoff`）对于[文本流](../c-runtime-library/text-and-binary-streams.md)、[二进制流](../c-runtime-library/text-and-binary-streams.md)和[宽流](../c-runtime-library/byte-and-wide-streams.md)有各种限制。

如果文件指针 `fp` 为 null 指针，则函数将失败。 否则，它会通过调用 `fseek(fp, _Off, _Way)` 来尝试更改流位置。 如果该函数成功并且 `fposn` 可以通过调用 `fgetpos(fp, &fposn)` 确定所得位置则该函数将成功。 如果函数成功，则返回包含 `fposn` 的类型 `pos_type` 的值。 否则，返回一个无效的流位置。

## <a name="seekpos"></a>  basic_filebuf::seekpos

尝试更改受控制流的当前位置。

```cpp
virtual pos_type seekpos(
    pos_type _Sp,
    ios_base::openmode _Which = ios_base::in | ios_base::out);
```

### <a name="parameters"></a>参数

*_Sp* \
要搜寻的位置。

*_Which* \
指定指针位置的模式。 默认值允许修改读取和写入位置。

### <a name="return-value"></a>返回值

如果文件指针 `fp` 为 null 指针，则函数将失败。 否则，它会通过调用 `fsetpos(fp, &fposn)` 来尝试更改流位置，其中 `fposn` 是 `pos` 中存储的 `fpos_t` 对象。 如果该函数成功，则该函数将返回 `pos`。 否则，返回一个无效的流位置。 若要确定流位置是否有效，请比较返回值和 `pos_type(off_type(-1))`。

### <a name="remarks"></a>备注

受保护的虚拟成员函数尝试更改受控流的当前位置。 对于类[`basic_filebuf`](../standard-library/basic-filebuf-class.md) `<Char_T, Tr>` 的对象，流位置可由 `fpos_t` 类型的对象表示，该对象存储偏移量以及分析宽流所需的任何状态信息。 偏移量为零表示流的第一个元素。 （类型为 `pos_type` 的对象存储至少一个 `fpos_t` 对象。）

对于打开供读取和写入的文件，输入流和输出流串联放置。 若要在插入和提取之间切换，必须调用[`pubseekoff`](../standard-library/basic-streambuf-class.md#pubseekoff)或[`pubseekpos`](../standard-library/basic-streambuf-class.md#pubseekpos)。 对文本流、二进制流和宽流的调用 `pubseekoff` （和 `seekoff`）有各种限制。

对于宽流，如果自打开流后，或者自上次调用 `streampos` 后发生任何插入，该函数都将调用 [overflow](#overflow)。 它还会插入还原初始转换状态所需的任何序列，方法是使用文件转换方面 `fac` 按需调用 `fac.unshift`。 **Char**类型的每个生成的元素 `byte` 都将写入文件指针所指定的关联流 `fp` 就像通过对窗体 `fputc(byte, fp)` 的连续调用一样。 如果对 `fac.unshift` 或任何写入操作失败，则该函数不会成功。

## <a name="setbuf"></a>  basic_filebuf::setbuf

执行特定于每个派生流缓冲区的操作。

```cpp
virtual basic_streambuf<Char_T, Tr> *setbuf(
    char_type* _Buffer,
    streamsize count);
```

### <a name="parameters"></a>参数

*_Buffer* \
指向缓冲区的指针。

*计数*\
缓冲区的大小。

### <a name="return-value"></a>返回值

如果文件指针 `fp` 为 null 指针，则受保护成员函数将返回零。

### <a name="remarks"></a>备注

`setbuf` 调用 `setvbuf( fp, (char*) _Buffer, _IOFBF, count * sizeof( Char_T))` 以提供从 *_Buffer*开始的 `count` 元素数组作为流的缓冲区。 如果该函数返回一个非零值，则该函数返回 null 指针。 否则，它将返回 **this** 表示成功。

## <a name="swap"></a>  basic_filebuf::swap

将此 `basic_filebuf` 的内容与提供的 `basic_filebuf` 的内容进行交换。

```cpp
void swap(basic_filebuf& right);
```

### <a name="parameters"></a>参数

*right* \
对另一 `basic_filebuf` 的左值引用。

## <a name="sync"></a>  basic_filebuf::sync

尝试将受控制流与任何关联的外部流同步。

```cpp
virtual int sync();
```

### <a name="return-value"></a>返回值

如果文件指针 `fp` 为 null 指针，则返回零。 否则，仅当对[溢出](#overflow)和 `fflush(fp)` 的调用成功刷新流的任何挂起输出时才返回零。

## <a name="traits_type"></a>  basic_filebuf::traits_type

将类型名与 `Tr` 模板参数关联。

```cpp
typedef Tr traits_type;
```

## <a name="underflow"></a>  basic_filebuf::underflow

从输入流中提取当前元素。

```cpp
virtual int_type underflow();
```

### <a name="return-value"></a>返回值

如果该函数不能成功，它将返回 `traits_type::`[ `eof`](../standard-library/char-traits-struct.md#eof)。 否则，它将返回 `ch`，如 "备注" 部分中所述进行转换。

### <a name="remarks"></a>备注

受保护的虚拟成员函数尝试从输入流中提取当前元素 `ch`，并将该元素作为 `traits_type::`[ `to_int_type`](../standard-library/char-traits-struct.md#to_int_type) `(ch)` 返回。 它可以用多种方法执行此操作：

- 如果读取位置可用，则它会将 `ch` 用作读取位置中存储的元素，并提升输入缓冲区的下一个指针。

- 它可以读取**char**类型的一个或多个元素，就像通过对 `fgetc(fp)` 的形式进行连续调用一样，并使用 "文件转换" facet `fac` 根据需要调用 `fac.in` 来将其转换为类型 `Char_T` 的元素 `ch`。 如果任何读取或转换失败，该函数不会成功。

## <a name="see-also"></a>请参阅

[\<fstream>](../standard-library/fstream.md)\
[C++ 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[iostream 编程](../standard-library/iostream-programming.md)\
[iostreams 约定](../standard-library/iostreams-conventions.md)
