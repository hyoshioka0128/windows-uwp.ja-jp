---
Description: メディア プレーヤーには、オーディオおよびビデオ コンテンツのコントロールを管理するためのカスタマイズ可能な XAML トランスポート コントロールがあります。
title: カスタム メディア トランスポート コントロールを作成する
ms.assetid: 6643A108-A6EB-42BC-B800-22EABD7B731B
label: Create custom media transport controls
template: detail.hbs
ms.date: 09/24/2020
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: fc68410a0e68d1c642057664bc9641669282bd7f
ms.sourcegitcommit: eda7bbe9caa9d61126e11f0f1a98b12183df794d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91219545"
---
# <a name="create-custom-transport-controls"></a>カスタム トランスポート コントロールを作成する



MediaPlayerElement には、Windows アプリ内でオーディオおよびビデオ コンテンツのコントロールを管理するためのカスタマイズ可能な XAML トランスポート コントロールがあります。 ここでは、MediaTransportControls テンプレートをカスタマイズする方法を示します。 オーバーフロー メニューの操作方法、カスタム ボタンの追加方法、スライダーの変更方法について説明します。

> **重要な API**:[MediaPlayerElement](/uwp/api/windows.ui.xaml.controls.mediaplayerelement)、[MediaPlayerElement.AreTransportControlsEnabled](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.aretransportcontrolsenabled)、[MediaTransportControls](/uwp/api/Windows.Media.SystemMediaTransportControls)

始める前に、MediaPlayerElement クラスと MediaTransportControls クラスについて理解している必要があります。 詳しくは、「MediaPlayerElement コントロール ガイド」をご覧ください。

> [!TIP]
> このトピックの例は、[メディア トランスポート コントロールのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlCustomMediaTransportControls)を基にしています。 サンプルをダウンロードし、詳細なコードを参照して実行することができます。

> [!NOTE]
> **MediaPlayerElement** は Windows 10 バージョン 1607 以降でのみ使用できます。 Windows 10 の以前のバージョン用にアプリを開発する場合は、代わりに [**MediaElement**](/uwp/api/Windows.UI.Xaml.Controls.MediaElement) を使用する必要があります。 このページのすべての例は **MediaElement**でも動作します。

## <a name="when-should-you-customize-the-template"></a>テンプレートをカスタマイズする必要がある状況

**MediaPlayerElement** には、変更しなくてもほとんどのビデオおよびオーディオ再生アプリで正常に動作するように設計されているトランスポート コントロールが組み込まれています。 これらのコントロールは、[**MediaTransportControls**](/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls) クラスによって提供され、再生、停止、メディアのナビゲーション、音量の調節、全画面表示の切り替え、2 台目のデバイスへのキャスト、字幕の有効化、オーディオ トラックの切り替え、再生速度の調整を行うためのボタンが含まれています。 MediaTransportControls には、各ボタンを表示し、有効にするかどうかを制御できるプロパティがあります。 [  **IsCompact**](/uwp/api/windows.ui.xaml.controls.mediatransportcontrols.iscompact) プロパティを設定して、コントロールを 1 行に表示するか、2 行に表示するかを指定することもできます。

ただし、コントロールの外観をさらにカスタマイズしたり、動作を変更したりする必要があるシナリオも考えられます。 例をいくつか紹介します。
- アイコン、スライダーの動作、色を変更する。
- 使用頻度の低いコマンド ボタンをオーバーフロー メニューに移動する。
- コントロールのサイズが変更されたときに、コマンドをドロップ アウトする順序を変更する。
- 既定のセットには含まれていないコマンド ボタンを提供する。

> [!NOTE]
> 画面に表示されているボタンは、画面に十分なスペースがない場合、組み込みのトランスポート コントロールから定義済みの順序でドロップ アウトします。 この順序を変更するか、オーバーフロー メニューに収まらないコマンドを配置するには、コントロールをカスタマイズする必要があります。

コントロールの外観をカスタマイズするには、既定のテンプレートを変更します。 コントロールの動作を変更したり、新しいコマンドを追加したりするには、MediaTransportControls から派生したカスタム コントロールを作成できます。

