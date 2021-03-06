---
Description: 既定の InkToolbar をユニバーサル Windows プラットフォーム (UWP) 手描き入力アプリに追加し、カスタム ペン ボタンを InkToolbar に追加して、カスタム ペン ボタンをカスタム ペン定義にバインドします。
title: InkToolbar をユニバーサル Windows プラットフォーム (UWP) アプリに追加する
label: Add an InkToolbar to a Universal Windows Platform (UWP) app
template: detail.hbs
keywords: Windows Ink, Windows の手書き入力, DirectInk, InkPresenter, InkCanvas, InkToolbar, ユニバーサル Windows プラットフォーム, UWP, ユーザー操作, 入力
ms.date: 02/08/2017
ms.topic: article
ms.assetid: d888f75f-c2a0-4134-81db-907b5e24fcc5
ms.localizationpriority: medium
ms.openlocfilehash: 05e10fd728930ea23615e11ffd5a004a420c9b64
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66365837"
---
# <a name="add-an-inktoolbar-to-a-universal-windows-platform-uwp-app"></a>InkToolbar をユニバーサル Windows プラットフォーム (UWP) アプリに追加する



ユニバーサル Windows プラットフォーム (UWP) アプリで手描き入力機能を容易にする 2 つの異なるコントロールがあります。[**InkCanvas** ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas)と[ **InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar)します。

[  **InkCanvas**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas) コントロールには、基本的な Windows Ink 機能が用意されています。 このコントロールを使用して、ペン入力をインク ストローク (色と太さの既定の設定を使う) か消去ストロークとしてレンダリングできます。

> InkCanvas の実装について詳しくは、「[UWP アプリのペン操作とスタイラス操作](pen-and-stylus-interactions.md)」をご覧ください。

InkCanvas は、完全に透明なオーバーレイであるため、インク ストロークのプロパティを設定するための UI は組み込まれていません。 既定の手書き入力エクスペリエンスを変更する場合、ユーザーがインク ストロークのプロパティを設定し、その他のカスタムの手書き入力機能を使用できるようにします。これには 2 つの方法があります。

- コード ビハインドで、InkCanvas にバインドされている、基になる [**InkPresenter**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter) オブジェクトを使用します。

  InkPresenter API では、手書き入力エクスペリエンスのさまざまなカスタマイズをサポートしています。 詳しくは、「[UWP アプリのペン操作とスタイラス操作](pen-and-stylus-interactions.md)」をご覧ください。

- [  **InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) を InkCanvas にバインドします。 既定では、InkToolbar には、インク機能をアクティブ化し、ストロークのサイズ、インクの色、ペン先の形状などのインク関連のプロパティを設定できる、カスタマイズ可能で拡張可能なボタンのコレクションが用意されています。

  ここでは、InkToolbar について説明します。

> **重要な API**:[**InkCanvas クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas)、 [ **InkToolbar クラス**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar)、 [ **InkPresenter クラス**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkpresenter)、 [**Windows.UI.Input.Inking**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking)

## <a name="default-inktoolbar"></a>既定の InkToolbar

既定では、[**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) には、描画、消去、強調表示、ステンシルの表示 (ルーラーまたは分度器) のボタンが含まれています。 機能に応じて、インクの色、ストロークの太さ、すべてのインクの消去など、他の設定やコマンドがポップアップに表示されます。

![InkToolbar](./images/ink/ink-tools-invoked-toolbar-small.png)  
*既定の Windows Ink ツールバー*

既定の [**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) を手描き入力のアプリに追加するには、[**InkCanvas**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas) と同じページに配置して、2 つのコントロールを関連付けます。

1. MainPage.xaml で、手書き入力面のコンテナー オブジェクト (ここでは Grid コントロールを使用します) を宣言します。
2. コンテナーの子として InkCanvas オブジェクトを宣言します  (InkCanvas サイズはコンテナーから継承されます)。
3. InkToolbar を宣言し、TargetInkCanvas 属性を使用して InkCanvas にバインドします。

> [!NOTE]
> InkToolbar が InkCanvas の後で宣言されるようにします。 そうでなければ、InkCanvas オーバーレイで InkToolbar にアクセスできなくなります。

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header"
                   Text="Basic ink sample"
                   Style="{ThemeResource HeaderTextBlockStyle}"
                   Margin="10,0,0,0" />
    </StackPanel>
    <Grid Grid.Row="1">
        <Image Source="Assets\StoreLogo.png" />
        <InkCanvas x:Name="inkCanvas" />
        <InkToolbar x:Name="inkToolbar"
          VerticalAlignment="Top"
          TargetInkCanvas="{x:Bind inkCanvas}" />
    </Grid>
</Grid>
```

## <a name="basic-customization"></a>基本的なカスタマイズ

このセクションでは、Windows Ink ツール バーの基本的なカスタマイズに関するシナリオについて説明します。

### <a name="specify-location-and-orientation"></a>位置と向きの指定

インク ツール バーをアプリに追加するとき、ツール バーの既定の位置と向きをそのまま使用したり、アプリやユーザーの必要に応じて位置と向きを設定したりすることができます。

**XAML**

ツール バーの [VerticalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.VerticalAlignment)、[HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.HorizontalAlignment)、[Orientation](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar?branch=rs3.Orientation) の各プロパティを使用して、ツール バーの位置と向きを明示的に指定します。

| Default | 明示的に指定 |
| --- | --- |
| ![インク ツール バーの既定の位置と向き](./images/ink/location-default-small.png) | ![明示的に指定したインク ツール バーの位置と向き](./images/ink/location-explicit-small.png) |
| *Windows Ink ツールバーの既定の場所と向き* | *Windows Ink ツールバーの明示的な位置と向き* |

XAML でインク ツール バーの位置と向きを明示的に設定する場合のコードを次に示します。
```xaml
<InkToolbar x:Name="inkToolbar" 
    VerticalAlignment="Center" 
    HorizontalAlignment="Right" 
    Orientation="Vertical" 
    TargetInkCanvas="{x:Bind inkCanvas}" />
