---
Description: コレクション内の画像 (アルバム内の写真や製品の詳細ページ内の項目など) を一度に 1 つずつ表示します。
title: FlipView コントロールのガイドライン
ms.assetid: A4E05D92-1A0E-4CDD-84B9-92199FF8A8A3
label: Flip view
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: predavid
design-contact: kimsea
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 7e498caa51aa0820b8fb8709f8da178bcee1de9b
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89160236"
---
# <a name="flip-view"></a>フリップ ビュー

コレクション内の画像やその他の項目 (アルバムの写真や製品の詳細ページの項目など) を一度に 1 つずつ表示するには、フリップ ビュー コントロールを使います。 タッチ デバイスでは、項目をスワイプしてコレクション内を移動します。 マウスでは、マウスをホバーするとナビゲーション ボタンが表示されます。 キーボードでは、方向キーを使ってコレクション内を移動します。

**Windows UI ライブラリを入手する**

<img src="images/winui-logo-64x64.png" alt="WinUI logo"
     style="float: left; margin-right: 15px;" />

Windows UI ライブラリ 2.2 以降には、丸めた角を使用するこのコントロールの新しいテンプレートが含まれます。 詳しくは、「[角の半径](../style/rounded-corner.md)」をご覧ください。 WinUI は、Windows アプリの新しいコントロールと UI 機能が含まれる NuGet パッケージです。 インストール手順などについて詳しくは、「[Windows UI Library (Windows UI ライブラリ)](/uwp/toolkits/winui/)」をご覧ください。

> **プラットフォーム API:** [FlipView クラス](/uwp/api/windows.ui.xaml.controls.flipview)、[ItemsSource プロパティ](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource)、[ItemTemplate プロパティ](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemtemplate)

## <a name="is-this-the-right-control"></a>これは適切なコントロールですか?

フリップ ビューは、小規模から中規模のコレクション (最大で 25 個程度の項目を含むコレクション) の画像を参照する場合に最適です。 このようなコレクションの例として、製品の詳細ページ内の項目やフォト アルバム内の写真などがあります。 多くの場合、大規模なコレクションで FlipView を使うことはお勧めしませんが、このコントロールは、フォト アルバム内の個々の画像を表示するためによく使われます。

## <a name="examples"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/FlipView">アプリを開き、FlipView の動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

水平方向の閲覧、左端の項目から開始し、右にフリップするのが、FlipView の一般的なレイアウトです。 このレイアウトは、すべてのデバイス上で縦方向でも横方向でも正常に動作します。

![水平方向の FlipView のレイアウトに関する例](images/controls_flipview_horizonal.jpg)

フリップ ビューは、垂直方向にも閲覧できます。

![垂直方向のフリップ ビューに関する例](images/controls_flipview_vertical.jpg)

## <a name="create-a-flip-view"></a>フリップ ビューを作成する

FlipView は [ItemsControl](/uwp/api/windows.ui.xaml.controls.itemscontrol) であるため、あらゆる種類の項目をコレクションを含めることができます。 ビューのデータを設定するには、項目を [**Items**](/uwp/api/windows.ui.xaml.controls.itemscontrol.items) コレクションに追加するか、[**ItemsSource**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) プロパティをデータ ソースに設定します。

既定では、データ項目は、バインドされているデータ オブジェクトの文字列表現としてフリップ ビューに表示されます。 フリップ ビューでの項目の表示方法を正確に指定するには、[**DataTemplate**](/uwp/api/windows.ui.xaml.datatemplate) を作成して、個々の項目を表示するために使うコントロールのレイアウトを定義します。 レイアウト内のコントロールは、データ オブジェクトのプロパティにバインドすることも、インラインでコンテンツを定義することもできます。 DataTemplate は、FlipView の [**ItemTemplate**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemtemplate) プロパティに割り当てます。

### <a name="add-items-to-the-items-collection"></a>Items コレクションへの項目の追加

[  **Items**](/uwp/api/windows.ui.xaml.controls.itemscontrol.items) コレクションに項目を追加するには、XAML またはコードを使います。 通常、項目が少数で、その項目が変わらず、XAML で簡単に定義できる場合や、実行時にコードで項目を生成する場合は、この方法で項目を追加します。 項目をインラインで定義したフリップ ビューを次に示します。

```xaml
<FlipView x:Name="flipView1">
    <Image Source="Assets/Logo.png" />
    <Image Source="Assets/SplashScreen.png" />
    <Image Source="Assets/SmallLogo.png" />
</FlipView>
```

