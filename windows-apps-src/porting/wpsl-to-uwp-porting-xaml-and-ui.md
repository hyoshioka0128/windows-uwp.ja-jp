---
description: 宣言型 XAML マークアップ形式での UI の定義は、Windows Phone Silverlight からユニバーサル Windows プラットフォーム (UWP) アプリに非常に適切に変換されます。
title: Windows Phone Silverlight の XAML と UI の UWP への移植
ms.assetid: 49aade74-5dc6-46a5-89ef-316dbeabbebe
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 9a6f78d30b1366078f2094aa17ab15c65a050c43
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89164346"
---
#  <a name="porting-windowsphone-silverlight-xaml-and-ui-to-uwp"></a>Windows Phone Silverlight の XAML と UI の UWP への移植



前のトピックでは、 [トラブルシューティング](wpsl-to-uwp-troubleshooting.md)を行っていました。

宣言型 XAML マークアップ形式での UI の定義は、Windows Phone Silverlight からユニバーサル Windows プラットフォーム (UWP) アプリに非常に適切に変換されます。 システムのリソース キーの参照の更新、いくつかの要素型名の変更、"clr-namespace" から "using" への変更を行うことによって、大きなマークアップ セクションで互換性が得られることがわかります。 プレゼンテーション層のビュー モデルの命令型コード、および UI 要素を操作するコードの大半でも、簡単に移植できます。

## <a name="a-first-look-at-the-xaml-markup"></a>初めての XAML マークアップ

前のトピックでは、新しい Windows 10 の Visual Studio プロジェクトに XAML と分離コード ファイルをコピーする方法について説明しました。 Visual Studio XAML デザイナーで強調表示され、認識される最初の問題の 1 つは、XAML ファイルのルートで `PhoneApplicationPage` 要素がユニバーサル Windows プラットフォーム (UWP) プロジェクトに対して有効ではないことです。 前のトピックでは、Windows 10 プロジェクトの作成時に Visual Studio で生成される XAML ファイルのコピーを保存しました。 MainPage.xaml の該当バージョンを開くと、ルートに [**Windows.UI.Xaml.Controls**](/uwp/api/Windows.UI.Xaml.Controls) 名前空間の [**Page**](/uwp/api/Windows.UI.Xaml.Controls.Page) 型があることに気付きます。 したがって、すべての `<phone:PhoneApplicationPage>` 要素を `<Page>` に変更できます (プロパティ要素の構文を忘れないでください)。また、`xmlns:phone` 宣言は削除できます。

Silverlight 型 Windows Phone に対応する UWP 型を検索するための一般的な方法については、「 [名前空間とクラスのマッピング](wpsl-to-uwp-namespace-and-class-mappings.md)」を参照してください。

## <a name="xaml-namespace-prefix-declarations"></a>XAML 名前空間のプレフィックス宣言


ビュー (ビュー モデル インスタンスまたは値コンバーターなど) でカスタム型のインスタンスを使う場合、XAML マークアップに XAML 名前空間のプレフィックス宣言が含まれます。 これらの構文は、Windows Phone Silverlight と UWP で異なります。 次に例をいくつか示します。

```xml
    xmlns:ContosoTradingCore="clr-namespace:ContosoTradingCore;assembly=ContosoTradingCore"
    xmlns:ContosoTradingLocal="clr-namespace:ContosoTradingLocal"
```

"clr-namespace" を "using" に変更し、アセンブリ トークンとセミコロンを削除します (アセンブリが推論されます)。 結果は次のようになります。

```xml
    xmlns:ContosoTradingCore="using:ContosoTradingCore"
    xmlns:ContosoTradingLocal="using:ContosoTradingLocal"
```

システムによって種類が定義されるリソースが存在する場合があります。

```xml
    xmlns:System="clr-namespace:System;assembly=mscorlib"
    /* ... */
    <System:Double x:Key="FontSizeLarge">40</System:Double>
```

UWP で、"System" プレフィックス宣言を省略し、(既に宣言されている) "x" プレフィックスを代わりに使います。

```xml
    <x:Double x:Key="FontSizeLarge">40</x:Double>
```

## <a name="imperative-code"></a>命令型コード


ビュー モデルは、UI の種類を参照する命令型コードが存在する場所の 1 つです。 もう 1 つの場所は、UI 要素を直接操作するコード ビハインド ファイルです。 たとえば、次のようなコード行がまだコンパイルされていないことに気が付くことがあります。


```csharp
    return new BitmapImage(new Uri(this.CoverImagePath, UriKind.Relative));
```

**BitmapImage** は Windows Phone Silverlight 内の **System.Windows.Media.Imaging** 名前空間にあり、同じファイル内の using ディレクティブによって、前記のスニペットのように、名前空間の認定資格なしに **BitmapImage** を使うことができます。 同様の場合に、Visual Studio で型名 (**BitmapImage**) を右クリックし、コンテキスト メニューの [**解決**] コマンドを使って新しい名前空間のディレクティブをファイルに追加できます。 この場合、該当する型が UWP に存在している、[**Windows.UI.Xaml.Media.Imaging**](/uwp/api/Windows.UI.Xaml.Media.Imaging) 名前空間が追加されます。 **System.Windows.Media.Imaging** の using ディレクティブは削除できます。また、前記のスニペットのようなコードの移植で必要になるのはこれだけです。 これによって、Windows Phone Silverlight 名前空間がすべて削除されます。

