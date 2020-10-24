---
ms.assetid: 26DF15E8-2C05-4174-A714-7DF2E8273D32
title: ListView と GridView の UI の最適化
description: ListView と GridView のパフォーマンスと起動時間を、UI の仮想化や要素の削減、項目の段階的な更新を通して向上させます。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 19749ff80401ccb8a3a4fae0ef6e237f42aeeb40
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89166076"
---
# <a name="listview-and-gridview-ui-optimization"></a>ListView と GridView の UI の最適化


**注**   詳しくは、//build/ セッション「[ユーザーが GridView と ListView で大量のデータを操作するときのパフォーマンスを大幅に向上させる](https://channel9.msdn.com/events/build/2013/3-158)」をご覧ください。

[  **ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) と [**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) のパフォーマンスと起動時間を、UI の仮想化や要素の削減、項目の段階的な更新を通して向上させます。 データ仮想化の手法については、[ListView と GridView のデータ仮想化](listview-and-gridview-data-optimization.md)」をご覧ください。

## <a name="two-key-factors-in-collection-performance"></a>コレクションのパフォーマンスの主要な 2 つの要因

コレクションの操作は、よくある状況です。 フォト ビューアーには写真のコレクションが、リーダーには記事/書籍/ストーリーのコレクションが、ショッピング アプリには製品のコレクションがあります。 このトピックでは、アプリでコレクションの操作を効率よく行うために何ができるかについて説明します。

コレクションのパフォーマンスに関しては、2 つの主要な要因があります。1 つは項目を作成する UI スレッドによって費やされる時間で、もう 1 つは生のデータ セットとそのデータをレンダリングするために使用される UI 要素の両方で使用されるメモリです。

スムーズなパン/スクロールを行うには、UI スレッドで効率的かつスマートなインスタンス化、データ バインド、および項目のレイアウトを実行することが不可欠です。

## <a name="ui-virtualization"></a>UI の仮想化

UI の仮想化は、実行できる最も重要な改善策です。 これは、項目を表す UI 要素がオンデマンドで作成されることを意味します。 1,000 項目のコレクションにバインドされている項目コントロールでは、すべての項目の UI を同時に作成しても、同時に全部を表示することはできないため、リソースを無駄に使うことになります。 UI の仮想化は、[**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) と [**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) (およびその他の [**ItemsControl**](/uwp/api/Windows.UI.Xaml.Controls.ItemsControl) から派生した標準コントロール) によって自動的に実行されます。 数ページ先にある項目がスクロールされて表示されそうになると、フレームワークがその項目用の UI を生成してキャッシュします。 項目がもう一度表示される可能性が低い場合、フレームワークはメモリを解放します。

カスタム項目パネル テンプレート ([**ItemsPanel**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemspanel) をご覧ください) を用意する場合は、[**ItemsWrapGrid**](/uwp/api/Windows.UI.Xaml.Controls.ItemsWrapGrid) や [**ItemsStackPanel**](/uwp/api/Windows.UI.Xaml.Controls.ItemsStackPanel) などの仮想パネルを必ず使用してください。 [  **VariableSizedWrapGrid**](/uwp/api/Windows.UI.Xaml.Controls.VariableSizedWrapGrid)、[**WrapGrid**](/uwp/api/Windows.UI.Xaml.Controls.WrapGrid)、または [**StackPanel**](/uwp/api/Windows.UI.Xaml.Controls.StackPanel) を使用した場合、仮想化は得られません。 また、[**ChoosingGroupHeaderContainer**](/uwp/api/windows.ui.xaml.controls.listviewbase.choosinggroupheadercontainer)、[**ChoosingItemContainer**](/uwp/api/windows.ui.xaml.controls.listviewbase.choosingitemcontainer)、[**ContainerContentChanging**](/uwp/api/windows.ui.xaml.controls.listviewbase.containercontentchanging) の各 [**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) イベントは、[**ItemsWrapGrid**](/uwp/api/Windows.UI.Xaml.Controls.ItemsWrapGrid) または [**ItemsStackPanel**](/uwp/api/Windows.UI.Xaml.Controls.ItemsStackPanel) を使用したときにのみ発生します。

