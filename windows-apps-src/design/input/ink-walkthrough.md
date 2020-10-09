---
ms.assetid: ''
title: Windows アプリでのインクのサポート
description: 基本的なユニバーサル Windows プラットフォーム (UWP) アプリで Windows Ink を使用した書き込みと描画をサポートする方法については、このステップバイステップのチュートリアルを参照してください。
keywords: インク、インク、チュートリアル
ms.date: 09/24/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: f726f4ab4a422cc94f00493261620ddff8b6122b
ms.sourcegitcommit: d786d084dafee5da0268ebb51cead1d8acb9b13e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91860197"
---
# <a name="tutorial-support-ink-in-your-windows-app"></a>チュートリアル: Windows アプリでインクをサポートする

![表面ペンのヒーロー画像。](images/ink/ink-hero-small.png)  
*Surface ペン* ([Microsoft ストア](https://www.microsoft.com/p/surface-pen/8zl5c82qmg6b)で購入できます)。

このチュートリアルでは、Windows Ink での書き込みと描画をサポートする基本的な Windows アプリを作成する手順について説明します。 使用するサンプル アプリは GitHub ([サンプル コード](#sample-code)) からダウンロードできます。このサンプル アプリのスニペットは、各手順でのさまざまな機能と関連する Windows Ink API ([Windows Ink プラットフォームのコンポーネント](#components-of-the-windows-ink-platform)をご覧ください) の使い方を示します。

次の点を中心に説明します。
* 基本的なインクのサポートを追加する
* インク ツールバーを追加する
* 手書き認識をサポートする
* 基本的な図形の認識をサポートする
* インクを保存して読み込む

これらの機能の実装の詳細については、「 [windows アプリにおけるペンの相互作用と Windows Ink](./pen-and-stylus-interactions.md)」を参照してください。

## <a name="introduction"></a>はじめに

Windows Ink を使うと、ユーザーに、ペンと紙の体験とほぼ同等のデジタル エクスペリエンスを提供できます。すばやく手書きでメモを取ったり、ホワイトボードのデモに注釈を書き込んだり、建築製図や工業図面の作成から、個人的な作品の制作まで行えます。

## <a name="prerequisites"></a>前提条件

* 現在のバージョンの Windows 10 を実行するコンピューター (または仮想マシン)。
* [Visual Studio 2019 と RS2 SDK](https://developer.microsoft.com/windows/downloads)
* [Windows 10 SDK (10.0.15063.0)](https://developer.microsoft.com/windows/downloads/windows-10-sdk)
* 構成によっては、 [Microsoft.netcore.universalwindowsplatform](https://www.nuget.org/packages/Microsoft.NETCore.UniversalWindowsPlatform) NuGet パッケージをインストールし、システム設定で **開発者モード** を有効にすることが必要になる場合があります > (開発者向け > & のセキュリティ-> 開発者向けの機能を使用します)。
* Visual Studio を使用した Windows アプリの開発に慣れていない場合は、このチュートリアルを開始する前に、次のトピックを参照してください。  
    * [準備](../../get-started/get-set-up.md)
    * ["Hello, world" アプリを作成する (XAML)](../../get-started/create-a-hello-world-app-xaml-universal.md)
* **[オプション]** デジタル ペンと、そのデジタル ペンからの入力をサポートしているディスプレイを搭載したコンピューター。

> [!NOTE] 
> Windows Ink は、マウスとタッチを使った描画をサポートします (これについては、このチュートリアルの手順 3 で説明します) が、最適なWindows Ink エクスペリエンスのためには、デジタル ペンとそのデジタル ペンからの入力をサポートしているディスプレイを備えたコンピューターの使用を推奨します。

## <a name="sample-code"></a>サンプル コード
このチュートリアル全体で、1 つサンプル インク アプリを使って概念と機能を説明します。

この Visual Studio サンプルとソース コードは [GitHub](https://github.com/) の [windows-appsample-get-started-ink sample](https://github.com/Microsoft/Windows-tutorials-inputs-and-devices/tree/master/GettingStarted-Ink) からダウンロードできます。

1. 緑色の **複製またはダウンロード** ボタンを選択します。  
![リポジトリを複製しています。](images/ink/ink-clone.png)
2. GitHub のアカウントを使っている場合には、[**Open in Visual Studio**] (Visual Studio で開く) を選択して、リポジトリをローカル コンピューターに複製できます。 
3. GitHub アカウントを持っていない場合、またはプロジェクトのローカルコピーが必要な場合は、[ **ZIP のダウンロード** ] を選択します (最新の更新プログラムをダウンロードするには、定期的に確認する必要があります)。

> [!IMPORTANT]
> サンプル コードのほとんどの部分はコメント アウトされています。各手順を進めていく際に、コードの各セクションのコメントを解除します。 Visual Studio では、コードの行を強調表示して Ctrl + K キーを押して Ctrl + U キーを押します。

## <a name="components-of-the-windows-ink-platform"></a>Windows Ink プラットフォームのコンポーネント

これらのオブジェクトは、Windows アプリのインク操作の大部分を提供します。

| コンポーネント | 説明 |
| --- | --- |
| [**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) | 既定でペンからのすべての入力を受け取ってインク ストロークか消去ストロークとして表示する XAML UI プラットフォーム コントロールです。 |
| [**System.windows.controls.inkpresenter>**](/uwp/api/Windows.UI.Input.Inking.InkPresenter) | [**InkCanvas**](/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールと共にインスタンス化される分離コード オブジェクトです ([**InkCanvas.InkPresenter**](/uwp/api/windows.ui.xaml.controls.inkcanvas.InkPresenter) プロパティによって公開されます)。 このオブジェクトは、 [**system.windows.controls.inkcanvas>**](/uwp/api/windows.ui.xaml.controls.inkcanvas)によって公開されるすべての既定のインク機能を提供し、さらにカスタマイズと個人用設定のための包括的な api のセットを提供します。 |
| [**InkToolbar**](/uwp/api/Windows.UI.Xaml.Controls.InkToolbar) | 関連付けられた [**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) のインク関連機能をアクティブ化する、カスタマイズと拡張が可能なボタンのコレクションが含まれている XAML UI プラットフォーム コントロールです。 |
| [**IInkD2DRenderer**](/windows/desktop/api/inkrenderer/nn-inkrenderer-iinkd2drenderer)<br/>この機能は、このドキュメントの対象範囲外です。詳しくは、「[複雑なインクのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ComplexInk)」をご覧ください。 | 既定の [**InkCanvas**](/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールの代わりに、ユニバーサル Windows アプリが指定した Direct2D デバイス コンテキストにインク ストロークをレンダリングできます。 |

## <a name="step-1-run-the-sample"></a>手順 1: サンプルを実行する

RadialController サンプル アプリをダウンロードしたら、実行できることを確認します。
1. Visual Studio でサンプル プロジェクトを開きます。
2. [**ソリューション プラットフォーム**] のドロップダウンを ARM 以外の選択肢に設定します。
3. F5 キーを押して、コンパイル、展開、および実行します。  

   > [!NOTE]
   > または、 **[デバッグ**  >  ] [**デバッグの開始**] メニュー項目を選択するか、ここに表示されている [**ローカルコンピューター**の実行] ボタンを選択します。
   > ![Visual Studio の [プロジェクトのビルド] ボタン。](images/ink/ink-vsrun-small.png)

アプリ ウィンドウが開き、スプラッシュ画面が数秒表示されて、次のような初期画面が表示されます。

![空のアプリのスクリーンショット。](images/ink/ink-app-step1-empty-small.png)

これで、このチュートリアルの残りの部分で使用する基本的な Windows アプリが完成しました。 これ以降の手順では、インク機能を追加します。

## <a name="step-2-use-inkcanvas-to-support-basic-inking"></a>手順 2: InkCanvas を使って基本的な手描き入力をサポートする

お気付きのように、このアプリは初期状態では、ペンを使って手描きを行うことはできません (ただし、標準のポインター デバイスとしてペンを使用してアプリを操作することはできます)。 

この手順では、その欠点を修正します。

基本的なインク機能を追加するには、アプリの適切なページに [**system.windows.controls.inkcanvas>**](/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) コントロールを配置するだけです。

> [!NOTE]
> InkCanvas の[**高さ**](/uwp/api/windows.ui.xaml.frameworkelement.Height)と[**幅**](/uwp/api/windows.ui.xaml.frameworkelement.Width)のプロパティは、子要素のサイズを自動的に設定する要素の子である場合を除き、既定では 0 です。 

### <a name="in-the-sample"></a>このサンプルを使って、次を行います:
1. MainPage.xaml.cs ファイルを開きます。
2. この手順のタイトル ("// Step 2: Use InkCanvas to support basic inking") が付いているコードを見つけます。
3. 以下の行のコメントを解除します。 (これらの参照は、これ以降の手順で使用される機能に必要です。)  

``` csharp
    using Windows.UI.Input.Inking;
    using Windows.UI.Input.Inking.Analysis;
    using Windows.UI.Xaml.Shapes;
    using Windows.Storage.Streams;
```

4. MainPage.xaml ファイルを開きます。
5. この手順のタイトル ("") でマークされたコードを見つけ \<!-- Step 2: Basic inking with InkCanvas --> ます。
6. 以下の行のコメントを解除します。  

``` xaml
    <InkCanvas x:Name="inkCanvas" />
```

これで完了です。 

ここで、アプリをもう一度実行します。 何でも自由に書き込んだり、自画像の絵などを描いてみてください。

![このトピックで強調表示されている基本的なインクサンプルアプリのスクリーンショット。](images/ink/ink-app-step1-name-small.png)

## <a name="step-3-support-inking-with-touch-and-mouse"></a>手順 3: タッチとマウスを使って手描き入力をサポートする

お気付きのように、既定では、インクはペン入力のみをサポートします。 指、マウス、またはタッチパッドを使って描画することはできません。

それを可能にするには、コードの 2 行目を追加する必要があります。 それは、[**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) を宣言した XAML ファイルのコードビハインドにあります。 

この手順では、[**InkPresenter**](/uwp/api/windows.ui.input.inking.inkpresenter) オブジェクトを説明します。このオブジェクトは [**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) の手描き入力 (標準および変更) の入力、処理、レンダリングの細かい管理を提供します。

> [!NOTE]
> 標準のインク入力 (ペン先または消しゴムの先端やボタン) は、セカンダリ ハードウェア アフォーダンス (ペン バレル ボタン、マウスの右ボタン、または類似のメカニズムなど) で変更されません。 

マウスとタッチによる手描き入力を有効化するには、[**InkPresenter**](/uwp/api/windows.ui.input.inking.inkpresenter) の [**InputDeviceTypes**](/uwp/api/windows.ui.input.inking.inkpresenter.InputDeviceTypes) プロパティを、必要な [**CoreInputDeviceTypes**](/uwp/api/windows.ui.core.coreinputdevicetypes) 値の組み合わせに設定します。

### <a name="in-the-sample"></a>このサンプルを使って、次を行います:
1. MainPage.xaml.cs ファイルを開きます。
2. この手順のタイトル ("// Step 3: Support inking with touch and mouse") が付いているコードを見つけます。
3. 以下の行のコメントを解除します。  

``` csharp
    inkCanvas.InkPresenter.InputDeviceTypes =
        Windows.UI.Core.CoreInputDeviceTypes.Mouse | 
        Windows.UI.Core.CoreInputDeviceTypes.Touch | 
        Windows.UI.Core.CoreInputDeviceTypes.Pen;
```

アプリをもう一度実行して、指を使って手描き入力ができることを確認します。

> [!NOTE]
> 入力デバイスの種類を指定する場合は、特定の入力の種類のサポート (ペンを含む) を指定する必要があります。このプロパティの設定は既定の [**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) 設定を上書きするためです。

## <a name="step-4-add-an-ink-toolbar"></a>手順 4: インク ツールバーを追加する

[**InkToolbar**](/uwp/api/windows.ui.xaml.controls.inktoolbar) は、インク関連の機能を有効化するための、カスタマイズと拡張が可能なボタンのコレクションを提供する、UWP プラットフォーム コントロールです。 

[**InkToolbar**](/uwp/api/windows.ui.xaml.controls.inktoolbar) には、既定では、ボタンの基本的なセットが含まれています。ユーザーはこれを使って、ペン、鉛筆、蛍光ペン、消しゴムをすばやく選択でき、これらはいずれもステンシル (ルーラーまたは分度器) と共に使用できます。 ペン、鉛筆、および蛍光ペンのボタンは、インクの色と線のサイズを選択できるポップアップも提供します。

既定の [**InkToolbar**](/uwp/api/windows.ui.xaml.controls.inktoolbar) を手描き入力のアプリに追加するには、[**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) と同じページに配置して、2 つのコントロールを関連付けます。

### <a name="in-the-sample"></a>このサンプルを使って、次を行います:
1. MainPage.xaml ファイルを開きます。
2. この手順のタイトル ("") でマークされたコードを見つけ \<!-- Step 4: Add an ink toolbar --> ます。
3. 以下の行のコメントを解除します。  

``` xaml
    <InkToolbar x:Name="inkToolbar" 
                        VerticalAlignment="Top" 
                        Margin="10,0,10,0"
                        TargetInkCanvas="{x:Bind inkCanvas}">
    </InkToolbar>
```

> [!NOTE]
> UI とコードをなるべくクリーンでシンプルにするため、基本的なグリッド レイアウトを使って、グリッド行で [**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) の後で、[**InkToolbar**](/uwp/api/windows.ui.xaml.controls.inktoolbar) を宣言します。 [**InkCanvas**](/uwp/api/windows.ui.xaml.controls.inkcanvas) の前で宣言すると、キャンバスの下で [**InkToolbar**](/uwp/api/windows.ui.xaml.controls.inktoolbar) が先にレンダリングされ、ユーザーはアクセスできません。  

アプリを再度実行し、[**InkToolbar**](/uwp/api/windows.ui.xaml.controls.inktoolbar) が表示されることを確認してツールを試します。

![このトピックで強調表示されている基本的なインクサンプルアプリのスクリーンショット (既定の InkToolbar)](images/ink/ink-inktoolbar-default-small.png)

### <a name="challenge-add-a-custom-button"></a>課題: カスタム ボタンを追加する
<table class="wdg-noborder">
<tr>
<td>

:::image type="icon" source="images/challenge-icon.png":::

</td>
<td>

カスタムの **[InkToolbar](/uwp/api/windows.ui.xaml.controls.inktoolbar)** の例 (Windows Ink ワークスペースのスケッチパッド) を示します。

![インクワークスペースの Sketchpad の [インク] ツールバーのスクリーンショット。](images/ink/ink-inktoolbar-sketchpad-small.png)

[Inktoolbar](/uwp/api/windows.ui.xaml.controls.inktoolbar)のカスタマイズの詳細については、「 [Windows アプリインクアプリに Inktoolbar を追加する](ink-toolbar.md)」を参照してください。

</td>
</tr>
</table>

## <a name="step-5-support-handwriting-recognition"></a>手順 5: 手書き認識をサポートする

これでアプリで手描きや描画ができるようになりました。これを使って、さらに便利な機能を追加します。

この手順では、Windows Ink の手書き認識機能を使用して、手描き入力を解読します。

> [!NOTE]
> 手書き認識は [**ペンと Windows Ink**] の設定を使って改善できます。
> 1. スタート メニューを開き、[**設定**] を選択します。
> 2. [設定] 画面で、[**デバイス**] [  >  **ペン & Windows Ink**] を選択します。
> ![[ペン & Windows Ink 設定] ページのスクリーンショット。](images/ink/ink-settings-small.png)
> 3. [**手書き入力を認識します**] を選択して、[**手書き認識の個人用設定**] ダイアログを開きます。
> ![[手書き認識の個人用設定] ダイアログボックスのスクリーンショット。](images/ink/ink-settings-handwritingpersonalization-small.png)

### <a name="in-the-sample"></a>このサンプルを使って、次を行います:
1. MainPage.xaml ファイルを開きます。
2. この手順のタイトル ("") でマークされたコードを見つけ \<!-- Step 5: Support handwriting recognition --> ます。
3. 以下の行のコメントを解除します。  

``` xaml
    <Button x:Name="recognizeText" 
            Content="Recognize text"  
            Grid.Row="0" Grid.Column="0"
            Margin="10,10,10,10"
            Click="recognizeText_ClickAsync"/>
    <TextBlock x:Name="recognitionResult" 
                Text="Recognition results: "
                VerticalAlignment="Center" 
                Grid.Row="0" Grid.Column="1"
                Margin="50,0,0,0" />
```

4. MainPage.xaml.cs ファイルを開きます。
5. この手順のタイトル  (" Step 5: Support handwriting recognition") が付いているコードを見つけます。
6. 以下の行のコメントを解除します。  

- これらは、この手順で必要なグローバル変数です。

``` csharp
    InkAnalyzer analyzerText = new InkAnalyzer();
    IReadOnlyList<InkStroke> strokesText = null;
    InkAnalysisResult resultText = null;
    IReadOnlyList<IInkAnalysisNode> words = null;
```

- これは、[**Recognize text**] (テキストの認識) ボタンのハンドラーで、これにより認識処理を行います。

``` csharp
    private async void recognizeText_ClickAsync(object sender, RoutedEventArgs e)
    {
        strokesText = inkCanvas.InkPresenter.StrokeContainer.GetStrokes();
        // Ensure an ink stroke is present.
        if (strokesText.Count > 0)
        {
            analyzerText.AddDataForStrokes(strokesText);

            resultText = await analyzerText.AnalyzeAsync();

            if (resultText.Status == InkAnalysisStatus.Updated)
            {
                words = analyzerText.AnalysisRoot.FindNodes(InkAnalysisNodeKind.InkWord);
                foreach (var word in words)
                {
                    InkAnalysisInkWord concreteWord = (InkAnalysisInkWord)word;
                    foreach (string s in concreteWord.TextAlternates)
                    {
                        recognitionResult.Text += s;
                    }
                }
            }
            analyzerText.ClearDataForAllStrokes();
        }
    }
```

7. アプリを再び実行し、何かを書き込んで、[**Recognize text**] (テキストの認識) ボタンをクリックします。
8. 認識の結果は、ボタンの横に表示されます。

### <a name="challenge-1-international-recognition"></a>課題1: 地域と言語の認識
<table class="wdg-noborder">
<tr>
<td>

:::image type="icon" source="images/challenge-icon.png":::

</td>
<td>

Windows Ink は、Windowsでサポートされている多くの言語のテキスト認識をサポートします。 各言語パックには、言語パックと共にインストールできる、手書き認識エンジンが含まれています。

インストール済みの手書き認識エンジンにクエリを行って、特定の言語をターゲットにします。

地域と言語の手書き認識について詳しくは、「[Windows Ink でのストロークのテキスト認識](convert-ink-to-text.md)」をご覧ください。

</td>
</tr>
</table>

### <a name="challenge-2-dynamic-recognition"></a>課題 2: 動的な認識
<table class="wdg-noborder">
<tr>
<td>

:::image type="icon" source="images/challenge-icon.png":::

</td>
<td>

このチュートリアルでは、認識を開始するためにボタンを押す必要があります。 基本的なタイミング関数を使って、動的な認識を実行することもできます。

動的な認識について詳しくは、「[Windows Ink でのストロークのテキスト認識](convert-ink-to-text.md)」をご覧ください。

</td>
</tr>
</table>

## <a name="step-6-recognize-shapes"></a>手順 6: 図形を認識する

これで手書きのメモを判読可能なものに変換できるようになりました。 では、手書きのフローチャートなどを認識することはできるでしょうか。

インクの分析を使うと、アプリは次のような基本的な図形を認識することができます。

- Circle
- ひし形
- 描画
- Ellipse
- 正三角形
- 六角形
- 二等辺三角形
- 平行四辺形
- 五角形
- 四辺形
- Rectangle
- 直角三角形
- Square
- 台形
- Triangle

この手順では、Windows Ink の図形認識機能を使用して、手書きの図形をクリーンにします。

この例では、インク ストロークの再描画は (可能ですが) 行いません。 代わりに、InkCanvas の下に標準のキャンバスを追加し、元の手書き図形から作成された、楕円や多角形オブジェクトをそこに描画します。 次に、対応するインク ストロークを削除します。

### <a name="in-the-sample"></a>このサンプルを使って、次を行います:
1. MainPage.xaml ファイルを開きます。
2. このステップのタイトル ("") でマークされたコードを探します \<!-- Step 6: Recognize shapes --> 。
3. この行のコメントを解除します。  

``` xaml
   <Canvas x:Name="canvas" />

   And these lines.

    <Button Grid.Row="1" x:Name="recognizeShape" Click="recognizeShape_ClickAsync"
        Content="Recognize shape" 
        Margin="10,10,10,10" />
```

4. MainPage.xaml.cs ファイルを開きます。
5. この手順のタイトル ("// Step 6: Recognize shapes") が付いているコードを見つけます。
6. これらの行のコメントを解除します。  

``` csharp
    private async void recognizeShape_ClickAsync(object sender, RoutedEventArgs e)
    {
        ...
    }

    private void DrawEllipse(InkAnalysisInkDrawing shape)
    {
        ...
    }

    private void DrawPolygon(InkAnalysisInkDrawing shape)
    {
        ...
    }
```

7. アプリを実行し、いくつかの図形を描画して、[**Recognize shape**] (図形の認識) ボタンをクリックします。

デジタルの走り書きを使った、基本的なフローチャートの例を示します。

![デジタルナプキンからの基本的なフローチャートのスクリーンショット。](images/ink/ink-app-step6-shapereco1-small.png)

図形認識後の同じフローチャートを次に示します。

![ユーザーが [認識図形] を選択した後のフローチャートのスクリーンショット。](images/ink/ink-app-step6-shapereco2-small.png)


## <a name="step-7-save-and-load-ink"></a>手順 7: インクの保存と読み込み

手書きの文字や図形の認識ができるようになりましたが、それらを後から使いたい場合にはどうすればよいでしょうか。 インク ストロークを Ink Serialized Format (ISF) ファイルに保存し、後でそれを読み込んで編集することができます。 

ISF ファイルは、インク ストロークのプロパティと動作に関する追加のメタデータを含む、基本的な GIF 画像です。 インク対応でないアプリでは、追加のメタデータを無視して、基本的な GIF 画像 (アルファ チャンネルの背景の透明度を含む) を読み込むことができます。

この手順では、インク ツールバーの横にある、[**保存**] と [**読み込み**] ボタンをフックします。

### <a name="in-the-sample"></a>このサンプルを使って、次を行います:
1. MainPage.xaml ファイルを開きます。
2. この手順のタイトル ("") でマークされたコードを見つけ \<!-- Step 7: Saving and loading ink --> ます。
3. 以下の行のコメントを解除します。 

``` xaml
    <Button x:Name="buttonSave" 
            Content="Save" 
            Click="buttonSave_ClickAsync"
            Width="100"
            Margin="5,0,0,0"/>
    <Button x:Name="buttonLoad" 
            Content="Load"  
            Click="buttonLoad_ClickAsync"
            Width="100"
            Margin="5,0,0,0"/>
```

4. MainPage.xaml.cs ファイルを開きます。
5. この手順のタイトル ("// Step 7: Save and load ink") が付いているコードを見つけます。
6. 以下の行のコメントを解除します。  

``` csharp
    private async void buttonSave_ClickAsync(object sender, RoutedEventArgs e)
    {
        ...
    }

    private async void buttonLoad_ClickAsync(object sender, RoutedEventArgs e)
    {
        ...
    }
```

7. アプリを実行し、何かを描画します。
8. [**保存**] ボタンを選択し、描画を保存します。
9. インクを消去するか、またはアプリを再起動します。
10. [**読み込み**] ボタンを選択して、保存したインク ファイルを開きます。

### <a name="challenge-use-the-clipboard-to-copy-and-paste-ink-strokes"></a>課題: クリップボードを使って、インク ストロークをコピーして貼り付ける 
<table class="wdg-noborder">
<tr>
<td>

:::image type="icon" source="images/challenge-icon.png":::

</td>

<td>

Windows Ink は、インク ストロークのクリップボードへのコピーと貼り付けもサポートしています。

Windows Ink とクリップボードの使用について詳しくは、「[Windows Ink ストローク データの保存と取得](save-and-load-ink.md)」をご覧ください。

</td>
</tr>
</table>

## <a name="summary"></a>まとめ

これで、 **「Windows アプリでのインクのサポート」** チュートリアルが完了しました。 Windows アプリでインクをサポートするために必要な基本的なコードと、Windows Ink プラットフォームでサポートされている充実したユーザーエクスペリエンスを提供する方法について説明しました。

## <a name="related-articles"></a>関連記事

* [Windows アプリでのペン操作と Windows Ink](pen-and-stylus-interactions.md)

### <a name="samples"></a>サンプル

* [インクの分析のサンプル (基本) (C#)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-analysis-basic.zip)
* [インクの手書き認識のサンプル (C#)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-handwriting-reco.zip)
* [インク ストロークを Ink Serialized Format (ISF) ファイルに保存し、読み込む](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store.zip)
* [インク ストロークをクリップボードに保存し、読み込む](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-store-clipboard.zip)
* [インク ツール バーの位置と向きのサンプル (基本)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness.zip)
* [インク ツール バーの位置と向きのサンプル (動的)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness-dynamic.zip)
* [単純なインクのサンプル (C#/C++)](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SimpleInk)
* [複雑なインクのサンプル (C++)](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ComplexInk)
* [インクのサンプル (JavaScript)](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Windows%208%20app%20samples/%5BJavaScript%5D-Windows%208%20app%20samples/JavaScript/Windows%208%20app%20samples/Input%20Ink%20sample%20(Windows%208))
* [入門チュートリアル: Windows アプリでインクをサポートする](https://github.com/Microsoft/Windows-tutorials-inputs-and-devices/tree/master/GettingStarted-Ink)
* [塗り絵帳のサンプル](https://github.com/Microsoft/Windows-appsample-coloringbook)
* [Family Notes のサンプル](https://github.com/Microsoft/Windows-appsample-familynotes)
