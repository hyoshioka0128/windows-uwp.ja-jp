---
Description: ボタンは、特定の操作を直ちに実行する手段をユーザーに提供します。
title: ボタン
label: Buttons
template: detail.hbs
ms.date: 10/02/2018
ms.topic: article
keywords: windows 10, uwp
ms.assetid: f04d1a3c-7dcd-4bc8-9586-3396923b312e
pm-contact: kisai
design-contact: kimsea
dev-contact: mitra
doc-status: Published
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 210431928c5dd7c5d5dfb99855322f1560e91dd7
ms.sourcegitcommit: aaa4b898da5869c064097739cf3dc74c29474691
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "66363229"
---
# <a name="buttons"></a>ボタン

ボタンは、特定の操作を直ちに実行する手段をユーザーに提供します。 一部のボタンは、ナビゲーション、繰り返し操作、メニューの表示など、特定のタスクに特化されています。

![ボタンの例](images/controls/button.png)

XAML フレームワークには、標準のボタン コントロールといくつかの特殊なボタン コントロールが提供されています。

コントロール | 説明
------- | -----------
[ボタン](/uwp/api/windows.ui.xaml.controls.button) | 直ちに操作を開始します。 Click イベントまたはコマンド バインディングと共に使用することができます。
[RepeatButton](/uwp/api/windows.ui.xaml.controls.primitives.repeatbutton) | 押されている間は継続的に Click イベントを発生させるボタン。
[HyperlinkButton](/uwp/api/windows.ui.xaml.controls.hyperlinkbutton) | ハイパーリンクのようなスタイルに設定された、ナビゲーションに使用されるボタン。 詳しくは、「[ハイパーリンク](hyperlinks.md)」をご覧ください。
[DropDownButton](/uwp/api/windows.ui.xaml.controls.dropdownbutton) | アタッチされたポップアップを開くシェブロンが付いたボタン。
[SplitButton](/uwp/api/windows.ui.xaml.controls.splitbutton) | 2 つの側面を持つボタン。 一方の側に操作を示し、もう一方の側でメニューを開きます。
[ToggleSplitButton](/uwp/api/windows.ui.xaml.controls.togglesplitbutton) | 2 つの側面を持つトグル ボタン。 一方の側でオンとオフを切り替え、もう一方の側でメニューを開きます。

