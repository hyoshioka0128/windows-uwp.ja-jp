---
description: With C++/WinRT では、標準的な C++ ワイド文字列型を使用して Windows ランタイム API を呼び出すか、または winrt::hstring 型を使用することができます。
title: C++/WinRT での文字列の処理
ms.date: 04/23/2019
ms.topic: article
keywords: Windows 10、uwp、標準、c++、cpp、winrt、プロジェクション、文字列
ms.localizationpriority: medium
ms.openlocfilehash: 56b75710c2d259e59dac476bcb860a5e4c6938d6
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89154396"
---
# <a name="string-handling-in-cwinrt"></a>C++/WinRT での文字列の処理

[C++/WinRT](./intro-to-using-cpp-with-winrt.md) では、C++ 標準ライブラリの **std::wstring** などのワイド文字列型 (注: **std::string** などのナロー文字列ではない) を使用して Windows ランタイム API を呼び出すことができます。 C++/WinRT には [**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring) というカスタム文字列型があります (C++/WinRT 基本ライブラリ、`%WindowsSdkDir%Include\<WindowsTargetPlatformVersion>\cppwinrt\winrt\base.h` で定義)。 これは、Windows ランタイムのコンストラクター、関数、およびプロパティで実際に受け取られ、返される文字列型です。 ただし、多くの場合、**hstring** の変換コンストラクターと変換演算子のおかげで、ご自分のクライアント コードで **hstring** を認識するかどうかを選択できます。 API を*作成している*場合は、**hstring** を理解しておく必要性が高くなると思われます。

C++ には多くの文字列型があります。 C++ 標準ライブラリの **std::basic_string** に加えて、多くのライブラリにバリアントが存在します。 C++17 には、すべての文字列型間のギャップの橋渡しをする文字列変換ユーティリティと **std::basic_string_view** があります。  [**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring) は **std::wstring_view** と互換性があり、これにより **std::basic_string_view** の設計目的である相互運用性が提供されます。

## <a name="using-stdwstring-and-optionally-winrthstring-with-uri"></a>**Uri** での **std::wstring** (および必要に応じて **winrt::hstring**) の使用
[**Windows::Foundation::Uri**](/uwp/api/windows.foundation.uri) は [**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring) から作成されます。

```cppwinrt
public:
    Uri(winrt::hstring uri) const;
```