> [!TIP]
> カスタマイズ可能なコントロール テンプレートは XAML プラットフォームの強力な機能ですが、考慮すべき影響もあります。 テンプレートをカスタマイズすると、アプリの静的な部分となるため、Microsoft によって行われるプラットフォームの更新を受け取らなくなります。 Microsoft によってテンプレートの更新が加えられた場合、更新されたテンプレートを利用するには、新しいテンプレートを取得して再変更する必要があります。

## <a name="template-structure"></a>テンプレートの構造

[  **ControlTemplate**](/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) は既定のスタイルに含まれます。 この既定のスタイルをプロジェクトにコピーして変更できます。 ControlTemplate は、他の XAML コントロール テンプレートと同様のセクションに分かれています。
- テンプレートの最初のセクションには、MediaTransportControls のさまざまなコンポーネントの [**Style**](/uwp/api/Windows.UI.Xaml.Style) 定義が含まれています。
- 2 番目のセクションでは、MediaTransportControls が使うさまざまな表示状態が定義されています。
- 3 番目のセクションには、さまざまな MediaTransportControls 要素をまとめて保持し、コンポーネントのレイアウトを定義する [**Grid**](/uwp/api/Windows.UI.Xaml.Controls.Grid) が含まれています。

> [!NOTE]
> テンプレートの変更について詳しくは、「[コントロール テンプレート](./control-templates.md)」をご覧ください。 テキスト エディターか、IDE の同様のエディターを使って、\(*Program Files*)\Windows Kits\10\DesignTime\CommonConfiguration\Neutral\UAP\\(*SDK version*)\Generic にある XAML ファイルを開くことができます。 各コントロールの既定のスタイルとテンプレートは、**generic.xaml** ファイルで定義されています。 MediaTransportControls テンプレートは、generic.xaml で "MediaTransportControls" を検索すると見つけることができます。

以下のセクションでは、トランスポート コントロールの主な要素のいくつかをカスタマイズする方法について説明します。
- [**Slider**](/uwp/api/Windows.UI.Xaml.Controls.Slider): ユーザーがメディアをスクラブし、進行状況も表示できるようにします。
- [**CommandBar**](/uwp/api/Windows.UI.Xaml.Controls.CommandBar): すべてのボタンが含まれています。
詳しくは、MediaTransportControls リファレンス トピックの構造セクションをご覧ください。

## <a name="customize-the-transport-controls"></a>トランスポート コントロールをカスタマイズする

MediaTransportControls の外観のみを変更する場合、既定のコントロールのスタイルとテンプレートのコピーを作成し、変更することができます。 ただし、コントロールの機能を追加または変更する場合は、MediaTransportControls から派生した新しいクラスを作成する必要があります。

### <a name="re-template-the-control"></a>コントロールのテンプレートの再適用

**MediaTransportControls の既定のスタイルとテンプレートをカスタマイズするには**
1. 「MediaTransportControls スタイルとテンプレート」に示されている既定のスタイルを、プロジェクトの ResourceDictionary にコピーします。
2. 次のように、Style に、識別するための x:Key 値を指定します。

```xaml
<Style TargetType="MediaTransportControls" x:Key="myTransportControlsStyle">
    <!-- Style content ... -->
</Style>
```

3. UI に MediaPlayerElement を MediaTransportControls と共に追加します。
4. 次に示すように、MediaTransportControls 要素の Style プロパティを、カスタム Style リソースに設定します。

```xaml
<MediaPlayerElement AreTransportControlsEnabled="True">
    <MediaPlayerElement.TransportControls>
        <MediaTransportControls Style="{StaticResource myTransportControlsStyle}"/>
    </MediaPlayerElement.TransportControls>
</MediaPlayerElement>
```

スタイルとテンプレートの変更について詳しくは、「[コントロールのスタイル](./xaml-styles.md)」と「[コントロール テンプレート](./control-templates.md)」をご覧ください。

### <a name="create-a-derived-control"></a>派生コントロールの作成

トランスポート コントロールの機能を追加または変更するには、MediaTransportControls から派生した新しいクラスを作成する必要があります。 [メディア トランスポート コントロールのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlCustomMediaTransportControls)と、このページの他の例では、`CustomMediaTransportControls` という名前の派生クラスが使用されています。

