---
description: XAML コントロールに効果的にバインドできるプロパティは、*監視可能な*プロパティと呼ばれます。 このトピックでは、監視可能なプロパティを実装および使用する方法と、XAML コントロールをバインドする方法を示します。
title: 'XAML コントロール: C++/WinRT プロパティへのバインド'
ms.date: 04/24/2019
ms.topic: article
keywords: windows 10, uwp, 標準, c++, cpp, winrt, プロジェクション, XAML, コントロール, バインド, プロパティ
ms.localizationpriority: medium
ms.openlocfilehash: 2fe5c03eebd2b68e98ae908ea4624471fbd2b3d2
ms.sourcegitcommit: d23dab1533893b7fe0f01ca6eb273edfac4705e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65627668"
---
# <a name="xaml-controls-bind-to-a-cwinrt-property"></a>XAML コントロール: C++/WinRT プロパティへのバインド
XAML コントロールに効果的にバインドできるプロパティは、*監視可能な*プロパティと呼ばれます。 この概念は、*オブザーバー パターン*と呼ばれるソフトウェアの設計パターンに基づいています。 このトピックで監視可能なプロパティを実装する方法を示しています。 [C +/cli WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)、および XAML コントロールをバインドする方法。

> [!IMPORTANT]
> C++/WinRT でランタイム クラスを使用および作成する方法についての理解をサポートするために重要な概念と用語については、「[C++/WinRT での API の使用](consume-apis.md)」と「[C++/WinRT での作成者 API](author-apis.md)」を参照してください。

## <a name="what-does-observable-mean-for-a-property"></a>プロパティの*監視可能*とはどういう意味ですか?
たとえば、**BookSku** という名前のランタイム クラスに **Title** という名前のプロパティがあるとします。 **Title** の値が変わるたびに **BookSku** が [**INotifyPropertyChanged::PropertyChanged**](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) イベントを発生させることを選択する場合、**Title** は監視可能なプロパティです。 そのプロパティ (あれば) のどれが監視可能かを決定するのは **BookSku** の動作 (イベントを発生させるまたは発生させない) です。

XAML テキスト要素、またはコントロールでは、更新された値を取得して、新しい値を表示するためにそれ自体を更新することで、これらのイベントをバインドし、処理することができます。