表示される可能性のある要素の作成はフレームワークが行う必要があるため、ビューポートの概念は UI の仮想化にとって非常に重要です。 一般的に、[**ItemsControl**](/uwp/api/Windows.UI.Xaml.Controls.ItemsControl) のビューポートは論理コントロールの範囲を指します。 たとえば、[**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) のビューポートは **ListView** 要素の幅と高さです。 一部のパネルでは子要素に制限のない空間を与えることができます。たとえば [**ScrollViewer**](/uwp/api/Windows.UI.Xaml.Controls.ScrollViewer) や [**Grid**](/uwp/api/Windows.UI.Xaml.Controls.Grid) では、行または列のサイズが自動的に調整されます。 このようなパネルに仮想化された **ItemsControl** を配置すると、すべての項目を表示できるスペースが用意され、仮想化の意味がなくなります。 仮想化を復元するには、**ItemsControl** に幅と高さを設定します。

## <a name="element-reduction-per-item"></a>項目ごとの要素の削減

項目をレンダリングするために使う UI 要素の数を、妥当と思われる最小限の数に抑えます。

項目コントロールが初めて表示されるとき、すべての項目を含むビューポートをレンダリングするために必要なすべての要素が作成されます。 さらに、項目がビューポートに近づくにつれて、キャッシュされている項目テンプレート内の UI 要素が、フレームワークによって、バインドされたデータ オブジェクトで更新されます。 テンプレート内のマークアップの複雑さを最小限に抑えると、メモリと UI スレッドで費やされる時間の減少という効果が生まれ、特にパン/スクロール中の応答性が向上します。 問題のテンプレートは、項目テンプレート ([**ItemTemplate**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemtemplate) をご覧ください) と、[**ListViewItem**](/uwp/api/windows.ui.xaml.controls.listviewitem) または [**GridViewItem**](/uwp/api/windows.ui.xaml.controls.gridviewitem) のコントロール テンプレート (項目コントロール テンプレート、つまり [**ItemContainerStyle**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemcontainerstyle)) です。 要素の数を少し減らすだけでも、その効果は、表示される項目の数と比例して大きくなります。

要素の削減の例については、「[XAML マークアップの最適化](optimize-xaml-loading.md)」をご覧ください。

[  **ListViewItem**](/uwp/api/windows.ui.xaml.controls.listviewitem) と [**GridViewItem**](/uwp/api/windows.ui.xaml.controls.gridviewitem) 用の既定のコントロール テンプレートには、[**ListViewItemPresenter**](/uwp/api/Windows.UI.Xaml.Controls.Primitives.ListViewItemPresenter) 要素が含まれています。 このプレゼンターは、フォーカス状態や選択状態などの複雑な視覚効果を表示する、1 つの最適化された要素です。 カスタム項目コントロール テンプレート ([**ItemContainerStyle**](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemcontainerstyle)) が既に存在する場合、または今後項目コントロール テンプレートのコピーを編集する場合は、**ListViewItemPresenter** を使うことをお勧めします。この要素を使うと、ほとんどの場合、パフォーマンスとカスタム可能性の最適バランスを得ることができます。 このプレゼンターは、プロパティを設定することによってカスタマイズできます。 例として、項目が選ばれたときに既定で表示されるチェック マークを削除し、選ばれた項目の背景色をオレンジ色に変更するマークアップを次に示します。

```xml
...
<ListView>
 ...
 <ListView.ItemContainerStyle>
 <Style TargetType="ListViewItem">
 <Setter Property="Template">
 <Setter.Value>
 <ControlTemplate TargetType="ListViewItem">
 <ListViewItemPresenter SelectionCheckMarkVisualEnabled="False" SelectedBackground="Orange"/>
 </ControlTemplate>
 </Setter.Value>
 </Setter>
 </Style>
 </ListView.ItemContainerStyle>
</ListView>
<!-- ... -->
```

[  **SelectionCheckMarkVisualEnabled**](/uwp/api/windows.ui.xaml.controls.primitives.listviewitempresenter.selectioncheckmarkvisualenabled) と [**SelectedBackground**](/uwp/api/windows.ui.xaml.controls.primitives.listviewitempresenter.selectedbackground) に似た 25 個のわかりやすい名前のプロパティがあります。 これらのプレゼンターを使用目的に合うように十分にカスタマイズできないことがわかった場合は、`ListViewItemExpanded` または `GridViewItemExpanded` コントロール テンプレートのコピーを代わりに編集できます。 これらは、`\Program Files (x86)\Windows Kits\10\DesignTime\CommonConfiguration\Neutral\UAP\<version>\Generic\generic.xaml` の中にあります。 ただし、これらのテンプレートの使用は、パフォーマンスを多少低下させる代償としてカスタマイズの可能性を大きくする意味があることに注意してください。