**MediaTransportControls から派生した新しいクラスを作成するには**
1. プロジェクトに新しいクラス ファイルを追加します。
    - Visual Studio で、[プロジェクト] の [クラスの追加] をクリックします。 [新しい項目の追加] ダイアログ ボックスが開きます。
    - [新しい項目の追加] ダイアログで、クラス ファイルの名前を入力し、[追加] をクリックします。 (メディア トランスポート コントロールのサンプルでは、このクラスに `CustomMediaTransportControls` という名前を付けています。)
2. このクラスのコードを変更して、MediaTransportControls クラスから派生クラスを作成します。

```csharp
public sealed class CustomMediaTransportControls : MediaTransportControls
{
}
```

3. [  **MediaTransportControls**](/uwp/api/Windows.UI.Xaml.Controls.MediaTransportControls) の既定のスタイルをプロジェクトの [ResourceDictionary](/uwp/api/Windows.UI.Xaml.ResourceDictionary) にコピーします。 これが変更する対象のスタイルとテンプレートです。
(メディア トランスポート コントロールのサンプルでは、"Themes" という新しいフォルダーが作成され、generic.xaml という ResourceDictionary ファイルがそのフォルダーに追加されます。)
4. スタイルの [**TargetType**](/uwp/api/windows.ui.xaml.style.targettype) を、新しいカスタム コントロール型に変更します。 (サンプルでは、TargetType を `local:CustomMediaTransportControls` に変更しています。)

```xaml
xmlns:local="using:CustomMediaTransportControls">
...
<Style TargetType="local:CustomMediaTransportControls">
```

5. カスタム クラスの [**DefaultStyleKey**](/uwp/api/windows.ui.xaml.controls.control.defaultstylekey) を設定します。 これにより、TargetType が `local:CustomMediaTransportControls` である Style を使用するようにカスタム クラスに指示します。

```csharp
public sealed class CustomMediaTransportControls : MediaTransportControls
{
    public CustomMediaTransportControls()
    {
        this.DefaultStyleKey = typeof(CustomMediaTransportControls);
    }
}
```

6. XAML マークアップに [**MediaPlayerElement**](/uwp/api/windows.ui.xaml.controls.mediaplayerelement) を追加し、この MediaPlayerElement にカスタム トランスポート コントロールを追加します。 注意が必要な 1 つの点は、既定のボタンを非表示、表示、無効、有効にする API は、カスタマイズされたテンプレートでも機能するという点です。

```xaml
<MediaPlayerElement Name="MediaPlayerElement1" AreTransportControlsEnabled="True" Source="video.mp4">
    <MediaPlayerElement.TransportControls>
        <local:CustomMediaTransportControls x:Name="customMTC"
                                            IsFastForwardButtonVisible="True"
                                            IsFastForwardEnabled="True"
                                            IsFastRewindButtonVisible="True"
                                            IsFastRewindEnabled="True"
                                            IsPlaybackRateButtonVisible="True"
                                            IsPlaybackRateEnabled="True"
                                            IsCompact="False">
        </local:CustomMediaTransportControls>
    </MediaPlayerElement.TransportControls>
</MediaPlayerElement>
```

これで、コントロールのスタイルとテンプレートを変更してカスタム コントロールの外観を更新し、コントロールのコードを変更して動作を更新できました。

### <a name="working-with-the-overflow-menu"></a>オーバーフロー メニューを使う

MediaTransportControls のコマンド ボタンをオーバーフロー メニューに移動し、ユーザーが必要になるまでに使用頻度の低いコマンドを非表示にすることができます。

MediaTransportControls テンプレートでは、コマンド ボタンは [**CommandBar**](/uwp/api/Windows.UI.Xaml.Controls.CommandBar) 要素に含まれています。 コマンド バーには、プライマリ コマンドとセカンダリ コマンドの概念があります。 プライマリ コマンドは、既定でコントロールに表示されるボタンであり、常に表示されます (ボタンを無効または非表示にした場合や十分なスペースがない場合を除く)。 セカンダリ コマンドはオーバーフロー メニューに表示されます。オーバーフロー メニューは、ユーザーが省略記号 (...) ボタンをクリックしたときに表示されます。 詳しくは、「[アプリ バーとコマンド バー](app-bars.md)」をご覧ください。

