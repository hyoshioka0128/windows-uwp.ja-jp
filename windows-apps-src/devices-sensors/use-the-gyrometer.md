---
ms.assetid: 454953E1-DD8F-44B7-A614-7BAD8C683536
title: ジャイロメーターの使用
description: ジャイロ API を使用して、傾斜速度や回転運動などのユーザー移動の変化を検出するジャイロ入力をアプリに統合する方法について説明します。
ms.date: 06/06/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 2e82b2e7de98c28bba860fd1c935a63b06390a4b
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89159536"
---
# <a name="use-the-gyrometer"></a>ジャイロメーターの使用


**重要な API**

-   [**Windows.Devices.Sensors**](/uwp/api/Windows.Devices.Sensors)
-   [**Gyrometer**](/uwp/api/Windows.Devices.Sensors.Gyrometer)

**サンプル**

-   より完全な実装については、[ジャイロメーターのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/gyrometer)をご覧ください。

ジャイロメーターを使ってユーザーの動きの変化を検出する方法を説明します。

ゲーム コントローラーとして使う場合、ジャイロメーターは加速度計の機能を補完します。 加速度計で直線的な動きを計測し、ジャイロメーターで角速度、つまり回転の動きを計測します。

## <a name="prerequisites"></a>前提条件

Extensible Application Markup Language (XAML)、Microsoft Visual C#、イベントについて理解している必要があります。

使うデバイスやエミュレーターがジャイロメーターをサポートしている必要があります。

## <a name="create-a-simple-gyrometer-app"></a>シンプルなジャイロメーター アプリを作成する

このセクションは、次の 2 つのサブセクションに分かれています。 最初のサブセクションでは、シンプルなジャイロメーター アプリケーションを最初から作成するために必要な手順を示します。 次のサブセクションでは、作成したアプリについて説明します。

###  <a name="instructions"></a>Instructions

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
    using Windows.Devices.Sensors; // Required to access the sensor platform and the gyrometer


    namespace App1
    {
        /// <summary>
        /// An empty page that can be used on its own or navigated to within a Frame.
        /// </summary>
        public sealed partial class MainPage : Page
        {
            private Gyrometer _gyrometer; // Our app' s gyrometer object

            // This event handler writes the current gyrometer reading to
            // the three textblocks on the app' s main page.

            private async void ReadingChanged(object sender, GyrometerReadingChangedEventArgs e)
            {
                await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
                {
                    GyrometerReading reading = e.Reading;
                    txtXAxis.Text = String.Format("{0,5:0.00}", reading.AngularVelocityX);
                    txtYAxis.Text = String.Format("{0,5:0.00}", reading.AngularVelocityY);
                    txtZAxis.Text = String.Format("{0,5:0.00}", reading.AngularVelocityZ);
                });
            }

            public MainPage()
            {
                this.InitializeComponent();
                _gyrometer = Gyrometer.GetDefault(); // Get the default gyrometer sensor object

                if (_gyrometer != null)
                {
                    // Establish the report interval for all scenarios
                    uint minReportInterval = _gyrometer.MinimumReportInterval;
                    uint reportInterval = minReportInterval > 16 ? minReportInterval : 16;
                    _gyrometer.ReportInterval = reportInterval;

                    // Assign an event handler for the gyrometer reading-changed event
                    _gyrometer.ReadingChanged += new TypedEventHandler<Gyrometer, GyrometerReadingChangedEventArgs>(ReadingChanged);
                }

            }
        }
    }
```

元のスニペットの名前空間の名前を、自分のプロジェクトに指定した名前に変更する必要があります。 たとえば、作成したプロジェクトの名前が **GyrometerCS** だとすると、`namespace App1` を `namespace GyrometerCS` に置き換えます。

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
            <TextBlock HorizontalAlignment="Left" Height="23" Margin="8,8,0,0" TextWrapping="Wrap" Text="X-Axis:" VerticalAlignment="Top" Width="46" Foreground="#FFFDFDFD"/>
            <TextBlock x:Name="txtXAxis" HorizontalAlignment="Left" Height="23" Margin="67,8,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="88" Foreground="#FFFDFAFA"/>
            <TextBlock HorizontalAlignment="Left" Height="20" Margin="8,52,0,0" TextWrapping="Wrap" Text="Y Axis:" VerticalAlignment="Top" Width="46" Foreground="White"/>
            <TextBlock x:Name="txtYAxis" HorizontalAlignment="Left" Height="24" Margin="54,48,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="80" Foreground="#FFFBFBFB"/>
            <TextBlock HorizontalAlignment="Left" Height="21" Margin="8,93,0,0" TextWrapping="Wrap" Text="Z Axis:" VerticalAlignment="Top" Width="46" Foreground="#FFFEFBFB"/>
            <TextBlock x:Name="txtZAxis" HorizontalAlignment="Left" Height="21" Margin="54,93,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="63" Foreground="#FFF8F3F3"/>

        </Grid>
    </Page>
```