> [!NOTE]
> インストールと使用について、 C++WinRT Visual Studio Extension (VSIX) と (をまとめてプロジェクト テンプレートを提供し、ビルドのサポート)、NuGet パッケージを参照してください。 [Visual Studio のサポートC++/WinRT](intro-to-using-cpp-with-winrt.md#visual-studio-support-for-cwinrt-xaml-the-vsix-extension-and-the-nuget-package)します。

## <a name="create-a-blank-app-bookstore"></a>空のアプリ (Bookstore) を作成する
まず、Microsoft Visual Studio で、新しいプロジェクトを作成します。 作成、**空のアプリ (C++/WinRT)** プロジェクト、および名前を付けます*書店*します。

監視可能なタイトルのプロパティを持つブックを表すための新しいクラスを作成します。 同じコンパイル ユニット内のクラスを作成および使用しています。 ただし、XAML からこのクラスへバインドできるようにしたいため、ランタイム クラスにします。 また、この作成と使用のどちらにも C++/WinRT を使用します。

新しいランタイム クラスの作成の最初の手順では、新しい **Midl ファイル (.idl)** 項目をプロジェクトに追加します。 「`BookSku.idl`」という名前を入力します。 `BookSku.idl` の既定のコンテンツを削除し、このランタイム クラスの宣言に貼り付けます。

```idl
// BookSku.idl
namespace Bookstore
{
    runtimeclass BookSku : Windows.UI.Xaml.Data.INotifyPropertyChanged
    {
        String Title;
    }
}
```

> [!NOTE]
> ビュー モデル クラス&mdash;実際には、アプリケーションで宣言された任意のランタイム クラス&mdash;基底クラスから派生していない必要があります。 **BookSku**上で宣言されたクラスがその例を示します。 インターフェイスを実装しますが、任意の基本クラスから派生していません。
>
> アプリケーションで宣言された任意のランタイム クラスを*は*ベースからの派生クラスと呼ばれる、*コンポーザブル*クラス。 構成可能なクラスに関する制約があります。 アプリケーションに渡す、 [Windows アプリ認定キット](../debug-test-perf/windows-app-certification-kit.md)Visual Studio では、Microsoft Store での送信を検証するために使用するテスト (ため Microsoft Store に正常に取り込まれるアプリケーションの)、コンポーザブル クラスは、Windows の基本クラスから最終的に派生する必要があります。 つまり、継承階層の非常にルートにあるクラスは、Windows.* 名前空間で生成された型である必要があります。 ランタイム クラスを基底クラスから派生する必要は場合&mdash;を実装する例を**BindableBase**クラスから派生するは、ビュー モデルのすべての&mdash;から派生できます[ **Windows.UI.Xaml.DependencyObject**](/uwp/api/windows.ui.xaml.dependencyobject)します。
>
> ビュー モデルは、ビューの抽象化と表示 (XAML マークアップ) に直接バインドされているためです。 データ モデルは、データの抽象化と、ビュー モデルからのみ使用され、XAML に直接バインドされていないことができます。 そのため、ランタイム クラス、としてではなく C++ 構造体またはクラスとしては、データ モデルを宣言できます。 MIDL、内で宣言する必要はありませんし、自由に好きな継承階層を使用します。

ファイルを保存し、プロジェクトをビルドします。 ビルド プロセス中に、`midl.exe` ツールが実行されて、ランタイム クラスを記述する Windows ランタイム メタデータ ファイル (`\Bookstore\Debug\Bookstore\Unmerged\BookSku.winmd`) が作成されます。 次に、`cppwinrt.exe` ツールが実行され、ランタイム クラスの作成と使用をサポートするソース コード ファイルが生成されます。 これらのファイルには、IDL で宣言した **BookSku** ランタイム クラスの実装を開始するためのスタブが含まれています。 これらのスタブは `\Bookstore\Bookstore\Generated Files\sources\BookSku.h` と `BookSku.cpp` です。

プロジェクト ノードを右クリックし、をクリックして**ファイル エクスプ ローラーでフォルダーを開く**します。 これは、ファイル エクスプ ローラーでプロジェクト フォルダーを開きます。 スタブ ファイルをコピー、`BookSku.h`と`BookSku.cpp`から、`\Bookstore\Bookstore\Generated Files\sources\`フォルダー、プロジェクト フォルダーにある`\Bookstore\Bookstore\`します。 **ソリューション エクスプ ローラー**、プロジェクト ノードを選択したことを確認します**すべてのファイル**がオンにします。 コピーしたスタブ ファイルを右クリックし、**[プロジェクトに含める]** をクリックします。

## <a name="implement-booksku"></a>**BookSku** を実装する
ここで、`\Bookstore\Bookstore\BookSku.h` と `BookSku.cpp` を開いてランタイム クラスを実装してみましょう。 `BookSku.h` で、[**winrt::hstring**](/uwp/cpp-ref-for-winrt/hstring) を取るコンストラクター、タイトル文字列を格納するためのプライベート メンバー、およびタイトルが変更されたときに発生させるイベントのための別のプライベート メンバーを追加します。 これらの変更を行った後、`BookSku.h`ようになります。

```cppwinrt
// BookSku.h
#pragma once
#include "BookSku.g.h"

namespace winrt::Bookstore::implementation
{
    struct BookSku : BookSkuT<BookSku>
    {
        BookSku() = delete;
        BookSku(winrt::hstring const& title);

        winrt::hstring Title();
        void Title(winrt::hstring const& value);
        winrt::event_token PropertyChanged(Windows::UI::Xaml::Data::PropertyChangedEventHandler const& value);
        void PropertyChanged(winrt::event_token const& token);
    
    private:
        winrt::hstring m_title;
        winrt::event<Windows::UI::Xaml::Data::PropertyChangedEventHandler> m_propertyChanged;
    };
}
```

`BookSku.cpp` では、次のように関数を実装します。

```cppwinrt
// BookSku.cpp
#include "pch.h"
#include "BookSku.h"
#include "BookSku.g.cpp"

namespace winrt::Bookstore::implementation
{
    BookSku::BookSku(winrt::hstring const& title) : m_title{ title }
    {
    }

    winrt::hstring BookSku::Title()
    {
        return m_title;
    }

    void BookSku::Title(winrt::hstring const& value)
    {
        if (m_title != value)
        {
            m_title = value;
            m_propertyChanged(*this, Windows::UI::Xaml::Data::PropertyChangedEventArgs{ L"Title" });
        }
    }

    winrt::event_token BookSku::PropertyChanged(Windows::UI::Xaml::Data::PropertyChangedEventHandler const& handler)
    {
        return m_propertyChanged.add(handler);
    }

    void BookSku::PropertyChanged(winrt::event_token const& token)
    {
        m_propertyChanged.remove(token);
    }
}
```

**タイトル**かどうか、値が設定されていますが、現在の値を異なるを確認しましたミューテーターの関数。 そのため、タイトルを更新するとを発生させることも、 [ **INotifyPropertyChanged::PropertyChanged** ](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged)変更されたプロパティの名前と同じ引数を持つイベント。 これにより、ユーザー インターフェイス (UI) はどのプロパティの値を再クエリするのか分かるようになります。

## <a name="declare-and-implement-bookstoreviewmodel"></a>**BookstoreViewModel** を宣言および実装する
メイン XAML ページが、メイン ビュー モデルにバインドします。 またそのビュー モデルは、**BookSku** 型のいずれかを含む、いくつかのプロパティを持つようになります。 この手順では、メイン ビュー モデル ランタイム クラスを宣言および実装します。

`BookstoreViewModel.idl` という名前の新しい **Midl ファイル (.idl)** 項目を追加します。

```idl
// BookstoreViewModel.idl
import "BookSku.idl";

namespace Bookstore
{
    runtimeclass BookstoreViewModel
    {
        BookSku BookSku{ get; };
    }
}
```

保存してビルドします。 `Generated Files\sources` フォルダーから `BookstoreViewModel.h` と `BookstoreViewModel.cpp` をプロジェクト フォルダーにコピーし、プロジェクトに追加します。 これらのファイルを開き、次に示すように、ランタイム クラスを実装します。 注方法で、 `BookstoreViewModel.h`、含まれています`BookSku.h`の実装の種類を宣言する**BookSku** (これは**winrt::Bookstore::implementation::BookSku**)。 削除する予定していると`= default`既定のコンス トラクターから。

```cppwinrt
// BookstoreViewModel.h
#pragma once
#include "BookstoreViewModel.g.h"
#include "BookSku.h"

namespace winrt::Bookstore::implementation
{
    struct BookstoreViewModel : BookstoreViewModelT<BookstoreViewModel>
    {
        BookstoreViewModel();

        Bookstore::BookSku BookSku();

    private:
        Bookstore::BookSku m_bookSku{ nullptr };
    };
}
```

```cppwinrt
// BookstoreViewModel.cpp
#include "pch.h"
#include "BookstoreViewModel.h"
#include "BookstoreViewModel.g.cpp"

namespace winrt::Bookstore::implementation
{
    BookstoreViewModel::BookstoreViewModel()
    {
        m_bookSku = winrt::make<Bookstore::implementation::BookSku>(L"Atticus");
    }

    Bookstore::BookSku BookstoreViewModel::BookSku()
    {
        return m_bookSku;
    }
}
```

> [!NOTE]
> 型`m_bookSku`射影の型は、(**winrt::Bookstore::BookSku**) とで使用するテンプレート パラメーター [ **winrt::make** ](/uwp/cpp-ref-for-winrt/make)が、実装の種類 (**winrt::Bookstore::implementation::BookSku**)。 この場合も、**[make]** は投影型のインスタンスを返します。

## <a name="add-a-property-of-type-bookstoreviewmodel-to-mainpage"></a>**BookstoreViewModel** 型のプロパティを **MainPage** に追加する
`MainPage.idl` を開きます。ここでメインの UI ページを表すランタイム クラスを宣言しています。 インポート ステートメントを追加して `BookstoreViewModel.idl` をインポートし、**BookstoreViewModel** 型の MainViewModel という名前の読み取り専用プロパティを追加します。 削除しても、 **MyProperty**プロパティ。 また、`import`ディレクティブでは、以下のリスト。

```idl
// MainPage.idl
import "BookstoreViewModel.idl";

namespace Bookstore
{
    runtimeclass MainPage : Windows.UI.Xaml.Controls.Page
    {
        MainPage();
        BookstoreViewModel MainViewModel{ get; };
    }
}
```

ファイルを保存します。 現時点では、完了するまで、プロジェクトをビルドしませんをソース コード ファイルを再生成しているため、有用なことは、今すぐ構築、 **MainPage**ランタイム クラスが実装されている (`\Bookstore\Bookstore\Generated Files\sources\MainPage.h`と`MainPage.cpp`)。 これを今すぐビルドしてみてください。 この段階で表示するビルド エラーが **'MainViewModel': 'winrt::Bookstore::implementation::MainPage' のメンバーではない**します。

Include を省略した場合`BookstoreViewModel.idl`(の一覧を参照してください`MainPage.idl`上)、エラーが表示されます**を指定してください\<"MainViewModel"近く**。 別のヒントは、同じ名前空間のすべての種類のままにすることを確認する: コードの一覧に表示される名前空間。

表示される予定ですエラーを解決するようになりましたする必要がありますのアクセサーのスタブをコピー、 **MainViewModel**生成されたファイルからのプロパティ (`\Bookstore\Bookstore\Generated Files\sources\MainPage.h`と`MainPage.cpp`) に`\Bookstore\Bookstore\MainPage.h`と`MainPage.cpp`します。 そのための手順は次に説明します。

`\Bookstore\Bookstore\MainPage.h`、含める`BookstoreViewModel.h`の実装の種類を宣言する**BookstoreViewModel** (これは**winrt::Bookstore::implementation::BookstoreViewModel**)。 ビュー モデルを格納するプライベート メンバーを追加します。 プロパティのアクセサー関数 (およびメンバー m_mainViewModel) が、射影された型の観点から実装されることに注意してください。 **BookstoreViewModel** (これは**Bookstore::BookstoreViewModel**)。 M_mainViewModel を受け取るコンス トラクター オーバー ロードを使用して作成するため、アプリケーションと同じプロジェクト (コンパイル単位) での実装の種類は`nullptr_t`します。 削除しても、 **MyProperty**プロパティ。

```cppwinrt
// MainPage.h
...
#include "BookstoreViewModel.h"
...
namespace winrt::Bookstore::implementation
{
    struct MainPage : MainPageT<MainPage>
    {
        MainPage();

        Bookstore::BookstoreViewModel MainViewModel();

        void ClickHandler(Windows::Foundation::IInspectable const&, Windows::UI::Xaml::RoutedEventArgs const&);

    private:
        Bookstore::BookstoreViewModel m_mainViewModel{ nullptr };
    };
}
...
```

`\Bookstore\Bookstore\MainPage.cpp`、呼び出す[ **winrt::make** ](/uwp/cpp-ref-for-winrt/make) (実装の種類) で m_mainViewModel に射影された型の新しいインスタンスを割り当てる。 ブックのタイトルの初期値を割り当てます。 MainViewModel プロパティのアクセサーを実装します。 最後に、ボタンのイベント ハンドラーでブックのタイトルを更新します。 削除しても、 **MyProperty**プロパティ。

```cppwinrt
// MainPage.cpp
#include "pch.h"
#include "MainPage.h"
#include "MainPage.g.cpp"

using namespace winrt;
using namespace Windows::UI::Xaml;

namespace winrt::Bookstore::implementation
{
    MainPage::MainPage()
    {
        m_mainViewModel = winrt::make<Bookstore::implementation::BookstoreViewModel>();
        InitializeComponent();
    }

    void MainPage::ClickHandler(Windows::Foundation::IInspectable const& /* sender */, Windows::UI::Xaml::RoutedEventArgs const& /* args */)
    {
        MainViewModel().BookSku().Title(L"To Kill a Mockingbird");
    }

    Bookstore::BookstoreViewModel MainPage::MainViewModel()
    {
        return m_mainViewModel;
    }
}
```

## <a name="bind-the-button-to-the-title-property"></a>**Title** プロパティにボタンをバインドする
メイン UI ページの XAML マークアップが含まれている `MainPage.xaml` を開きます。 次の一覧に示すように、ボタンから名前を削除し、変更、**コンテンツ**バインディング式にリテラルからプロパティ値。 バインド式の `Mode=OneWay` プロパティをメモします (ビュー モデルから UI へ一方向)。 そのプロパティが無いと、UI はプロパティの変更イベントに応答しません。

```xaml
<Button Click="ClickHandler" Content="{x:Bind MainViewModel.BookSku.Title, Mode=OneWay}"/>
```

ここでプロジェクトをビルドして実行します。 ボタンをクリックして**クリック** イベント ハンドラーを実行します。 そのハンドラーがブックのタイトル ミューテーター関数を呼び出します。そのミューテーターがイベントを発生させるので、UI は **Title** プロパティが変更されたことがわかります。ボタンはそのプロパティの値を再クエリして、そのボタンの **Content** 値を更新します。

## <a name="using-the-binding-markup-extension-with-cwinrt"></a>{バインド} マークアップ拡張機能を使用して c++/cli WinRT
現在リリースされているバージョンの C++/cli を実装する必要があります {binding} マークアップ拡張機能を使用するには、WinRT、 [ICustomPropertyProvider](/uwp/api/windows.ui.xaml.data.icustompropertyprovider)と[ICustomProperty](/uwp/api/windows.ui.xaml.data.icustomproperty)インターフェイス。

## <a name="important-apis"></a>重要な API
* [INotifyPropertyChanged::PropertyChanged](/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged)
* [winrt::make 関数テンプレート](/uwp/cpp-ref-for-winrt/make)

## <a name="related-topics"></a>関連トピック
* [C++/WinRT で API を使用する](consume-apis.md)
* [C++/WinRT で API を作成する](author-apis.md)