```csharp
// Create a new flip view, add content, 
// and add a SelectionChanged event handler.
FlipView flipView1 = new FlipView();
flipView1.Items.Add("Item 1");
flipView1.Items.Add("Item 2");

// Add the flip view to a parent container in the visual tree.
stackPanel1.Children.Add(flipView1);
```

フリップ ビューに項目を追加すると、追加した項目は [**FlipViewItem**](/uwp/api/Windows.UI.Xaml.Controls.FlipViewItem) コンテナーに自動的に設定されます。 項目の表示方法を変更するには、[**ItemContainerStyle**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemcontainerstyle) プロパティを設定して、項目コンテナーにスタイルを適用します。 

XAML で項目を定義すると、定義した項目は Items コレクションに自動的に追加されます。

### <a name="set-the-items-source"></a>項目ソースの設定

通常、フリップ ビューを使って、データベースやインターネットなどのソースからデータを表示します。 データ ソースからフリップ ビューのデータを設定するには、[**ItemsSource**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) プロパティをデータ項目のコレクションに設定します。

以下の例では、コードでコレクションのインスタンスに直接フリップ ビューの ItemsSource を設定しています。

```csharp
// Data source.
List<String> itemsList = new List<string>();
itemsList.Add("Item 1");
itemsList.Add("Item 2");

// Create a new flip view, add content, 
// and add a SelectionChanged event handler.
FlipView flipView1 = new FlipView();
flipView1.ItemsSource = itemsList;
flipView1.SelectionChanged += FlipView_SelectionChanged;

// Add the flip view to a parent container in the visual tree.
stackPanel1.Children.Add(flipView1);
```

ItemsSource プロパティを、XAML でコレクションにバインドすることもできます。 詳しくは、「[XAML を使ったデータ バインディング](../../data-binding/data-binding-quickstart.md)」をご覧ください。

ItemsSource が `itemsViewSource` という名前の [**CollectionViewSource**](/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) にバインドされている例を次に示します。 

```xaml
<Page.Resources>
    <!-- Collection of items displayed by this page -->
    <CollectionViewSource x:Name="itemsViewSource" Source="{Binding Items}"/>
</Page.Resources>

...

<FlipView x:Name="itemFlipView" 
          ItemsSource="{Binding Source={StaticResource itemsViewSource}}"/>
```

>**注**&nbsp;&nbsp;フリップ ビューのデータを設定するには、その Items コレクションに項目を追加するか ItemsSource プロパティを設定しますが、同時に両方の方法で設定することはできません。 ItemsSource プロパティを設定して XAML で項目を追加した場合、追加された項目は無視されます。 ItemsSource プロパティを設定してコードで Items コレクションに項目を追加した場合、例外がスローされます。

### <a name="specify-the-look-of-the-items"></a>項目の表示方法の指定

既定では、データ項目は、バインドされているデータ オブジェクトの文字列表現としてフリップ ビューに表示されます。 通常は、よりリッチな表現でデータを表示する必要があります。 フリップ ビューでの項目の表示方法を正確に指定するには、[**DataTemplate**](/uwp/api/Windows.UI.Xaml.DataTemplate) を作成します。 DataTemplate の XAML では、個々の項目を表示するために使うコントロールのレイアウトと外観を定義します。 レイアウト内のコントロールは、データ オブジェクトのプロパティにバインドすることも、インラインでコンテンツを定義することもできます。 DataTemplate は、FlipView の [**ItemTemplate**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemtemplate) プロパティに割り当てます。

この例では、FlipView の ItemTemplate がインラインで定義されています。 画像名を表示するためにオーバーレイが画像に追加されます。 

```XAML
<FlipView x:Name="flipView1" Width="480" Height="270" 
          BorderBrush="Black" BorderThickness="1">
    <FlipView.ItemTemplate>
        <DataTemplate>
            <Grid>
                <Image Width="480" Height="270" Stretch="UniformToFill"
                       Source="{Binding Image}"/>
                <Border Background="#A5000000" Height="80" VerticalAlignment="Bottom">
                    <TextBlock Text="{Binding Name}" 
                               FontFamily="Segoe UI" FontSize="26.667" 
                               Foreground="#CCFFFFFF" Padding="15,20"/>
                </Border>
            </Grid>
        </DataTemplate>
    </FlipView.ItemTemplate>
</FlipView>
```

このデータ テンプレートで定義されたレイアウトは次のように表示されます。

フリップ ビュー データ テンプレート。

### <a name="set-the-orientation-of-the-flip-view"></a>フリップ ビューの向きの設定