```

**ユーザーの設定やデバイスの状態に基づいて初期化**

場合によっては、ユーザー設定またはデバイスの状態に基づいてインク ツール バーの位置と向きを設定する必要があります。 次の例は、 **[設定] > [デバイス] > [ペンと Windows Ink] > [ペン] > [利き手を選択してください]** で指定されている、左利きや右利きに関する設定に基づいてインク ツール バーの位置と向きを設定する方法を示しています。

![主要な手の形の設定](./images/ink/location-handedness-setting.png)  
*主要な手の形の設定*

Windows.UI.ViewManagement の HandPreference プロパティを使用してこの設定を照会し、返された値に基づいて [HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.HorizontalAlignment) を設定できます。 この例では、左利きのユーザーに対してはアプリの左側にツール バーを配置し、右利きのユーザーに対しては右側に配置します。

**このサンプルをからダウンロード[インクのツールバーの位置や向きサンプルの (basic)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness.zip)**

```csharp
public MainPage()
{
    this.InitializeComponent();

    Windows.UI.ViewManagement.UISettings settings = 
        new Windows.UI.ViewManagement.UISettings();
    HorizontalAlignment alignment = 
        (settings.HandPreference == 
            Windows.UI.ViewManagement.HandPreference.LeftHanded) ? 
            HorizontalAlignment.Left : HorizontalAlignment.Right;
    inkToolbar.HorizontalAlignment = alignment;
}
```

**ユーザーまたはデバイスの状態に動的に調整します。**

バインドを使用し、ユーザー設定、デバイス設定、デバイスの状態に対する変更に基づいて UI の更新を操作することもできます。 次の例では、前の例を拡張し、バインド、ViewMOdel オブジェクト、[INotifyPropertyChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.inotifypropertychanged) インターフェイスを使用して、デバイスの向きに基づいてインク ツール バーを動的に配置する方法を示しています。 

**このサンプルをからダウンロード[インクのツールバーの位置や向きサンプルの (動的)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness-dynamic.zip)**

1. 最初に、ViewModel を追加しましょう。
    1. 新しいフォルダーをプロジェクトに追加し、そのフォルダーに **ViewModels** という名前を付けます。
    1. 新しいクラスを ViewModels フォルダーに追加します (この例では、**InkToolbarSnippetHostViewModel.cs** という名前です)。
        > [!NOTE] 
        > アプリケーションの有効期間中に必要となるこの種類のオブジェクトは 1 つのみであるため、[シングルトン パターン](https://docs.microsoft.com/previous-versions/msp-n-p/ff650849(v=pandp.10))を使用しました。

    1. `using System.ComponentModel` 名前空間をファイルに追加します。
    1. **instance** という静的メンバー変数、および **Instance** という名前の静的な読み取り専用プロパティを追加します。 コンストラクターをプライベートにして、このクラスには Instance プロパティ経由でのみアクセスできるようにします。   
        > [!NOTE] 
        > このクラスは [INotifyPropertyChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.inotifypropertychanged) インターフェイスを継承します。このインターフェイスは、プロパティの値が変化したことをクライアントに通知するために使用されます (通常、クライアントをバインドします)。 これを利用して、デバイスの向きの変化を処理します (後の手順で、このコードを展開して、詳しく説明します)。  

        ```csharp
        using System.ComponentModel;

        namespace locationandorientation.ViewModels
        {
            public class InkToolbarSnippetHostViewModel : INotifyPropertyChanged
            {
                private static InkToolbarSnippetHostViewModel instance;
                
                public static InkToolbarSnippetHostViewModel Instance
                {
                    get
                    {
                        if (null == instance)
                        {
                            instance = new InkToolbarSnippetHostViewModel();
                        }
                        return instance;
                    }
                }
            }

            private InkToolbarSnippetHostViewModel() { }
        }
        ```

    1. InkToolbarSnippetHostViewModel クラスには、2 つのブール型プロパティを追加します。**LeftHandedLayout** (前の XAML 専用の例と同じ機能) と**PortraitLayout** (デバイスの向き)。
        >[!NOTE] 
        > PortraitLayout プロパティは設定可能なプロパティであり、[PropertyChanged](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.inotifypropertychanged.PropertyChanged) イベントの定義を含んでいます。

        ```csharp
        public bool LeftHandedLayout
        {
            get
            {
                bool leftHandedLayout = false;
                Windows.UI.ViewManagement.UISettings settings =
                    new Windows.UI.ViewManagement.UISettings();
                leftHandedLayout = (settings.HandPreference ==
                    Windows.UI.ViewManagement.HandPreference.LeftHanded);
                return leftHandedLayout;
            }
        }

        public bool portraitLayout = false;
        public bool PortraitLayout
        {
            get
            {
                Windows.UI.ViewManagement.ApplicationViewOrientation winOrientation = 
                    Windows.UI.ViewManagement.ApplicationView.GetForCurrentView().Orientation;
                portraitLayout = 
                    (winOrientation == 
                        Windows.UI.ViewManagement.ApplicationViewOrientation.Portrait);
                return portraitLayout;
            }
            set
            {
                if (value.Equals(portraitLayout)) return;
                portraitLayout = value;
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("PortraitLayout"));
            }
        }
        ```

1. 次に、いくつかのコンバーター クラスをプロジェクトに追加しましょう。 各クラスには、配置の値 ([HorizontalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.horizontalalignment) または [VerticalAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.verticalalignment)) を返す Convert オブジェクトが含まれています。
    1. 新しいフォルダーをプロジェクトに追加し、そのフォルダーに **Converters** という名前を付けます。
    1. 2 つの新しいクラスを Converters フォルダーに追加します (この例では、これらのクラスは **HorizontalAlignmentFromHandednessConverter.cs** および **VerticalAlignmentFromAppViewConverter.cs** という名前です)。
    1. `using Windows.UI.Xaml` 名前空間と `using Windows.UI.Xaml.Data` 名前空間を各ファイルに追加します。
    1. 各クラスを `public` に変更し、[IValueConverter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.data.ivalueconverter) インターフェイスを実装するように指定します。
    1. 次に示すように、[Convert](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.ivalueconverter.convert) メソッドと [ConvertBack](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.data.ivalueconverter.convertback) メソッドを各ファイルに追加します (ConvertBack メソッドは実装されない状態のままにしてあります)。
        - HorizontalAlignmentFromHandednessConverter によって、右利きのユーザーに対してはアプリの右側にインク ツール バーが配置され、左利きのユーザーに対してはアプリの左側に配置されます。
        ```csharp
        using System;

        using Windows.UI.Xaml;
        using Windows.UI.Xaml.Data;

        namespace locationandorientation.Converters
        {
            public class HorizontalAlignmentFromHandednessConverter : IValueConverter
            {
                public object Convert(object value, Type targetType,
                    object parameter, string language)
                {
                    bool leftHanded = (bool)value;
                    HorizontalAlignment alignment = HorizontalAlignment.Right;
                    if (leftHanded)
                    {
                        alignment = HorizontalAlignment.Left;
                    }
                    return alignment;
                }

                public object ConvertBack(object value, Type targetType,
                    object parameter, string language)
                {
                    throw new NotImplementedException();
                }
            }
        }
        ```

        - VerticalAlignmentFromAppViewConverter によって、縦長の向きの場合はアプリの中心にインク ツール バーが配置され、横長の向きの場合はアプリの上部にインク ツール バーが配置されます (使いやすさの向上を目的としていますが、これはデモンストレーションを行うために任意に選択した配置です)。
        ```csharp
        using System;

        using Windows.UI.Xaml;
        using Windows.UI.Xaml.Data;

        namespace locationandorientation.Converters
        {
            public class VerticalAlignmentFromAppViewConverter : IValueConverter
            {
                public object Convert(object value, Type targetType,
                    object parameter, string language)
                {
                    bool portraitOrientation = (bool)value;
                    VerticalAlignment alignment = VerticalAlignment.Top;
                    if (portraitOrientation)
                    {
                        alignment = VerticalAlignment.Center;
                    }
                    return alignment;
                }

                public object ConvertBack(object value, Type targetType,
                    object parameter, string language)
                {
                    throw new NotImplementedException();
                }
            }
        }
        ```

1. ここで、MainPage.xaml.cs ファイルを開きます。
    1. 追加`using using locationandorientation.ViewModels`ViewModel を関連付ける名前空間の一覧にします。
    1. 追加`using Windows.UI.ViewManagement`デバイスの方向に変更のリッスンを有効にする名前空間の一覧にします。
    1. 追加、 [WindowSizeChangedEventHandler](https://docs.microsoft.com/uwp/api/windows.ui.xaml.windowsizechangedeventhandler)コード。
    1. 設定、 [DataContext](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.FrameworkElement.DataContext) InkToolbarSnippetHostViewModel クラスのシングルトン インスタンスを表示します。 
    ```csharp
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Controls;

    using locationandorientation.ViewModels;
    using Windows.UI.ViewManagement;

    namespace locationandorientation
    {
        public sealed partial class MainPage : Page
        {
            public MainPage()
            {
                this.InitializeComponent();

                Window.Current.SizeChanged += (sender, args) =>
                {
                    ApplicationView currentView = ApplicationView.GetForCurrentView();

                    if (currentView.Orientation == ApplicationViewOrientation.Landscape)
                    {
                        InkToolbarSnippetHostViewModel.Instance.PortraitLayout = false;
                    }
                    else if (currentView.Orientation == ApplicationViewOrientation.Portrait)
                    {
                        InkToolbarSnippetHostViewModel.Instance.PortraitLayout = true;
                    }
                };

                DataContext = InkToolbarSnippetHostViewModel.Instance;
            }
        }
    }
    ```

1. 次に、MainPage.xaml ファイルを開きます。
    1. 追加`xmlns:converters="using:locationandorientation.Converters"`を`Page`コンバーターへのバインド要素。
        ```xaml
        <Page
        x:Class="locationandorientation.MainPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:locationandorientation"
        xmlns:converters="using:locationandorientation.Converters"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">
        ```

    1. 追加、`PageResources`要素と、コンバーターへの参照を指定します。
        ```xaml
        <Page.Resources>
            <converters:HorizontalAlignmentFromHandednessConverter x:Key="HorizontalAlignmentConverter"/>
            <converters:VerticalAlignmentFromAppViewConverter x:Key="VerticalAlignmentConverter"/>
        </Page.Resources>
        ```

    1. InkCanvas と InkToolbar 要素を追加し、InkToolbar の verticalalignment と HorizontalAlignment プロパティをバインドします。
        ```xaml
        <InkCanvas x:Name="inkCanvas" />
        <InkToolbar x:Name="inkToolbar" 
                    VerticalAlignment="{Binding PortraitLayout, Converter={StaticResource VerticalAlignmentConverter} }" 
                    HorizontalAlignment="{Binding LeftHandedLayout, Converter={StaticResource HorizontalAlignmentConverter} }" 
                    Orientation="Vertical" 
                    TargetInkCanvas="{x:Bind inkCanvas}" />
        ```

1. 追加する InkToolbarSnippetHostViewModel.cs ファイルに戻り、`PortraitLayout`と`LeftHandedLayout`にブール型のプロパティ、`InkToolbarSnippetHostViewModel`クラスを再バインドのサポートと共に`PortraitLayout`そのプロパティ値が変更されたとき。 
    ```csharp
    public bool LeftHandedLayout
    {
        get
        {
            bool leftHandedLayout = false;
            Windows.UI.ViewManagement.UISettings settings =
                new Windows.UI.ViewManagement.UISettings();
            leftHandedLayout = (settings.HandPreference ==
                Windows.UI.ViewManagement.HandPreference.LeftHanded);
            return leftHandedLayout;
        }
    }

    public bool portraitLayout = false;
    public bool PortraitLayout
    {
        get
        {
            Windows.UI.ViewManagement.ApplicationViewOrientation winOrientation = 
                Windows.UI.ViewManagement.ApplicationView.GetForCurrentView().Orientation;
            portraitLayout = 
                (winOrientation == 
                    Windows.UI.ViewManagement.ApplicationViewOrientation.Portrait);
            return portraitLayout;
        }
        set
        {
            if (value.Equals(portraitLayout)) return;
            portraitLayout = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("PortraitLayout"));
        }
    }

    #region INotifyPropertyChanged Members

    public event PropertyChangedEventHandler PropertyChanged;

    protected void OnPropertyChanged(string property)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(property));
    }

    #endregion
    ```

これで、ユーザーの手の主要な設定に適応し、ユーザーのデバイスの向きに動的に応答するインク対応アプリケーションが必要です。

### <a name="specify-the-selected-button"></a>選択されるボタンを指定する  
![初期化時に選択した鉛筆ボタン](./images/ink/ink-tools-default-toolbar.png)  
*初期化時に選択した鉛筆ボタンを使用して Windows インク ツールバー*

既定では、アプリが起動し、ツール バーが初期化されると、最初 (または左端) のボタンが選択されます。 既定の Windows Ink ツール バーでは、ボールペン ボタンが選択されます。

フレームワークで組み込みのボタンの順序が定義されるため、最初のボタンが既定でアクティブ化したいペンやツールでない場合があります。

この既定の動作を上書きし、ツール バーで選択されるボタンを指定できます。

ここでは、(ボールペンではなく) 鉛筆ボタンが選択され、鉛筆がアクティブになるように、既定のツール バーを初期化します。

1. 前の例から、InkCanvas と InkToolbar の XAML 宣言を使用します。
2. コード ビハインドで、[InkToolbar](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) オブジェクトの [Loaded](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.loaded) イベントのハンドラーを設定します。

  ```csharp
  /// <summary>
  /// An empty page that can be used on its own or navigated to within a Frame.
  /// Here, we set up InkToolbar event listeners.
  /// </summary>
  public MainPage_CodeBehind()
  {
      this.InitializeComponent();
      // Add handlers for InkToolbar events.
      inkToolbar.Loaded += inkToolbar_Loaded;
  }
  ```

3. [Loaded](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.loaded) イベントのハンドラーで次の処理を行います。
    1. 組み込みの [InkToolbarPencilButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpencilbutton) への参照を取得します。

    [GetToolButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar.gettoolbutton) メソッドで [InkToolbarTool.Pencil](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbartool) オブジェクトを渡すことで、[InkToolbarPencilButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpencilbutton) の [InkToolbarToolButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbartoolbutton) オブジェクトが返されます。

    2. 前の手順で返されたオブジェクトに [ActiveTool](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar.activetool) を設定します。

```CSharp
/// <summary>
/// Handle the Loaded event of the InkToolbar.
/// By default, the active tool is set to the first tool on the toolbar.
/// Here, we set the active tool to the pencil button.
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void inkToolbar_Loaded(object sender, RoutedEventArgs e)
{
    InkToolbarToolButton pencilButton = inkToolbar.GetToolButton(InkToolbarTool.Pencil);
    inkToolbar.ActiveTool = pencilButton;
}
```

### <a name="specify-the-built-in-buttons"></a>組み込みのボタンを指定する

![初期化時に含まれる特定のボタン](./images/ink/ink-tools-specific.png)  
*初期化時に含まれる特定のボタン*

既に説明したように、Windows Ink ツール バーには既定の組み込みボタンのコレクションが含まれます。 これらのボタンは次の順序で (左から右に) 表示されます。

- [InkToolbarBallpointPenButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarballpointpenbutton)
- [InkToolbarPencilButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpencilbutton)
- [InkToolbarHighlighterButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarhighlighterbutton)
- [InkToolbarEraserButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbareraserbutton)
- [InkToolbarRulerButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarrulerbutton)

ここでは、組み込みのボールペン、鉛筆、および消しゴムのボタンのみ表示されるようにツール バーを初期化します。

これは、XAML またはコード ビハインドを使用して実行できます。

**XAML**

最初の例から、InkCanvas と InkToolbar の XAML 宣言を変更します。
- [InitialControls](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar.initialcontrols) 属性を追加し、値を "[None](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarinitialcontrols)" に設定します。 これで組み込みボタンの既定のコレクションがクリアされます。
- アプリで必要な特定の InkToolbar ボタンを追加します。 ここでは、[InkToolbarBallpointPenButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarballpointpenbutton)、[InkToolbarPencilButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpencilbutton)、および [InkToolbarEraserButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbareraserbutton) のみ追加します。
> [!NOTE]
> ボタンは、ここで指定した順序ではなく、フレームワークで定義されている順序でツール バーに追加されます。

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header"
                   Text="Basic ink sample"
                   Style="{ThemeResource HeaderTextBlockStyle}"
                   Margin="10,0,0,0" />
    </StackPanel>
    <Grid Grid.Row="1">
        <Image Source="Assets\StoreLogo.png" />
        <!-- Clear the default InkToolbar buttons by setting InitialControls to None. -->
        <!-- Set the active tool to the pencil button. -->
        <InkCanvas x:Name="inkCanvas" />
        <InkToolbar x:Name="inkToolbar"
                    VerticalAlignment="Top"
                    TargetInkCanvas="{x:Bind inkCanvas}"
                    InitialControls="None">
            <!--
             Add only the ballpoint pen, pencil, and eraser.
             Note that the buttons are added to the toolbar in the order
             defined by the framework, not the order we specify here.
            -->
            <InkToolbarEraserButton />
            <InkToolbarBallpointPenButton />
            <InkToolbarPencilButton/>
        </InkToolbar>
    </Grid>
</Grid>
```