<span id="update-items-incrementally"/>

## <a name="update-listview-and-gridview-items-progressively"></a>GridView と ListView の項目を段階的に更新する

データ仮想化を使う場合は、項目の読み込み中に一時的な UI 要素をレンダリングするようにコントロールを構成することで、[**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) と [**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) の高い応答性を維持できます。 一時的な要素は、データが読み込まれるときに実際の UI と段階的に置き換えることができます。

また、データの読み込み元 (ローカル ディスク、ネットワーク、またはクラウド) に関係なく、ユーザーは、[**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) または [**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) をすばやくパン/スクロールできます。この間、スピードが速すぎて完全な忠実度で各項目をレンダリングすることはできませんが、スムーズなパン/スクロールは維持されます。 スムーズなパン/スクロールを維持するために、プレース ホルダーを使うだけでなく、項目を複数のフェーズでレンダリングすることを選ぶことができます。

これらの手法の使用例は、写真表示アプリでよく見られます。画像のすべてが読み込まれて表示されていない場合でも、ユーザーはコレクションをパン/スクロールして操作できます。 または、「映画」の項目の場合は、第 1 のフェーズでタイトルを表示し、第 2 のフェーズでその評価を表示し、第 3 のフェーズでポスターの画像を表示できます。 ユーザーは各項目について最も重要なデータをできるだけ早く見ることができ、それはユーザーがすぐに行動を起こせることを意味します。 その後、時間の許す限り、重要度の低い情報を表示します。 これらの手法を実装するために使うことができるプラットフォームの機能を次に示します。

### <a name="placeholders"></a>プレースホルダー

一時的なプレースホルダーの視覚効果機能は、既定でオンになっています。それは [**ShowsScrollingPlaceholders**](/uwp/api/windows.ui.xaml.controls.listviewbase.showsscrollingplaceholders) プロパティによって制御されます。 高速なパン/スクロールが行われている間、この機能は、滑らかな動きを維持したまま、完全に表示されていない項目が存在することを示す視覚的なヒントをユーザーに与えます。 次のいずれかの手法を使う場合は、必要に応じて **ShowsScrollingPlaceholders** を false に設定して、プレースホルダーが表示されないようにすることができます。

**x:Phase を使用した段階的なデータ テンプレートの更新**

[x:Phase 属性](../xaml-platform/x-phase-attribute.md)と [{x:Bind}](../xaml-platform/x-bind-markup-extension.md) バインドを使って段階的なデータ テンプレートの更新を実装する方法を次に示します。

1.  これは、バインディング ソースがどのようになるかを示しています (これは、バインド先のデータ ソースです)。

    ```csharp
    namespace LotsOfItems
    {
        public class ExampleItem
        {
            public string Title { get; set; }
            public string Subtitle { get; set; }
            public string Description { get; set; }
        }

        public class ExampleItemViewModel
        {
            private ObservableCollection<ExampleItem> exampleItems = new ObservableCollection<ExampleItem>();
            public ObservableCollection<ExampleItem> ExampleItems { get { return this.exampleItems; } }

            public ExampleItemViewModel()
            {
                for (int i = 1; i < 150000; i++)
                {
                    this.exampleItems.Add(new ExampleItem(){
                        Title = "Title: " + i.ToString(),
                        Subtitle = "Sub: " + i.ToString(),
                        Description = "Desc: " + i.ToString()
                    });
                }
            }
        }
    }
    ```
