---
ms.assetid: 90BB59FC-90FE-453E-A8DE-9315E29EB98C
title: バッテリー情報の取得
description: Windows.Devices.Power 名前空間で、API を使って詳細なバッテリー情報を取得する方法について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 383cb37e044e7e13080526d8e8270e7fc36560ff
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89172236"
---
# <a name="get-battery-information"></a>バッテリー情報の取得


** 重要な API **

-   [**Windows.Devices.Power**](/uwp/api/Windows.Devices.Power)
-   [**DeviceInformation.FindAllAsync**](/uwp/api/windows.devices.enumeration.deviceinformation.findallasync)

[**Windows.Devices.Power**](/uwp/api/Windows.Devices.Power) 名前空間で、API を使って詳細なバッテリー情報を取得する方法について説明します。 *バッテリー レポート* ([**BatteryReport**](/uwp/api/Windows.Devices.Power.BatteryReport)) は、バッテリーの充電量、容量、状態や、バッテリーの集計を示します。 このトピックでは、アプリでバッテリー レポートを取得したり、変更に関する通知を受け取ったりする方法を紹介します。 コード例は基本的なバッテリー アプリからの抜粋で、このトピックの末尾の一覧で確認できます。

## <a name="get-aggregate-battery-report"></a>バッテリー集計レポートの取得


一部のデバイスにはバッテリーが複数あり、各バッテリーがデバイスの消費エネルギー全体にどのように関与しているのか明確でない場合があります。 [**AggregateBattery**](/uwp/api/windows.devices.power.battery.aggregatebattery) クラスはまさにそのような用途に使います。 *バッテリー集計*レポートはデバイスに接続されたすべてのバッテリー コントローラーを表し、1 つの全体的な [**BatteryReport**](/uwp/api/Windows.Devices.Power.BatteryReport) オブジェクトを提供できます。

**メモ**   [**バッテリ**](/uwp/api/Windows.Devices.Power.Battery)クラスは、実際にはバッテリコントローラーに対応しています。 デバイスに応じて、コントローラーは物理的なバッテリーに接続されることもあれば、デバイス エンクロージャに接続されることもあります。 そのため、バッテリーがなくても、バッテリ オブジェクトを作ることができます。 また、バッテリ オブジェクトは **null** にすることもできます。

集計バッテリー オブジェクトを指定したら、[**GetReport**](/uwp/api/windows.devices.power.battery.getreport) を呼び出して、対応する [**BatteryReport**](/uwp/api/Windows.Devices.Power.BatteryReport) を取得します。

```csharp
private void RequestAggregateBatteryReport()
{
    // Create aggregate battery object
    var aggBattery = Battery.AggregateBattery;

    // Get report
    var report = aggBattery.GetReport();

    // Update UI
    AddReportUI(BatteryReportPanel, report, aggBattery.DeviceId);
}
```

## <a name="get-individual-battery-reports"></a>個々のバッテリー レポートを取得する

