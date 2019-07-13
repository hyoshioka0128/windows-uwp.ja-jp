---
description: このガイドは、WPF および Windows フォーム アプリケーションで直接 Fluent ベースの UWP UI を作成するのに役立ちます。
title: デスクトップ アプリでの UWP コントロール
ms.date: 04/16/2019
ms.topic: article
keywords: windows 10、uwp、windows フォーム、wpf、xaml islands
ms.author: mcleans
author: mcleanbyron
ms.localizationpriority: medium
ms.custom: RS5, 19H1
ms.openlocfilehash: 8ceb314424ae2611e141ef866a84c08e55b0ba2d
ms.sourcegitcommit: f9a30bfd1e8eab50d0b1db97dd2f650ce66b5d34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2019
ms.locfileid: "67690886"
---
# <a name="host-uwp-xaml-controls-in-desktop-apps-xaml-islands"></a>デスクトップ アプリ でUWP XAMLコントロールをホストする(XAML Islands)

Windows 10 バージョン1903以降では、*XAML Islands* と呼ばれる機能を使用して、UWP 以外のデスクトップアプリケーションでUWPコントロールをホストできます。 この機能を使用すると、UWPコントロールを介してのみ利用可能な最新の Windows 10 UI機能を使用して、既存のデスクトップアプリケーションの外観、操作性、および機能性を向上させることができます。 つまり、既存の WPF、Windowsフォーム、およびC ++ Win32 アプリケーションで [Windows Ink](/windows/uwp/design/input/pen-and-stylus-interactions)などの UWP 機能と [Fluent Design System](/windows/uwp/design/fluent-design-system/index) をサポートするコントロールを使用できます。

XAML Islands で、Windows フォーム、WPF を使用するいくつかの方法を紹介し、C++テクノロジまたは使用しているフレームワークに応じて、Win32 アプリケーション。 

> [!NOTE]
> XAML Islands に関するフィードバックがある場合は、 [Microsoft.Toolkit.Win32 リポジトリ](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) に新しい問題を作成し、そこにコメントを残してください。 個人的にフィードバックを送信したい場合は、XamlIslandsFeedback@microsoft.com に送信できます。 あなたの洞察とシナリオは弊社にとって非常に重要です。

## <a name="how-do-xaml-islands-work"></a>XAML Islands のしくみ

Windows フォーム、WPF の XAML Islands を使用する 2 つの方法を説明する Windows 10、バージョンが 1903 年以降とC++Win32 アプリケーション。

* Windows SDK には、いくつかの Windows ランタイム クラスと COM インターフェイスから派生した任意の UWP コントロールをホストするアプリケーションが使用できる[ **Windows.UI.Xaml.UIElement**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement)します。 総称して、これらのクラスとインターフェイスを呼び出す、 *API をホストしている UWP XAML*、関連するウィンドウ ハンドル (HWND) を含む、アプリケーションで任意の UI 要素に UWP コントロールをホストすることができるとします。 この API の詳細については、次を参照してください。 [API をホストしている XAML を使用して](using-the-xaml-hosting-api.md)します。