ただし、**hstring** には[変換コンストラクター](/uwp/cpp-ref-for-winrt/hstring#hstringhstring-constructor)があるため、それを意識せずに操作することができます。 次のコード例で、ワイド文字列リテラル、ワイド文字列ビュー、および **std::wstring** から **Uri** を作成する方法を示します。

```cppwinrt
#include <winrt/Windows.Foundation.h>
#include <string_view>

using namespace winrt;
using namespace Windows::Foundation;

int main()
{
    using namespace std::literals;

    winrt::init_apartment();

    // You can make a Uri from a wide string literal.
    Uri contosoUri{ L"http://www.contoso.com" };

    // Or from a wide string view.
    Uri contosoSVUri{ L"http://www.contoso.com"sv };

    // Or from a std::wstring.
    std::wstring wideString{ L"http://www.adventure-works.com" };
    Uri awUri{ wideString };
}
```

プロパティ アクセサー [**Uri::Domain**](/uwp/api/windows.foundation.uri.Domain) の型は **hstring** です。

```cppwinrt
public:
    winrt::hstring Domain();
```

ただし、この場合も、**hstring** の [**std::wstring_view への変換演算子**](/uwp/cpp-ref-for-winrt/hstring#hstringoperator-stdwstring_view)のおかげで、その詳細を認識するかどうかは任意です。

```cppwinrt
// Access a property of type hstring, via a conversion operator to a standard type.
std::wstring domainWstring{ contosoUri.Domain() }; // L"contoso.com"
domainWstring = awUri.Domain(); // L"adventure-works.com"

// Or, you can choose to keep the hstring unconverted.
hstring domainHstring{ contosoUri.Domain() }; // L"contoso.com"
domainHstring = awUri.Domain(); // L"adventure-works.com"
```

同様に、[**IStringable::ToString**](/windows/desktop/api/windows.foundation/nf-windows-foundation-istringable-tostring) は hstring を返します。

```cppwinrt
public:
    hstring ToString() const;
```

**Uri** は [**IStringable**](/windows/desktop/api/windows.foundation/nn-windows-foundation-istringable) インターフェイスを実装しています。

```cppwinrt
// Access hstring's IStringable::ToString, via a conversion operator to a standard type.
std::wstring tostringWstring{ contosoUri.ToString() }; // L"http://www.contoso.com/"
tostringWstring = awUri.ToString(); // L"http://www.adventure-works.com/"

// Or you can choose to keep the hstring unconverted.
hstring tostringHstring{ contosoUri.ToString() }; // L"http://www.contoso.com/"
tostringHstring = awUri.ToString(); // L"http://www.adventure-works.com/"
```

[  **hstring::c_str 関数**](/uwp/cpp-ref-for-winrt/hstring#hstringc_str-function)を使用して、**hstring** から標準ワイド文字列を取得することができます (**std::wstring** から取得する場合と同様)。

```cppwinrt
#include <iostream>
std::wcout << tostringHstring.c_str() << std::endl;
```
**hstring** がある場合、そこから **Uri** を作成することができます。

```cppwinrt
Uri awUriFromHstring{ tostringHstring };
```

**hstring** を受け取るメソッドを考えてみます。

```cppwinrt
public:
    Uri CombineUri(winrt::hstring relativeUri) const;
```

そのような場合にも、前述したすべてのオプションが適用されます。

```cppwinrt
std::wstring contact{ L"contact" };
contosoUri = contosoUri.CombineUri(contact);
    
std::wcout << contosoUri.ToString().c_str() << std::endl;
```

**hstring** は、メンバー **std::wstring_view** という変換演算子を持っており、コストを伴わずに変換が実行されます。

```cppwinrt
void legacy_print(std::wstring_view view);

void Print(winrt::hstring const& hstring)
{
    legacy_print(hstring);
}
```

## <a name="winrthstring-functions-and-operators"></a>**winrt::hstring** の関数と演算子
コンストラクター、演算子、関数、および反復子のホストが [**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring) に対して実装されています。

**hstring** は範囲であるため、範囲ベースの `for`、または `std::for_each` で使用できます。 C++ 標準ライブラリ内の対応部分と自然かつ効率的に比較するための比較演算子も提供されます。 また、関連コンテナーのキーとして **hstring** を使用するために必要なものがすべて含まれています。

多くの C++ ライブラリが **std::string** を使用し、UTF-8 テキストでのみ動作することは認識されています。 利便性を考慮して、双方向に変換するための [**winrt::to_string**](/uwp/cpp-ref-for-winrt/to-string) や [**winrt::to_hstring**](/uwp/cpp-ref-for-winrt/to-hstring) などのヘルパーが提供されています。

`WINRT_ASSERT` はマクロ定義であり、[_ASSERTE](/cpp/c-runtime-library/reference/assert-asserte-assert-expr-macros) に展開されます。

```cppwinrt
winrt::hstring w{ L"Hello, World!" };

std::string c = winrt::to_string(w);
WINRT_ASSERT(c == "Hello, World!");

w = winrt::to_hstring(c);
WINRT_ASSERT(w == L"Hello, World!");
```

**hstring** の関数および演算子のその他の例および詳細については、[**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring) API リファレンス トピックをご覧ください。

## <a name="the-rationale-for-winrthstring-and-winrtparamhstring"></a>**winrt::hstring** および **winrt::param::hstring** の原理
Windows ランタイムは **wchar_t** 文字によって実装されていますが、Windows ランタイムのアプリケーション バイナリ インターフェイス (ABI) は **std::wstring** や **std::wstring_view** が提供するもののサブセットではありません。 これらを使用すると、効率が大幅に低下します。 代わりに、C++/WinRT は **winrt::hstring** を提供します。これは、基礎となる [HSTRING](/windows/desktop/WinRT/hstring) と互換性がある不変文字列を表し、**std::wstring** の場合と同様にインターフェイスの背後に実装されています。 

論理的に **winrt::hstring** を受け入れるはずの C++/WinRT 入力パラメーターが、実際には **winrt::param::hstring** を予期している場合があります。 **param** 名前空間には、自然に C++ 標準ライブラリにバインドしてコピーやその他の非効率性を回避するために、入力パラメーターの最適化にのみ使用される一連の型が含まれています。 これらの型は直接使用しないでください。 独自の関数で最適化を使用する場合は、**std::wstring_view** を使用します。 「[ABI 境界へのパラメーターの受け渡し](./pass-parms-to-abi.md)」もご覧ください。

重要なことは、Windows ランタイムの文字列管理の詳細はほとんど無視して、自分が理解していることを効率的に操作することができるということです。 また、これは Windows ランタイムで文字列を大量に使用する場合は重要になります。

## <a name="formatting-strings"></a>文字列の書式設定
文字列の書式設定のための 1 つのオプションは **std::wostringstream** です。 次の例では、単純なデバッグ トレース メッセージを書式設定して表示します。

```cppwinrt
#include <sstream>
#include <winrt/Windows.UI.Input.h>
#include <winrt/Windows.UI.Xaml.Input.h>
...
void MainPage::OnPointerPressed(winrt::Windows::UI::Xaml::Input::PointerRoutedEventArgs const& e)
{
    winrt::Windows::Foundation::Point const point{ e.GetCurrentPoint(nullptr).Position() };
    std::wostringstream wostringstream;
    wostringstream << L"Pointer pressed at (" << point.X << L"," << point.Y << L")" << std::endl;
    ::OutputDebugString(wostringstream.str().c_str());
}
```

## <a name="the-correct-way-to-set-a-property"></a>プロパティを設定する正しい方法

setter 関数に値渡しでプロパティを設定します。 次に例を示します。

```cppwinrt
// The right way to set the Text property.
myTextBlock.Text(L"Hello!");
```

次のコードは正しくありません。 コンパイルはされますが、行われることは、**Text()** アクセサー関数によって返される一時的な **winrt::hstring** を変更した後、結果を破棄するだけです。

```cppwinrt
// *Not* the right way to set the Text property.
myTextBlock.Text() = L"Hello!";
```

## <a name="important-apis"></a>重要な API
* [winrt::hstring 構造体](/uwp/cpp-ref-for-winrt/hstring)
* [winrt::to_hstring function](/uwp/cpp-ref-for-winrt/to-hstring)
* [winrt::to_string function](/uwp/cpp-ref-for-winrt/to-string)