| **Windows UI ライブラリを入手する** |
| - |
| DropDownButton、SplitButton、ToggleSplitButton は、Windows UI ライブラリの NuGet パッケージの一部として組み込まれており、パッケージには、UWP アプリの新しいコントロールと UI 機能が含まれています。 インストール手順などの詳細については、[Windows UI ライブラリの概要](https://docs.microsoft.com/uwp/toolkits/winui/)に関するページを参照してください。 |

| **プラットフォーム API** | **Windows UI ライブラリ API** |
| - | - |
| [Click イベント](/uwp/api/windows.ui.xaml.controls.primitives.buttonbase.click)、[Command プロパティ](/uwp/api/windows.ui.xaml.controls.primitives.buttonbase.command) | [DropDownButton クラス](/uwp/api/microsoft.ui.xaml.controls.dropdownbutton)、[SplitButton クラス](/uwp/api/microsoft.ui.xaml.controls.splitbutton)、[ToggleSplitButton クラス](/uwp/api/microsoft.ui.xaml.controls.togglesplitbutton) |

## <a name="is-this-the-right-control"></a>適切なコントロールの選択

**ボタン**を使用すると、ユーザーは直ちに操作を開始できます (フォームの送信など)。

他のページに移動する操作では、ボタンは使わず、代わりに [HyperlinkButton](/uwp/api/windows.ui.xaml.controls.hyperlinkbutton) リンクを使用します。 詳しくは、「[ハイパーリンク](hyperlinks.md)」をご覧ください。
> 例外:ウィザードでの移動には、[戻る] と [次へ] というラベルのボタンを使用します。 他の種類の前に戻る移動や上位レベルへの移動では、[[戻る] ボタン](../basics/navigation-history-and-backwards-navigation.md)を使用します。

ユーザーが操作を繰り返しトリガーする可能性があるときは、**RepeatButton** を使用します。 たとえば、カウンターの値を増減させるときに RepeatButton を使用します。

ボタンに追加のオプションを含むポップアウトがある場合は、**DropDownButton** を使用します。 既定のシェブロンにより、ボタンにポップアップが含まれていることが視覚的に示されます。

ユーザーが直ちに操作を開始できるようにする場合や、追加のオプションから独立して選択できるようにする場合は、**SplitButton** を使用します。

## <a name="examples"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/Button">アプリを開き、Button の動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

この例では、一情報へのアクセスを求めるダイアログ ボックスで、2 つのボタン ([Allow] (許可) と [Block] (禁止)) を使っています。

![ダイアログで使われるボタンの例](images/dialogs/dialog_RS2_two_button.png)

## <a name="create-a-button"></a>ボタンの作成

クリックに応答するボタンの例を次に示します。

XAML でボタンを作成します。

```xaml
<Button Content="Subscribe" Click="SubscribeButton_Click"/>
```

または、コードでボタンを作成します。

```csharp
Button subscribeButton = new Button();
subscribeButton.Content = "Subscribe";
subscribeButton.Click += SubscribeButton_Click;

// Add the button to a parent container in the visual tree.
stackPanel1.Children.Add(subscribeButton);
```

Click イベントを処理します。

```csharp
private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
{
    // Call app specific code to subscribe to the service. For example:
    ContentDialog subscribeDialog = new ContentDialog
    {
        Title = "Subscribe to App Service?",
        Content = "Listen, watch, and play in high definition for only $9.99/month. Free to try, cancel anytime.",
        CloseButtonText = "Not Now",
        PrimaryButtonText = "Subscribe",
        SecondaryButtonText = "Try it"
    };

    ContentDialogResult result = await subscribeDialog.ShowAsync();
}
```

### <a name="button-interaction"></a>ボタンの対話式操作

ポインターがボタンの上にあるときに、指やスタイラスでそのボタンをタップするか、マウスの左ボタンを押すと、ボタンでは [Click](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.buttonbase.click) イベントが発生します。 ボタンにキーボード フォーカスがある場合は、Enter キーまたは Space キーを押しても、Click イベントが発生します。

通常、ボタンでは低レベルな [PointerPressed](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed) イベントを処理できません。これに代わる Click 動作があるためです。 詳しくは、「[イベントとルーティング イベントの概要](https://docs.microsoft.com/windows/uwp/xaml-platform/events-and-routed-events-overview)」をご覧ください。

ボタンで Click イベントが発生する方法を変えるには、[ClickMode](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.clickmode) プロパティを変更します。 ClickMode の既定値は **Release** ですが、ボタンの ClickMode を **Hover** または **Press** に設定することもできます。 ClickMode が **Hover** の場合、キーボード操作やタッチ操作によって Click イベントを発生させることはできません。


### <a name="button-content"></a>ボタンのコンテンツ

ボタンは [ContentControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ContentControl) です。 その XAML コンテンツ プロパティは [Content](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.contentcontrol.content) であり、`<Button>A button's content</Button>` のような XAML 構文を使用できます。 任意のオブジェクトをボタンのコンテンツとして設定できます。 コンテンツが [UIElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement) の場合、ボタンにレンダリングされます。 コンテンツが別のタイプのオブジェクトの場合、その文字列表現がボタンに表示されます。

ボタンのコンテンツは、通常はテキストです。 テキスト コンテンツの付いたボタンの設計に関する推奨事項を次に示します。
-   ボタンによって行われる操作を明確に説明する、簡潔で具体的でわかりやすいテキストを使います。 通常、ボタンのテキスト コンテンツは、1 語の動詞です。
-   ブランドのガイドラインで別のフォントが指示されていない限り、既定のフォントを使います。
-   短いテキストでは、120px の最小ボタン幅を使用し、幅が狭いコマンド ボタンは使わないようにします。
- 長いテキストでは、テキストを最大文字数 26 文字に制限し、さまざまなコマンド ボタンは使わないようにします。
-   ボタンのテキスト コンテンツが動的な場合 ([ローカライズされる](../globalizing/globalizing-portal.md) 場合など) は、ボタンのサイズがどのように変化し、その周囲のコントロールに何が起こるかを考えます。

<table>
<tr>
<td> <b>必要な修正:</b><br> オーバーフロー テキストの付いたボタン。 </td>
<td> <img src="images/button-wraptext.png"/> </td>
</tr>
<tr>
<td> <b>選択肢 1:</b><br> テキストの長さが 26 文字より大きい場合は、ボタンの幅やスタック ボタンを増やし、テキストを折り返します。 </td>
<td> <img src="images/button-wraptext1.png"> </td>
</tr>
<tr>
<td> <b>選択肢 2:</b><br> ボタンの高さを増やし、テキストを折り返します。 </td>
<td> <img src="images/button-wraptext2.png"> </td>
</tr>
</table>

ボタンの外観を構成する視覚効果をカスタマイズすることもできます。 たとえば、テキストをアイコンに置き換えたり、アイコンとテキストを使用したりできます。

ここでは、画像とテキストを含む **StackPanel** がボタンのコンテンツとして設定されます。

```xaml
<Button Click="Button_Click"
        Background="LightGray"
        Height="100" Width="80">
    <StackPanel>
        <Image Source="Assets/Photo.png" Height="62"/>
        <TextBlock Text="Photos" Foreground="Black"
                   HorizontalAlignment="Center"/>
    </StackPanel>
</Button>
```

ボタンは次のように表示されます。

![画像とテキスト コンテンツがあるボタン](images/button-orange.png)

## <a name="create-a-repeat-button"></a>繰り返しボタンの作成

[RepeatButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.repeatbutton) は、ボタンが押されてから離されるまで、繰り返し [Click](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.buttonbase.click) イベントを発生させるボタンです。 ボタンが押されてからクリック操作の繰り返しを始めるまでの RepeatButton の待ち時間を指定するには、[Delay](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.repeatbutton.delay) プロパティを設定します。 クリック操作の繰り返し間隔を指定するには、[Interval](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.repeatbutton.interval) プロパティを設定します。 これらのプロパティの時間はどちらもミリ秒単位で指定します。

次の例は 2 つの RepeatButton コントロールを示しています。それぞれの Click イベントを使って、テキスト ブロックに表示される値を増減します。

```xaml
<StackPanel>
    <RepeatButton Width="100" Delay="500" Interval="100" Click="Increase_Click">Increase</RepeatButton>
    <RepeatButton Width="100" Delay="500" Interval="100" Click="Decrease_Click">Decrease</RepeatButton>
    <TextBlock x:Name="clickTextBlock" Text="Number of Clicks:" />
</StackPanel>
```

```csharp
private static int _clicks = 0;
private void Increase_Click(object sender, RoutedEventArgs e)
{
    _clicks += 1;
    clickTextBlock.Text = "Number of Clicks: " + _clicks;
}

private void Decrease_Click(object sender, RoutedEventArgs e)
{
    if(_clicks > 0)
    {
        _clicks -= 1;
        clickTextBlock.Text = "Number of Clicks: " + _clicks;
    }
}
```

## <a name="create-a-drop-down-button"></a>ドロップダウン ボタンの作成

> DropDownButton には、Windows 10 Version 1809 ([SDK 17763](https://developer.microsoft.com/windows/downloads/windows-10-sdk)) 以降、または [Windows UI ライブラリ](https://docs.microsoft.com/uwp/toolkits/winui/)が必要です。

[DropDownButton](/uwp/api/windows.ui.xaml.controls.dropdownbutton) は、その他のオプションを含むアタッチされたポップアップがあることを示す視覚的なインジケーターとしてシェブロンを表示するボタンです。 ポップアップがある標準の Button と動作は同じであり、外観だけが異なります。

ドロップダウン ボタンでは Click イベントが継承されますが、通常はそれを使用することはありません。 その代わりに、Flyout プロパティを使用してポップアップをアタッチし、ポップアップ内のメニュー オプションを使用して操作を呼び出します。 ポップアップは、ボタンがクリックされたときに自動的に開きます。 ポップアップの [Placement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.flyoutbase.placement) プロパティを指定して、ボタンに対して相対的に目的の配置が確実に行われるようにします。 既定の配置アルゴリズムでは、すべての状況において目的の配置になるとは限りません。

> [!TIP]
> ポップアップの詳細については、「[メニューとショートカット メニュー](menus.md)」を参照してください。

### <a name="example---drop-down-button"></a>例 - ドロップダウン ボタン

この例では、RichEditBox に段落配置用のコマンドを含むポップアップ付きのドロップダウン ボタンを作成する方法を示します (詳細な情報とコードについては、「[リッチ エディット ボックス](rich-edit-box.md)」を参照してください)。

![配置コマンドを含むドロップダウン ボタン](images/drop-down-button-align.png)

```xaml
<DropDownButton ToolTipService.ToolTip="Alignment">
    <TextBlock FontFamily="Segoe MDL2 Assets" FontSize="14" Text="&#xE8E4;"/>
    <DropDownButton.Flyout>
        <MenuFlyout Placement="BottomEdgeAlignedLeft">
            <MenuFlyoutItem Text="Left" Icon="AlignLeft" Tag="left"
                            Click="AlignmentMenuFlyoutItem_Click"/>
            <MenuFlyoutItem Text="Center" Icon="AlignCenter" Tag="center"
                            Click="AlignmentMenuFlyoutItem_Click"/>
            <MenuFlyoutItem Text="Right" Icon="AlignRight" Tag="right"
                            Click="AlignmentMenuFlyoutItem_Click"/>
        </MenuFlyout>
    </DropDownButton.Flyout>
</DropDownButton>
```

```csharp
private void AlignmentMenuFlyoutItem_Click(object sender, RoutedEventArgs e)
{
    var option = ((MenuFlyoutItem)sender).Tag.ToString();

    Windows.UI.Text.ITextSelection selectedText = editor.Document.Selection;
    if (selectedText != null)
    {
        // Apply the alignment to the selected paragraphs.
        var paragraphFormatting = selectedText.ParagraphFormat;
        if (option == "left")
        {
            paragraphFormatting.Alignment = Windows.UI.Text.ParagraphAlignment.Left;
        }
        else if (option == "center")
        {
            paragraphFormatting.Alignment = Windows.UI.Text.ParagraphAlignment.Center;
        }
        else if (option == "right")
        {
            paragraphFormatting.Alignment = Windows.UI.Text.ParagraphAlignment.Right;
        }
    }
}
```

## <a name="create-a-split-button"></a>分割ボタンの作成

> SplitButton には、Windows 10 Version 1809 ([SDK 17763](https://developer.microsoft.com/windows/downloads/windows-10-sdk)) 以降、または [Windows UI ライブラリ](https://docs.microsoft.com/uwp/toolkits/winui/)が必要です。

[SplitButton](/uwp/api/windows.ui.xaml.controls.splitbutton) には、個別に呼び出せる 2 つのパーツがあります。 1 つのパーツは標準のボタンのように動作し、即座にアクションを呼び出します。 もう一方のパーツは、ユーザーが選択できる追加オプションを含むポップアップを呼び出します。

> [!NOTE]
> タッチによって呼び出されると、分割ボタンはドロップダウン ボタンとして動作します。ボタンの両方の部分でポップアップが呼び出されます。 その他の入力方法を使用すると、ユーザーはボタンのいずれかの半分を個別に呼び出すことができます。

分割ボタンの一般的な動作は次のとおりです。

- ユーザーがボタンの部分をクリックしたときに、ドロップダウンで現在選択されているオプションを呼び出すために Click イベントを処理します。
- ドロップダウンが開いているとき、ドロップダウン内の項目の呼び出しを処理して、どのオプションが選択されているかの変更と、その呼び出しの両方を行います。 ボタンの Click イベントはタッチ使用時には発生しないので、ポップアップ項目を呼び出すことが重要です。

> [!TIP]
> ドロップダウンに項目を配置し、それらの呼び出しを処理するには、多くの方法があります。 ListView または GridView を使用する場合、1 つの方法は、SelectionChanged イベントを処理することです。 これを行う場合は、[SingleSelectionFollowsFocus](/uwp/api/windows.ui.xaml.controls.listviewbase.singleselectionfollowsfocus) を **false** に設定します。 これによりユーザーは、変更のたびに項目を呼び出すことなく、キーボードを使用してオプション間を移動できます。

### <a name="example---split-button"></a>例 - 分割ボタン

この例では、RichEditBox 内で選択されたテキストの前景色を変更するために使う分割ボタンの作成方法を示します (詳細な情報とコードについては、「[リッチ エディット ボックス](rich-edit-box.md)」を参照してください)。
分割ボタンのポップアップでは、[BottomEdgeAlignedLeft](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.flyoutplacementmode) を [Placement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.flyoutbase.placement) プロパティの既定値として使用します。 この値のオーバーライドはできません。

![前景色を選択するための分割ボタン](images/split-button-rtb.png)

```xaml
<SplitButton ToolTipService.ToolTip="Foreground color"
             Click="BrushButtonClick">
    <Border x:Name="SelectedColorBorder" Width="20" Height="20"/>
    <SplitButton.Flyout>
        <Flyout x:Name="BrushFlyout">
            <!-- Set SingleSelectionFollowsFocus="False"
                 so that keyboard navigation works correctly. -->
            <GridView ItemsSource="{x:Bind ColorOptions}" 
                      SelectionChanged="BrushSelectionChanged"
                      SingleSelectionFollowsFocus="False"
                      SelectedIndex="0" Padding="0">
                <GridView.ItemTemplate>
                    <DataTemplate>
                        <Rectangle Fill="{Binding}" Width="20" Height="20"/>
                    </DataTemplate>
                </GridView.ItemTemplate>
                <GridView.ItemContainerStyle>
                    <Style TargetType="GridViewItem">
                        <Setter Property="Margin" Value="2"/>
                        <Setter Property="MinWidth" Value="0"/>
                        <Setter Property="MinHeight" Value="0"/>
                    </Style>
                </GridView.ItemContainerStyle>
            </GridView>
        </Flyout>
    </SplitButton.Flyout>
</SplitButton>
```

```csharp
public sealed partial class MainPage : Page
{
    // Color options that are bound to the grid in the split button flyout.
    private List<SolidColorBrush> ColorOptions = new List<SolidColorBrush>();
    private SolidColorBrush CurrentColorBrush = null;

    public MainPage()
    {
        this.InitializeComponent();

        // Add color brushes to the collection.
        ColorOptions.Add(new SolidColorBrush(Colors.Black));
        ColorOptions.Add(new SolidColorBrush(Colors.Red));
        ColorOptions.Add(new SolidColorBrush(Colors.Orange));
        ColorOptions.Add(new SolidColorBrush(Colors.Yellow));
        ColorOptions.Add(new SolidColorBrush(Colors.Green));
        ColorOptions.Add(new SolidColorBrush(Colors.Blue));
        ColorOptions.Add(new SolidColorBrush(Colors.Indigo));
        ColorOptions.Add(new SolidColorBrush(Colors.Violet));
        ColorOptions.Add(new SolidColorBrush(Colors.White));
    }

    private void BrushButtonClick(object sender, object e)
    {
        // When the button part of the split button is clicked,
        // apply the selected color.
        ChangeColor();
    }

    private void BrushSelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        // When the flyout part of the split button is opened and the user selects
        // an option, set their choice as the current color, apply it, then close the flyout.
        CurrentColorBrush = (SolidColorBrush)e.AddedItems[0];
        SelectedColorBorder.Background = CurrentColorBrush;
        ChangeColor();
        BrushFlyout.Hide();
    }

    private void ChangeColor()
    {
        // Apply the color to the selected text in a RichEditBox.
        Windows.UI.Text.ITextSelection selectedText = editor.Document.Selection;
        if (selectedText != null)
        {
            Windows.UI.Text.ITextCharacterFormat charFormatting = selectedText.CharacterFormat;
            charFormatting.ForegroundColor = CurrentColorBrush.Color;
            selectedText.CharacterFormat = charFormatting;
        }
    }
}
```

## <a name="create-a-toggle-split-button"></a>分割トグル ボタンの作成

> ToggleSplitButton には、Windows 10 Version 1809 ([SDK 17763](https://developer.microsoft.com/windows/downloads/windows-10-sdk)) 以降、または [Windows UI ライブラリ](https://docs.microsoft.com/uwp/toolkits/winui/)が必要です。

[ToggleSplitButton](/uwp/api/windows.ui.xaml.controls.togglesplitbutton) には、個別に呼び出せる 2 つのパーツがあります。 1 つのパーツは、オンまたはオフにできるトグル ボタンのように動作します。 もう一方のパーツは、ユーザーが選択できる追加オプションを含むポップアップを呼び出します。

通常、分割トグル ボタンは、1 つの機能にユーザーが選択できるオプションが複数あるときに、その機能を有効または無効にするために使用されます。 たとえばドキュメント エディターで、ドロップダウンが箇条書きのスタイルを選択するために使用されているとき、箇条書きのオンとオフを切り替えるために使用できます。

> [!NOTE]
> タッチによって呼び出された場合、分割トグル ボタンはドロップダウン ボタンとして動作します。 その他の入力方法を使用すると、ユーザーはボタンの 2 つの部分を個別に切り替えて呼び出すことができます。 タッチでは、ボタンの両方の部分でポップアウトが呼び出されます。 そのため、ボタンのオンとオフを切り替えるためのオプションをポップアウトの内容に含める必要があります。

### <a name="differences-with-togglebutton"></a>ToggleButton との違い

[ToggleButton](/uwp/api/windows.ui.xaml.controls.primitives.togglebutton) とは異なり、ToggleSplitButton には不確定の状態はありません。 その結果、これらの違いに注意する必要があります。

- ToggleSplitButton には、**IsThreeState** プロパティまたは **Indeterminate** イベントはありません。
- [ToggleSplitButton.IsChecked](/uwp/api/windows.ui.xaml.controls.togglesplitbutton.ischecked) プロパティは単なる**ブール値**であり、**null 許容ブール値**ではありません。
- ToggleSplitButton には、[IsCheckedChanged](/uwp/api/windows.ui.xaml.controls.togglesplitbutton.ischeckedchanged) イベントしかありません。独立した **Checked** イベントと **Unchecked** イベントはありません。

### <a name="example---toggle-split-button"></a>例 - 分割トグル ボタン

次の例では、RichEditBox の分割トグル ボタンを使用して箇条書きの書式設定のオンとオフを切り替え、箇条書きのスタイルを変更する方法を示します (詳細な情報とコードについては、「[リッチ エディット ボックス](rich-edit-box.md)」を参照してください)。
分割トグル ボタンのポップアップでは、[BottomEdgeAlignedLeft](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.flyoutplacementmode) を [Placement](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.flyoutbase.placement) プロパティの既定値として使用します。 この値のオーバーライドはできません。

![箇条書きのスタイルを選択するための分割トグル ボタン](images/toggle-split-button-open.png)

```xaml
<ToggleSplitButton x:Name="ListButton"
                   ToolTipService.ToolTip="List style"
                   Click="ListButton_Click"
                   IsCheckedChanged="ListStyleButton_IsCheckedChanged">
    <TextBlock FontFamily="Segoe MDL2 Assets" FontSize="14" Text="&#xE8FD;"/>
    <ToggleSplitButton.Flyout>
        <Flyout>
            <ListView x:Name="ListStylesListView"
                      SelectionChanged="ListStylesListView_SelectionChanged" 
                      SingleSelectionFollowsFocus="False">
                <StackPanel Tag="bullet" Orientation="Horizontal">
                    <FontIcon FontFamily="Segoe MDL2 Assets" Glyph="&#xE7C8;"/>
                    <TextBlock Text="Bullet" Margin="8,0"/>
                </StackPanel>
                <StackPanel Tag="alpha" Orientation="Horizontal">
                    <TextBlock Text="A" FontSize="24" Margin="2,0"/>
                    <TextBlock Text="Alpha" Margin="8"/>
                </StackPanel>
                <StackPanel Tag="numeric" Orientation="Horizontal">
                    <FontIcon FontFamily="Segoe MDL2 Assets" Glyph="&#xF146;"/>
                    <TextBlock Text="Numeric" Margin="8,0"/>
                </StackPanel>
                <TextBlock Tag="none" Text="None" Margin="28,0"/>
            </ListView>
        </Flyout>
    </ToggleSplitButton.Flyout>
</ToggleSplitButton>
```

```csharp
private void ListStyleButton_IsCheckedChanged(ToggleSplitButton sender, ToggleSplitButtonIsCheckedChangedEventArgs args)
{
    // Use the toggle button to turn the selected list style on or off.
    if (((ToggleSplitButton)sender).IsChecked == true)
    {
        // On. Apply the list style selected in the drop down to the selected text.
        var listStyle = ((FrameworkElement)(ListStylesListView.SelectedItem)).Tag.ToString();
        ApplyListStyle(listStyle);
    }
    else
    {
        // Off. Make the selected text not a list,
        // but don't change the list style selected in the drop down.
        ApplyListStyle("none");
    }
}

private void ListStylesListView_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    var listStyle = ((FrameworkElement)(e.AddedItems[0])).Tag.ToString();

    if (ListButton.IsChecked == true)
    {
        // Toggle button is on. Turn it off...
        if (listStyle == "none")
        {
            ListButton.IsChecked = false;
        }
        else
        {
            // or apply the new selection.
            ApplyListStyle(listStyle);
        }
    }
    else
    {
        // Toggle button is off. Turn it on, which will apply the selection
        // in the IsCheckedChanged event handler.
        ListButton.IsChecked = true;
    }
}

private void ApplyListStyle(string listStyle)
{
    Windows.UI.Text.ITextSelection selectedText = editor.Document.Selection;
    if (selectedText != null)
    {
        // Apply the list style to the selected text.
        var paragraphFormatting = selectedText.ParagraphFormat;
        if (listStyle == "none")
        {  
            paragraphFormatting.ListType = Windows.UI.Text.MarkerType.None;
        }
        else if (listStyle == "bullet")
        {
            paragraphFormatting.ListType = Windows.UI.Text.MarkerType.Bullet;
        }
        else if (listStyle == "numeric")
        {
            paragraphFormatting.ListType = Windows.UI.Text.MarkerType.Arabic;
        }
        else if (listStyle == "alpha")
        {
            paragraphFormatting.ListType = Windows.UI.Text.MarkerType.UppercaseEnglishLetter;
        }
        selectedText.ParagraphFormat = paragraphFormatting;
    }
}
```

## <a name="recommendations"></a>推奨事項

- ボタンの用途と状態をユーザーがはっきりと理解できるようにします。
- 同じ意思決定に対して複数のボタンが存在する場合 (確認のダイアログなど)、コミット ボタンは次の順番で提示します。この "[実行する]" と "[実行しない]" は、メインの指示に対応する具体的な文になります。
    - [OK]/[実行する]/[はい]
    - [実行しない]/[いいえ]
    - Cancel
- ユーザーに対して表示するボタンは、1 つまたは 2 つにします (例: [承諾] と [キャンセル])。 3 つ以上の操作をユーザーに示す必要がある場合は、ユーザーが操作を選択できる [チェック ボックス](checkbox.md) または [オプション ボタン](radio-button.md) を、それらの操作を開始するための 1 つのコマンド ボタンと共に使うことを検討します。
- ある操作をアプリの複数のページで実行できるようにするには、各ページでボタンを使うのではなく、[下部のアプリ バー](app-bars.md) を使うことを検討します。

### <a name="recommended-single-button-layout"></a>単一のボタンの推奨レイアウト

ボタンを 1 つしか必要としないレイアウトでは、コンテナーのコンテキストに応じて、左揃えまたは右揃えにします。

- ボタンが 1 つだけのダイアログでは、ボタンを**右揃え**にします。 ダイアログにボタンが 1 つしかない場合は、ボタンによって安全で非破壊的な操作が実行されるようにします。 [ContentDialog](dialogs.md) を使い、単一のボタンを指定する場合は、自動的に右揃えになります。

![ダイアログ内のボタン](images/pushbutton_doc_dialog.png)

- ボタンがコンテナー UI 内 (トースト通知、ポップアップ、またはリスト ビュー項目内など) に表示される場合は、コンテナー内でボタンを**左揃え**にします。

![コンテナー内のボタン](images/pushbutton_doc_container.png)

- ページに含まれるボタンが 1 つだけの場合は (設定ページの下部にある [適用] ボタンなど)、ボタンを**左揃え**にします。 これで、ページのその他のコンテンツとボタンを揃えて配置できます。

![ページのボタン](images/pushbutton_doc_page.png)

## <a name="back-buttons"></a>戻るボタン

戻るボタンは、バック スタックまたはユーザーのナビゲーション履歴を使って "戻る" ナビゲーションを実現する、システムの UI 要素です。 独自の"戻る"ボタンを作成する必要はありませんが、前に戻る移動で適切なエクスペリエンスを提供するために作業が必要になることがあります。 詳しくは、「[履歴と前に戻る移動](../basics/navigation-history-and-backwards-navigation.md)」をご覧ください。

## <a name="get-the-sample-code"></a>サンプル コードを入手する

- [XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。

## <a name="related-articles"></a>関連記事

- [Button クラス](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.button)
- [ラジオ ボタン](radio-button.md)
- [チェック ボックス](checkbox.md)
- [トグル スイッチ](toggles.md)
