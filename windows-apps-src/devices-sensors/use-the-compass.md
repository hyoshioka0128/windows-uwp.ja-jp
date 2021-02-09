---
ms.assetid: 5B30E32F-27E0-4656-A834-391A559AC8BC
title: コンパスの使用
description: ユニバーサル Windows プラットフォーム (UWP) コンパス API を使用して、ナビゲーションアプリの現在の見出しを確認する方法について説明します。
ms.date: 06/06/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 4ddd5ddddb31cf93977cb0d5bd9c16e916c4126b
ms.sourcegitcommit: e81227399ba0f286e74e4977d757237829440a2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96310200"
---
# <a name="use-the-compass"></a>コンパスの使用


**重要な API**

-   [**Windows.Devices.Sensors**](/uwp/api/Windows.Devices.Sensors)
-   [**コンパス**](/uwp/api/Windows.Devices.Sensors.Compass)

**サンプル**

-   より完全な実装については、[コンパスのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Compass)をご覧ください。

コンパスを使って現在の方位を検出する方法を説明します。

磁北または真北を基準とした現在の方位をアプリで取得できます。 ナビゲーション アプリでは、コンパスを使ってデバイスが向いている方位を検出し、それに応じて地図の向きを設定します。

## <a name="prerequisites"></a>[前提条件]

Extensible Application Markup Language (XAML)、Microsoft Visual C#、イベントについて理解している必要があります。

使うデバイスやエミュレーターがコンパスをサポートしている必要があります。

## <a name="create-a-simple-compass-app"></a>シンプルなコンパス アプリを作成する

このセクションは、次の 2 つのサブセクションに分かれています。 最初のサブセクションでは、シンプルなコンパス アプリケーションを最初から作成するために必要な手順を示します。 次のサブセクションでは、作成したアプリについて説明します。

### <a name="instructions"></a>手順