個々のバッテリーに対する [**BatteryReport**](/uwp/api/Windows.Devices.Power.BatteryReport) オブジェクトを作ることもできます。 [**GetDeviceSelector**](/uwp/api/windows.devices.power.battery.getdeviceselector) を [**FindAllAsync**](/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) メソッドと共に使って、デバイスに接続されているバッテリー コントローラーがあるかどうかを表す [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトのコレクションを取得します。 次に、必要な **DeviceInformation** オブジェクトの **Id** プロパティを使って、[**FromIdAsync**](/uwp/api/windows.devices.power.battery.fromidasync) メソッドを使い、対応する [**Battery**](/uwp/api/Windows.Devices.Power.Battery) を作ります。 最後に、[**GetReport**](/uwp/api/windows.devices.power.battery.getreport) を呼び出して、各バッテリー レポートを取得します。

次の例は、デバイスに接続されているすべてのバッテリーのバッテリー レポートを作る方法を示しています。

```csharp
async private void RequestIndividualBatteryReports()
{
    // Find batteries 
    var deviceInfo = await DeviceInformation.FindAllAsync(Battery.GetDeviceSelector());
    foreach(DeviceInformation device in deviceInfo)
    {
        try
        {
        // Create battery object
        var battery = await Battery.FromIdAsync(device.Id);

        // Get report
        var report = battery.GetReport();

        // Update UI
        AddReportUI(BatteryReportPanel, report, battery.DeviceId);
        }
        catch { /* Add error handling, as applicable */ }
    }
}
```

## <a name="access-report-details"></a>レポートの詳細にアクセスする

[**BatteryReport**](/uwp/api/Windows.Devices.Power.BatteryReport) オブジェクトは、多くのバッテリー情報を提供します。 詳しくは、次のプロパティの API リファレンスをご覧ください。**Status** ([**BatteryStatus**](/previous-versions/windows/dn818458(v=win.10)) 列挙体)、[**ChargeRateInMilliwatts**](/uwp/api/windows.devices.power.batteryreport.chargerateinmilliwatts)、[**DesignCapacityInMilliwattHours**](/uwp/api/windows.devices.power.batteryreport.designcapacityinmilliwatthours)、[**FullChargeCapacityInMilliwattHours**](/uwp/api/windows.devices.power.batteryreport.fullchargecapacityinmilliwatthours)、および [**RemainingCapacityInMilliwattHours**](/uwp/api/windows.devices.power.batteryreport.remainingcapacityinmilliwatthours)。 次の例は、基本的なバッテリー アプリで使用される一部のバッテリー レポート プロパティを示しています。このプロパティについては、このトピックで後ほど説明します。

```csharp
...
TextBlock txt3 = new TextBlock { Text = "Charge rate (mW): " + report.ChargeRateInMilliwatts.ToString() };
TextBlock txt4 = new TextBlock { Text = "Design energy capacity (mWh): " + report.DesignCapacityInMilliwattHours.ToString() };
TextBlock txt5 = new TextBlock { Text = "Fully-charged energy capacity (mWh): " + report.FullChargeCapacityInMilliwattHours.ToString() };
TextBlock txt6 = new TextBlock { Text = "Remaining energy capacity (mWh): " + report.RemainingCapacityInMilliwattHours.ToString() };
...
...
```

## <a name="request-report-updates"></a>レポートの更新を要求する

[**Battery**](/uwp/api/Windows.Devices.Power.Battery) オブジェクトは、バッテリーの充電量、容量、状態が変わると [**ReportUpdated**](/uwp/api/windows.devices.power.battery.reportupdated) イベントをトリガーします。 通常、これは、ステータスの変更についてはすぐに、その他のすべての変更については定期的に発生します。 次の例は、バッテリー レポートの更新に登録する方法を示しています。

```csharp
...
Battery.AggregateBattery.ReportUpdated += AggregateBattery_ReportUpdated;
...
```

## <a name="handle-report-updates"></a>レポートの更新を処理する

バッテリーの更新が発生すると、[**ReportUpdated**](/uwp/api/windows.devices.power.battery.reportupdated) イベントは対応する [**Battery**](/uwp/api/Windows.Devices.Power.Battery) オブジェクトをイベント ハンドラー メソッドに渡します。 ただし、このイベント ハンドラーは、UI スレッドから呼び出されません。 次の例で示すように、[**Dispatcher**](/uwp/api/Windows.UI.Core.CoreDispatcher) オブジェクトを使って任意の UI の変更を呼び出す必要があります。

```csharp
async private void AggregateBattery_ReportUpdated(Battery sender, object args)
{
    if (reportRequested)
    {

        await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            // Clear UI
            BatteryReportPanel.Children.Clear();


            if (AggregateButton.IsChecked == true)
            {
                // Request aggregate battery report
                RequestAggregateBatteryReport();
            }
            else
            {
                // Request individual battery report
                RequestIndividualBatteryReports();
            }
        });
    }
}
```

## <a name="example-basic-battery-app"></a>例: 基本的なバッテリー アプリ

Microsoft Visual Studio で次の基本的なバッテリー アプリをビルドすることによって、これらの API をテストします。 Visual Studio のスタート ページで **[新しいプロジェクト]** をクリックし、**[Visual C#] &gt; [Windows] &gt; [ユニバーサル]** テンプレートで **[空のアプリケーション]** テンプレートを使って新しいアプリを作ります。

次に、**MainPage.xaml** ファイルを開き、次の XML をこのファイルにコピーします (元の内容を置き換えます)。

```xml
<Page
    x:Class="App1.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:App1"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Background="{ThemeResource ApplicationPageBackgroundThemeBrush}" >
        <StackPanel VerticalAlignment="Center" Margin="15,30,0,0" >
            <RadioButton x:Name="AggregateButton" Content="Aggregate results" GroupName="Type" IsChecked="True" />
            <RadioButton x:Name="IndividualButton" Content="Individual results" GroupName="Type" IsChecked="False" />
        </StackPanel>
        <StackPanel Orientation="Horizontal">
        <Button x:Name="GetBatteryReportButton" 
                Content="Get battery report" 
                Margin="15,15,0,0" 
                Click="GetBatteryReport"/>
        </StackPanel>
        <StackPanel x:Name="BatteryReportPanel" Margin="15,15,0,0"/>
    </StackPanel>
</Page>
```

自分のアプリの名前が **App1** ではない場合、元のスニペットのクラス名の最初の部分を、自分のアプリの名前空間に置き換える必要があります。 たとえば、作成したプロジェクトの名前が **BasicBatteryApp** だとすると、`x:Class="App1.MainPage"` を `x:Class="BasicBatteryApp.MainPage"` に置き換えます。 また、`xmlns:local="using:App1"` を `xmlns:local="using:BasicBatteryApp"` に置き換える必要があります。

次に、プロジェクトの **MainPage.xaml.cs** ファイルを開き、記載されているコードを次のコードで置き換えます。

```csharp
using System;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Media;
using Windows.Devices.Enumeration;
using Windows.Devices.Power;
using Windows.UI.Core;

namespace App1
{
    public sealed partial class MainPage : Page
    {
        bool reportRequested = false;
        public MainPage()
        {
            this.InitializeComponent();
            Battery.AggregateBattery.ReportUpdated += AggregateBattery_ReportUpdated;
        }


        private void GetBatteryReport(object sender, RoutedEventArgs e)
        {
            // Clear UI
            BatteryReportPanel.Children.Clear();


            if (AggregateButton.IsChecked == true)
            {
                // Request aggregate battery report
                RequestAggregateBatteryReport();
            }
            else
            {
                // Request individual battery report
                RequestIndividualBatteryReports();
            }

            // Note request
            reportRequested = true;
        }

        private void RequestAggregateBatteryReport()
        {
            // Create aggregate battery object
            var aggBattery = Battery.AggregateBattery;

            // Get report
            var report = aggBattery.GetReport();

            // Update UI
            AddReportUI(BatteryReportPanel, report, aggBattery.DeviceId);
        }

        async private void RequestIndividualBatteryReports()
        {
            // Find batteries 
            var deviceInfo = await DeviceInformation.FindAllAsync(Battery.GetDeviceSelector());
            foreach(DeviceInformation device in deviceInfo)
            {
                try
                {
                // Create battery object
                var battery = await Battery.FromIdAsync(device.Id);

                // Get report
                var report = battery.GetReport();

                // Update UI
                AddReportUI(BatteryReportPanel, report, battery.DeviceId);
                }
                catch { /* Add error handling, as applicable */ }
            }
        }


        private void AddReportUI(StackPanel sp, BatteryReport report, string DeviceID)
        {
            // Create battery report UI
            TextBlock txt1 = new TextBlock { Text = "Device ID: " + DeviceID };
            txt1.FontSize = 15;
            txt1.Margin = new Thickness(0, 15, 0, 0);
            txt1.TextWrapping = TextWrapping.WrapWholeWords;

            TextBlock txt2 = new TextBlock { Text = "Battery status: " + report.Status.ToString() };
            txt2.FontStyle = Windows.UI.Text.FontStyle.Italic;
            txt2.Margin = new Thickness(0, 0, 0, 15);

            TextBlock txt3 = new TextBlock { Text = "Charge rate (mW): " + report.ChargeRateInMilliwatts.ToString() };
            TextBlock txt4 = new TextBlock { Text = "Design energy capacity (mWh): " + report.DesignCapacityInMilliwattHours.ToString() };
            TextBlock txt5 = new TextBlock { Text = "Fully-charged energy capacity (mWh): " + report.FullChargeCapacityInMilliwattHours.ToString() };
            TextBlock txt6 = new TextBlock { Text = "Remaining energy capacity (mWh): " + report.RemainingCapacityInMilliwattHours.ToString() };

            // Create energy capacity progress bar & labels
            TextBlock pbLabel = new TextBlock { Text = "Percent remaining energy capacity" };
            pbLabel.Margin = new Thickness(0,10, 0, 5);
            pbLabel.FontFamily = new FontFamily("Segoe UI");
            pbLabel.FontSize = 11;

            ProgressBar pb = new ProgressBar();
            pb.Margin = new Thickness(0, 5, 0, 0);
            pb.Width = 200;
            pb.Height = 10;
            pb.IsIndeterminate = false;
            pb.HorizontalAlignment = HorizontalAlignment.Left;

            TextBlock pbPercent = new TextBlock();
            pbPercent.Margin = new Thickness(0, 5, 0, 10);
            pbPercent.FontFamily = new FontFamily("Segoe UI");
            pbLabel.FontSize = 11;

            // Disable progress bar if values are null
            if ((report.FullChargeCapacityInMilliwattHours == null)||
                (report.RemainingCapacityInMilliwattHours == null))
            {
                pb.IsEnabled = false;
                pbPercent.Text = "N/A";
            }
            else
            {
                pb.IsEnabled = true;
                pb.Maximum = Convert.ToDouble(report.FullChargeCapacityInMilliwattHours);
                pb.Value = Convert.ToDouble(report.RemainingCapacityInMilliwattHours);
                pbPercent.Text = ((pb.Value / pb.Maximum) * 100).ToString("F2") + "%";
            }

            // Add controls to stackpanel
            sp.Children.Add(txt1);
            sp.Children.Add(txt2);
            sp.Children.Add(txt3);
            sp.Children.Add(txt4);
            sp.Children.Add(txt5);
            sp.Children.Add(txt6);
            sp.Children.Add(pbLabel);
            sp.Children.Add(pb);
            sp.Children.Add(pbPercent);
        }

        async private void AggregateBattery_ReportUpdated(Battery sender, object args)
        {
            if (reportRequested)
            {

                await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
                {
                    // Clear UI
                    BatteryReportPanel.Children.Clear();


                    if (AggregateButton.IsChecked == true)
                    {
                        // Request aggregate battery report
                        RequestAggregateBatteryReport();
                    }
                    else
                    {
                        // Request individual battery report
                        RequestIndividualBatteryReports();
                    }
                });
            }
        }
    }
}
```

自分のアプリの名前が **App1** ではない場合、元のサンプルの名前空間の名前を、自分のプロジェクトに指定した名前に変更する必要があります。 たとえば、作成したプロジェクトの名前が **BasicBatteryApp** だとすると、`App1` 名前空間を `BasicBatteryApp` 名前空間に置き換えます。

最後に、この基本的なバッテリー アプリを実行します: **[デバッグ]** メニューで **[デバッグの開始]** をクリックしてソリューションをテストします。

**ヒント**   [**BatteryReport**](/uwp/api/Windows.Devices.Power.BatteryReport)オブジェクトから数値を受け取るには、**ローカルコンピューター**または外部**デバイス**(Windows Phone など) でアプリをデバッグします。 デバイス エミュレーターでデバッグした場合、**BatteryReport** オブジェクトは容量や消費率のプロパティに **null** を返します。

 