コマンド バーのプライマリ コマンドの要素をオーバーフロー メニューに移動するには、XAML コントロール テンプレートを編集する必要があります。

**オーバーフロー メニューにコマンドを移動するには:**
1. コントロール テンプレートで、`MediaControlsCommandBar` という名前の CommandBar 要素を検索します。
2. CommandBar の XAML に [**SecondaryCommands**](/uwp/api/windows.ui.xaml.controls.commandbar.secondarycommands) セクションを追加します。 このセクションは、[**PrimaryCommands**](/uwp/api/windows.ui.xaml.controls.commandbar.primarycommands) の終了タグの後に配置します。

```xaml
<CommandBar x:Name="MediaControlsCommandBar" ... >  
  <CommandBar.PrimaryCommands>
...
    <AppBarButton x:Name='PlaybackRateButton'
                    Style='{StaticResource AppBarButtonStyle}'
                    MediaTransportControlsHelper.DropoutOrder='4'
                    Visibility='Collapsed'>
      <AppBarButton.Icon>
        <FontIcon Glyph="&#xEC57;"/>
      </AppBarButton.Icon>
    </AppBarButton>
...
  </CommandBar.PrimaryCommands>
<!-- Add secondary commands (overflow menu) here -->
  <CommandBar.SecondaryCommands>
    ...
  </CommandBar.SecondaryCommands>
</CommandBar>
```

3. このメニューにコマンドを表示するには、目的の [**AppBarButton**](/uwp/api/Windows.UI.Xaml.Controls.AppBarButton) オブジェクトの XAML を PrimaryCommands から切り取って SecondaryCommands に貼り付けます。 この例では、`PlaybackRateButton` をオーバーフロー メニューに移動します。

4. 次に示すように、ボタンにラベルを追加し、スタイル情報を削除します。
オーバーフロー メニューはテキスト ボタンで構成されているため、ボタンにテキスト ラベルを追加し、ボタンの高さと幅を設定するスタイルを削除する必要があります。 そうしないと、ボタンはオーバーフロー メニューに正しく表示されません。

```xaml
<CommandBar.SecondaryCommands>
    <AppBarButton x:Name='PlaybackRateButton'
                  Label='Playback Rate'>
    </AppBarButton>
</CommandBar.SecondaryCommands>
```

> [!IMPORTANT]
> ボタンをオーバーフロー メニューで使用するには、ボタンを表示して有効にする必要があります。 この例では、IsPlaybackRateButtonVisible プロパティが true ではない場合、PlaybackRateButton 要素はオーバーフロー メニューに表示されません。 IsPlaybackRateEnabled プロパティが true ではない場合、この要素は有効ではありません。 これらのプロパティの設定は、前のセクションに示されています。

### <a name="adding-a-custom-button"></a>カスタム ボタンの追加

MediaTransportControls をカスタマイズする理由の 1 つは、コントロールにカスタム コマンドを追加するためです。 コマンドをプライマリ コマンドとセカンダリ コマンドのどちらとして追加するかに関係なく、コマンド ボタンを作成し、その動作を変更する手順は同じです。 [メディア トランスポート コントロールのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlCustomMediaTransportControls)では、"評価" ボタンをプライマリ コマンドに追加しています。

**カスタム コマンド ボタンを追加するには**
1. AppBarButton オブジェクトを作成し、コントロール テンプレートの CommandBar に追加します。

```xaml
<AppBarButton x:Name="LikeButton"
              Icon="Like"
              Style="{StaticResource AppBarButtonStyle}"
              MediaTransportControlsHelper.DropoutOrder="3"
              VerticalAlignment="Center" />
```

適切な場所で CommandBar に追加する必要があります。 (詳細については、オーバーフロー メニューを使用した作業に関するセクションを参照してください。)UI にどのように配置されるかは、ボタンがマークアップのどこにあるかによって決まります。 たとえば、このボタンを主要なコマンドの最後の要素として表示するには、プライマリ コマンド一覧の末尾に追加します。