-   **[Visual C#]** プロジェクト テンプレートから **[空白のアプリ (ユニバーサル Windows]** を選んで、新しいプロジェクトを作成します。

-   プロジェクトの MainPage.xaml.cs ファイルを開き、記載されているコードを次のコードで置き換えます。

```csharp
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using Windows.Foundation;
    using Windows.Foundation.Collections;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Controls;
    using Windows.UI.Xaml.Controls.Primitives;
    using Windows.UI.Xaml.Data;
    using Windows.UI.Xaml.Input;
    using Windows.UI.Xaml.Media;
    using Windows.UI.Xaml.Navigation;

    using Windows.UI.Core; // Required to access the core dispatcher object
    using Windows.Devices.Sensors; // Required to access the sensor platform and the compass


    namespace App1
    {
        /// <summary>
        /// An empty page that can be used on its own or navigated to within a Frame.
        /// </summary>
        public sealed partial class MainPage : Page
        {
            private Compass _compass; // Our app' s compass object

            // This event handler writes the current compass reading to
            // the textblocks on the app' s main page.

            private async void ReadingChanged(object sender, CompassReadingChangedEventArgs e)
            {
               await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
                {
                    CompassReading reading = e.Reading;
                    txtMagnetic.Text = String.Format("{0,5:0.00}", reading.HeadingMagneticNorth);
                    if (reading.HeadingTrueNorth.HasValue)
                        txtNorth.Text = String.Format("{0,5:0.00}", reading.HeadingTrueNorth);
                    else
                        txtNorth.Text = "No reading.";
                });
            }

            public MainPage()
            {
                this.InitializeComponent();
               _compass = Compass.GetDefault(); // Get the default compass object

                // Assign an event handler for the compass reading-changed event
                if (_compass != null)
                {
                    // Establish the report interval for all scenarios
                    uint minReportInterval = _compass.MinimumReportInterval;
                    uint reportInterval = minReportInterval > 16 ? minReportInterval : 16;
                    _compass.ReportInterval = reportInterval;
                    _compass.ReadingChanged += new TypedEventHandler<Compass, CompassReadingChangedEventArgs>(ReadingChanged);
                }
            }
        }
    }
```

元のスニペットの名前空間の名前を、自分のプロジェクトに指定した名前に変更する必要があります。 たとえば、作成したプロジェクトの名前が **CompassCS** だとすると、`namespace App1` を `namespace CompassCS` に置き換えます。

-   MainPage.xaml ファイルを開き、元の内容を次の XML に置き換えます。

```xml
    <Page
        x:Class="App1.MainPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:App1"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid x:Name="LayoutRoot" Background="#FF0C0C0C">
            <TextBlock HorizontalAlignment="Left" Height="22" Margin="8,18,0,0" TextWrapping="Wrap" Text="Magnetic Heading:" VerticalAlignment="Top" Width="104" Foreground="#FFFBF9F9"/>
            <TextBlock HorizontalAlignment="Left" Height="18" Margin="8,58,0,0" TextWrapping="Wrap" Text="True North Heading:" VerticalAlignment="Top" Width="104" Foreground="#FFF3F3F3"/>
            <TextBlock x:Name="txtMagnetic" HorizontalAlignment="Left" Height="22" Margin="130,18,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top" Width="116" Foreground="#FFFBF6F6"/>
            <TextBlock x:Name="txtNorth" HorizontalAlignment="Left" Height="18" Margin="130,58,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top" Width="116" Foreground="#FFF5F1F1"/>

         </Grid>
    </Page>
```

元のスニペットのクラス名の最初の部分を、自分のアプリの名前空間に置き換える必要があります。 たとえば、作成したプロジェクトの名前が **CompassCS** だとすると、`x:Class="App1.MainPage"` を `x:Class="CompassCS.MainPage"` に置き換えます。 また、`xmlns:local="using:App1"` を `xmlns:local="using:CompassCS"` に置き換える必要があります。

-   F5 キーを押すか **、[デバッグ**] [デバッグの開始] を選択してアプリを  >  **Start Debugging** ビルド、デプロイ、実行します。

アプリを実行した後、デバイスを移動するか、エミュレーター ツールを使うことによって、コンパスの値を変更できます。

-   Visual Studio に戻り、Shift キーを押しながら F5 キーを押すか、[**デバッグ**] [  >  **デバッグの停止**] を選択してアプリを停止し、アプリを停止します。

### <a name="explanation"></a>説明

上に示した例では、ごく短いコードを作成するだけで、コンパス入力をアプリに組み込むことができることがわかります。

このアプリでは、**MainPage** メソッドで、既定のコンパスとの接続を確立しています。

```csharp
_compass = Compass.GetDefault(); // Get the default compass object
```

このアプリでは、**MainPage** メソッドで、レポート間隔を設定しています。 次のコードは、デバイスでサポートされる最小の間隔を取得し、要求される 16 ミリ秒の間隔 (約 60 Hz のリフレッシュ レート) と比較します。 サポートされる最小の間隔が要求される間隔よりも大きい場合は、値を最小値に設定します。 それ以外の場合は、値を要求される間隔に設定します。

```csharp
uint minReportInterval = _compass.MinimumReportInterval;
uint reportInterval = minReportInterval > 16 ? minReportInterval : 16;
_compass.ReportInterval = reportInterval;
```

**ReadingChanged** メソッドで、新しいコンパス データをキャプチャしています。 センサーのドライバーは、センサーから新しいデータを受け取るたびに、このイベント ハンドラーを使ってアプリに値を渡します。 このアプリの場合、このイベント ハンドラーが次の行で登録されています。

```csharp
_compass.ReadingChanged += new TypedEventHandler<Compass,
CompassReadingChangedEventArgs>(ReadingChanged);
```

プロジェクトの XAML 内にある TextBlock に、これらの新しい値が書き込まれます。

```xml
 <TextBlock HorizontalAlignment="Left" Height="22" Margin="8,18,0,0" TextWrapping="Wrap" Text="Magnetic Heading:" VerticalAlignment="Top" Width="104" Foreground="#FFFBF9F9"/>
 <TextBlock HorizontalAlignment="Left" Height="18" Margin="8,58,0,0" TextWrapping="Wrap" Text="True North Heading:" VerticalAlignment="Top" Width="104" Foreground="#FFF3F3F3"/>
 <TextBlock x:Name="txtMagnetic" HorizontalAlignment="Left" Height="22" Margin="130,18,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top" Width="116" Foreground="#FFFBF6F6"/>
 <TextBlock x:Name="txtNorth" HorizontalAlignment="Left" Height="18" Margin="130,58,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top" Width="116" Foreground="#FFF5F1F1"/>
```
 

 