古い名前空間の型を新しい名前空間の同じ型でマッピングするこのような簡単なケースでは、ソース コードに一括変更を加えるために、Visual Studio の [**検索と置換**] コマンドを使うこともできます。 [**解決**] コマンドは、型の新しい名前空間を検索するための効果的な方法です。 別の例として、すべての "System.Windows" を "Windows.UI.Xaml" に置換できます。 これによって基本的には、該当する名前空間を参照するすべての using ディレクティブおよび完全修飾されたすべての型名が移植されます。

古い using ディレクティブをすべて削除し、新しい using ディレクティブを追加したら、Visual Studio の [**using の整理**] コマンドを使ってディレクティブを並べ替えて、未使用のディレクティブを削除できます。

命令型コードの修正がパラメーターの型の変更のみになることもあります。 または、.NET Api ではなく、Windows ランタイム Api を使用して Windows ランタイム2.x アプリを使用する必要があります。 サポートされている Api を特定するには、この移植ガイドの残りの部分を [Windows ランタイム 8. x アプリの概要](/previous-versions/windows/apps/br230302(v=vs.140)) と [Windows ランタイムリファレンス](/uwp/api/)の .net と組み合わせて使用します。

また、プロジェクトのビルド段階にただ進むだけであれば、重要でないコードをコメントアウトするか、スタブを挿入できます。 次に、このセクションの以降のトピック (および前のトピック「[トラブルシューティング](wpsl-to-uwp-troubleshooting.md)」) を参考にして、ビルドとランタイムの問題が解決して移植が完了するまで一度に 1 つの問題について反復作業を行います。

## <a name="adaptiveresponsive-ui"></a>アダプティブ/応答性の高い UI

Window 10 アプリは潜在的に多様なデバイス (それぞれ独自の画面サイズと解像度を持つ) で実行できるため、最小限の手順でアプリを移植するだけでなく、各デバイスで最適な外観になるように UI を調整できます。 アダプティブな Visual State Manager の機能を使って、ウィンドウのサイズを動的に検出し、それに応じてレイアウトを変更できます。その方法を示す例を、Bookstore2 ケース スタディの「[アダプティブ UI](wpsl-to-uwp-case-study-bookstore2.md)」に示します。

## <a name="alarms-and-reminders"></a>アラームとリマインダー