ボタンのアイコンをカスタマイズすることもできます。 詳細については、<a href="/uwp/api/Windows.UI.Xaml.Controls.AppBarButton"><b>AppBarButton</b></a> のリファレンスを参照してください。
    

2. [  **OnApplyTemplate**](/uwp/api/windows.ui.xaml.frameworkelement.onapplytemplate) のオーバーライドで、テンプレートからボタンを取得し、その [**Click**](/uwp/api/windows.ui.xaml.controls.primitives.buttonbase.click) イベントのハンドラーを登録します。 次のコードを `CustomMediaTransportControls` クラスに追加します。

```csharp
public sealed class CustomMediaTransportControls :  MediaTransportControls
{
    // ...

    protected override void OnApplyTemplate()
    {
        // Find the custom button and create an event handler for its Click event.
        var likeButton = GetTemplateChild("LikeButton") as Button;
        likeButton.Click += LikeButton_Click;
        base.OnApplyTemplate();
    }

    //...
}
```

3. Click イベント ハンドラーに、ボタンがクリックされたときに発生するアクションを実行するコードを追加します。
このクラスのコード全体を次に示します。

```csharp
public sealed class CustomMediaTransportControls : MediaTransportControls
{
    public event EventHandler< EventArgs> Liked;

    public CustomMediaTransportControls()
    {
        this.DefaultStyleKey = typeof(CustomMediaTransportControls);
    }

    protected override void OnApplyTemplate()
    {
        // Find the custom button and create an event handler for its Click event.
        var likeButton = GetTemplateChild("LikeButton") as Button;
        likeButton.Click += LikeButton_Click;
        base.OnApplyTemplate();
    }

    private void LikeButton_Click(object sender, RoutedEventArgs e)
    {
        // Raise an event on the custom control when 'like' is clicked.
        var handler = Liked;
        if (handler != null)
        {
            handler(this, EventArgs.Empty);
        }
    }
}
```

**"いいね" ボタンが追加された、カスタム メディア トランスポート コントロール**
![いいねボタンが追加されたカスタム メディア トランスポート コントロール](images/controls/mtc_double_custom_inprod.png)

### <a name="modifying-the-slider"></a>スライダーを変更する

MediaTransportControls の "seek" コントロールは、[**Slider**](/uwp/api/Windows.UI.Xaml.Controls.Slider) 要素により提供されます。 このコントロールをカスタマイズする 1 つの方法として、シーク動作の細かさを変更できます。

既定のシーク スライダーは 100 の部分に分かれているため、シーク動作はその数のセクションに限定されます。 シーク スライダーの細かさを変更するには、[**MediaPlayerElement.MediaPlayer**](/uwp/api/windows.ui.xaml.controls.mediaplayerelement) の [**MediaOpened**](/uwp/api/windows.media.playback.mediaplayer.mediaopened) イベント ハンドラーで XAML ビジュアル ツリーから Slider を取得します。 この例では、[**VisualTreeHelper**](/uwp/api/Windows.UI.Xaml.Media.VisualTreeHelper) を使って Slider への参照を取得し、メディアが 120 分より長い場合に、スライダーの既定のステップ間隔を 1% から 0.1% (1000 ステップ) に変更する方法を示しています。 MediaPlayerElement には、`MediaPlayerElement1` という名前が付けられています。

```csharp
protected override void OnNavigatedTo(NavigationEventArgs e)
{
  MediaPlayerElement1.MediaPlayer.MediaOpened += MediaPlayerElement_MediaPlayer_MediaOpened;
  base.OnNavigatedTo(e);
}

private void MediaPlayerElement_MediaPlayer_MediaOpened(object sender, RoutedEventArgs e)
{
  FrameworkElement transportControlsTemplateRoot = (FrameworkElement)VisualTreeHelper.GetChild(MediaPlayerElement1.TransportControls, 0);
  Slider sliderControl = (Slider)transportControlsTemplateRoot.FindName("ProgressSlider");
  if (sliderControl != null && MediaPlayerElement1.NaturalDuration.TimeSpan.TotalMinutes > 120)
  {
    // Default is 1%. Change to 0.1% for more granular seeking.
    sliderControl.StepFrequency = 0.1;
  }
}
```
## <a name="related-articles"></a>関連記事

- [メディア再生](media-playback.md)
