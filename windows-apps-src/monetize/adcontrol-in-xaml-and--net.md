---
ms.assetid: 4e7c2388-b94e-4828-a104-14fa33f6eb2d
description: Windows 10 (UWP) 用の XAML アプリで AdControl クラスを使ってバナー広告を表示する方法について説明します。
title: XAML および .NET の AdControl
ms.date: 03/22/2018
ms.topic: article
keywords: Windows 10, UWP, 広告, 宣伝, AdControl, 広告コントロール, XAML, .NET, チュートリアル
ms.localizationpriority: medium
ms.openlocfilehash: 8784de7025a2e9efa8e9e02be14c94579730a1dd
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57608647"
---
# <a name="adcontrol-in-xaml-and-net"></a>XAML および .NET の AdControl


このチュートリアルでは、C# を使用して実装された Windows 10 用のユニバーサル Windows プラットフォーム (UWP) XAML アプリで、[AdControl](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol) クラスを使ってバナー広告を表示する方法について説明します。

> [!NOTE]
> Microsoft Advertising SDK は、C++ で実装された XAML アプリもサポートしています。 完全なサンプル プロジェクトについては、[GitHub の広告サンプル](https://aka.ms/githubads)をご覧ください。

## <a name="prerequisites"></a>前提条件

* Visual Studio 2015 以降の Visual Studio のリリースと共に [Microsoft Advertising SDK](https://aka.ms/ads-sdk-uwp) をインストールします。 インストール手順については、[この記事](install-the-microsoft-advertising-libraries.md)をご覧ください。

## <a name="integrate-a-banner-ad-into-your-app"></a>バナー広告をアプリに統合する

1. Visual Studio でプロジェクトを開くか、新しいプロジェクトを作ります。

    > [!NOTE]
    > 既存のプロジェクトを使用している場合、プロジェクトの Package.appxmanifest ファイルを開き、**インターネット (クライアント)** 機能が選択されていることを確認します。 アプリでは、テスト広告やライブ広告を受信するためにこの機能が必要になります。

2. プロジェクトのターゲットが **[Any CPU]** (任意の CPU) になっている場合は、アーキテクチャ固有のビルド出力 (たとえば、**[x86]**) を使うようにプロジェクトを更新します。 プロジェクトのターゲットが **[Any CPU]** (任意の CPU) になっていると、次の手順で Microsoft Advertising ライブラリへの参照を正常に追加できません。 詳しくは、「[プロジェクトのターゲットを "Any CPU" に設定すると参照エラーが発生する](known-issues-for-the-advertising-libraries.md#reference_errors)」をご覧ください。

3. プロジェクトで Microsoft Advertising SDK への参照を追加します。

    1. **[ソリューション エクスプローラー]** ウィンドウで、**[参照設定]** を右クリックし、**[参照の追加]** を選択します。
    2.  **[参照マネージャー]** で、**[Universal Windows]** を展開し、**[拡張]** をクリックして、**[Microsoft Advertising SDK for XAML]** (バージョン 10.0) の横にあるチェック ボックスをオンにします。
    3.  **[参照マネージャー]** で、[OK] をクリックします。

4.  広告を埋め込むページの XAML を変更して、**Microsoft.Advertising.WinRT.UI** 名前空間を追加します。 たとえば、Visual Studio によって生成される既定のサンプル アプリ (この例では MyAdFundedWindows10AppXAML という名前) では、**MainPage.XAML** という XAML ページに追加します。

    Visual Studio によって生成される MainPage.xaml ファイルの **Page** セクションには、次のようなコードが含まれています。

    ``` xml
    <Page
      x:Class="MyAdFundedWindows10AppXAML.MainPage"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:local="using:MyAdFundedWindows10AppXAML"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      mc:Ignorable="d">
      <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
      </Grid>
    </Page>
    ```

    **Microsoft.Advertising.WinRT.UI** 名前空間の参照を追加すると、MainPage.xaml ファイルの **Page** セクションのコードが次のようになります。

    ``` xml
    <Page
      x:Class="MyAdFundedWindows10AppXAML.MainPage"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:local="using:MyAdFundedWindows10AppXAML"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      xmlns:UI="using:Microsoft.Advertising.WinRT.UI"
      mc:Ignorable="d">
      <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
      </Grid>
    </Page>
    ```

5. **Grid** タグに、**AdControl** のコードを追加します。 [AdUnitId](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.adunitid) プロパティと [ApplicationId](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.applicationid) プロパティに、[広告ユニットのテスト値](set-up-ad-units-in-your-app.md#test-ad-units)を割り当てます。 また、コントロールの**高さ**と**幅**を、[バナー広告でサポートされている広告サイズ](supported-ad-sizes-for-banner-ads.md)のいずれかに合わせて調整します。

    > [!NOTE]
    > 各 **AdControl** に、対応する*広告ユニット*があります。広告ユニットは、コントロールに広告を提供するためにサービスで使用されます。すべての広告ユニットは、*広告ユニット ID* と*アプリケーション ID* で構成されます。 ここでは、広告ユニット ID とアプリケーション ID のテスト値をコントロールに割り当てます。 これらのテスト値は、テスト バージョンのアプリでのみ使用できます。 ストアにアプリを発行する前にする必要があります[を交換してこれらのテストのライブの値を持つ値](#release)パートナー センターから。

    完成した **Grid** タグのコードは、次のようになります。

    ``` xml
    <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <UI:AdControl ApplicationId="3f83fe91-d6be-434d-a0ae-7351c5a997f1"
            AdUnitId="test"
            HorizontalAlignment="Left"
            Height="250"
            VerticalAlignment="Top"
            Width="300"/>
    </Grid>
    ```

    MainPage.xaml ファイルの完全なコードは、次のようになります。

    ``` xml
    <Page
      x:Class="MyAdFundedWindows10AppXAML.MainPage"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:local="using:MyAdFundedWindows10AppXAML"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      xmlns:UI="using:Microsoft.Advertising.WinRT.UI"
      mc:Ignorable="d">
      <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <UI:AdControl ApplicationId="3f83fe91-d6be-434d-a0ae-7351c5a997f1"
                  AdUnitId="test"
                  HorizontalAlignment="Left"
                  Height="250"
                  VerticalAlignment="Top"
                  Width="300"/>
      </Grid>
    </Page>
    ```

6.  アプリをコンパイルして実行し、広告が表示されることを確認します。

<span id="release" />

## <a name="release-your-app-with-live-ads"></a>ライブ広告を表示するアプリをリリースする

1. アプリでのバナー広告の使用方法が[バナー広告のガイドライン](ui-and-user-experience-guidelines.md#guidelines-for-banner-ads)に従っていることを確認します。

2.  パートナー センターに移動、[アプリ内広告](../publish/in-app-ads.md)ページと[ad 単位を作成](set-up-ad-units-in-your-app.md#live-ad-units)です。 広告ユニットの種類として、**[バナー]** を指定します。 広告ユニット ID とアプリケーション ID の両方をメモしておきます。
    > [!NOTE]
    > テスト広告ユニットとライブ UWP 広告ユニットでは、アプリケーション ID の値の形式が異なります。 テスト アプリケーション ID の値は GUID です。 パートナー センターでライブ UWP ad 単位を作成するときに ad 単体のアプリケーション ID の値は常に (Store ID 値の例を次のように 9NBLGGH4R315) アプリの Store ID を一致します。

3. 必要に応じて、[[アプリ内広告]](../publish/in-app-ads.md) ページの [[仲介設定]](../publish/in-app-ads.md#mediation) セクションで設定を構成することで、**AdControl** の広告仲介を有効にできます。 広告仲介を使うと、複数の広告ネットワークから広告を表示して、広告収益とアプリ プロモーションの機能を最大限に引き出すことができます。表示される広告には、Taboola や Smaato などの他の有料広告ネットワークからの広告や、Microsoft のアプリ プロモーション キャンペーン用の広告などが含まれます。

4.  コード、テスト ad 単位の値に置き換えてください (**ApplicationId**と**AdUnitId**) パートナー センターで生成したライブの値を使用します。

5.  [アプリの提出](../publish/app-submissions.md)パートナー センターを使用して、ストアにします。

6.  レビュー、[広告のパフォーマンス レポート](../publish/advertising-performance-report.md)パートナー センターでします。

<span id="manage" />

## <a name="manage-ad-units-for-multiple-ad-controls-in-your-app"></a>アプリで複数の広告コントロールの広告ユニットを管理する

1 つのアプリで複数の **AdControl** オブジェクトを使うことができます (たとえば、アプリの各ページに異なる **AdControl** オブジェクトをホストできます)。 このシナリオでは、各コントロールに異なる広告ユニットを割り当てることをお勧めします。 各コントロールに異なる広告ユニットを使用することで、別々に[仲介の設定を構成](../publish/in-app-ads.md#mediation)して、個別の[報告データ](../publish/advertising-performance-report.md)を取得することが可能です。 また、これにより、Microsoft のサービスはアプリに提供する広告を最適化できます。

> [!IMPORTANT]
> 各広告ユニットは 1 つのアプリのみで使用できます。 同じ広告ユニットを複数のアプリで使うと、その広告ユニットには広告が配信されません。

## <a name="related-topics"></a>関連トピック

* [バナー広告のガイドライン](ui-and-user-experience-guidelines.md#guidelines-for-banner-ads)
* [XAML/C# ウォークスルーでのエラー処理](error-handling-in-xamlc-walkthrough.md)
* [GitHub の広告サンプル](https://aka.ms/githubads)
* [アプリの ad 単位を設定します](set-up-ad-units-in-your-app.md)