**分離コード**
1. 最初の例から、InkCanvas と InkToolbar の XAML 宣言を使用します。

  ```xaml
  <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
      <Grid.RowDefinitions>
          <RowDefinition Height="Auto"/>
          <RowDefinition Height="*"/>
      </Grid.RowDefinitions>
      <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
          <TextBlock x:Name="Header"
                     Text="Basic ink sample"
                     Style="{ThemeResource HeaderTextBlockStyle}"
                     Margin="10,0,0,0" />
      </StackPanel>
      <Grid Grid.Row="1">
          <Image Source="Assets\StoreLogo.png" />
          <InkCanvas x:Name="inkCanvas" />
          <InkToolbar x:Name="inkToolbar"
          VerticalAlignment="Top"
          TargetInkCanvas="{x:Bind inkCanvas}" />
      </Grid>
  </Grid>
  ```

2. コード ビハインドで、[InkToolbar](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar) オブジェクトの [Loading](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.loading) イベントのハンドラーを設定します。

  ```csharp
  /// <summary>
  /// An empty page that can be used on its own or navigated to within a Frame.
  /// Here, we set up InkToolbar event listeners.
  /// </summary>
  public MainPage_CodeBehind()
  {
      this.InitializeComponent();
      // Add handlers for InkToolbar events.
      inkToolbar.Loading += inkToolbar_Loading;
  }
  ```

