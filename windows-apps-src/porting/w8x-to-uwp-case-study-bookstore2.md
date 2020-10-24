---
ms.assetid: 333f67f5-f012-4981-917f-c6fd271267c6
description: このケース スタディは、Bookstore1 で説明されている情報に基づいて作成されています。ここでは最初に、グループ化されたデータを SemanticZoom コントロールに表示するユニバーサル 8.1 アプリについて取り上げます。
title: Windows ランタイム 8.x から UWP へのケース スタディ - Bookstore2
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: b2681eb1fd14ed7e86c00054c5f5c7ba3efb97c6
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89167616"
---
# <a name="windows-runtime-8x-to-uwp-case-study-bookstore2"></a>Windows ランタイム 8.x から UWP へのケース スタディ - Bookstore2


このケース スタディは、「[Bookstore1](w8x-to-uwp-case-study-bookstore1.md)」で説明されている情報に基づいて作成されています。ここでは最初に、グループ化されたデータを [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) コントロールに表示するユニバーサル 8.1 アプリについて取り上げます。 ビュー モデルでは、**Author** クラスの各インスタンスが該当する著者によって書かれた書籍のグループを表します。**SemanticZoom** では、著者ごとにグループ化された書籍の一覧を表示したり、縮小して著者のジャンプ リストを表示したりすることができます。 ジャンプ リストを使うと、書籍の一覧をスクロールするよりもすばやく移動することができます。 ここでは、アプリを Windows 10 ユニバーサル Windows プラットフォーム (UWP) アプリに移植する手順について説明します。

**メモ**   Visual Studio で Bookstore2Universal 10 を開くときに、 \_ "Visual studio 更新プログラムが必要です" というメッセージが表示された場合は、 [Targetplatformversion](w8x-to-uwp-troubleshooting.md)の手順に従います。

## <a name="downloads"></a>ダウンロード