既定では、フリップ ビューは横方向にめくれます。 縦方向にめくれるようにするには、フリップ ビューの [**ItemsPanel**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemspanel) として縦方向のスタック パネルを使います。

次の例は、FlipView の ItemsPanel として縦方向のスタック パネルを使う方法を示しています。

```XAML
<FlipView x:Name="flipViewVertical" Width="480" Height="270" 
          BorderBrush="Black" BorderThickness="1">
    
    <!-- Use a vertical stack panel for vertical flipping. -->
    <FlipView.ItemsPanel>
        <ItemsPanelTemplate>
            <VirtualizingStackPanel Orientation="Vertical"/>
        </ItemsPanelTemplate>
    </FlipView.ItemsPanel>
    
    <FlipView.ItemTemplate>
        <DataTemplate>
            <Grid>
                <Image Width="480" Height="270" Stretch="UniformToFill"
                       Source="{Binding Image}"/>
                <Border Background="#A5000000" Height="80" VerticalAlignment="Bottom">
                    <TextBlock Text="{Binding Name}" 
                               FontFamily="Segoe UI" FontSize="26.667" 
                               Foreground="#CCFFFFFF" Padding="15,20"/>
                </Border>
            </Grid>
        </DataTemplate>
    </FlipView.ItemTemplate>
</FlipView>
```

縦方向のフリップ ビューは次のように表示されます。

![垂直方向のフリップ ビューに関する例](images/controls_flipview_vertical.jpg)

## <a name="adding-a-context-indicator"></a>コンテキスト インジケーターの追加

フリップ ビュー内のコンテキスト インジケーターによって、便利な基準点を設けることができます。 標準的なコンテキスト インジケーターに含まれるドットは、対話型です。 次の例に示されているように、最適な配置は、通常はギャラリーの下中央です。

![ページ インジケーターの例](images/controls_pageindicator.png)

比較的大きなコレクション (10 ～ 25 個の項目) の場合、より多くのコンテキストを提供するインジケーター (縮小表示のフィルム ストリップなど) を使用することを検討します。 単純なドットを使用するコンテキスト インジケーターとは異なり、フィルム ストリップ内の各サムネイルは対応する画像の小さいバージョンであり、選択可能にする必要があります。

![コンテキスト インジケーターの例](images/controls_contextindicator.jpg)

コンテキスト インジケーターを FlipView に追加する方法を示すサンプル コードについては、[XAML FlipView のサンプルに関するページ](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Windows%208%20app%20samples/%5BC%23%5D-Windows%208%20app%20samples/C%23/Windows%208%20app%20samples/XAML%20FlipView%20control%20sample%20(Windows%208))をご覧ください。

## <a name="dos-and-donts"></a>推奨と非推奨

-   FlipView は最大 25 個程度の項目のコレクションに最適です。
-   大規模なコレクションでは FlipView コントロールを使わないでください。これは、項目ごとにフリップ操作を繰り返す必要があり、ユーザーの負担になるためです。 フォト アルバムは例外です。フォト アルバムには数百または数千の画像が含まれている場合があります。 ほとんどの場合、フォト アルバムでは、グリッド ビューのレイアウトで写真を選ぶと、フリップ ビューに切り替わります。 他の大きいコレクションについては、[リスト ビューまたはグリッド ビュー](lists.md)を検討してください。
-   コンテキスト インジケーターの場合:
    -   ドット (または選択した任意の視覚的マーカー) の順序は、中央に配置され、水平方向にパンするギャラリーの下にあるときに最適に動作します。
    -   垂直方向にパンするギャラリーでコンテキスト インジケーターを使う場合は、中央に配置され、画像の右側にあるときに最適な動作になります。
    -   強調表示されているドットは現在の項目を示します。 通常、強調表示されているドットは白で、その他のドットは灰色で表されます。
    -   ドットの数は変更できますが、多すぎるとユーザーは現在の場所を把握することが難しくなります。通常、表示するドットの最大数は 10 個です。

## <a name="globalization-and-localization-checklist"></a>グローバリゼーションとローカライズのチェックリスト

<table>
<tr>
<th>双方向対応に関する考慮事項</th><td>RTL 言語には標準の左右反転を使用します。 "戻る" と "進む" のコントロールは言語の方向に基づく必要があります。RTL 言語では、右ボタンが "戻る" で、左ボタンが "進む" となります。</td>
</tr>

</table>

## <a name="get-the-sample-code"></a>サンプル コードの入手

- [XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。

## <a name="related-articles"></a>関連記事

- [リストのガイドライン](lists.md)
- [**FlipView クラス**](/uwp/api/Windows.UI.Xaml.Controls.FlipView)