3. [InitialControls](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar.initialcontrols) を "[None](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarinitialcontrols)" に設定します。
4. アプリで必要なボタンのオブジェクト参照を作成します。 ここでは、[InkToolbarBallpointPenButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarballpointpenbutton)、[InkToolbarPencilButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpencilbutton)、および [InkToolbarEraserButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbareraserbutton) のみ追加します。
  > [!NOTE]
  > ボタンは、ここで指定した順序ではなく、フレームワークで定義されている順序でツール バーに追加されます。

5. [Add](https://docs.microsoft.com/uwp/api/windows.ui.xaml.dependencyobjectcollection.add) メソッドを使用して、ボタンを InkToolbar に追加します。

  ```csharp
  /// <summary>
  /// Handles the Loading event of the InkToolbar.
  /// Here, we identify the buttons to include on the InkToolbar.
  /// </summary>
  /// <param name="sender">The InkToolbar</param>
  /// <param name="args">The InkToolbar event data.
  /// If there is no event data, this parameter is null</param>
  private void inkToolbar_Loading(FrameworkElement sender, object args)
  {
      // Clear all built-in buttons from the InkToolbar.
      inkToolbar.InitialControls = InkToolbarInitialControls.None;

      // Add only the ballpoint pen, pencil, and eraser.
      // Note that the buttons are added to the toolbar in the order
      // defined by the framework, not the order we specify here.
      InkToolbarBallpointPenButton ballpoint = new InkToolbarBallpointPenButton();
      InkToolbarPencilButton pencil = new InkToolbarPencilButton();
      InkToolbarEraserButton eraser = new InkToolbarEraserButton();
      inkToolbar.Children.Add(eraser);
      inkToolbar.Children.Add(ballpoint);
      inkToolbar.Children.Add(pencil);
  }
  ```

<!--
### Support touch input
By default, the InkToolbar supports both pen and mouse input, you have to enable support for touch input.
-->

## <a name="custom-buttons-and-inking-features"></a>カスタム ボタンおよび手書き入力機能

InkToolbar を通じて提供されるボタン (および関連する手書き入力機能) のコレクションをカスタマイズして拡張できます。

InkToolbar は、次のような 2 つの異なるボタンの種類のグループで構成されます。

1. "ツール" ボタンのグループ。組み込みの描画ボタン、消去ボタン、強調表示ボタンが含まれます。 カスタム ペンとカスタム ツールはここに追加されます。
> **注**&nbsp;&nbsp;機能の選択は相互に排他的です。

2. "トグル" ボタンのグループ。組み込みのルーラー ボタンが含まれます。 カスタム トグルはここに追加されます。
> **注**&nbsp;&nbsp;機能は、相互に排他的でないし、その他のアクティブなツールと同時に使用することができます。

お使いのアプリケーションと必要なインク機能によって異なりますが、InkToolbar には次のボタン (カスタムの手書き入力機能にバインドされます) を追加できます。

- カスタム ペン – インクのカラー パレットやペン先のプロパティ (形状、回転、サイズなど) がホスト アプリで定義されるペン。
- カスタム ツール – ホスト アプリで定義されるペン不使用ツール。
- カスタム トグル – アプリで定義された機能の状態をオンまたはオフに設定します。 オンにすると、機能はアクティブなツールと連携して動作します。

> **注**&nbsp;&nbsp;組み込みのボタンの表示順序を変更することはできません。 既定の表示順序は次のとおりです。ボールペン、鉛筆、蛍光ペン、消しゴムをルーラー。 カスタム ペンは最後の既定のペンに追加され、カスタム ツール ボタンは最後のペン ボタンと消しゴム ボタンの間に追加され、カスタム トグル ボタンはルーラー ボタンの後に追加されます  (カスタム ボタンは、指定されている順序で追加されます)。

### <a name="custom-pen"></a>カスタム ペン

形状、回転、サイズなどのインク カラー パレットと、ペン先のプロパティを定義するカスタムペン (カスタム ペン ボタンを使用してアクティブ化されます) を作成できます。

![カスタム カリグラフィ ペン ボタン](./images/ink/ink-tools-custompen.png)  
*カスタム カリグラフィ ペン ボタン*

ここでは、幅広のペン先で、基本的な筆記体のインク ストロークを可能にするカスタム ペンを定義します。 また、ボタン ポップアップに表示されるパレットのブラシのコレクションもカスタマイズします。

**分離コード**

まず、コード ビハインドでカスタム ペンを定義し、描画の属性を指定します。 このカスタム ペンを後で XAML から参照します。

1. ソリューション エクスプローラーでプロジェクトを右クリックし、[追加]、[新しい項目] の順に選びます。
2. [Visual C#] の [コード] で、新しいクラス ファイルを追加し、CalligraphicPen.cs という名前を付けます。
3. Calligraphic.cs で、既定の using ブロックを次のように置き換えます。
```csharp
using System.Numerics;
using Windows.UI;
using Windows.UI.Input.Inking;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Media;
```

4. CalligraphicPen クラスが [InkToolbarCustomPen](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarcustompen) から派生するように指定します。
```csharp
class CalligraphicPen : InkToolbarCustomPen
{
}
```

5. [CreateInkDrawingAttributesCore](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarcustompen.createinkdrawingattributescore) をオーバーライドし、ブラシとストロークのサイズを独自に指定します。
```csharp
class CalligraphicPen : InkToolbarCustomPen
{
    protected override InkDrawingAttributes
      CreateInkDrawingAttributesCore(Brush brush, double strokeWidth)
    {
    }
}
```

6. [InkDrawingAttributes](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkdrawingattributes) オブジェクトを作成し、[ペン先の形状](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkdrawingattributes.pentip)、[ペン先の回転](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkdrawingattributes.pentiptransform)、[ストロークのサイズ](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkdrawingattributes.size)、および[インクの色](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkdrawingattributes.color)を設定します。
```csharp
class CalligraphicPen : InkToolbarCustomPen
{
    protected override InkDrawingAttributes
      CreateInkDrawingAttributesCore(Brush brush, double strokeWidth)
    {
        InkDrawingAttributes inkDrawingAttributes =
          new InkDrawingAttributes();
        inkDrawingAttributes.PenTip = PenTipShape.Circle;
        inkDrawingAttributes.Size =
          new Windows.Foundation.Size(strokeWidth, strokeWidth * 20);
        SolidColorBrush solidColorBrush = brush as SolidColorBrush;
        if (solidColorBrush != null)
        {
            inkDrawingAttributes.Color = solidColorBrush.Color;
        }
        else
        {
            inkDrawingAttributes.Color = Colors.Black;
        }

        Matrix3x2 matrix = Matrix3x2.CreateRotation(45);
        inkDrawingAttributes.PenTipTransform = matrix;

        return inkDrawingAttributes;
    }
}
```

**XAML**

次に、MainPage.xaml で、カスタム ペンへの必要な参照を追加します。

1. CalligraphicPen.cs で定義したカスタム ペン (`CalligraphicPen`) と、カスタム ペンでサポートされる[ブラシ コレクション](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.BrushCollection) (`CalligraphicPenPalette`) への参照を作成するローカル ページのリソース ディクショナリを宣言します。
```xaml
<Page.Resources>
    <!-- Add the custom CalligraphicPen to the page resources. -->
    <local:CalligraphicPen x:Key="CalligraphicPen" />
    <!-- Specify the colors for the palette of the custom pen. -->
    <BrushCollection x:Key="CalligraphicPenPalette">
        <SolidColorBrush Color="Blue" />
        <SolidColorBrush Color="Red" />
    </BrushCollection>
</Page.Resources>
```

2. 次に、InkToolbar と子要素の [InkToolbarCustomPenButton](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarcustompenbutton) を追加します。

  カスタム ペン ボタンには、ページ リソースで宣言された `CalligraphicPen` と `CalligraphicPenPalette` の 2 つの静的なリソース参照が含まれます。

  また、ストローク サイズのスライダーの範囲 ([MinStrokeWidth](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpenbutton.minstrokewidth)、[MaxStrokeWidth](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpenbutton.maxstrokewidth)、および [SelectedStrokeWidth](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpenbutton.selectedstrokewidthproperty))、選択されたブラシ ([SelectedBrushIndex](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbarpenbutton.selectedbrushindex))、カスタム ペン ボタンのアイコン ([SymbolIcon](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.symbolicon)) も指定します。
```xaml
<Grid Grid.Row="1">
    <InkCanvas x:Name="inkCanvas" />
    <InkToolbar x:Name="inkToolbar"
                VerticalAlignment="Top"
                TargetInkCanvas="{x:Bind inkCanvas}">
        <InkToolbarCustomPenButton
            CustomPen="{StaticResource CalligraphicPen}"
            Palette="{StaticResource CalligraphicPenPalette}"
            MinStrokeWidth="1" MaxStrokeWidth="3" SelectedStrokeWidth="2"
            SelectedBrushIndex ="1">
            <SymbolIcon Symbol="Favorite" />
            <InkToolbarCustomPenButton.ConfigurationContent>
                <InkToolbarPenConfigurationControl />
            </InkToolbarCustomPenButton.ConfigurationContent>
        </InkToolbarCustomPenButton>
    </InkToolbar>
</Grid>
```

### <a name="custom-toggle"></a>カスタム トグル

カスタム トグル (カスタム トグル ボタンを使用してアクティブ化されます) を作成して、アプリ定義の機能の状態をオンまたはオフに設定できます。 オンにすると、機能はアクティブなツールと連携して動作します。

この例では、タッチ入力による手書き入力を可能にするカスタム トグル ボタンを定義しています (既定では、タッチの手書き入力は有効化されていません)。

> [!NOTE]  
> タッチを使った手書き入力をサポートする必要がある場合は、この例で指定されたアイコンとツールチップを使い、CustomToggleButton を使用して手書き入力を有効化することをお勧めします。

通常タッチ入力は、オブジェクトまたはアプリの UI を直接操作するために使用されます。 タッチによる手書き入力を有効化したときの動作の違いを示すために、InkCanvas を ScrollViewer コンテナ内に配置し、ScrollViewer のサイズを InkCanvas よりも小さく設定します。 

アプリが起動すると、ペンによる手書き入力のみがサポートされ、タッチは手書き入力の入力面をパンまたはズームするために使用されます。 タッチによる手書き入力が有効化されていると、手書き入力の入力面をタッチ入力でパンまたはズームすることはできません。

> [!NOTE]
> [  **InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) および [**InkToolbar**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkToolbar) の UX ガイドラインは、「[インク コントロール](../controls-and-patterns/inking-controls.md)」をご覧ください。 次の推奨事項は、この例に関連したものです。
> - [  **InkToolbar**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkToolbar) と手書き入力全般は、アクティブなペンを通じて最適なエクスペリエンスを実現します。 ただし、アプリで必要な場合は、マウスやタッチによる手書き入力をサポートできます。 
> - タッチ入力による手書き入力をサポートする場合、トグル ボタンに "Segoe MLD2 アセット" フォントの "ED5F" アイコンを使うと共に、"タッチによる手書き" というヒントを表示することをお勧めします。 

**XAML**

1. まず、イベント ハンドラー (Toggle_Custom) を指定する Click イベント リスナーを持つ [**InkToolbarCustomToggleButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkToolbarCustomToggleButton) 要素 (toggleButton) を宣言します。

```xaml 
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <StackPanel Grid.Row="0" 
                x:Name="HeaderPanel" 
                Orientation="Horizontal">
        <TextBlock x:Name="Header" 
                   Text="Basic ink sample" 
                   Style="{ThemeResource HeaderTextBlockStyle}" 
                   Margin="10" />
    </StackPanel>

    <ScrollViewer Grid.Row="1" 
                  HorizontalScrollBarVisibility="Auto" 
                  VerticalScrollBarVisibility="Auto">
        
        <Grid HorizontalAlignment="Left" VerticalAlignment="Top">
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
            
            <InkToolbar Grid.Row="0" 
                        Margin="10"
                        x:Name="inkToolbar" 
                        VerticalAlignment="Top"
                        TargetInkCanvas="{x:Bind inkCanvas}">
                <InkToolbarCustomToggleButton 
                x:Name="toggleButton" 
                Click="CustomToggle_Click" 
                ToolTipService.ToolTip="Touch Writing">
                    <SymbolIcon Symbol="{x:Bind TouchWritingIcon}"/>
                </InkToolbarCustomToggleButton>
            </InkToolbar>
            
            <ScrollViewer Grid.Row="1" 
                          Height="500"
                          Width="500"
                          x:Name="scrollViewer" 
                          ZoomMode="Enabled" 
                          MinZoomFactor=".1" 
                          VerticalScrollMode="Enabled" 
                          VerticalScrollBarVisibility="Auto" 
                          HorizontalScrollMode="Enabled" 
                          HorizontalScrollBarVisibility="Auto">
                
                <Grid x:Name="outputGrid" 
                      Height="1000"
                      Width="1000"
                      Background="{ThemeResource SystemControlBackgroundChromeWhiteBrush}">
                    <InkCanvas x:Name="inkCanvas"/>
                </Grid>
                
            </ScrollViewer>
        </Grid>
    </ScrollViewer>
</Grid>
```

**分離コード**

2. 前のスニペットでは、タッチによる手書き入力 (toggleButton) のカスタム トグル ボタンの Click イベント リスナーとハンドラー (Toggle_Custom) を宣言しました。 このハンドラーは、InkPresenter の InputDeviceTypes プロパティを使って、CoreInputDeviceTypes.Touch のサポートを単にトグルします。

   また、SymbolIcon 要素と、コードビハインド ファイル (TouchWritingIcon) で定義されたフィールドにバインドする {x：Bind} マークアップ拡張を使用して、ボタンのアイコンを指定しました。

   次のスニペットには、Click イベント ハンドラーと TouchWritingIcon の定義の両方が含まれています。

```csharp 
namespace Ink_Basic_InkToolbar
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage_AddCustomToggle : Page
    {
        Symbol TouchWritingIcon = (Symbol)0xED5F;

        public MainPage_AddCustomToggle()
        {
            this.InitializeComponent();
        }

        // Handler for the custom toggle button that enables touch inking.
        private void CustomToggle_Click(object sender, RoutedEventArgs e)
        {
            if (toggleButton.IsChecked == true)
            {
                inkCanvas.InkPresenter.InputDeviceTypes |= CoreInputDeviceTypes.Touch;
            }
            else
            {
                inkCanvas.InkPresenter.InputDeviceTypes &= ~CoreInputDeviceTypes.Touch;
            }
        }
    }
}
```

### <a name="custom-tool"></a>カスタム ツール

カスタム ツール ボタンを作成して、アプリで定義されたペン以外のツールを呼び出すことができます。

既定では、[**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) はすべての入力をインク ストロークか消去ストロークとして処理します。 これには、セカンダリ ハードウェア アフォーダンス (ペン バレル ボタン、マウスの右ボタンなど) によって変更された入力も含まれます。 ただし、[**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) は、特定の入力を未処理のままにするように設定でき、それをカスタム処理のためにアプリに渡すことができます。

この例では、カスタム ツール ボタンを定義しており、これを選択すると、後続のストロークはインクではなく、なげなわ選択 (破線) として処理されてレンダリングされます。 選択領域の範囲内のすべてのインク ストロークが [**Selected**](https://docs.microsoft.com/uwp/api/windows.ui.input.inking.inkstroke.selected) に設定されます。

> [!NOTE]
> InkCanvas および InkToolbar の UX ガイドラインは、「インク コントロール」をご覧ください。 次の推奨事項は、この例に関連したものです。
> - ストローク選択を提供する場合は、「選択ツール」ツールチップを使用して、ツール ボタンの "Segoe MLD2 アセット" フォントの "EF20" アイコンを使用することをお勧めします。 
 
**XAML**

1. まず、ストローク選択が構成されているイベント ハンドラー (customToolButton_Click) を指定する Click イベント リスナーを持つ [**InkToolbarCustomToolButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkToolbarCustomToolButton) 要素 (customToolButton) を宣言します。 (ストローク選択のコピー、切り取り、貼り付けのための一連のボタンも追加しました。)

2. 選択ストロークを描画するための Canvas 要素も追加します。 別のレイヤーを使って選択ストロークを描画すると、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) とそのコンテンツは影響を受けることがありません。 

```xaml
<Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <StackPanel x:Name="HeaderPanel" Orientation="Horizontal" Grid.Row="0">
        <TextBlock x:Name="Header" 
                   Text="Basic ink sample" 
                   Style="{ThemeResource HeaderTextBlockStyle}" 
                   Margin="10,0,0,0" />
    </StackPanel>
    <StackPanel x:Name="ToolPanel" Orientation="Horizontal" Grid.Row="1">
        <InkToolbar x:Name="inkToolbar" 
                    VerticalAlignment="Top" 
                    TargetInkCanvas="{x:Bind inkCanvas}">
            <InkToolbarCustomToolButton 
                x:Name="customToolButton" 
                Click="customToolButton_Click" 
                ToolTipService.ToolTip="Selection tool">
                <SymbolIcon Symbol="{x:Bind SelectIcon}"/>
            </InkToolbarCustomToolButton>
        </InkToolbar>
        <Button x:Name="cutButton" 
                Content="Cut" 
                Click="cutButton_Click"
                Width="100"
                Margin="5,0,0,0"/>
        <Button x:Name="copyButton" 
                Content="Copy"  
                Click="copyButton_Click"
                Width="100"
                Margin="5,0,0,0"/>
        <Button x:Name="pasteButton" 
                Content="Paste"  
                Click="pasteButton_Click"
                Width="100"
                Margin="5,0,0,0"/>
    </StackPanel>
    <Grid Grid.Row="2" x:Name="outputGrid" 
              Background="{ThemeResource SystemControlBackgroundChromeWhiteBrush}" 
              Height="Auto">
        <!-- Canvas for displaying selection UI. -->
        <Canvas x:Name="selectionCanvas"/>
        <!-- Canvas for displaying ink. -->
        <InkCanvas x:Name="inkCanvas" />
    </Grid>
</Grid>
```

**分離コード**

2. 次に、MainPage.xaml.cs コードビハインド ファイルの [**InkToolbarCustomToolButton**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkToolbarCustomToolButton) の Click イベントを処理します。

   このハンドラは、未処理の入力をアプリに渡すように [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) を設定します。 

   このコードをより詳細なステップ。パススルーの入力の高度な処理のセクションを参照してください[UWP アプリでの相互作用と Windows の手描き入力をペン](pen-and-stylus-interactions.md)します。

   また、SymbolIcon 要素と、コードビハインド ファイル (SelectIcon) で定義されたフィールドにバインドする {x：Bind} マークアップ拡張を使用して、ボタンのアイコンを指定しました。

   次のスニペットには、Click イベント ハンドラーと SelectIcon の定義の両方が含まれています。

```csharp
namespace Ink_Basic_InkToolbar
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage_AddCustomTool : Page
    {
        // Icon for custom selection tool button.
        Symbol SelectIcon = (Symbol)0xEF20;

        // Stroke selection tool.
        private Polyline lasso;
        // Stroke selection area.
        private Rect boundingRect;

        public MainPage_AddCustomTool()
        {
            this.InitializeComponent();

            // Listen for new ink or erase strokes to clean up selection UI.
            inkCanvas.InkPresenter.StrokeInput.StrokeStarted +=
                StrokeInput_StrokeStarted;
            inkCanvas.InkPresenter.StrokesErased +=
                InkPresenter_StrokesErased;
        }

        private void customToolButton_Click(object sender, RoutedEventArgs e)
        {
            // By default, the InkPresenter processes input modified by 
            // a secondary affordance (pen barrel button, right mouse 
            // button, or similar) as ink.
            // To pass through modified input to the app for custom processing 
            // on the app UI thread instead of the background ink thread, set 
            // InputProcessingConfiguration.RightDragAction to LeaveUnprocessed.
            inkCanvas.InkPresenter.InputProcessingConfiguration.RightDragAction =
                InkInputRightDragAction.LeaveUnprocessed;

            // Listen for unprocessed pointer events from modified input.
            // The input is used to provide selection functionality.
            inkCanvas.InkPresenter.UnprocessedInput.PointerPressed +=
                UnprocessedInput_PointerPressed;
            inkCanvas.InkPresenter.UnprocessedInput.PointerMoved +=
                UnprocessedInput_PointerMoved;
            inkCanvas.InkPresenter.UnprocessedInput.PointerReleased +=
                UnprocessedInput_PointerReleased;
        }

        // Handle new ink or erase strokes to clean up selection UI.
        private void StrokeInput_StrokeStarted(
            InkStrokeInput sender, Windows.UI.Core.PointerEventArgs args)
        {
            ClearSelection();
        }

        private void InkPresenter_StrokesErased(
            InkPresenter sender, InkStrokesErasedEventArgs args)
        {
            ClearSelection();
        }

        private void cutButton_Click(object sender, RoutedEventArgs e)
        {
            inkCanvas.InkPresenter.StrokeContainer.CopySelectedToClipboard();
            inkCanvas.InkPresenter.StrokeContainer.DeleteSelected();
            ClearSelection();
        }

        private void copyButton_Click(object sender, RoutedEventArgs e)
        {
            inkCanvas.InkPresenter.StrokeContainer.CopySelectedToClipboard();
        }

        private void pasteButton_Click(object sender, RoutedEventArgs e)
        {
            if (inkCanvas.InkPresenter.StrokeContainer.CanPasteFromClipboard())
            {
                inkCanvas.InkPresenter.StrokeContainer.PasteFromClipboard(
                    new Point(0, 0));
            }
            else
            {
                // Cannot paste from clipboard.
            }
        }

        // Clean up selection UI.
        private void ClearSelection()
        {
            var strokes = inkCanvas.InkPresenter.StrokeContainer.GetStrokes();
            foreach (var stroke in strokes)
            {
                stroke.Selected = false;
            }
            ClearBoundingRect();
        }

        private void ClearBoundingRect()
        {
            if (selectionCanvas.Children.Any())
            {
                selectionCanvas.Children.Clear();
                boundingRect = Rect.Empty;
            }
        }

        // Handle unprocessed pointer events from modifed input.
        // The input is used to provide selection functionality.
        // Selection UI is drawn on a canvas under the InkCanvas.
        private void UnprocessedInput_PointerPressed(
            InkUnprocessedInput sender, PointerEventArgs args)
        {
            // Initialize a selection lasso.
            lasso = new Polyline()
            {
                Stroke = new SolidColorBrush(Windows.UI.Colors.Blue),
                StrokeThickness = 1,
                StrokeDashArray = new DoubleCollection() { 5, 2 },
            };

            lasso.Points.Add(args.CurrentPoint.RawPosition);

            selectionCanvas.Children.Add(lasso);
        }

        private void UnprocessedInput_PointerMoved(
            InkUnprocessedInput sender, PointerEventArgs args)
        {
            // Add a point to the lasso Polyline object.
            lasso.Points.Add(args.CurrentPoint.RawPosition);
        }

        private void UnprocessedInput_PointerReleased(
            InkUnprocessedInput sender, PointerEventArgs args)
        {
            // Add the final point to the Polyline object and 
            // select strokes within the lasso area.
            // Draw a bounding box on the selection canvas 
            // around the selected ink strokes.
            lasso.Points.Add(args.CurrentPoint.RawPosition);

            boundingRect =
                inkCanvas.InkPresenter.StrokeContainer.SelectWithPolyLine(
                    lasso.Points);

            DrawBoundingRect();
        }

        // Draw a bounding rectangle, on the selection canvas, encompassing 
        // all ink strokes within the lasso area.
        private void DrawBoundingRect()
        {
            // Clear all existing content from the selection canvas.
            selectionCanvas.Children.Clear();

            // Draw a bounding rectangle only if there are ink strokes 
            // within the lasso area.
            if (!((boundingRect.Width == 0) ||
                (boundingRect.Height == 0) ||
                boundingRect.IsEmpty))
            {
                var rectangle = new Rectangle()
                {
                    Stroke = new SolidColorBrush(Windows.UI.Colors.Blue),
                    StrokeThickness = 1,
                    StrokeDashArray = new DoubleCollection() { 5, 2 },
                    Width = boundingRect.Width,
                    Height = boundingRect.Height
                };

                Canvas.SetLeft(rectangle, boundingRect.X);
                Canvas.SetTop(rectangle, boundingRect.Y);

                selectionCanvas.Children.Add(rectangle);
            }
        }
    }
}
```



### <a name="custom-ink-rendering"></a>カスタム インク レンダリング

既定では、手書き入力は低待機時間のバックグラウンド スレッドで処理され、描画と同時に "ウェット" レンダリングが行われます。 ストロークが完了すると (ペンまたは指が画面を離れるか、マウスのボタンが離されると)、UI スレッドでストロークが処理されて、[**InkCanvas**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) レイヤーへの "ドライ" レンダリングが行われます (アプリケーション コンテンツの上にレンダリングされてウェット インクが置き換えられます)。

インク プラットフォームでは、この動作を上書きして、手書き入力のカスタム ドライ レンダリングによって手書き入力エクスペリエンスを全面的にカスタマイズすることができます。

カスタム ドライ レンダリングについて詳しくは、「[UWP アプリでのペン操作と Windows Ink](https://docs.microsoft.com/windows/uwp/design/input/pen-and-stylus-interactions#custom-ink-rendering)」をご覧ください。

> [!NOTE]
> カスタム ドライ レンダリングと [**InkToolbar**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inktoolbar)  
> カスタム ドライの実装によって、アプリが [**InkPresenter**](https://docs.microsoft.com/uwp/api/Windows.UI.Input.Inking.InkPresenter) の既定のインク レンダリング動作を上書きすると、レンダリングされたインク ストロークが InkToolbar で利用できなくなり、InkToolbar の組み込みの消去コマンドが正常に機能しなくなります。 消去機能を提供するには、すべてのポインター イベントを処理し、ストロークごとにヒット テストを実行すると共に、組み込みの [すべてのインクのデータを消去] コマンドをオーバーライドする必要があります。

## <a name="related-articles"></a>関連記事

- [ペン操作とスタイラス操作](pen-and-stylus-interactions.md)

### <a name="topic-samples"></a>トピックのサンプル

- [インク ツールバー位置や向きのサンプル (基本)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness.zip)
- [インク ツールバー位置や向きのサンプル (動的)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-ink-toolbar-handedness-dynamic.zip)

### <a name="other-samples"></a>その他のサンプル

- [単純なインクのサンプル (C#/C++)](https://go.microsoft.com/fwlink/p/?LinkID=620312)
- [複雑なインクのサンプル (C++)](https://go.microsoft.com/fwlink/p/?LinkID=620314)
- [インクのサンプル (JavaScript)](https://go.microsoft.com/fwlink/p/?LinkID=620308)
- [チュートリアルを開始します。UWP アプリでのインクをサポートします。](https://aka.ms/appsample-ink)
- [書籍のサンプルを色分け表示](https://aka.ms/cpubsample-coloringbook)
- [ファミリのノートのサンプル](https://aka.ms/cpubsample-familynotessample)