2.  これは、`DeferMainPage.xaml` に含まれるマークアップです。 グリッド ビューには、**MyItem** クラスの **Title** プロパティ、**Subtitle** プロパティ、**Description** プロパティにバインドされた項目テンプレートが含まれます。 **x:Phase** の既定値は 0 であることに注意してください。 ここでは、項目は、そのタイトルだけが最初にレンダリングされます。 次に、サブタイトル要素がバインドされたデータになり、すべての項目に表示され、以下、同じようにすべてのフェーズが処理されます。
    ```xml
    <Page
        x:Class="LotsOfItems.DeferMainPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:lotsOfItems="using:LotsOfItems"
        mc:Ignorable="d">

        <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
            <GridView ItemsSource="{x:Bind ViewModel.ExampleItems}">
                <GridView.ItemTemplate>
                    <DataTemplate x:DataType="lotsOfItems:ExampleItem">
                        <StackPanel Height="100" Width="100" Background="OrangeRed">
                            <TextBlock Text="{x:Bind Title}"/>
                            <TextBlock Text="{x:Bind Subtitle}" x:Phase="1"/>
                            <TextBlock Text="{x:Bind Description}" x:Phase="2"/>
                        </StackPanel>
                    </DataTemplate>
                </GridView.ItemTemplate>
            </GridView>
        </Grid>
    </Page>
    ```

3.  今すぐアプリを実行し、グリッド ビューですばやくパン/スクロールすると、新しい項目が画面に表示されるとき、項目は最初は濃い灰色の四角形としてレンダリングされ ([**ShowsScrollingPlaceholders**](/uwp/api/windows.ui.xaml.controls.listviewbase.showsscrollingplaceholders) プロパティが既定で **true** に設定されているためです)、次にタイトルが表示され、その後にサブタイトルと説明が表示されることがわかります。

**ContainerContentChanging を使用した段階的なデータ テンプレートの更新**

[  **ContainerContentChanging**](/uwp/api/windows.ui.xaml.controls.listviewbase.containercontentchanging) の一般的な戦略は、**Opacity** を使ってすぐに表示する必要がない要素を非表示にすることです。 要素をリサイクルすると以前の値が保持されるため、新しいデータ項目の値で更新するまで、要素を非表示にします。 イベント引数で **Phase** プロパティを使って、どの要素を更新して表示するかを決めます。 追加のフェーズが必要な場合は、コールバックを登録します。

1.  **x:Phase** と同じバインド ソースを使用します。

2.  これは、`MainPage.xaml` に含まれるマークアップです。 グリッド ビューは、その [**ContainerContentChanging**](/uwp/api/windows.ui.xaml.controls.listviewbase.containercontentchanging) イベントに対してハンドラーを宣言します。その中には、**MyItem** クラスの **Title** プロパティ、**Subtitle** プロパティ、**Description** プロパティを表示するために使われる要素を持つ項目テンプレートが含まれます。 **ContainerContentChanging** を使ったパフォーマンス上の最大のメリットを得るため、マークアップではバインドを使わず、代わりに値をプログラムを使って割り当てます。 ここでの例外は、フェーズ 0 とみなしているタイトルを表示する要素です。
    ```xml
    <Page
        x:Class="LotsOfItems.MainPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:lotsOfItems="using:LotsOfItems"
        mc:Ignorable="d">

        <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
            <GridView ItemsSource="{x:Bind ViewModel.ExampleItems}" ContainerContentChanging="GridView_ContainerContentChanging">
                <GridView.ItemTemplate>
                    <DataTemplate x:DataType="lotsOfItems:ExampleItem">
                        <StackPanel Height="100" Width="100" Background="OrangeRed">
                            <TextBlock Text="{x:Bind Title}"/>
                            <TextBlock Opacity="0"/>
                            <TextBlock Opacity="0"/>
                        </StackPanel>
                    </DataTemplate>
                </GridView.ItemTemplate>
            </GridView>
        </Grid>
    </Page>
    ```
