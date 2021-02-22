---
description: 自動サイズ変更、レイアウト パネル、表示状態、個別の UI 定義を備えた XAML の柔軟なレイアウト システムを使用して、応答性の高い UI を作成する方法について説明します。
title: XAML でのレスポンシブ レイアウト
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.custom: contperf-fy21q2
dev_langs:
- csharp
- cppwinrt
ms.openlocfilehash: e2bc29acc63a5363891ad78b873db6c8311ac970
ms.sourcegitcommit: 06d59b59a95aad009acb947a0dac7432116bdb60
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2021
ms.locfileid: "100544652"
---
# <a name="responsive-layouts-with-xaml"></a>XAML でのレスポンシブ レイアウト

XAML レイアウト システムでは、応答性の高い UI を作成するために、要素の自動サイズ変更、レイアウト パネル、表示状態が提供されます。 レスポンシブ レイアウトを使用すると、サイズ、解像度、ピクセル密度、向きがさまざまに異なるアプリのウィンドウを画面で適切に表示できます。 「[レスポンシブ デザイン テクニック](responsive-design.md)」で説明されているように、位置変更、サイズ変更、リフロー、表示/非表示、再配置、またはアプリの UI の再構築にも XAML を使用できます。 ここでは、XAML を使ったレスポンシブ レイアウトを実装する方法について説明します。

## <a name="fluid-layouts-with-properties-and-panels"></a>プロパティとパネルを使用した柔軟なレイアウト

レスポンシブ レイアウトの基盤は、XAML レイアウト プロパティとパネルを適切に使用することにより、柔軟な方法でコンテンツの位置変更、サイズ変更、再配置を行うことです。

XAML レイアウト システムでは、静的レイアウトと柔軟なレイアウトの両方がサポートされます。 静的レイアウトでは、コントロールのピクセル サイズと位置を明示的に指定します。 ユーザーがデバイスの解像度や向きを変えても、UI は変更されません。 静的レイアウトは、フォーム ファクターやディスプレイ サイズが変わると、不適切にはみ出すことがあります。 一方、柔軟なレイアウトは、デバイス上で使用できる表示領域に合わせて縮小、拡大、再配置されます。

実際には、静的要素と柔軟な要素の組み合わせを使って UI を作成します。 場所によっては静的な要素と値を使うこともありますが、UI 全体のさまざまな解像度、画面サイズ、ビューへの応答性を高くする必要があります。

ここでは、XAML プロパティとレイアウト パネルを使って、柔軟なレイアウトを作成する方法を説明します。

### <a name="layout-properties"></a>レイアウト プロパティ
レイアウト プロパティは、要素のサイズと位置を制御します。 柔軟なレイアウトを作成するには、要素の自動または比例サイズ設定を使用し、必要に応じて、レイアウト パネルで子を配置できるようにします。

いくつかの一般的なレイアウト プロパティと、それらを使用して柔軟なレイアウトを作成する方法を示します。

**Height および Width**

[  **Height**](/uwp/api/windows.ui.xaml.frameworkelement.height) プロパティと [**Width**](/uwp/api/windows.ui.xaml.frameworkelement.width) プロパティは要素のサイズを指定します。 有効ピクセル単位で測定された固定値を使うことも、自動サイズ変更または比例サイズ変更を行うこともできます。

自動サイズ変更は、UI 要素をコンテンツや親コンテナーに合わせてサイズ変更します。 グリッドの行と列を使って、自動サイズ変更を行うこともできます。 自動サイズ変更を使うには、UI 要素の Height や Width を **Auto** に設定します。