**Alarm** クラスまたは **Reminder** クラスを使うコードは、バックグラウンド タスクを作成、登録して、関連する時間にトーストを表示するために、[**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) クラスを使って移植します。 「[バックグラウンド処理](wpsl-to-uwp-business-and-data.md)」と「[トースト](#toasts)」をご覧ください。

## <a name="animation"></a>アニメーション

キーフレーム アニメーションと from/to アニメーションに対して推奨される代替機能として、UWP アプリで UWP アニメーション ライブラリが利用できるようになりました。 こうしたアニメーションはスムーズかつ適切に表示されるように設計、調整されているために、組み込みのアプリのように Windows に統合されてアプリが動作します。 「[クイック スタート: ライブラリのアニメーションを使った UI のアニメーション化](/previous-versions/windows/apps/hh452703(v=win.10))」をご覧ください。

UWP アプリでキーフレーム アニメーションまたは from/to アニメーションを使う場合、新しいプラットフォームで導入された独立型アニメーションと依存型アニメーションの相違について理解することをお勧めします。 「[アニメーションとメディアの最適化](../debug-test-perf/optimize-animations-and-media.md)」をご覧ください。 UI スレッドで実行するアニメーション (たとえば、レイアウト プロパティをアニメーションするもの) は、依存型アニメーションと呼ばれ、新しいプラットフォーム上での実行時に、次の 2 つのいずれかを行わなければ無効になります。 いずれも、異なるプロパティ ([**RenderTransform**](/uwp/api/windows.ui.xaml.uielement.rendertransform) など) をアニメーションするためにターゲットを変更できるので、独立型にできます。 アニメーション要素で `EnableDependentAnimation="True"` を設定することによって、スムーズな実行を保証できないアニメーションを実行する意図を確認できます。 新しいアニメーションの作成のために Blend for Visual Studio を使っている場合、必要であればこのプロパティが自動的に設定されます。

## <a name="back-button-handling"></a>"戻る" ボタンの処理

Windows 10 アプリでは、単一のアプローチで "戻る" ボタンを処理し、すべてのデバイスに適用できます。 モバイル デバイスでは、このボタンはデバイス上の静電容量式のボタンまたはシェル内のボタンとして提供されます。 デスクトップ デバイスでは、アプリ内で戻るナビゲーションが可能な場合には常にアプリのクロムにボタンを追加します。このボタンは、ウィンドウ表示されたアプリのタイトル バーまたはタブレット モードのタスク バーに表示されます。 "戻る" ボタンのイベントはすべてのデバイス ファミリに共通するユニバーサルな概念であり、ハードウェアまたはソフトウェアに実装されるボタンは同じ [**BackRequested**](/uwp/api/windows.ui.core.systemnavigationmanager.backrequested) イベントを発生させます。

次の例は、すべてのデバイス ファミリについて機能し、同じ処理をすべてのページに適用し、ナビゲーションを確認する必要がない場合 (未保存の変更に関する警告を表示するなど) に適しています。

```csharp
   // app.xaml.cs

    protected override void OnLaunched(LaunchActivatedEventArgs e)
    {
        [...]

        Windows.UI.Core.SystemNavigationManager.GetForCurrentView().BackRequested += App_BackRequested;
        rootFrame.Navigated += RootFrame_Navigated;
    }

    private void RootFrame_Navigated(object sender, NavigationEventArgs e)
    {
        Frame rootFrame = Window.Current.Content as Frame;

        // Note: On device families that have no title bar, setting AppViewBackButtonVisibility can safely execute 
        // but it will have no effect. Such device families provide a back button UI for you.
        if (rootFrame.CanGoBack)
        {
            Windows.UI.Core.SystemNavigationManager.GetForCurrentView().AppViewBackButtonVisibility = 
                Windows.UI.Core.AppViewBackButtonVisibility.Visible;
        }
        else
        {
            Windows.UI.Core.SystemNavigationManager.GetForCurrentView().AppViewBackButtonVisibility = 
                Windows.UI.Core.AppViewBackButtonVisibility.Collapsed;
        }
    }

    private void App_BackRequested(object sender, Windows.UI.Core.BackRequestedEventArgs e)
    {
        Frame rootFrame = Window.Current.Content as Frame;

        if (rootFrame.CanGoBack)
        {
            rootFrame.GoBack();
        }
    }
```

プログラムを使ったアプリの終了に関しても、すべてのデバイス ファミリに対する単一のアプローチがあります。

```csharp
   Windows.UI.Xaml.Application.Current.Exit();
```

## <a name="binding-and-compiled-bindings-with-xbind"></a>バインドおよび {x:Bind} でコンパイル済みのバインド

次に、バインドに関するトピックをいくつか示します。

-   UI 要素から "データ" (つまり、ビュー モデルのプロパティとコマンド) へのバインド
-   UI 要素から別の UI 要素へのバインド
-   監視可能なビュー モデルの記述 (つまり、プロパティ値の変更時およびコマンドの可用性の変更時に通知が発生します)

こうした要素はすべて、引き続きサポートされていますが、名前空間には違いがあります。 たとえば、 **system.componentmodel**は、INotifyPropertyChanged にマップ[**され、**](/uwp/api/Windows.UI.Xaml.Data.Binding) [**INotifyPropertyChanged**](/uwp/api/Windows.UI.Xaml.Data.INotifyPropertyChanged)にマップされ、INotifyPropertyChanged はにマップされます。には、INotifyCollectionChanged が割り当てられています。 **System.Collections.Specialized.INotifyPropertyChanged**に**は、** [**Windows.UI.Xaml.Interop.INotifyCollectionChanged**](/uwp/api/Windows.UI.Xaml.Interop.INotifyCollectionChanged)が割り当てられていることになります。

Windows Phone Silverlight のアプリ バーとアプリ バーのボタンは、UWP アプリとは異なり、バインドできません。 アプリ バーとそのボタンを構築し、プロパティとローカライズされた文字列にバインドして、イベントを処理する命令型コードを使う場合もあります。 その場合、プロパティとコマンドにバインドされた宣言型マークアップ、および静的なリソース参照によって置き換えることで、該当する命令型コードを移植し、アプリの安全性と保守性を段階的に高めることができます。 Visual Studio または Blend for Visual Studio を使って、他の XAML 要素と同様に、UWP アプリ バーのボタンのバインドとスタイル設定を行うことができます。 UWP アプリでは、使う型名は [**CommandBar**](/uwp/api/Windows.UI.Xaml.Controls.CommandBar) および [**AppBarButton**](/uwp/api/Windows.UI.Xaml.Controls.AppBarButton) であることに注意してください。

ただし、現在 UWP アプリのバインド関連の機能には以下の制限があります。

-   データ エントリ検証と [**IDataErrorInfo**](/dotnet/api/system.componentmodel.idataerrorinfo) インターフェイスおよび [**INotifyDataErrorInfo**](/dotnet/api/system.componentmodel.inotifydataerrorinfo) インターフェイスには、サポートが組み込まれていません。
-   [**Binding**](/uwp/api/Windows.UI.Xaml.Data.Binding) クラスには、Windows Phone Silverlight で利用できる拡張書式設定プロパティが含まれていません。 ただし、[**IValueConverter**](/uwp/api/Windows.UI.Xaml.Data.IValueConverter) を実装してカスタム書式設定を提供することはできます。
-   [**IValueConverter**](/uwp/api/Windows.UI.Xaml.Data.IValueConverter) メソッドは、言語文字列を、[**CultureInfo**](/dotnet/api/system.globalization.cultureinfo) オブジェクトではなくパラメーターとして受け取ります。
-   [**CollectionViewSource**](/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) クラスには、並べ替えとフィルター処理、さまざまなグループへの作業のグループ化のサポートが組み込まれていません。 詳しくは、「[データ バインディングの詳細](../data-binding/data-binding-in-depth.md)」と[データ バインディングのサンプルに関するページ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlBind)をご覧ください。

同じバインド機能が引き続き広くサポートされていますが、Windows 10 では、コンパイル済みバインドと呼ばれる新しい高パフォーマンスのバインド メカニズムのオプションが用意されています。このオプションでは、{x:Bind} マークアップ拡張を使います。 「 [データバインディング: XAML データバインディングの新機能](https://channel9.msdn.com/Events/Build/2015/3-635)と [X:Bind サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlBind)を使用したアプリのパフォーマンスの向上」を参照してください。

## <a name="binding-an-image-to-a-view-model"></a>ビュー モデルへの画像のバインド

[**Image.Source**](/uwp/api/windows.ui.xaml.controls.image.source) プロパティは、ビュー モデルの [**ImageSource**](/uwp/api/Windows.UI.Xaml.Media.ImageSource) 型であるどのプロパティにもバインドできます。 次に、Windows Phone Silverlight アプリのそのようなプロパティの一般的な実装を示します。

```csharp
    // this.BookCoverImagePath contains a path of the form "/Assets/CoverImages/one.png".
    return new BitmapImage(new Uri(this.CoverImagePath, UriKind.Relative));
```

UWP アプリでは、ms-appx [URI スキーム](/previous-versions/windows/apps/jj655406(v=win.10))を使います。 残るコードを変更せずに維持するために、**System.Uri** コンストラクターの異なるオーバーロードを使って、ベース URI に ms-appx URI スキームを格納し、パスの残る部分を追加できます。 以下に例を示します。

```csharp
    // this.BookCoverImagePath contains a path of the form "/Assets/CoverImages/one.png".
    return new BitmapImage(new Uri(new Uri("ms-appx://"), this.CoverImagePath));
```

これによって、ビュー モデル、画像のパス プロパティのパス値、XAML マークアップのバインドの残る部分をすべて、まったく変更せずに維持できます。

## <a name="controls-and-control-stylestemplates"></a>コントロールとコントロール スタイル/テンプレート

Windows Phone Silverlight アプリは、**Microsoft.Phone.Controls** 名前空間と **System.Windows.Controls** 名前空間で定義されたコントロールを使います。 XAML UWP アプリは、[**Windows.UI.Xaml.Controls**](/uwp/api/Windows.UI.Xaml.Controls) 名前空間で定義されたコントロールを使います。 UWP の XAML コントロールのアーキテクチャと設計は、Windows Phone Silverlight コントロールと事実上同じです。 ただし、使用可能なコントロール セットの向上と Windows アプリとの一体化のために、若干の変更が加えられています。 具体的な例をいくつか紹介します。

| コントロール名 | 変更 |
|--------------|--------|
| ApplicationBar | [Page.TopAppBar](/uwp/api/windows.ui.xaml.controls.page.topappbar) プロパティです。 |
| ApplicationBarIconButton | UWP の相当要素は [Glyph](/uwp/api/windows.ui.xaml.controls.fonticon.glyph) プロパティです。 PrimaryCommands は CommandBar のコンテンツ プロパティです。 XAML パーサーは、コンテンツ プロパティの値として要素の内部 xml を解釈します。 |
| ApplicationBarMenuItem | UWP の相当要素は、メニュー項目のテキストに設定された [AppBarButton.Label](/uwp/api/windows.ui.xaml.controls.appbarbutton.label) です。 |
| ContextMenu (Windows Phone Toolkit 内) | 単一選択ポップアップの場合は、[Flyout](/uwp/api/Windows.UI.Xaml.Controls.Flyout) を使います。 |
| ControlTiltEffect.TiltEffect クラス | UWP アニメーション ライブラリのアニメーションは、共通のコントロールの既定のスタイルに組み込まれています。 「[ポインター操作のアニメーション化](/previous-versions/windows/apps/jj649432(v=win.10))」をご覧ください。 |
| グループ化されたデータを含む LongListSelector | Windows Phone Silverlight の LongListSelector は、連携する 2 つの方法で動作します。 まず、キーによってグループ化したデータを表示できます、たとえば、名前の一覧を最初の文字によってグループ化できます。 次に、2 つのセマンティック ビュー (名前などの項目のグループ化されたリストと、最初の文字などのグループ キー自体に限られるリスト) の間で "ズーム" できます。 UWP では、[リスト ビュー コントロールとグリッド ビュー コントロールのガイドライン](../design/controls-and-patterns/lists.md)に従ってグループ化されたデータを表示できます。 |
| フラット データを含む LongListSelector | パフォーマンス上の理由から、非常に長いリストの場合、グループ化されていないフラットなデータであっても Windows Phone Silverlight のリスト ボックスではなく LongListSelector を使うことをお勧めします。 UWP アプリでは、データのグループ化が可能であるかどうかにかかわらず、長い項目リストで [GridView](/uwp/api/Windows.UI.Xaml.Controls.GridView) を使うことをお勧めします。 |
| Panorama | Windows Phone Silverlight パノラマコントロールは、 [Windows ランタイム8.x アプリのハブコントロールのガイドライン](../design/basics/navigation-basics.md) とハブコントロールのガイドラインにマップされます。 <br/> Panorama コントロールは、最後のセクションから最初のセクションに折り返され、背景画像はセクションを基準とした視差効果で移動します。 [Hub](/uwp/api/Windows.UI.Xaml.Controls.Hub) セクションは折り返されず、視差効果は使われません。 |
| ピボット | Windows Phone Silverlight の Pivot コントロールに相当する UWP のコントロールは、[Windows.UI.Xaml.Controls.Pivot](/uwp/api/Windows.UI.Xaml.Controls.Pivot) です。 これはすべてのデバイス ファミリで利用できます。 |

**メモ**   視覚的な状態を上回るポインターは、Windows 10 アプリのカスタムスタイル/テンプレートに関連しますが、Windows Phone Silverlight アプリには関係ありません。 既にあるカスタム スタイル/テンプレートが Windows 10 アプリで適切ではない場合があるのには、他の理由もあります。たとえば、使っているシステム リソース キー、使われる表示状態のセットへの変更、Windows 10 の既定のスタイル/テンプレートに対するパフォーマンスの向上が挙げられます。 Windows 10 用のコントロールの新しい既定のテンプレートのコピーを編集し、そのコピーにスタイルやテンプレートのカスタマイズをもう一度適用することをお勧めします。

UWP コントロールの詳細については、「 [関数別のコントロール](../design/controls-and-patterns/controls-by-function.md)、コントロールの [一覧](../design/controls-and-patterns/index.md)、および [コントロールのガイドライン](../design/controls-and-patterns/index.md)」を参照してください。

##  <a name="design-language-in-windows10"></a>Windows 10 でのデザイン言語

Windows Phone Silverlight アプリと Windows 10 アプリでは、デザイン言語に関して若干の違いがあります。 詳しくは、「[Design](https://developer.microsoft.com/windows/apps/design)」(UWP アプリの設計) をご覧ください。 デザイン言語に変更が加えられていますが、設計原則は維持されています。細部にまで注意を払いながら、簡潔さを追求しています。そのために、クロムよりもコンテンツを優先し、視覚要素を大幅に減らし、真のデジタル領域を常に意識しています。また、視覚的な階層の利用 (特に文字体裁に対して)、グリッド内でのデザイン、滑らかなアニメーションを使ったエクスペリエンスの実現も行っています。

## <a name="localization-and-globalization"></a>ローカリゼーションとグローバリゼーション

ローカライズ文字列については、UWP アプリ プロジェクトで、Windows Phone Silverlight プロジェクトの .resx ファイルを再利用できます。 ファイルをコピーしてプロジェクトに追加し、検索メカニズムによって既定で検索されるように名前を Resources.resw に変更します **[ビルド アクション]** を **[PRIResource]** に設定し、**[出力ディレクトリにコピー]** を **[コピーしない]** に設定します。 次に、XAML 要素で **x:Uid** 属性を指定することにより、マークアップで文字列を使うことができます。 「 [クイックスタート: 文字列リソースの使用」を](/previous-versions/windows/apps/hh965329(v=win.10))参照してください。

Windows Phone Silverlight アプリは、アプリのグローバル化のために **CultureInfo** クラスを使います。 UWP アプリは、MRT (Modern Resource Technology) を使います。これによって、実行時および Visual Studio デザイン サーフェイスで、アプリ リソース (ローカライズ、サイズ調整、テーマ) の動的な読み込みが可能になります。 詳細については、「 [ファイル、データ、およびグローバリゼーションのガイドライン](../design/usability/index.md)」を参照してください。

「[**ResourceContext.QualifierValues**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.qualifiervalues)」トピックでは、デバイス ファミリのリソースを選ぶ要因に基づいてデバイス ファミリ固有のリソースを読み込む方法について説明しています。

## <a name="media-and-graphics"></a>メディアとグラフィックス

UWP のメディアとグラフィックスに関する説明では、Windows の設計原則で、視覚的な複雑さや混乱を含めて、不用なあらゆるものの極度の簡略化を促している点に注意してください。 Windows 設計は、明確かつ明瞭な視覚効果、文字体裁、モーションによって特徴付けられます。 アプリが同じ原則に従えば、組み込みアプリのように振る舞うことができます。

Windows Phone Silverlight にある **RadialGradientBrush** 型は UWP にありませんが、他の [**Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) 型は UWP にもあります。 場合によっては、ビットマップでも同様の効果を得ることができます。 [Microsoft DirectX](/windows/desktop/directx) および XAML C++ UWP では、Direct2D により[放射状グラデーションのブラシを作成](/windows/desktop/Direct2D/how-to-create-a-radial-gradient-brush)できることに注意してください。

Windows Phone Silverlight には **System.Windows.UIElement.OpacityMask** プロパティがありますが、このプロパティは UWP の  [**UIElement**](/uwp/api/Windows.UI.Xaml.UIElement) 型のメンバーではありません。 場合によっては、ビットマップでも同様の効果を得ることができます。 また、[Microsoft DirectX](/windows/desktop/directx) および XAML C++ UWP アプリでは、Direct2D により[不透明マスクを作成](/windows/desktop/Direct2D/opacity-masks-overview)できます。 ただし、**OpacityMask** の一般的な使用事例の 1 つに、淡色テーマと濃色テーマの両方に適合する単一のビットマップを使うことがあります。 ベクター グラフィック (次に示す円グラフなど) では、テーマに対応するシステム ブラシを使うことができます。 ただし、テーマに対応するビットマップ (次に示すチェック マークなど) を作成するには、別のアプローチが必要です。

![テーマに対応するビットマップ](images/wpsl-to-uwp-case-studies/wpsl-to-uwp-theme-aware-bitmap.png)

Windows Phone Silverlight アプリではこの手法は、前景ブラシにより塗りつぶした **Rectangle** に対して **OpacityMask** として、(ビットマップの形式で) アルファ マスクを使うことです。

```xml
    <Rectangle Fill="{StaticResource PhoneForegroundBrush}" Width="26" Height="26">
        <Rectangle.OpacityMask>
            <ImageBrush ImageSource="/Assets/wpsl_check.png"/>
        </Rectangle.OpacityMask>
    </Rectangle>
```

UWP アプリにこれを移植する最も簡単な方法は、[**BitmapIcon**](/uwp/api/Windows.UI.Xaml.Controls.BitmapIcon) を使うことです。

```xml
    <BitmapIcon UriSource="Assets/winrt_check.png" Width="21" Height="21"/>
```

ここで、winrt \_check.png は、wpslcheck.png と同じようにビットマップ形式のアルファマスクであり、 \_ 同じファイルである可能性があります。 ただし、 \_ さまざまなスケールファクターに使用する winrtcheck.png の複数のサイズを指定することもできます。 この詳細および **Width** 値と **Height** 値の変更については、このトピックの「[表示ピクセルと有効ピクセル、視聴距離、スケール ファクター](#view-or-effective-pixels-viewing-distance-and-scale-factors)」をご覧ください。

淡色テーマと濃色テーマのビットマップ形式に違いがある場合に適切であるより一般的なアプローチは、2 つの画像アセット (一方が淡色テーマ用の濃色の前景、他方が濃色テーマ用の淡色の前景) を使うことです。 この一連のビットマップアセットに名前を設定する方法の詳細については、「 [言語、スケール、およびその他の修飾子用にリソースを調整](../app-resources/tailor-resources-lang-scale-contrast.md)する」を参照してください。 イメージ ファイル セットに正しい名前を付けた後、次のようにしてルート名を使って抽象内で参照できます。

```xml
    <Image Source="Assets/winrt_check.png" Stretch="None"/>
```

Windows Phone Silverlight では **UIElement.Clip** プロパティには、**Geometry** により表現できる任意の図形を指定でき、通常は **StreamGeometry** ミニ言語の XAML マークアップでシリアル化されます。 UWP では、[**Clip**](/uwp/api/windows.ui.xaml.uielement.clip) プロパティの型は [**RectangleGeometry**](/uwp/api/Windows.UI.Xaml.Media.RectangleGeometry) です。したがって、四角形の領域のみを切り取ることができます。 ミニ言語を使った四角形の定義を許可することは寛容すぎる場合もあります。 したがって、マークアップ内の切り取り領域を移植するには、**Clip** 属性構文を置き換え、次のようなプロパティ要素構文にします。

```xml
    <UIElement.Clip>
        <RectangleGeometry Rect="10 10 50 50"/>
    </UIElement.Clip>
```

[Microsoft DirectX](/windows/desktop/Direct2D/direct2d-layers-overview) アプリおよび XAML C++ UWP アプリで Direct2D により[レイヤー内でマスクとして任意のジオメトリを使用](/windows/desktop/directx)できることに注意してください。

## <a name="navigation"></a>ナビゲーション

Windows Phone Silverlight ストア アプリでページに移動する際、Uniform Resource Identifier (URI) アドレス指定スキーマは使いません。

```csharp
    NavigationService.Navigate(new Uri("/AnotherPage.xaml", UriKind.Relative)/*, navigationState*/);
```

UWP アプリでは、[**Frame.Navigate**](/uwp/api/windows.ui.xaml.controls.frame.navigate) メソッドを呼び出し、(ページの XAML マークアップ定義の **x:Class** 属性によって定義された) 移動先ページの種類を指定します。


```csharp
    // In a page:
    this.Frame.Navigate(typeof(AnotherPage)/*, parameter*/);

    // In a view model, perhaps inside an ICommand implementation:
    var rootFrame = Windows.UI.Xaml.Window.Current.Content as Windows.UI.Xaml.Controls.Frame;
    rootFrame.Navigate(typeof(AnotherPage)/*, parameter*/);
```

WMAppManifest.xml で Windows Phone Silverlight アプリの起動ページを定義します。

```xml
    <DefaultTask Name="_default" NavigationPage="MainPage.xaml" />
```

UWP アプリでは、起動ページを定義するために命令型コードを使います。 次の例は、そのための方法を示す App.xaml.cs からのコードです。

```csharp
    if (!rootFrame.Navigate(typeof(MainPage), e.Arguments))
```

URI マッピングとフラグメント ナビゲーションは URI ナビゲーションの手法であり、したがって URI に基づく UWP ナビゲーションには該当しません。 URI マッピングは、ページが異なるフォルダー、したがって異なる相対パスに移動したときに脆弱性と保守性の問題が生じる URI 文字列によるターゲット ページの特定における弱い型の特性への対応として用意されているものです。 UWP アプリでは、厳密に型指定され、コンパイラで確認される型ベースのナビゲーションを使っており、URI マッピングの解決における問題がありません。 フラグメント ナビゲーションの使用事例は、ページでコンテンツの特定のフラグメントにビューをスクロールするか、または表示できるように、ターゲット ページにコンテキストを渡すことです。 [**Navigate**](/uwp/api/windows.ui.xaml.controls.frame.navigate) メソッドの呼び出し時にナビゲーション パラメーターを渡すことでも、これは実現できます。

詳しくは、「[ナビゲーション](../design/basics/navigation-basics.md)」をご覧ください。

## <a name="resource-key-reference"></a>リソースのキーの参照

デザイン言語は Windows 10 で改善され、特定のシステム スタイルが変更されました。また、多くのシステム リソースのキーが削除または名前が変更されました。 Visual Studio の XAML マークアップ エディターでは、解決できないリソース キーへの参照が強調表示されます。 たとえば XAML マークアップ エディターでは、スタイル キー `PhoneTextNormalStyle` への参照の下に赤い波線が引かれます。 これを修正しない場合、エミュレーターかデバイスに展開しようとしたときにアプリが直ちに終了します。 したがって、XAML マークアップの正確性に関する作業に着手することが重要です。 また、そのような問題を検出するために Visual Studio が優れたツールであることがわかります。

この後の「[テキスト](#text)」もご覧ください。

## <a name="status-bar-system-tray"></a>ステータス バー (システム トレイ)

システム トレイ (`shell:SystemTray.IsVisible` により XAML マークアップで設定される) は、現在ではステータス バーと呼ばれており、既定で示されます。 [**Windows.UI.ViewManagement.StatusBar.ShowAsync**](/uwp/api/windows.ui.viewmanagement.statusbar.showasync) メソッドと [**HideAsync**](/uwp/api/windows.ui.viewmanagement.statusbar.hideasync) メソッドを呼び出すことによって、表示するかどうかを命令型コードで制御できます。

## <a name="text"></a>テキスト

テキスト (または文字体裁) は UWP アプリの重要な要素です。移植するときには、ビューの視覚的なデザインが新しいデザイン言語に適合するように、ビューの視覚的なデザインを再検討することが必要になる場合があります。 次の図を使って、利用可能な UWP の **TextBlock** システム スタイルを見つけます。 使用した Windows Phone Silverlight スタイルに対応するものを見つけます。 また、独自のユニバーサル スタイルを作成し、Windows Phone Silverlight システム スタイルからプロパティをコピーすることもできます。

![Windows 10 アプリのシステム TextBlock スタイル](images/label-uwp10stylegallery.png)

Windows 10 アプリのシステム TextBlock スタイル

Windows Phone Silverlight アプリでは、既定のフォント ファミリは Segoe WP です。 Windows 10 アプリでは、既定のフォント ファミリは Segoe UI です。 この結果、アプリでのフォント メトリックの表示が異なる可能性があります。 Windows Phone Silverlight のテキストの外観を再現する場合は、[**LineHeight**](/uwp/api/windows.ui.xaml.controls.textblock.lineheight) や [**LineStackingStrategy**](/uwp/api/windows.ui.xaml.controls.textblock.linestackingstrategy) などのプロパティを使って、独自のメトリックを設定できます。 詳しくは、「[フォントのガイドライン](https://docs.microsoft.com/windows/uwp/controls-and-patterns/fonts)」と「[UWP アプリの設計](https://developer.microsoft.com/windows/apps/design)」をご覧ください。

## <a name="theme-changes"></a>テーマの変更

Windows Phone Silverlight アプリの場合、既定のテーマは濃色になっています。 Windows 10 デバイスでは既定のテーマが変更されていますが、App.xaml で要求するテーマを宣言して、使うテーマを制御できます。 たとえば、すべてのデバイスで濃色テーマを使うには、`RequestedTheme="Dark"` をルートの Application 要素に追加します。

## <a name="tiles"></a>タイル

UWP アプリのタイルの動作は Windows Phone Silverlight アプリ用のライブ タイルに似ていますが、違いがいくつかあります。 たとえば、セカンダリ タイルを作成するために **Microsoft.Phone.Shell.ShellTile.Create** メソッドを呼び出すコードは、[**SecondaryTile.RequestCreateAsync**](/uwp/api/windows.ui.startscreen.secondarytile.requestcreateasync) を呼び出すように移植する必要があります。 ここでは、まず Windows Phone Silverlight バージョンの移植前後の例を示します。


```csharp
    var tileData = new IconicTileData()
    {
        Title = this.selectedBookSku.Title,
        WideContent1 = this.selectedBookSku.Title,
        WideContent2 = this.selectedBookSku.Author,
        SmallIconImage = this.SmallIconImageAsUri,
        IconImage = this.IconImageAsUri
    };

    ShellTile.Create(this.selectedBookSku.NavigationUri, tileData, true);
```

次に相当する UWP の要素を示します。

```csharp
    var tile = new SecondaryTile(
        this.selectedBookSku.Title.Replace(" ", string.Empty),
        this.selectedBookSku.Title,
        this.selectedBookSku.ArgumentString,
        this.IconImageAsUri,
        TileSize.Square150x150);

    await tile.RequestCreateAsync();
```

**Microsoft.Phone.Shell.ShellTile.Update** メソッドまたは **Microsoft.Phone.Shell.ShellTileSchedule** クラスによりタイルを更新するコードは、[**TileUpdateManager**](/uwp/api/Windows.UI.Notifications.TileUpdateManager) クラス、[**TileUpdater**](/uwp/api/Windows.UI.Notifications.TileUpdater) クラス、[**TileNotification**](/uwp/api/Windows.UI.Notifications.TileNotification) クラス、[**ScheduledTileNotification**](/uwp/api/Windows.UI.Notifications.ScheduledTileNotification) クラスを使うように移植する必要があります。

タイル、トースト、バッジ、バナー、通知について詳しくは、「[タイルの作成](/previous-versions/windows/apps/hh868260(v=win.10))」と「[タイル、バッジ、トースト通知の操作](/previous-versions/windows/apps/hh868259(v=win.10))」をご覧ください。 UWP タイルに使うビジュアル アセットのサイズの仕様については、「[タイルとトーストのビジュアル資産](/previous-versions/windows/apps/hh781198(v=win.10))」をご覧ください。

## <a name="toasts"></a>トースト

**Microsoft.Phone.Shell.ShellToast** クラスによりトーストを表示するコードは、[**ToastNotificationManager**](/uwp/api/Windows.UI.Notifications.ToastNotificationManager) クラス、[**ToastNotifier**](/uwp/api/Windows.UI.Notifications.ToastNotifier) クラス、[**ToastNotification**](/uwp/api/Windows.UI.Notifications.ToastNotification) クラス、[**ScheduledToastNotification**](/uwp/api/Windows.UI.Notifications.ScheduledToastNotification) クラスを使うように移植する必要があります。 モバイル デバイスでは、"トースト" の利用者向け用語が "バナー" であることに注意してください。

「 [タイル、バッジ、およびトースト通知の操作](/previous-versions/windows/apps/hh868259(v=win.10))」を参照してください。

## <a name="view-or-effective-pixels-viewing-distance-and-scale-factors"></a>表示ピクセルと有効ピクセル、視聴距離、スケール ファクター

Windows Phone Silverlight アプリと Windows 10 アプリでは、デバイスの実際の物理サイズと解像度から UI 要素のサイズとレイアウトを抽象化する方法が異なります。 Windows Phone Silverlight アプリでは、このために表示ピクセルを使います。 Windows 10 では、表示ピクセルの概念が有効ピクセルの概念として改良されました。 有効ピクセルの用語の説明、有効ピクセルが何をするものなのか、および有効ピクセルで使うことができる追加の値について、以下に示します。

一般的な考えとは異なり、"解像度" という用語はピクセル密度の測定値を表しており、ピクセル数ではありません。 "有効解像度" は、画像またはグリフを構成する物理ピクセルを解決して、デバイスの視聴距離と物理ピクセル サイズでの目視による相違の度合を取得する方法です (物理ピクセル サイズの逆数であるピクセル密度)。 有効解像度は、ユーザー中心であるために、エクスペリエンスの構築に適したメトリックです。 すべての要因について理解し、UI 要素のサイズを制御することによって、ユーザーのエクスペリエンスを適切なものにすることができます。

画面の物理ピクセル数、ピクセル密度、物理サイズにかかわらず、Windows Phone Silverlight アプリに対してすべての電話画面は例外なく正確に 480 表示ピクセル幅です。 これは、`Width="48"` を含む **Image** 要素が Windows Phone Silverlight アプリを実行できるすべての電話画面の幅に対して正確に 1/10 であることを示します。

Windows 10 アプリに対しては、すべてのデバイスが固定数の有効ピクセル幅になるわけでは*ありません*。 これは、UWP アプリが広範なデバイスで実行できることから、おそらく明白です。 デバイスによって、有効ピクセルの幅の値が異なります。その範囲は、320 epx (最小のデバイス) から 1024 epx (一般的なサイズのモニター)、またはそれ以上のさらに広い幅になります。 これまでと同様に、自動的にサイズ調整される要素と動的レイアウト パネルを引き続き使うことで十分に対応できます。 ただし、場合によっては、UI 要素のプロパティを XAML マークアップで固定サイズに設定することがあります。 スケール ファクターは、アプリが実行されているデバイスやユーザーが行った表示設定に応じて、アプリに自動的に適用されます。 スケール ファクターによって、さまざまな幅の画面サイズでユーザーに対してほぼ一定サイズのタッチ (または読み取り) ターゲットを提示するように、すべての UI 要素を固定サイズで維持できます。 また、動的レイアウトと共に使うことで、UI は単にさまざまなデバイスで光学的なスケーリングを行うだけでなく、利用可能な領域に合わせて適切な量のコンテンツを表示するために必要となる処理も実行します。

以前は電話サイズの画面の表示ピクセル単位の固定幅が 480 でしたが、現在はその値が有効ピクセル単位では一般的に小さくなるため、経験則として、Windows Phone Silverlight アプリのマークアップのサイズにすべて 0.8 の係数を乗算します。

すべてのディスプレイで最適なアプリのエクスペリエンスが実現できるように、一連のサイズで各ビットマップ アセットを作成し、各アセットが特定のスケール ファクターに適合するように設定することをお勧めします。 ただし、100% スケール、200% スケール、および 400% スケール (この優先順位で) でアセットを作成するほうが、多くの場合、すべての中間スケール ファクターで適切な結果を得ることができます。

**メモ**   何らかの理由で、複数のサイズでアセットを作成できない場合は、100% スケールのアセットを作成します。 Microsoft Visual Studio では、UWP アプリの既定のプロジェクト テンプレートには 1 つのサイズのみのブランド アセット (タイル イメージとロゴ) が用意されていますが、これらは 100% のスケールではありません。 独自のアプリのアセットを作成する場合は、このセクションに示したガイドラインに従って、100%、200%、400% のサイズを用意し、アセット パックを使います。

複雑なアートワークがある場合は、さらに多くのサイズに対応したアセットが必要になることがあります。 ベクター アートを使って作業を始める場合は、どのようなスケール ファクターでも高品質なアセットを比較的簡単に生成できます。

Windows 10 アプリ向けのすべてスケール ファクターは 100%、125%、150%、200%、250%、300%、400% ですが、すべてのスケール ファクターをサポートすることはお勧めしません。 すべてのスケール ファクターのアセットを提供した場合、ストアでは、各デバイスに合った適切なサイズのアセットが選ばれ、それらのアセットのみがダウンロードされます。 ストアでは、デバイスの DPI に基づいて、ダウンロードするアセットが選ばれます。

詳しくは、「[UWP アプリ用レスポンシブ デザイン 101](../design/layout/screen-sizes-and-breakpoints-for-responsive-design.md)」をご覧ください。

## <a name="window-size"></a>ウィンドウ サイズ

UWP アプリでは、命令型コードを使って最小サイズ (幅と高さ) を指定できます。 既定の最小サイズは 500 x 320 epx で、このサイズは受け入れられる最も小さいサイズでもあります。 受け入れられる最も大きいサイズは 500 x 500 epx です。

```csharp
   Windows.UI.ViewManagement.ApplicationView.GetForCurrentView().SetPreferredMinSize
        (new Size { Width = 500, Height = 500 });
```

次のトピックは、「[入出力、デバイス、アプリ モデルの移植](wpsl-to-uwp-input-and-sensors.md)」です。

## <a name="related-topics"></a>関連トピック

* [名前空間とクラス マッピング](wpsl-to-uwp-namespace-and-class-mappings.md)