* [Windows Community Toolkit](https://docs.microsoft.com/windows/uwpcommunitytoolkit/) WPF と Windows フォームの他の XAML 島コントロールも提供します。 これらのコントロールでは、内部的に API をホストしている UWP XAML を使用し、すべてのキーボード ナビゲーションとレイアウトの変更を含め、直接 API をホストしている UWP XAML を使用している場合、自分で処理する必要がなくなり、動作を実装します。 WPF と Windows フォーム アプリケーションでは、強くお勧め UWP XAML ではなく、これらのコントロールを使用していた多くの API を使用して実装の詳細の抽象化されため、直接 API をホストします。 Windows 10、バージョンが 1903 年の時点でこれらのコントロールは[開発者プレビューとして利用できる](#feature-roadmap)します。

> [!NOTE]
> C++ Win32 デスクトップ アプリケーションでは、UWP コントロールをホストする API をホストしている UWP XAML を使用する必要があります。 Windows コミュニティのツールキットで XAML 島コントロールは使用できませんC++Win32 デスクトップ アプリケーションです。

WPF と Windows フォーム アプリケーションの Windows コミュニティのツールキットで提供される XAML 島コントロールの 2 種類があります:*コントロールをラップ*と*ホスト コントロール*します。 

### <a name="wrapped-controls"></a>ラップされたコントロール

WPF と Windows フォーム アプリケーションは、ラップされた UWP コントロールの選択範囲を使用できます、 [Windows Community Toolkit](https://docs.microsoft.com/windows/uwpcommunitytoolkit/)します。 これらと呼ばれます*コントロールをラップ*インターフェイスと特定の UWP コントロールの機能をラップするためです。 これらのコントロールを WPF や Windows フォーム プロジェクトのデザイン画面に直接追加し、デザイナーで、他の WPF や Windows フォーム コントロールのように使用できます。

XAML Islands を実装するための次のラップされた UWP コントロールは、現在 WPF および Windows フォームアプリケーションで利用できます。

| コントロール | サポートされている OS の最小値 | 説明 |
|-----------------|-------------------------------|-------------|
| [InkCanvas](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/inkcanvas)<br>[InkToolbar](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/inktoolbar) | Windows 10 バージョン 1903 | Windows フォームまたは WPF デスクトップ アプリケーションでのインクの Windows ベースのユーザーの相互作用のサーフェスと関連するツールバーを提供します。 |
| [MediaPlayerElement](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/mediaplayerelement) | Windows 10 バージョン 1903 | ストリームし、Windows フォームまたは WPF デスクトップ アプリケーションでのビデオなどのメディア コンテンツをレンダリングするビューを埋め込みます。 |
| [MapControl](https://docs.microsoft.com/en-us/windows/communitytoolkit/controls/wpf-winforms/mapcontrol) | Windows 10 バージョン 1903 | Windows フォームまたは WPF デスクトップ アプリケーションでシンボリックまたは写実的なマップを表示できます。 |

Windows の Community Toolkit は XAML の島をラップされたコントロールのほか、web コンテンツをホストするため、次のコントロールを提供します。

| コントロール | サポートされている OS の最小値 | 説明 |
|-----------------|-------------------------------|-------------|
| [WebView](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/webview) | Windows 10 バージョン 1803 | Web コンテンツを表示するのにには、Microsoft Edge のレンダリング エンジンを使用します。 |
| [WebViewCompatible](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/webviewcompatible) | Windows 7 | バージョンを提供します**WebView**より多くの OS バージョンと互換性があります。 このコントロールが Windows 10 バージョン 1803 以降の web コンテンツを表示する Microsoft Edge のレンダリング エンジンと以前のバージョンの Windows 10、Windows 上の web コンテンツを表示する Internet Explorer のレンダリング エンジンを使用して、8.x および Windows 7。 |

### <a name="host-controls"></a>ホスト コントロール

利用可能なラップされたコントロールで対応できないシナリオでは、WPF と Windows フォーム アプリケーションを使用できますも、 [WindowsXamlHost](https://docs.microsoft.com/windows/communitytoolkit/controls/wpf-winforms/windowsxamlhost)を制御、 [Windows Community Toolkit](https://docs.microsoft.com/windows/uwpcommunitytoolkit/)します。 このコントロールから派生した任意の UWP コントロールをホストできる[ **Windows.UI.Xaml.UIElement**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement)など、UWP、Windows SDK によって提供されるだけではなくカスタム ユーザー コントロール。 このコントロールは、Windows 10 Insider Preview SDK ビルド 17709 およびそれ以降のリリースをサポートします。

### <a name="architecture-overview"></a>アーキテクチャの概要

これらのコントロールがアーキテクチャ的に編成されるしくみの概要を次に示します。

![ホスト コントロール アーキテクチャ](images/xaml-islands/host-controls.png)

この図の下部に表示されている API は、Windows SDK に付属しています。 ラップされたコントロールとホスト コントロールは、Windows の Community Toolkit の Nuget パッケージから入手できます。

## <a name="requirements"></a>要件

XAML Islandsには、Windows 10、バージョン1903以降が必要です。 アプリケーションで XAML Islands を使用するには、まずプロジェクトを設定する必要があります。

### <a name="step-1-modify-your-project-to-use-windows-runtime-apis"></a>手順 1:Windows ランタイム Api を使用して、プロジェクトを変更します。

手順については、次を参照してください。[今回](desktop-to-uwp-enhance.md#set-up-your-project)します。

### <a name="step-2-enable-xaml-island-support-in-your-project"></a>手順 2:プロジェクトでサポートを有効にする XAML 島

プロジェクトに XAML 島サポートを有効にすることを次の変更のいずれか。 詳細については、[このブログの投稿](https://techcommunity.microsoft.com/t5/Windows-Dev-AppConsult/Using-XAML-Islands-on-Windows-10-19H1-fixing-the-quot/ba-p/376330#M117)を参照してください。

#### <a name="option-1-package-your-application-in-an-msix-package"></a>オプション 1:MSIX パッケージ内のアプリケーションをパッケージ化します。  

Windows 10、バージョン 1903 SDK (またはそれ以降のリリース) をインストールします。 次に、MSIX パッケージ内のアプリケーションを追加することでパッケージを[Windows アプリケーション パッケージ プロジェクト](https:/docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-packaging-dot-net)ソリューションと、WPF や Windows フォーム プロジェクトへの参照を追加します。

#### <a name="option-2-set-the-maxversiontested-value-in-your-assembly-manifest"></a>オプション 2:アセンブリ マニフェストで maxVersionTested 値を設定します。

追加できるかどうか MSIX パッケージ内のアプリケーションをパッケージ化したくない、[アプリケーション マニフェスト](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests)をプロジェクトに追加し、 **maxVersionTested**要素を指定するマニフェスト、アプリケーションは、Windows 10、1903 またはそれ以降のバージョンとの互換性。

1. アプリケーション マニフェストのプロジェクトで、新しい XML ファイルをプロジェクトに追加およびという名前を付けますがまだしていない場合**app.manifest**します。 WPF や Windows フォーム アプリケーションの場合も割り当てることを確認します、**マニフェスト**プロパティを **. app.manifest**で、**アプリケーション**のページ、[プロジェクトプロパティ](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-csharp?view=vs-2019#resources)します。
2. アプリケーション マニフェストで含める、**互換性**要素と子要素を次の例に示すようにします。 置換、 **Id**の属性、 **maxVersionTested**対象としている Windows 10 のバージョン番号を持つ要素 (これは、Windows 10、バージョンが 1903 または今後のリリースをする必要があります)。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">
        <compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
            <application>
                <!-- Windows 10 -->
                <maxversiontested Id="10.0.18362.0"/>
                <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
            </application>
        </compatibility>
    </assembly>
    ```

> [!NOTE]
> 追加すると、 **maxVersionTested**要素内のアプリケーション マニフェストに、 C++ Win32 プロジェクト (Visual Studio では、Windows デスクトップ アプリケーション プロジェクト テンプレートを使用して)、プロジェクトで、次のビルド警告を表示可能性があります: `manifest authoring warning 81010002: Unrecognized Element "maxversiontested" in namespace "urn:schemas-microsoft-com:compatibility.v1"`. この警告は、プロジェクトで、間違いがあることと、無視することが示されません。

## <a name="feature-roadmap"></a>機能のロードマップ

Windows 10、バージョンが 1903 年のリリースの時点で、ラップされたコントロールとホスト コントロール Windows コミュニティのツールキットではまだ開発者プレビューの段階で、コントロールのバージョン 1.0 のリリースが利用可能になるまでです。

* バージョン 1.0、.NET Framework 4.6.2 のコントロールの後にリリースされる予定と、[ツールキットの 6.0 リリース](https://github.com/windows-toolkit/WindowsCommunityToolkit/milestones)します。
* 1\.0 のバージョンの .NET Core 3 のコントロールは、toolkit の今後のリリースの予定です。
* .NET Framework と .NET Core 3 をこれらのコントロールのバージョン 1.0 のリリースの最新のプレビューを試す場合を参照してください、 **6.0.0-preview3**で NuGet のパッケージ、 [UWP Community Toolkit](https://dotnet.myget.org/gallery/uwpcommunitytoolkit)ギャラリー。

詳細については、[このブログの投稿](https://blogs.windows.com/windowsdeveloper/2019/06/13/xaml-islands-v1-updates-and-roadmap)を参照してください。

## <a name="additional-resources"></a>その他の資料

詳細な背景情報と XAML Islandsを使用したチュートリアルについては、次の記事やリソースを参照してください。

* [WPF アプリのチュートリアルを最新化](modernize-wpf-tutorial.md):このチュートリアルでは、既存の WPF 基幹業務アプリケーションに UWP コントロールを追加する Windows の Community Toolkit でラップされたコントロールとホスト コントロールを使用して手順に沿って説明します。 このチュートリアルには、プロセスで、WPF アプリケーションの完全なコードおよび各手順の詳細な手順が含まれています。
* [XAML 諸島 v1 - 更新プログラムとロードマップ](https://blogs.windows.com/windowsdeveloper/2019/06/13/xaml-islands-v1-updates-and-roadmap):このブログの投稿では、XAML 諸島に関する多くの一般的な質問を説明し、開発の詳細なロードマップを提供します。