> [!NOTE]
> コンテンツやコンテナーに合わせて要素のサイズが変更されるかどうかは、親コンテナーで子のサイズ変更を処理する方法によって決まります。 詳しくは、この記事の「[レイアウト パネル](#layout-panels)」をご覧ください。

比例サイズ変更 (*スター サイズ指定* とも呼ばれる) を使うと、使用可能なスペースが加重比率によりグリッドの行と列の間で分散されます。 XAML では、スター値は \* (重み付きのスター サイズ指定の場合は *n*\*) として表されます。 たとえば、2 段組レイアウトで 1 つの列と、幅が 5 倍の列とを指定するには、[**ColumnDefinition**](/uwp/api/Windows.UI.Xaml.Controls.ColumnDefinition) 要素の [**Width**](/uwp/api/windows.ui.xaml.controls.columndefinition.width) プロパティで "5\*" と "\*" を使います。

次の例では、4 つの列を含む [**Grid**](/uwp/api/Windows.UI.Xaml.Controls.Grid) で、固定、自動、比例サイズ指定を組み合わせています。

| 列 | サイズ変更 | 説明 |
| ------ | ------ | ----------- |
Column_1 | **自動** | 列は、コンテンツが収まるようにサイズ変更されます。
Column_2 | * | [自動] 列の計算後、この列は残りの幅の一部を取得します。 Column_2 の幅は Column_4 の半分になります。
Column_3 | **44** | 列の幅は 44 ピクセルに設定されます。
Column_4 | **2**\* | [自動] 列の計算後、この列は残りの幅の一部を取得します。 Column_4 の幅は Column_2 の 2 倍になります。

既定の列の幅は "*" であるため、2 つ目の列については、この値を明示的に設定する必要はありません。

```xaml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition/>
        <ColumnDefinition Width="44"/>
        <ColumnDefinition Width="2*"/>
    </Grid.ColumnDefinitions>
    <TextBlock Text="Column 1 sizes to its content." FontSize="24"/>
</Grid>
```

Visual Studio の XAML デザイナーでは、結果は次のように表示されます。

![Visual Studio デザイナーでの 4 列のグリッド](images/xaml-layout-grid-in-designer.png)

実行時に要素のサイズを取得するには、Height と Width の代わりに、読み取り専用の [**ActualHeight**](/uwp/api/windows.ui.xaml.frameworkelement.actualheight) プロパティと [**ActualWidth**](/uwp/api/windows.ui.xaml.frameworkelement.actualwidth) プロパティを使います。

**サイズの制約**

UI で自動サイズ変更を使用する場合でも、要素のサイズに制約を設けることが必要になる可能性があります。 [  **MinWidth**](/uwp/api/windows.ui.xaml.frameworkelement.minwidth)/[**MaxWidth**](/uwp/api/windows.ui.xaml.frameworkelement.maxwidth) と [**MinHeight**](/uwp/api/windows.ui.xaml.frameworkelement.minheight)/[**MaxHeight**](/uwp/api/windows.ui.xaml.frameworkelement.maxheight) の各プロパティを設定することによって、柔軟なサイズ変更を許可しながら、要素のサイズを制約する値を指定できます。

また、Grid では、MinWidth/MaxWidth を列定義と共に使用でき、MinHeight/MaxHeight を行定義と共に使用できます。

**配置**

親コンテナー内の要素の配置方法を指定するには、[**HorizontalAlignment**](/uwp/api/windows.ui.xaml.frameworkelement.horizontalalignment) プロパティと [**VerticalAlignment**](/uwp/api/windows.ui.xaml.frameworkelement.verticalalignment) プロパティを使います。
- **HorizontalAlignment** の値は、**Left**、**Center**、**Right**、**Stretch** です。
- **VerticalAlignment** の値は、**Top**、**Center**、**Bottom**、**Stretch** です。

**Stretch** 配置にすると、要素は、親コンテナーで提供されたスペース全体に配置されます。 Stretch は、両方の配置プロパティの既定値です。 ただし、[**Button**](/uwp/api/Windows.UI.Xaml.Controls.Button) などの一部のコントロールでは、その既定のスタイルでこの値がオーバーライドされます。
子要素を持つことができるすべての要素で、HorizontalAlignment プロパティと VerticalAlignment プロパティの Stretch 値を一意に処理することができます。 たとえば、既定の Stretch 値を使用する要素が Grid に配置された場合、要素はその要素を含むセルいっぱいに拡大されます。 同じ要素が Canvas に配置された場合は、そのコンテンツに合わせてサイズが変更されます。 各パネルでの Stretch 値の処理方法について詳しくは、「[レイアウト パネル](layout-panels.md)」をご覧ください。

詳しくは、「[配置、余白、およびパディング](alignment-margin-padding.md)」や、[**HorizontalAlignment**](/uwp/api/windows.ui.xaml.frameworkelement.horizontalalignment) と [**VerticalAlignment**](/uwp/api/windows.ui.xaml.frameworkelement.verticalalignment) のリファレンス ページをご覧ください。

**可視性**

[**Visibility**](/uwp/api/windows.ui.xaml.uielement.visibility) プロパティを次の [**Visibility** 列挙値](/uwp/api/Windows.UI.Xaml.Visibility)のいずれかに設定することによって、要素の表示と非表示を切り替えることができます:**Visible** または **Collapsed**。 要素が Collapsed である場合、UI レイアウト内の領域は使用されません。

コードまたは表示状態で、要素の Visibility プロパティを変更できます。 要素の Visibility が変更されると、そのすべての子要素も変更されます。 1 つのパネルを表示して別のパネルを折りたたむことによって、UI のセクションを置き換えることができます。

> [!Tip]
> UI に既定で **Collapsed** である要素がある場合、要素が表示されていなくても、オブジェクトは起動時に作成されます。 これらの要素の読み込みを表示されたときまで遅延するには、**x:DeferLoadStrategy 属性** を "Lazy" に設定します。 これにより起動時のパフォーマンスが向上することがあります。 詳しくは、「[x:DeferLoadStrategy 属性](../../xaml-platform/x-deferloadstrategy-attribute.md)」をご覧ください。

### <a name="style-resources"></a>Style リソース

コントロールに対して各プロパティ値を個別に設定する必要はありません。 通常、プロパティ値を [**Style**](/uwp/api/Windows.UI.Xaml.Style) リソースとしてグループ化し、Style をコントロールに適用する方が効率的です。 これは、特に、同じプロパティ値を多くのコントロールに適用する必要がある場合に当てはまります。 スタイルの使用について詳しくは、「[コントロールのスタイル](../controls-and-patterns/xaml-styles.md)」をご覧ください。

### <a name="layout-panels"></a>レイアウト パネル

ビジュアル オブジェクトを配置するには、パネルなどのコンテナー オブジェクトにビジュアル オブジェクトを配置する必要があります。 XAML フレームワークには、UI 要素を内部に配置できるコンテナーとしての役割を持つさまざまなパネル クラス ([**Canvas**](/uwp/api/Windows.UI.Xaml.Controls.Canvas)、[**Grid**](/uwp/api/Windows.UI.Xaml.Controls.Grid)、[**RelativePanel**](/uwp/api/Windows.UI.Xaml.Controls.RelativePanel)、[**StackPanel**](/uwp/api/Windows.UI.Xaml.Controls.StackPanel) など) が用意されています。

レイアウト パネルを選ぶ際に主に考慮が必要なのは、パネルでの子要素の配置とサイズです。 重複する子要素をお互いに重ねる方法を検討する必要があることもあります。

XAML フレームワークで提供されるパネル コントロールの主な機能の比較を以下に示します。

パネル コントロール | 説明
--------------|------------
[**Canvas**](/uwp/api/Windows.UI.Xaml.Controls.Canvas) | **Canvas** は柔軟な UI をサポートしていません。子要素の配置とサイズに関するすべての側面を制御します。 通常、グラフィックスの作成などの特殊な場合や、大規模なアダプティブ UI の小さな静的領域を定義するために使用します。 コードまたは表示状態を使って、実行時に要素の位置を変更できます。<li>Canvas.Top 添付プロパティと Canvas.Left 添付プロパティを使って、要素を絶対的に配置します。</li><li>Canvas.ZIndex 添付プロパティを使って、重なりを明示的に指定することもできます。</li><li>HorizontalAlignment/VerticalAlignment の Stretch の値は無視されます。 要素のサイズが明示的に設定されていない場合は、そのコンテンツに合わせてサイズ変更されます。</li><li>パネルより大きい場合、子のコンテンツは視覚上クリップされません。 </li><li>子のコンテンツはパネルの境界によって制約されません。</li>
[**Grid**](/uwp/api/Windows.UI.Xaml.Controls.Grid) | **Grid** は、子要素の柔軟なサイズ変更をサポートしています。 コードまたは表示状態を使って、要素の位置の変更や再配置を実行できます。<li>Grid.Row 添付プロパティと Grid.Column 添付プロパティを使って、要素は行と列に配置されます。</li><li>行や列をまたいで要素を表示するには、Grid.RowSpan 添付プロパティと Grid.ColumnSpan 添付プロパティを使います。</li><li>HorizontalAlignment/VerticalAlignment の Stretch の値は考慮されます。 要素のサイズを明示的に設定しないと、グリッド セルの利用可能な領域いっぱいに拡大されます。</li><li>パネルより大きい場合、子のコンテンツは視覚上クリップされます。</li><li>コンテンツのサイズはパネルの境界によって制約されるため、スクロール可能なコンテンツでは必要に応じてスクロール バーが表示されます。</li>
[**RelativePanel**](/uwp/api/Windows.UI.Xaml.Controls.RelativePanel) | <li>要素は、パネルの端または中央を基準として、および互いを基準として配置されます。</li><li>要素は、パネルの配置、兄弟の配置、兄弟の位置を制御するさまざまな添付プロパティを使用して配置されます。 </li><li>HorizontalAlignment/VerticalAlignment の Stretch 値は、配置の RelativePanel 添付プロパティが拡大の原因である場合 (要素がパネルの右端と左端の両方に整列される場合など) を除き、無視されます。 要素のサイズが明示的に設定されておらず、要素が拡大されていない場合、要素はそのコンテンツに合わせてサイズ変更されます。</li><li>パネルより大きい場合、子のコンテンツは視覚上クリップされます。</li><li>コンテンツのサイズはパネルの境界によって制約されるため、スクロール可能なコンテンツでは必要に応じてスクロール バーが表示されます。</li>
[**StackPanel**](/uwp/api/Windows.UI.Xaml.Controls.StackPanel) |<li>要素は、水平方向または垂直方向に 1 列に並べて表示されます。</li><li>HorizontalAlignment/VerticalAlignment の Stretch 値は、Orientation プロパティとは逆の方向で考慮されます。 要素のサイズが明示的に設定されていない場合、利用可能な幅 (Orientation が Horizontal の場合は高さ) いっぱいに拡大されます。 要素は、Orientation プロパティで指定された方向に、そのコンテンツに合わせてサイズ変更されます。</li><li>パネルより大きい場合、子のコンテンツは視覚上クリップされます。</li><li>コンテンツのサイズは、Orientation プロパティで指定された方向では、パネルの境界によって制約されないため、スクロール可能なコンテンツはパネルの境界を越えて拡大され、スクロール バーは表示されません。 スクロール バーを表示するには、子のコンテンツの高さ (または幅) を明示的に制約する必要があります。</li>
[**VariableSizedWrapGrid**](/uwp/api/Windows.UI.Xaml.Controls.VariableSizedWrapGrid) |<li>要素は、複数行、複数列に配置され、MaximumRowsOrColumns 値に達すると新しい行または列に自動的に折り返して配置されます。</li><li>要素を行と列のどちらの形式で配置するかは、Orientation プロパティで指定します。</li><li>行や列をまたいで要素を表示するには、VariableSizedWrapGrid.RowSpan 添付プロパティと VariableSizedWrapGrid.ColumnSpan 添付プロパティを使います。</li><li>HorizontalAlignment/VerticalAlignment の Stretch の値は無視されます。 ItemHeight プロパティと ItemWidth プロパティを指定すると、要素のサイズが変更されます。 これらのプロパティが設定されていない場合は、最初のセルのサイズから値が取得されます。</li><li>パネルより大きい場合、子のコンテンツは視覚上クリップされます。</li><li>コンテンツのサイズはパネルの境界によって制約されるため、スクロール可能なコンテンツでは必要に応じてスクロール バーが表示されます。</li>

これらのパネルの例および詳細情報については、「[レイアウト パネル](layout-panels.md)」をご覧ください。 [レスポンシブな手法のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlResponsiveTechniques)に関するページもご覧ください。

レイアウト パネルでは、コントロールの論理グループに UI を整理することができます。 適切なプロパティの設定で使用する場合、UI 要素の自動サイズ変更、位置変更、再配置などのサポートを取得します。 ただし、ほとんどの UI レイアウトでは、ウィンドウのサイズに大幅な変更がある場合、さらに変更が必要です。 これには、表示状態を使うことができます。

## <a name="adaptive-layouts-with-visual-states-and-state-triggers"></a>表示状態と状態トリガーを使ったアダプティブ レイアウト
ウィンドウのサイズまたはその他の変更に基づいて、UI に大幅な変更を行うには、表示状態を使用します。

アプリ ウィンドウを一定量を超えて拡大/縮小するときに、レイアウト プロパティを変更して、UI のセクションの位置変更、サイズ変更、再配置、表示、置換を行うことが必要になる可能性があります。 UI のさまざまな表示状態を定義し、ウィンドウの幅や高さが指定したしきい値を超えたときに適用できます。

[  **VisualState**](/uwp/api/Windows.UI.Xaml.VisualState) は、要素が特定の状態にあるときに、要素に適用されるプロパティ値を定義します。 指定された条件が満たされたときに適切な VisualState を適用する [**VisualStateManager**](/uwp/api/Windows.UI.Xaml.VisualStateManager) で表示状態をグループ化します。 [**AdaptiveTrigger**](/uwp/api/Windows.UI.Xaml.AdaptiveTrigger) を使うと、XAML に状態を適用するしきい値 ("ブレークポイント" とも呼ばれます) を簡単に設定できます。 または、コードで [**VisualStateManager.GoToState**](/uwp/api/windows.ui.xaml.visualstatemanager.gotostate) メソッドを呼び出して表示状態を適用することもできます。 次のセクションで、両方の方法の例を示します。

### <a name="set-visual-states-in-code"></a>コードでの表示状態の設定

コードで表示状態を適用するには、[**VisualStateManager.GoToState**](/uwp/api/windows.ui.xaml.visualstatemanager.gotostate) メソッドを呼び出します。 たとえば、アプリ ウィンドウが特定のサイズであるときに状態を適用するには、[**SizeChanged**](/uwp/api/windows.ui.xaml.window.sizechanged) イベントを処理し、**GoToState** を呼び出して適切な状態を適用します。

ここでは、[**VisualStateGroup**](/uwp/api/Windows.UI.Xaml.VisualStateGroup) に 2 つの VisualState の定義が含まれています。 最初の `DefaultState` は空です。 これが適用される場合、XAML ページで定義されている値が適用されます。 2 番目の `WideState` は、[**SplitView**](/uwp/api/Windows.UI.Xaml.Controls.SplitView) の [**DisplayMode**](/uwp/api/windows.ui.xaml.controls.splitview.displaymode) プロパティを **Inline** に変更し、ウィンドウを開きます。 この状態は、ウィンドウの幅が 640 有効ピクセルより大きい場合に、SizeChanged イベント ハンドラーで適用されます。

> [!NOTE]
> 先に進む前に知っておくべきですが、アプリが実行されている特定のデバイスをアプリが検出する手段は、Windows では提供されていません。 アプリが実行されているデバイス ファミリー (モバイル、デスクトップなど)、効果的な解像度、およびアプリが利用できる画面領域の量 (アプリのウィンドウのサイズ) は伝えることができます。 [画面のサイズとブレークポイント](screen-sizes-and-breakpoints-for-responsive-design.md)の表示状態を定義することをお勧めします。

```xaml
<Page ...
    SizeChanged="CurrentWindow_SizeChanged">
    <Grid>
        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup>
                <VisualState x:Name="DefaultState">
                        <Storyboard>
                        </Storyboard>
                    </VisualState>

                <VisualState x:Name="WideState">
                    <Storyboard>
                        <ObjectAnimationUsingKeyFrames
                            Storyboard.TargetProperty="SplitView.DisplayMode"
                            Storyboard.TargetName="mySplitView">
                            <DiscreteObjectKeyFrame KeyTime="0">
                                <DiscreteObjectKeyFrame.Value>
                                    <SplitViewDisplayMode>Inline</SplitViewDisplayMode>
                                </DiscreteObjectKeyFrame.Value>
                            </DiscreteObjectKeyFrame>
                        </ObjectAnimationUsingKeyFrames>
                        <ObjectAnimationUsingKeyFrames
                            Storyboard.TargetProperty="SplitView.IsPaneOpen"
                            Storyboard.TargetName="mySplitView">
                            <DiscreteObjectKeyFrame KeyTime="0" Value="True"/>
                        </ObjectAnimationUsingKeyFrames>
                    </Storyboard>
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>

        <SplitView x:Name="mySplitView" DisplayMode="CompactInline"
                   IsPaneOpen="False" CompactPaneLength="20">
            <!-- SplitView content -->

            <SplitView.Pane>
                <!-- Pane content -->
            </SplitView.Pane>
        </SplitView>
    </Grid>
</Page>
```

```csharp
private void CurrentWindow_SizeChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
{
    if (e.Size.Width > 640)
        VisualStateManager.GoToState(this, "WideState", false);
    else
        VisualStateManager.GoToState(this, "DefaultState", false);
}
```

```cppwinrt
// YourPage.h
void CurrentWindow_SizeChanged(winrt::Windows::Foundation::IInspectable const& sender, winrt::Windows::UI::Xaml::SizeChangedEventArgs const& e);

// YourPage.cpp
void YourPage::CurrentWindow_SizeChanged(IInspectable const& sender, SizeChangedEventArgs const& e)
{
    if (e.NewSize.Width > 640)
        VisualStateManager::GoToState(*this, "WideState", false);
    else
        VisualStateManager::GoToState(*this, "DefaultState", false);
}

```

### <a name="set-visual-states-in-xaml-markup"></a>XAML マークアップでの表示状態の設定

Windows 10 より前のバージョンでは、VisualState の定義にプロパティ変更のための [**Storyboard**](/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) オブジェクトが必要であり、コードで **GoToState** を呼び出して状態を適用する必要がありました。 これは前の例に示されています。 この構文はまだ多くの例で使用されており、この構文を使用する既存のコードがある可能性もあります。

Windows 10 以降では、ここで示す簡素化された [**Setter**](/uwp/api/Windows.UI.Xaml.Setter) 構文を使うことができ、XAML マークアップで [**StateTrigger**](/uwp/api/Windows.UI.Xaml.StateTrigger) を使って状態を適用できます。 状態トリガーを使って、アプリのイベントに応答して自動的に表示状態の変更をトリガーする単純な規則を作成します。

この例は前の例と同じですが、プロパティの変更を定義する Storyboard の代わりに、簡素化された **Setter** 構文を使用しています。 また、GoToState を呼び出す代わりに、組み込みの [**AdaptiveTrigger**](/uwp/api/Windows.UI.Xaml.AdaptiveTrigger) 状態トリガーを使って状態を適用しています。 状態トリガーを使う場合、空の `DefaultState` を定義する必要はありません。 状態トリガーの条件が満たされなくなったときには、既定の設定が自動的に再適用されます。

```xaml
<Page ...>
    <Grid>
        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup>
                <VisualState>
                    <VisualState.StateTriggers>
                        <!-- VisualState to be triggered when the
                             window width is >=640 effective pixels. -->
                        <AdaptiveTrigger MinWindowWidth="640" />
                    </VisualState.StateTriggers>

                    <VisualState.Setters>
                        <Setter Target="mySplitView.DisplayMode" Value="Inline"/>
                        <Setter Target="mySplitView.IsPaneOpen" Value="True"/>
                    </VisualState.Setters>
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>

        <SplitView x:Name="mySplitView" DisplayMode="CompactInline"
                   IsPaneOpen="False" CompactPaneLength="20">
            <!-- SplitView content -->

            <SplitView.Pane>
                <!-- Pane content -->
            </SplitView.Pane>
        </SplitView>
    </Grid>
</Page>
```

> [!Important]
> 前の例では、**Grid** 要素に対して VisualStateManager.VisualStateGroups 添付プロパティが設定されています。 StateTriggers を使う場合は、トリガーを自動的に有効にするために、常にルートの最初の子に VisualStateGroups が添付されていることを確認します  (ここでは、**Grid** がルートの **Page** 要素の最初の子です)。

### <a name="attached-property-syntax"></a>添付プロパティの構文

VisualState では、通常、コントロールのプロパティの値、つまりコントロールを含むパネルのいずれかの添付プロパティの値を設定します。 添付プロパティを設定するときは、添付プロパティ名をかっこで囲みます。

この例では、`myTextBox` という名前の TextBox に対して、[**RelativePanel.AlignHorizontalCenterWithPanel**](/uwp/api/windows.ui.xaml.controls.relativepanel.alignhorizontalcenterwithpanelproperty) 添付プロパティを設定する方法を示しています。 最初の XAML では [**ObjectAnimationUsingKeyFrames**](/uwp/api/Windows.UI.Xaml.Media.Animation.ObjectAnimationUsingKeyFrames) 構文を使用し、2 つ目の XAML では **Setter** 構文を使用しています。

```xaml
<!-- Set an attached property using ObjectAnimationUsingKeyFrames. -->
<ObjectAnimationUsingKeyFrames
    Storyboard.TargetProperty="(RelativePanel.AlignHorizontalCenterWithPanel)"
    Storyboard.TargetName="myTextBox">
    <DiscreteObjectKeyFrame KeyTime="0" Value="True"/>
</ObjectAnimationUsingKeyFrames>

<!-- Set an attached property using Setter. -->
<Setter Target="myTextBox.(RelativePanel.AlignHorizontalCenterWithPanel)" Value="True"/>
```

### <a name="custom-state-triggers"></a>カスタム状態トリガー

[  **StateTrigger**](/uwp/api/Windows.UI.Xaml.StateTrigger) クラスを拡張して、さまざまなシナリオに対するカスタム トリガーを作成できます。 たとえば、入力の種類に基づいてさまざまな状態をトリガーする StateTrigger を作成して、入力の種類がタッチである場合はコントロールの周囲の余白を増やすことができます。 また、アプリが実行されるデバイス ファミリに基づいてさまざまな状態を適用する StateTrigger を作成することもできます。 カスタム トリガーを作成し、それらを使用して単一の XAML ビュー内から最適化された UI エクスペリエンスを作成する方法の例については、[状態トリガーのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlStateTriggers)に関するページをご覧ください。

### <a name="visual-states-and-styles"></a>表示状態とスタイル

表示状態で Style リソースを使って、一連のプロパティの変更を複数のコントロールに適用できます。 スタイルの使用について詳しくは、「[コントロールのスタイル](../controls-and-patterns/xaml-styles.md)」をご覧ください。

状態トリガーのサンプルに関するページから引用したこの簡略化された XAML では、Style リソースを Button に適用して、マウスまたはタッチ入力の場合にサイズと余白を調整しています。 このカスタム状態トリガーの完全なコードおよび定義については、[状態トリガーのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlStateTriggers)に関するページをご覧ください。

```xaml
<Page ... >
    <Page.Resources>
        <!-- Styles to be used for mouse vs. touch/pen hit targets -->
        <Style x:Key="MouseStyle" TargetType="Rectangle">
            <Setter Property="Margin" Value="5" />
            <Setter Property="Height" Value="20" />
            <Setter Property="Width" Value="20" />
        </Style>
        <Style x:Key="TouchPenStyle" TargetType="Rectangle">
            <Setter Property="Margin" Value="15" />
            <Setter Property="Height" Value="40" />
            <Setter Property="Width" Value="40" />
        </Style>
    </Page.Resources>

    <RelativePanel>
        <!-- ... -->
        <Button Content="Color Palette Button" x:Name="MenuButton">
            <Button.Flyout>
                <Flyout Placement="Bottom">
                    <RelativePanel>
                        <Rectangle Name="BlueRect" Fill="Blue"/>
                        <Rectangle Name="GreenRect" Fill="Green" RelativePanel.RightOf="BlueRect" />
                        <!-- ... -->
                    </RelativePanel>
                </Flyout>
            </Button.Flyout>
        </Button>
        <!-- ... -->
    </RelativePanel>
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup x:Name="InputTypeStates">
            <!-- Second set of VisualStates for building responsive UI optimized for input type.
                 Take a look at InputTypeTrigger.cs class in CustomTriggers folder to see how this is implemented. -->
            <VisualState>
                <VisualState.StateTriggers>
                    <!-- This trigger indicates that this VisualState is to be applied when MenuButton is invoked using a mouse. -->
                    <triggers:InputTypeTrigger TargetElement="{x:Bind MenuButton}" PointerType="Mouse" />
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Target="BlueRect.Style" Value="{StaticResource MouseStyle}" />
                    <Setter Target="GreenRect.Style" Value="{StaticResource MouseStyle}" />
                    <!-- ... -->
                </VisualState.Setters>
            </VisualState>
            <VisualState>
                <VisualState.StateTriggers>
                    <!-- Multiple trigger statements can be declared in the following way to imply OR usage.
                         For example, the following statements indicate that this VisualState is to be applied when MenuButton is invoked using Touch OR Pen.-->
                    <triggers:InputTypeTrigger TargetElement="{x:Bind MenuButton}" PointerType="Touch" />
                    <triggers:InputTypeTrigger TargetElement="{x:Bind MenuButton}" PointerType="Pen" />
                </VisualState.StateTriggers>
                <VisualState.Setters>
                    <Setter Target="BlueRect.Style" Value="{StaticResource TouchPenStyle}" />
                    <Setter Target="GreenRect.Style" Value="{StaticResource TouchPenStyle}" />
                    <!-- ... -->
                </VisualState.Setters>
            </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>
</Page>
```

## <a name="related-topics"></a>関連トピック

- [チュートリアル: アダプティブ レイアウトを作成する](../basics/xaml-basics-adaptive-layout.md)
- [レスポンシブ手法のサンプル (GitHub)](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlResponsiveTechniques)
- [状態トリガーのサンプル (GitHub)](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlStateTriggers)
- [調整した複数のビューのサンプル (GitHub)](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlTailoredMultipleViews)