[Bookstore2 \_ 81 Universal 8.1 アプリをダウンロード](https://codeload.github.com/MicrosoftDocs/windows-topic-specific-samples/zip/Bookstore2_81)します。

[Bookstore2Universal \_ 10 Windows 10 アプリをダウンロード](https://codeload.github.com/MicrosoftDocs/windows-topic-specific-samples/zip/Bookstore2Universal_10)します。

## <a name="the-universal-81-app"></a>ユニバーサル 8.1 アプリ

ここでは \_ 、Bookstore2 81 (ポートに送信されるアプリ) は次のようになっています。 このアプリでは、著者ごとにグループ化された書籍を表示する [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) を横方向にスクロール (Windows Phone では縦方向にスクロール) します。 このリストを縮小してジャンプ リストを表示し、そこから任意のグループに移動できます。 このアプリには 2 つの重要な機能があります。それらは、グループ化されたデータ ソースを提供するビュー モデルと、そのビュー モデルにバインドされるユーザー インターフェイスです。 ここで説明するように、これら 2 つの機能は、WinRT 8.1 テクノロジから Windows 10 に簡単に移植できます。

![\-windows 上の bookstore2 81、拡大表示](images/w8x-to-uwp-case-studies/c02-01-win81-zi-how-the-app-looks.png)

\_Windows 上の Bookstore2 81、拡大表示
 

![\-windows 上の bookstore2 81、縮小表示](images/w8x-to-uwp-case-studies/c02-02-win81-zo-how-the-app-looks.png)

\_Windows 上の Bookstore2 81、縮小表示

![\-windows phone の bookstore2 81、拡大表示](images/w8x-to-uwp-case-studies/c02-03-wp81-zi-how-the-app-looks.png)

\_Windows Phone の Bookstore2 81、拡大表示

![\-windows phone での bookstore2 81、縮小表示](images/w8x-to-uwp-case-studies/c02-04-wp81-zo-how-the-app-looks.png)

\_Windows Phone での Bookstore2 81、縮小表示

##  <a name="porting-to-a-windows10-project"></a>Windows 10 プロジェクトへの移植

Bookstore2 \_ 81 ソリューションは、8.1 ユニバーサルアプリプロジェクトです。 Bookstore2 プロジェクトは、 \_ Windows 8.1 用のアプリパッケージをビルドし、Bookstore2 \_ 81. appname.windowsphone プロジェクトは Windows Phone 8.1 用のアプリパッケージをビルドします。 Bookstore2 \_ は、他の2つのプロジェクトの両方で使用されるソースコード、マークアップファイル、およびその他のアセットとリソースを含むプロジェクトです。

前のケース スタディと同様に、ここで使うオプション (「[ユニバーサル 8.1 アプリがある場合](w8x-to-uwp-root.md)」をご覧ください) は、共有プロジェクトの内容をユニバーサル デバイス ファミリを対象とする Windows 10 に移植するためのオプションです。

最初に、"新しいアプリケーション (Windows ユニバーサル)" プロジェクトを新規作成します。 「Bookstore2Universal 10」という名前 \_ を指定します。 これらは、Bookstore2 \_ 81 から Bookstore2Universal 10 にコピーするファイルです \_ 。

**共有プロジェクトから**

-   ブックのカバー画像 PNG ファイルを格納しているフォルダーをコピーします (フォルダーは [アセット] の画像になり \\ \\ ます)。 フォルダーをコピーしたら、**ソリューション エクスプローラー**で **[すべてのファイルを表示]** がオンであることを確認します。 コピーしたフォルダーを右クリックし、**[プロジェクトに含める]** をクリックします。 このコマンドは、ファイルまたはフォルダーをプロジェクトに "含める" ことを意味します。 ファイルやフォルダーをコピーするたびに、**ソリューション エクスプローラー**で **[更新]** をクリックしてから、ファイルまたはフォルダーをプロジェクトに含めます。 コピー先で置き換えるファイルについては、この手順を実行する必要はありません。
-   ビューモデルのソースファイルが格納されているフォルダーをコピーします (フォルダーはビューモデルです \\ )。
-   MainPage.xaml をコピーして、コピー先のファイルを置き換えます。

**Windows プロジェクトから**

-   BookstoreStyles.xaml をコピーします。 このファイル内のすべてのリソース キーが Windows 10 アプリで解決されるため、このファイルを出発点として使います。ただし、同等の Windows Phone ファイル内にある一部のリソース キーは解決されません。
-   SeZoUC.xaml と SeZoUC.xaml.cs をコピーします。 このビューの Windows バージョンで作業を始めます。このビューは、幅が広いウィンドウに適していますが、最終的には小型のデバイスで使うことができるように、より幅が狭いウィンドウに合わせて調整します。

コピーしたソースコードとマークアップファイルを編集し、Bookstore2 81 名前空間への参照を \_ Bookstore2Universal 10 に変更し \_ ます。 これをすばやく行うには、**[フォルダーを指定して置換]** 機能を使います。 ビュー モデルでも、その他の命令型コードでも、コードを変更する必要はありません。 ただし、実行されているアプリのバージョンを簡単に確認できるようにするには、 **Bookstore2Universal \_ 10. bookstoreviewmodel** 81 プロパティによって返される値を " \_ Bookstore2Universal \_ 10" に変更します。

これで、ビルドして実行することができます。 新しい UWP アプリの外観は、Windows 10 へ移植するための作業をまだ行っていませんが、次のようになります。

![デスクトップ デバイスで動作中の、最初のソース コードの変更を加えた Windows 10 アプリ (拡大表示)](images/w8x-to-uwp-case-studies/c02-05-desk10-zi-initial-source-code-changes.png)

デスクトップデバイスで実行されている最初のソースコードの変更を含む Windows 10 アプリ (拡大表示)

![デスクトップ デバイスで動作中の、最初のソース コードの変更を加えた Windows 10 アプリ (縮小表示)](images/w8x-to-uwp-case-studies/c02-06-desk10-zo-initial-source-code-changes.png)

デスクトップデバイスで実行されている最初のソースコードの変更を含む Windows 10 アプリの縮小表示

ビュー モデル、拡大表示、縮小表示は適切に連携しますが、確認するのが難しいという問題があります。 第 1 の問題は、[**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) がスクロールしないことです。 これは、Windows 10 では、[**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) の既定のスタイルが原因で縦方向にレイアウトされるためです (Windows 10 の設計ガイドラインでは、新しいアプリや移植されたアプリでそのように使うことが推奨されています)。 ただし、Bookstore2 81 プロジェクト (8.1 アプリ向けに設計されています) からコピーした [カスタム項目] パネルテンプレートの水平スクロールの設定は、windows \_ 10 アプリに移植した結果として適用されている windows 10 の既定のスタイルの垂直スクロール設定と競合しています。 第 2 の問題は、アプリでは、さまざまなサイズのウィンドウや小型のデバイスで最適なエクスペリエンスを実現するようにユーザー インターフェイスがまだ対応していないことです。 第 3 の問題は、適切なスタイルとブラシがまだ使われていないことです。このため、ほとんどのテキストが表示されていません (縮小表示のためにクリックできるグループ ヘッダーを含む)。 次の 3 つのセクション (「[SemanticZoom と GridView の設計変更](#semanticzoom-and-gridview-design-changes)」、「[アダプティブ UI](#adaptive-ui)」、「[ユニバーサル スタイル設定](#universal-styling)」) では、これら 3 つの問題に対処します。

## <a name="semanticzoom-and-gridview-design-changes"></a>SemanticZoom と GridView の設計変更

Windows 10 での [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) コントロールに対する設計変更については、「[SemanticZoom に関する変更](w8x-to-uwp-porting-xaml-and-ui.md)」のセクションをご覧ください。 これらの変更に対応するための作業は、このセクションでは行いません。

[**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) に対する変更については、「[GridView/ListView に関する変更](w8x-to-uwp-porting-xaml-and-ui.md)」のセクションをご覧ください。 これらの変更に対応するために、次に示す調整を行います。

-   SeZoUC.xaml の `ZoomedInItemsPanelTemplate` で、`Orientation="Horizontal"` と `GroupPadding="0,0,0,20"` を設定します。
-   SeZoUC.xaml で、`ZoomedOutItemsPanelTemplate` を削除し、縮小表示からは `ItemsPanel` 属性を削除します。

以上で作業は終了です。

## <a name="adaptive-ui"></a>アダプティブ UI

上記の変更を行うと、SeZoUC.xaml によって示される UI レイアウトは、幅の広いウィンドウでアプリを実行する場合に便利なレイアウトとなります (大型画面を持つデバイスでのみ役立つと考えられます)。 ただし、アプリのウィンドウが狭い場合は (小型のデバイスが該当しますが、大型のデバイスの場合もあります)、Windows Phone ストア アプリで使った UI が間違いなく最適な UI となります。

これを実現するために、アダプティブな Visual State Manager 機能を使うことができます。 Windows Phone ストア アプリで使っていた、より小さいサイズのテンプレートを利用して、既定で UI が幅の狭い状態でレイアウトされるように、視覚要素のプロパティを設定します。 その後で、アプリのウィンドウ幅が特定のサイズ以上になる状況を確認します (このサイズは[有効ピクセル](w8x-to-uwp-porting-xaml-and-ui.md)の単位で測定します)。また、より大きなレイアウトやより幅の広いレイアウトを実現できるように、視覚要素のプロパティを変更します。 これらのプロパティの変更を表示状態として設定し、アダプティブなトリガーを使って、有効ピクセル単位のウィンドウ幅に応じて、その表示状態を適用するかどうかを継続的に監視し判断します。 この場合はウィンドウの幅でトリガーしていますが、ウィンドウの高さでトリガーすることもできます。

この使用事例では、ウィンドウの最小幅は 548 epx が適しています。これは、最も小型のデバイスで幅の広いレイアウトを表示する際に適したサイズであるためです。 通常、電話は 548 epx よりも小さいため、電話のような小型のデバイスでは既定の幅の狭いレイアウトをそのまま使います。 PC では、既定で、ワイド状態への切り替えをトリガーできる十分な幅でウィンドウが開きます。 この状態でウィンドウをドラッグして、250 x 250 サイズの項目が示される 2 列分を表示できる幅の狭いウィンドウにすることができます。 これよりも幅を狭くすると、トリガーが非アクティブ化されます。これにより、幅の広い表示状態が削除され、既定である幅の狭いレイアウトが有効になります。

これら 2 つの異なるレイアウトを実現するためには、どのプロパティを設定 (および変更) する必要があるでしょうか。 そのためには 2 つの方法があり、それぞれの方法で異なるアプローチが必要です。

1.  2 つの [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) コントロールをマークアップ内に配置できます。 1つは、Windows ランタイム 8. x アプリで ( [**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) コントロールを使用して) 使用していたマークアップのコピーであり、既定では折りたたまれています。 もう 1 つは Windows Phone ストア アプリで使っていたマークアップのコピー (マークアップ内の [**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) コントロールを使っていました) であり、既定では表示されます。 表示状態によって、2 つの **SemanticZoom** コントロールが持つ表示に関するプロパティが切り替えられます。 この方法では、わずかな作業で 2 つのレイアウトを実現できますが、一般的には、高いパフォーマンスを得ることができる手法ではありません。 そのため、この方法を使う場合は、アプリをプロファイリングし、お客様のパフォーマンスの目標を達成できるかどうかを確認する必要があります。
2.  複数の [**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) コントロールを含んでいる 1 つの [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) を使うことができます。 2 つのレイアウトを実現するために、幅の広い表示状態について、**ListView** コントロールのプロパティ (コントロールに適用されるテンプレートなど) を変更します。このとき、[**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) と同じ方法でこのコントロールがレイアウトされるようにプロパティを変更します。 この方法では、より優れたパフォーマンスを得ることができる場合がありますが、**GridView** と **ListView** のさまざまなスタイルやテンプレートの間、およびこれらのコントロールにおけるさまざまな項目の種類の間に、細かな相違点が多数あります。このため、2 つのレイアウトを実現するには難しい解決策でもあります。 またこの解決策は、既定のスタイルとテンプレートに関する現時点での設計方法と緊密に関連しており、既定の設定に対して今後加えられる変更の影響を受けやすい、安定性に欠ける解決策でもあります。

このケース スタディでは、最初の方法を採用します。 2 番目の方法を試したい場合は、その方法が適切であるかどうかを確認してください。 最初の方法を実装するための手順を次に示します。

-   新しいプロジェクトのマークアップに含まれている [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) で、`x:Name="wideSeZo"` と `Visibility="Collapsed"` を設定します。
-   Bookstore2 \_ 81. appname.windowsphone プロジェクトに戻り、SeZoUC .xaml を開きます。 このファイルから [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) 要素のマークアップをコピーし、新しいプロジェクトの `wideSeZo` の直後に貼り付けます。 貼り付けた要素に対して `x:Name="narrowSeZo"` を設定します。
-   ただし、`narrowSeZo` には、まだコピーしていないスタイルがいくつか必要です。 Bookstore2 \_ 81. appname.windowsphone でも、2つのスタイル ( `AuthorGroupHeaderContainerStyle` と `ZoomedOutAuthorItemContainerStyle` ) を sezouc .xaml からコピーして、新しいプロジェクトの bookstorestyles. .xaml に貼り付けます。
-   これで、新しい SeZoUC.xaml には 2 つの [**SemanticZoom**](/uwp/api/Windows.UI.Xaml.Controls.SemanticZoom) 要素が指定されます。 これら 2 つの要素を **Grid** でラップします。
-   新しいプロジェクトの BookstoreStyles.xaml で、`Wide` という単語を、`AuthorGroupHeaderTemplate`、`ZoomedOutAuthorTemplate`、`BookTemplate` の 3 つのリソース キーに付加します (SeZoUC.xaml に含まれているこれらのリソース キーの参照にもこの語を付加しますが、`wideSeZo` 内にある参照にのみ付加します)。
-   Bookstore2 81. \_ appname.windowsphone プロジェクトで、BookstoreStyles. .xaml を開きます。 このファイルから、これらの同じ3つのリソース (上記を参照) と2つのジャンプリスト項目コンバーター、および名前空間プレフィックス宣言 Windows \_ UI \_ Xaml \_ コントロールの \_ プリミティブをコピーし、これらすべてを新しいプロジェクトの bookstorestyles .xaml に貼り付けます。
-   最後に、新しいプロジェクトの SeZoUC.xaml で、適切な Visual State Manager のマークアップを上で追加した **Grid** に追加します。

```xml
    <Grid>
        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup>
                <VisualState x:Name="WideState">
                    <VisualState.StateTriggers>
                        <AdaptiveTrigger MinWindowWidth="548"/>
                    </VisualState.StateTriggers>
                    <VisualState.Setters>
                        <Setter Target="wideSeZo.Visibility" Value="Visible"/>
                        <Setter Target="narrowSeZo.Visibility" Value="Collapsed"/>
                    </VisualState.Setters>
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>

    ...

    </Grid>
```

## <a name="universal-styling"></a>ユニバーサル スタイル設定

次に、スタイルの問題を解決します。以前のプロジェクトからコピーするときに、上で説明した問題も含みます。

-   MainPage.xaml で、`LayoutRoot` の Background を `"{ThemeResource ApplicationPageBackgroundThemeBrush}"` に変更します。
-   BookstoreStyles.xaml で、リソース `TitlePanelMargin` の値を `0` (または適切な外観になる任意の値) に設定します。
-   SeZoUC.xaml で、`wideSeZo` の Margin を `0` (または適切な外観になる任意の値) に設定します。
-   BookstoreStyles.xaml で、`AuthorGroupHeaderTemplateWide` から Margin 属性を削除します。
-   `AuthorGroupHeaderTemplate` と `ZoomedOutAuthorTemplate` から、FontFamily 属性を削除します。
-   Bookstore2 \_ 81 は `BookTemplateTitleTextBlockStyle` 、、 `BookTemplateAuthorTextBlockStyle` 、およびの `PageTitleTextBlockStyle` 各リソースキーを間接参照として使用し、1つのキーが2つのアプリで異なる実装を持つようにしました。 その間接参照は、必要ではなくなりました。システム スタイルを直接参照できます。 そのため、アプリ全体でこれらの参照をそれぞれ、`TitleTextBlockStyle`、`CaptionTextBlockStyle`、`HeaderTextBlockStyle` に置き換えます。 Visual Studio の **[フォルダーを指定して置換]** 機能を使って、この操作をすばやく正確に行うことができます。 その後で、使わなくなった 3 つのリソースを削除できます。
-   `AuthorGroupHeaderTemplate` で、`PhoneAccentBrush` を `SystemControlBackgroundAccentBrush` に置き換え、**TextBlock** に対して `Foreground="White"` を設定します。これにより、モバイル デバイス ファミリで実行したときに適切に表示されます。
-   `BookTemplateWide` で、2 番目の **TextBlock** から 1 番目のものに Foreground 属性をコピーします。
-   `ZoomedOutAuthorTemplateWide` で、`SubheaderTextBlockStyle` (今では少し大きすぎる) への参照を `SubtitleTextBlockStyle` への参照に変更します。
-   縮小表示 (ジャンプ リスト) は、新しいプラットフォームでの拡大表示ビューをオーバーレイしません。このため、`narrowSeZo` の縮小表示から `Background` 属性を削除できます。
-   すべてのスタイルとテンプレートを 1 つのファイルに格納するために、SeZoUC.xaml から BookstoreStyles.xaml に `ZoomedInItemsPanelTemplate` を移動します。

スタイル設定操作の最後のシーケンスで、アプリの外観は次のようになります。

![デスクトップ デバイスで動作中の、移植された Windows 10 アプリ (2 つのサイズのウィンドウによる拡大表示)](images/w8x-to-uwp-case-studies/c02-07-desk10-zi-ported.png)

デスクトップデバイスで実行される移植された Windows 10 アプリ、拡大ビュー、2つのサイズのウィンドウ

![デスクトップ デバイスで動作中の、移植された Windows 10 アプリ (2 つのサイズのウィンドウによる縮小表示)](images/w8x-to-uwp-case-studies/c02-08-desk10-zo-ported.png)

デスクトップ デバイスで動作中の、移植された Windows 10 アプリ (2 つのサイズのウィンドウによる縮小表示)

![モバイル デバイスで動作中の、移植された Windows 10 アプリ (拡大表示)](images/w8x-to-uwp-case-studies/c02-09-mob10-zi-ported.png)

モバイルデバイスで実行されている移植された Windows 10 アプリ (拡大表示)

![モバイル デバイスで動作中の、移植された Windows 10 アプリ (縮小表示)](images/w8x-to-uwp-case-studies/c02-10-mob10-zo-ported.png)

モバイルデバイスで実行されている移植された Windows 10 アプリ (縮小表示)

## <a name="conclusion"></a>まとめ

このケース スタディには、前のケース スタディよりも複雑なユーザー インターフェイスが関連しています。 前のケース スタディと同じように、この特定のビュー モデルでは特に作業を行わなくても、最初はユーザー インターフェイスがリファクタリングされました。 変更が必要となるのは、2 つのプロジェクトを 1 つのプロジェクトにまとめ、多くのフォーム ファクターをサポートする場合です (実際に、前のケース スタディよりも多くのフォーム ファクターを使いました)。 一部の変更点は、プラットフォームに加えられた変更に関連するものでした。

次のケース スタディは「[QuizGame](w8x-to-uwp-case-study-quizgame.md)」です。ここでは、グループ化されたデータへのアクセスと表示について説明します。