元のスニペットのクラス名の最初の部分を、自分のアプリの名前空間に置き換える必要があります。 たとえば、作成したプロジェクトの名前が **GyrometerCS** だとすると、`x:Class="App1.MainPage"` を `x:Class="GyrometerCS.MainPage"` に置き換えます。 また、`xmlns:local="using:App1"` を `xmlns:local="using:GyrometerCS"` に置き換える必要があります。

-   F5 キーを押すか **、[デバッグ**] [デバッグの開始] を選択してアプリを  >  **Start Debugging**ビルド、デプロイ、実行します。

アプリを実行した後、デバイスを移動するか、エミュレーター ツールを使うことによって、ジャイロメーターの値を変更できます。

-   Visual Studio に戻り、Shift キーを押しながら F5 キーを押すか、[**デバッグ**] [  >  **デバッグの停止**] を選択してアプリを停止し、アプリを停止します。

###  <a name="explanation"></a>説明

上に示した例では、ごく短いコードを作成するだけで、ジャイロメーター入力をアプリに組み込むことができることがわかります。

このアプリでは、**MainPage** メソッドで、既定のジャイロメーターとの接続を確立しています。

```csharp
_gyrometer = Gyrometer.GetDefault(); // Get the default gyrometer sensor object
```

このアプリでは、**MainPage** メソッドで、レポート間隔を設定しています。 次のコードは、デバイスでサポートされる最小の間隔を取得し、要求される 16 ミリ秒の間隔 (約 60 Hz のリフレッシュ レート) と比較します。 サポートされる最小の間隔が要求される間隔よりも大きい場合は、値を最小値に設定します。 それ以外の場合は、値を要求される間隔に設定します。

```csharp
uint minReportInterval = _gyrometer.MinimumReportInterval;
uint reportInterval = minReportInterval > 16 ? minReportInterval : 16;
_gyrometer.ReportInterval = reportInterval;
```

**ReadingChanged** メソッドで、新しいジャイロメーター データをキャプチャしています。 センサーのドライバーは、センサーから新しいデータを受け取るたびに、このイベント ハンドラーを使ってアプリに値を渡します。 このアプリの場合、このイベント ハンドラーが次の行で登録されています。

```csharp
_gyrometer.ReadingChanged += new TypedEventHandler<Gyrometer,
GyrometerReadingChangedEventArgs>(ReadingChanged);
```

プロジェクトの XAML 内にある TextBlock に、これらの新しい値が書き込まれます。

```xml
        <TextBlock HorizontalAlignment="Left" Height="23" Margin="8,8,0,0" TextWrapping="Wrap" Text="X-Axis:" VerticalAlignment="Top" Width="46" Foreground="#FFFDFDFD"/>
        <TextBlock x:Name="txtXAxis" HorizontalAlignment="Left" Height="23" Margin="67,8,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="88" Foreground="#FFFDFAFA"/>
        <TextBlock HorizontalAlignment="Left" Height="20" Margin="8,52,0,0" TextWrapping="Wrap" Text="Y Axis:" VerticalAlignment="Top" Width="46" Foreground="White"/>
        <TextBlock x:Name="txtYAxis" HorizontalAlignment="Left" Height="24" Margin="54,48,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="80" Foreground="#FFFBFBFB"/>
        <TextBlock HorizontalAlignment="Left" Height="21" Margin="8,93,0,0" TextWrapping="Wrap" Text="Z Axis:" VerticalAlignment="Top" Width="46" Foreground="#FFFEFBFB"/>
        <TextBlock x:Name="txtZAxis" HorizontalAlignment="Left" Height="21" Margin="54,93,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="63" Foreground="#FFF8F3F3"/>
```

 ## <a name="related-topics"></a>関連トピック

* [ジャイロメーター センサーのサンプルに関するページ](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Windows%208%20app%20samples/%5BC%23%5D-Windows%208%20app%20samples/C%23/Windows%208%20app%20samples/Gyrometer%20sensor%20sample%20(Windows%208))