3.  最後に、[**ContainerContentChanging**](/uwp/api/windows.ui.xaml.controls.listviewbase.containercontentchanging) イベント ハンドラーの実装を示します。 このコードは、**RecordingViewModel** 型のプロパティを **MainPage** に追加して、マークアップのページを表すクラスからバインディング ソース クラスを公開する方法も示しています。 データ テンプレート内に [{Binding}](../xaml-platform/binding-markup-extension.md) バインドが含まれていない限り、イベント引数オブジェクトをハンドラーの最初のフェーズで処理するようにマークして、データ コンテキストを設定する必要はないことを項目に通知します。
    ```csharp
    namespace LotsOfItems
    {
        /// <summary>
        /// An empty page that can be used on its own or navigated to within a Frame.
        /// </summary>
        public sealed partial class MainPage : Page
        {
            public MainPage()
            {
                this.InitializeComponent();
                this.ViewModel = new ExampleItemViewModel();
            }

            public ExampleItemViewModel ViewModel { get; set; }

            // Display each item incrementally to improve performance.
            private void GridView_ContainerContentChanging(ListViewBase sender, ContainerContentChangingEventArgs args)
            {
                if (args.Phase != 0)
                {
                    throw new System.Exception("We should be in phase 0, but we are not.");
                }

                // It's phase 0, so this item's title will already be bound and displayed.

                args.RegisterUpdateCallback(this.ShowSubtitle);

                args.Handled = true;
            }

            private void ShowSubtitle(ListViewBase sender, ContainerContentChangingEventArgs args)
            {
                if (args.Phase != 1)
                {
                    throw new System.Exception("We should be in phase 1, but we are not.");
                }

                // It's phase 1, so show this item's subtitle.
                var templateRoot = args.ItemContainer.ContentTemplateRoot as StackPanel;
                var textBlock = templateRoot.Children[1] as TextBlock;
                textBlock.Text = (args.Item as ExampleItem).Subtitle;
                textBlock.Opacity = 1;

                args.RegisterUpdateCallback(this.ShowDescription);
            }

            private void ShowDescription(ListViewBase sender, ContainerContentChangingEventArgs args)
            {
                if (args.Phase != 2)
                {
                    throw new System.Exception("We should be in phase 2, but we are not.");
                }

                // It's phase 2, so show this item's description.
                var templateRoot = args.ItemContainer.ContentTemplateRoot as StackPanel;
                var textBlock = templateRoot.Children[2] as TextBlock;
                textBlock.Text = (args.Item as ExampleItem).Description;
                textBlock.Opacity = 1;
            }
        }
    }
    ```

4.  今すぐアプリを実行し、グリッド ビューですばやくパン/スクロールすると、**x:Phase** と同じ動作が起こることがわかります。

## <a name="container-recycling-with-heterogeneous-collections"></a>異種コレクションでのコンテナー リサイクル

一部のアプリケーションでは、コレクション内のさまざまな種類の項目に合わせて異なる UI を用意する必要があります。 これにより、仮想化されるパネルで、項目を表示するために使用される視覚要素を再利用またはリサイクルすることができない状況が発生する場合があります。 パンした時に項目の視覚要素を再作成すると、仮想化によって得られた多くのパフォーマンスのメリットが取り消されます。 ただし、少し計画することで、仮想化されるパネルで要素を再利用できるようになります。 開発者には、シナリオに応じて、[**ChoosingItemContainer**](/uwp/api/windows.ui.xaml.controls.listviewbase.choosingitemcontainer) イベントまたは項目テンプレート セレクターの 2 つのオプションがあります。 **ChoosingItemContainer** アプローチでは、パフォーマンスが向上します。

**ChoosingItemContainer イベント**

[**ChoosingItemContainer**](/uwp/api/windows.ui.xaml.controls.listviewbase.choosingitemcontainer) は、起動時やリサイクル時に新しい項目が必要になったときに、[**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView)/[**GridView**](/uwp/api/Windows.UI.Xaml.Controls.GridView) に項目 (**ListViewItem**/**GridViewItem**) を提供できるようにするイベントです。 コンテナーが表示するデータ項目の種類に基づいてコンテナーを作成できます (次の例で示します)。 **ChoosingItemContainer** は、より効率よく、異なる項目に異なるデータ テンプレートを使用するための方法です。 **ChoosingItemContainer** を使って実現できるものとして、コンテナーのキャッシュがあります。 たとえば、5 種類のテンプレートがあり、そのうちの 1 つのテンプレートが、他と比べて 1 桁多く発生している場合、ChoosingItemContainer を使うと、必要な比率で項目を作成できるだけでなく、キャッシュされた要素とリサイクルに利用できる要素も適切な数に維持されます。 [**ChoosingGroupHeaderContainer**](/uwp/api/windows.ui.xaml.controls.listviewbase.choosinggroupheadercontainer) は、グループ ヘッダーと同じ機能を提供します。

```csharp
// Example shows how to use ChoosingItemContainer to return the correct
// DataTemplate when one is available. This example shows how to return different 
// data templates based on the type of FileItem. Available ListViewItems are kept
// in two separate lists based on the type of DataTemplate needed.
private void ListView_ChoosingItemContainer
    (ListViewBase sender, ChoosingItemContainerEventArgs args)
{
    // Determines type of FileItem from the item passed in.
    bool special = args.Item is DifferentFileItem;

    // Uses the Tag property to keep track of whether a particular ListViewItem's 
    // datatemplate should be a simple or a special one.
    string tag = special ? "specialFiles" : "simpleFiles";

    // Based on the type of datatemplate needed return the correct list of 
    // ListViewItems, this could have also been handled with a hash table. These 
    // two lists are being used to keep track of ItemContainers that can be reused.
    List<UIElement> relevantStorage = special ? specialFileItemTrees : simpleFileItemTrees;

    // args.ItemContainer is used to indicate whether the ListView is proposing an 
    // ItemContainer (ListViewItem) to use. If args.Itemcontainer, then there was a 
    // recycled ItemContainer available to be reused.
    if (args.ItemContainer != null)
    {
        // The Tag is being used to determine whether this is a special file or 
        // a simple file.
        if (args.ItemContainer.Tag.Equals(tag))
        {
            // Great: the system suggested a container that is actually going to 
            // work well.
        }
        else
        {
            // the ItemContainer's datatemplate does not match the needed 
            // datatemplate.
            args.ItemContainer = null;
        }
    }

    if (args.ItemContainer == null)
    {
        // see if we can fetch from the correct list.
        if (relevantStorage.Count > 0)
        {
            args.ItemContainer = relevantStorage[0] as SelectorItem;
        }
        else
        {
            // there aren't any (recycled) ItemContainers available. So a new one 
            // needs to be created.
            ListViewItem item = new ListViewItem();
            item.ContentTemplate = this.Resources[tag] as DataTemplate;
            item.Tag = tag;
            args.ItemContainer = item;
        }
    }
}
```

**項目テンプレート セレクター**

項目テンプレート セレクター ([**DataTemplateSelector**](/uwp/api/Windows.UI.Xaml.Controls.DataTemplateSelector)) により、アプリで、表示されるデータ項目の種類に基づいて、実行時に異なる項目テンプレートを返すことができます。 これにより、開発の生産性は向上しますが、すべてのデータ項目について、すべての項目テンプレートを再利用できるわけではないため、UI の仮想化はより難しくなります。

項目 (**ListViewItem**/**GridViewItem**) をリサイクルする場合、リサイクル キュー (リサイクル キューは現在データを表示するために使用されていない項目のキャッシュです) で使用できる項目の項目テンプレートが、現在のデータ項目で求められるテンプレートと一致するかどうかを、フレームワークが判断する必要があります。 リサイクル キューに適切な項目テンプレートを持つ項目がない場合、新しい項目が作成され、適切な項目テンプレートがインスタンス化されます。 一方、リサイクル キューに、適切な項目テンプレートを持つ項目が含まれている場合、その項目はリサイクル キューから削除され、現在のデータ項目のために使用されます。 項目テンプレート セレクターは、使用されている項目テンプレートの数が少なく、異なる項目テンプレートを使用する項目のコレクション全体にわたって項目がフラットに分布しているような状況に適しています。

異なる項目テンプレートを使う項目が均一に分布していない場合、パン中に新しい項目テンプレートを作成することが必要になる可能性が高く、仮想化によって提供される利点の多くが打ち消されます。 さらに、項目テンプレート セレクターでは、特定のコンテナーが現在のデータ項目用に再利用できるかどうかを評価する際に、対象として検討される候補は 5 つだけです。 このため、アプリで項目テンプレート セレクターを使用する前に、データが項目テンプレート セレクターでの使用に適しているかどうかを慎重に検討する必要があります。 コレクションがほぼ同種の項目で構成される場合、セレクターはほとんど毎回 (状況によっては常に) 同じ種類を返すことになります。 ほぼ同種の中のまれな例外を処理するためにかかるコストに注意し、[**ChoosingItemContainer**](/uwp/api/windows.ui.xaml.controls.listviewbase.choosingitemcontainer) (または 2 つの項目コントロール) の使用が妥当であるかどうかを検討します。

 