---
title: ジオフェンスのセットアップ
description: アプリでジオフェンスをセットアップし、フォアグラウンドとバックグラウンドで通知を処理する方法について説明します。
ms.assetid: A3A46E03-0751-4DBD-A2A1-2323DB09BDBA
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, 地図, 位置情報, ジオフェンス, 通知
ms.localizationpriority: medium
ms.openlocfilehash: b0f16b72e8dedd45a572562308d968d528393f70
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66371582"
---
# <a name="set-up-a-geofence"></a>ジオフェンスのセットアップ




アプリで[**ジオフェンス**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geofencing.Geofence)をセットアップし、フォアグラウンドとバックグラウンドで通知を処理する方法について説明します。

**ヒント** アプリで位置情報にアクセスする方法について詳しくは、GitHub の [Windows-universal-samples リポジトリ](https://go.microsoft.com/fwlink/p/?LinkId=619979)から次のサンプルをダウンロードしてください。

-   [ユニバーサル Windows プラットフォーム (UWP) の地図のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=619977)

## <a name="enable-the-location-capability"></a>位置情報機能を有効にする


1.  **ソリューション エクスプローラー**で、**package.appxmanifest** をダブルクリックし、 **[機能]** タブを選びます。
2.  **[機能]** ボックスの一覧で、 **[位置情報]** をオンにします。 これにより、`Location` デバイス機能がパッケージ マニフェスト ファイルに追加されます。

```xml
  <Capabilities>
    <!-- DeviceCapability elements must follow Capability elements (if present) -->
    <DeviceCapability Name="location"/>
  </Capabilities>
```

## <a name="set-up-a-geofence"></a>ジオフェンスのセットアップ


### <a name="step-1-request-access-to-the-users-location"></a>手順 1:ユーザーの場所へのアクセスを要求します。

**重要:** ユーザーの位置情報にアクセスする前に、[**RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geolocator.requestaccessasync) メソッドを使って、ユーザーに位置情報へのアクセス許可を求める必要があります。 **RequestAccessAsync** メソッドは UI スレッドから呼び出す必要があり、アプリがフォアグラウンドで実行されている必要があります。 アプリがユーザーの位置情報にアクセスするには、先にユーザーがその情報へのアクセス許可をアプリに与える必要があります。

```csharp
using Windows.Devices.Geolocation;
...
var accessStatus = await Geolocator.RequestAccessAsync();
```

[  **RequestAccessAsync**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geolocator.requestaccessasync) メソッドを使って、ユーザーに位置情報へのアクセス許可を求めます。 ユーザーに対するこの要求はアプリごとに 1 回だけ行われます。 アクセス許可の付与または拒否を行った後、このメソッドはユーザーにアクセス許可を求めなくなります。 ユーザーが位置情報へのアクセス許可を求められた後にそのアクセス許可を変更できるように、位置情報の設定へのリンクを用意することをお勧めします。これについては、このトピックの後半で紹介します。

### <a name="step-2-register-for-changes-in-geofence-state-and-location-permissions"></a>手順 2:ジオフェンスの状態と位置のアクセス許可の変更の登録します。

この例では、**switch** ステートメントを (前の例で示した) **accessStatus** と共に使って、ユーザーの位置情報へのアクセス許可が与えられている場合にのみ動作するように指定します。 ユーザーの位置情報へのアクセスが許可された場合、コードによって現在のジオフェンスにアクセスされ、ジオフェンスの状態変更が登録されます。また、位置情報のアクセス許可の変更も登録されます。

**ヒント** ジオフェンスを使うときは、Geolocator クラスの StatusChanged イベントではなく、GeofenceMonitor の [**StatusChanged**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofencemonitor.statuschanged) イベントを使って、位置情報のアクセス許可の変更を監視します。 **Disabled** の [**GeofenceMonitorStatus**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geofencing.GeofenceMonitorStatus) は、無効になった [**PositionStatus**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.PositionStatus) と同じです。どちらも、ユーザーの位置情報にアクセスするためのアクセス許可がアプリにないことを示します。

```csharp
switch (accessStatus)
{
    case GeolocationAccessStatus.Allowed:
        geofences = GeofenceMonitor.Current.Geofences;

        FillRegisteredGeofenceListBoxWithExistingGeofences();
        FillEventListBoxWithExistingEvents();

        // Register for state change events.
        GeofenceMonitor.Current.GeofenceStateChanged += OnGeofenceStateChanged;
        GeofenceMonitor.Current.StatusChanged += OnGeofenceStatusChanged;
        break;


    case GeolocationAccessStatus.Denied:
        _rootPage.NotifyUser("Access denied.", NotifyType.ErrorMessage);
        break;

    case GeolocationAccessStatus.Unspecified:
        _rootPage.NotifyUser("Unspecified error.", NotifyType.ErrorMessage);
        break;
}
```

次に、フォアグラウンド アプリから移動するときに、イベント リスナーの登録を解除します。

```csharp
protected override void OnNavigatingFrom(NavigatingCancelEventArgs e)
{
    GeofenceMonitor.Current.GeofenceStateChanged -= OnGeofenceStateChanged;
    GeofenceMonitor.Current.StatusChanged -= OnGeofenceStatusChanged;

    base.OnNavigatingFrom(e);
}
```

### <a name="step-3-create-the-geofence"></a>手順 3:ジオフェンスを作成します。

これで、[**Geofence**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geofencing.Geofence) オブジェクトを定義してセットアップする準備ができました。 必要に応じて、複数の異なるコンストラクター オーバーロードから選べます。 最も基本的なジオフェンスのコンストラクターで、次に示すように [**Id**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.id) と [**Geoshape**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.geoshape) のみを指定します。

```csharp
// Set the fence ID.
string fenceId = "fence1";

// Define the fence location and radius.
BasicGeoposition position;
position.Latitude = 47.6510;
position.Longitude = -122.3473;
position.Altitude = 0.0;
double radius = 10; // in meters

// Set a circular region for the geofence.
Geocircle geocircle = new Geocircle(position, radius);

// Create the geofence.
Geofence geofence = new Geofence(fenceId, geocircle);

```

他のコンストラクターのいずれかを使用して、ジオフェンスをさらに微調整できます。 次の例では、ジオフェンスのコンストラクターで次の追加のパラメーターを指定します。

-   [**MonitoredStates** ](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.monitoredstates) -定義済みの領域、または、ジオフェンスの削除を離れること、定義済みの領域を入力するための通知を受信するジオフェンス イベントを示します。
-   [**SingleUse** ](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.singleuse) -ジオフェンスが監視されているすべての状態を満たしていると、ジオフェンスが削除されます。
-   [**DwellTime** ](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.dwelltime) -どれくらいの時間、ユーザーがあります、定義済みの領域の内外で enter/終了イベントが発生する前にことを示します。
-   [**StartTime** ](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.starttime) -、ジオフェンスの監視を開始する日時を示します。
-   [**期間**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.duration) -、ジオフェンスを監視する期間を示します。

```csharp
// Set the fence ID.
string fenceId = "fence2";

// Define the fence location and radius.
BasicGeoposition position;
position.Latitude = 47.6510;
position.Longitude = -122.3473;
position.Altitude = 0.0;
double radius = 10; // in meters

// Set the circular region for geofence.
Geocircle geocircle = new Geocircle(position, radius);

// Remove the geofence after the first trigger.
bool singleUse = true;

// Set the monitored states.
MonitoredGeofenceStates monitoredStates =
                MonitoredGeofenceStates.Entered |
                MonitoredGeofenceStates.Exited |
                MonitoredGeofenceStates.Removed;

// Set how long you need to be in geofence for the enter event to fire.
TimeSpan dwellTime = TimeSpan.FromMinutes(5);

// Set how long the geofence should be active.
TimeSpan duration = TimeSpan.FromDays(1);

// Set up the start time of the geofence.
DateTimeOffset startTime = DateTime.Now;

// Create the geofence.
Geofence geofence = new Geofence(fenceId, geocircle, monitoredStates, singleUse, dwellTime, startTime, duration);
```

作成後、新しい [**Geofence**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geofencing.Geofence) を忘れずにモニターに登録してください。

```csharp
// Register the geofence
try {
   GeofenceMonitor.Current.Geofences.Add(geofence);
} catch {
   // Handle failure to add geofence
}
```

### <a name="step-4-handle-changes-in-location-permissions"></a>手順 4:場所のアクセス許可の変更を処理します。

[  **GeofenceMonitor**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geofencing.GeofenceMonitor) オブジェクトは [**StatusChanged**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofencemonitor.statuschanged) イベントをトリガーして、ユーザーの位置情報設定が変化したことを示します。 このイベントは、引数の **sender.Status** プロパティ ([**GeofenceMonitorStatus**](https://docs.microsoft.com/uwp/api/Windows.Devices.Geolocation.Geofencing.GeofenceMonitorStatus) 型) を使って、対応する状態を渡します。 このメソッドは UI スレッドから呼び出されず、[**Dispatcher**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreDispatcher) オブジェクトが UI の変更を呼び出します。

```csharp
using Windows.UI.Core;
...
public async void OnGeofenceStatusChanged(GeofenceMonitor sender, object e)
{
   await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
   {
    // Show the location setting message only if the status is disabled.
    LocationDisabledMessage.Visibility = Visibility.Collapsed;

    switch (sender.Status)
    {
     case GeofenceMonitorStatus.Ready:
      _rootPage.NotifyUser("The monitor is ready and active.", NotifyType.StatusMessage);
      break;

     case GeofenceMonitorStatus.Initializing:
      _rootPage.NotifyUser("The monitor is in the process of initializing.", NotifyType.StatusMessage);
      break;

     case GeofenceMonitorStatus.NoData:
      _rootPage.NotifyUser("There is no data on the status of the monitor.", NotifyType.ErrorMessage);
      break;

     case GeofenceMonitorStatus.Disabled:
      _rootPage.NotifyUser("Access to location is denied.", NotifyType.ErrorMessage);

      // Show the message to the user to go to the location settings.
      LocationDisabledMessage.Visibility = Visibility.Visible;
      break;

     case GeofenceMonitorStatus.NotInitialized:
      _rootPage.NotifyUser("The geofence monitor has not been initialized.", NotifyType.StatusMessage);
      break;

     case GeofenceMonitorStatus.NotAvailable:
      _rootPage.NotifyUser("The geofence monitor is not available.", NotifyType.ErrorMessage);
      break;

     default:
      ScenarioOutput_Status.Text = "Unknown";
      _rootPage.NotifyUser(string.Empty, NotifyType.StatusMessage);
      break;
    }
   });
}
```

## <a name="set-up-foreground-notifications"></a>フォアグラウンド通知のセットアップ


ジオフェンスを作成した後で、ジオフェンス イベントが発生したときの処理ロジックを追加する必要があります。 セットアップした [**MonitoredStates**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.monitoredstates) に応じて、次の場合にイベントを受け取ります。

-   ユーザーが関心領域に入った。
-   ユーザーが関心領域から離れた。
-   ジオフェンスが期限切れになったか、除去された。 除去イベントではバックグラウンド アプリがアクティブ化されないことに注意してください。

実行中のアプリからイベントを直接リッスンすることも、バックグラウンド タスクの登録を行い、イベントが発生するとバックグラウンド通知を受け取ることもできます。

### <a name="step-1-register-for-geofence-state-change-events"></a>手順 1:ジオフェンスの状態変更イベントを登録します。

アプリでジオフェンスの状態変更についてフォアグラウンド通知を受け取るには、イベント ハンドラーを登録する必要があります。 これは一般にジオフェンスの作成時にセットアップします。

```csharp
private void Initialize()
{
    // Other initialization logic

    GeofenceMonitor.Current.GeofenceStateChanged += OnGeofenceStateChanged;
}

```

### <a name="step-2-implement-the-geofence-event-handler"></a>手順 2:ジオフェンス イベント ハンドラーを実装します。

次の手順は、イベント ハンドラーの実装です。 ここで実行するアクションは、ジオフェンスの利用目的に応じて変わります。

```csharp
public async void OnGeofenceStateChanged(GeofenceMonitor sender, object e)
{
    var reports = sender.ReadReports();

    await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
    {
        foreach (GeofenceStateChangeReport report in reports)
        {
            GeofenceState state = report.NewState;

            Geofence geofence = report.Geofence;

            if (state == GeofenceState.Removed)
            {
                // Remove the geofence from the geofences collection.
                GeofenceMonitor.Current.Geofences.Remove(geofence);
            }
            else if (state == GeofenceState.Entered)
            {
                // Your app takes action based on the entered event.

                // NOTE: You might want to write your app to take a particular
                // action based on whether the app has internet connectivity.

            }
            else if (state == GeofenceState.Exited)
            {
                // Your app takes action based on the exited event.

                // NOTE: You might want to write your app to take a particular
                // action based on whether the app has internet connectivity.

            }
        }
    });
}



```

## <a name="set-up-background-notifications"></a>バックグラウンド通知のセットアップ


ジオフェンスを作成した後で、ジオフェンス イベントが発生したときの処理ロジックを追加する必要があります。 セットアップした [**MonitoredStates**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.monitoredstates) に応じて、次の場合にイベントを受け取ります。

-   ユーザーが関心領域に入った。
-   ユーザーが関心領域から離れた。
-   ジオフェンスが期限切れになったか、除去された。 除去イベントではバックグラウンド アプリがアクティブ化されないことに注意してください。

バックグラウンドでのジオフェンス イベントをリッスンするには

-   アプリのマニフェストでバックグラウンド タスクを宣言します。
-   アプリでバックグラウンド タスクを登録します。 クラウド サービスへのアクセスなど、インターネット アクセスがアプリに必要な場合は、イベントがトリガーされたときにそのためのフラグを設定できます。 イベントがトリガーされたときにユーザーがその場にいて、ユーザーに通知が確実に届くようにするために、フラグを設定することもできます。
-   アプリをフォアグラウンドで実行中に、位置情報のアクセス許可をアプリに与えるようユーザーに求めます。

### <a name="step-1-register-for-geofence-state-change-events"></a>手順 1:ジオフェンスの状態変更イベントを登録します。

アプリのマニフェストの **[宣言]** タブで、位置情報バックグラウンド タスクの宣言を追加します。 これには、次の手順を実行します。

-   タイプが **[バックグラウンド タスク]** の宣言を追加します。
-   プロパティのタスク タイプを **[位置情報]** に設定します。
-   イベントがトリガーされたときに呼び出すアプリのエントリ ポイントを設定します。

### <a name="step-2-register-the-background-task"></a>手順 2:バックグラウンド タスクの登録

この手順のコードでは、ジオフェンス バックグラウンド タスクを登録しています。 ジオフェンスを作成したときに、位置情報のアクセス許可を確認しました。

```csharp
async private void RegisterBackgroundTask(object sender, RoutedEventArgs e)
{
    // Get permission for a background task from the user. If the user has already answered once,
    // this does nothing and the user must manually update their preference via PC Settings.
    BackgroundAccessStatus backgroundAccessStatus = await BackgroundExecutionManager.RequestAccessAsync();

    // Regardless of the answer, register the background task. Note that the user can use
    // the Settings app to prevent your app from running background tasks.
    // Create a new background task builder.
    BackgroundTaskBuilder geofenceTaskBuilder = new BackgroundTaskBuilder();

    geofenceTaskBuilder.Name = SampleBackgroundTaskName;
    geofenceTaskBuilder.TaskEntryPoint = SampleBackgroundTaskEntryPoint;

    // Create a new location trigger.
    var trigger = new LocationTrigger(LocationTriggerType.Geofence);

    // Associate the location trigger with the background task builder.
    geofenceTaskBuilder.SetTrigger(trigger);

    // If it is important that there is user presence and/or
    // internet connection when OnCompleted is called
    // the following could be called before calling Register().
    // SystemCondition condition = new SystemCondition(SystemConditionType.UserPresent | SystemConditionType.InternetAvailable);
    // geofenceTaskBuilder.AddCondition(condition);

    // Register the background task.
    geofenceTask = geofenceTaskBuilder.Register();

    // Associate an event handler with the new background task.
    geofenceTask.Completed += new BackgroundTaskCompletedEventHandler(OnCompleted);

    BackgroundTaskState.RegisterBackgroundTask(BackgroundTaskState.LocationTriggerBackgroundTaskName);

    switch (backgroundAccessStatus)
    {
    case BackgroundAccessStatus.Unspecified:
    case BackgroundAccessStatus.Denied:
        rootPage.NotifyUser("This app is not allowed to run in the background.", NotifyType.ErrorMessage);
        break;

    }
}


```

### <a name="step-3-handling-the-background-notification"></a>手順 3:通知のバック グラウンド処理

ユーザーに通知するためにとるアクションは、アプリの用途に応じて変わりますが、トースト通知の表示、サウンドの再生、ライブ タイルの更新などが考えられます。 この手順のコードは通知を処理します。

```csharp
async private void OnCompleted(IBackgroundTaskRegistration sender, BackgroundTaskCompletedEventArgs e)
{
    if (sender != null)
    {
        // Update the UI with progress reported by the background task.
        await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            try
            {
                // If the background task threw an exception, display the exception in
                // the error text box.
                e.CheckResult();

                // Update the UI with the completion status of the background task.
                // The Run method of the background task sets the LocalSettings.
                var settings = ApplicationData.Current.LocalSettings;

                // Get the status.
                if (settings.Values.ContainsKey("Status"))
                {
                    rootPage.NotifyUser(settings.Values["Status"].ToString(), NotifyType.StatusMessage);
                }

                // Do your app work here.

            }
            catch (Exception ex)
            {
                // The background task had an error.
                rootPage.NotifyUser(ex.ToString(), NotifyType.ErrorMessage);
            }
        });
    }
}


```

## <a name="change-the-privacy-settings"></a>プライバシー設定の変更


位置情報のプライバシー設定でアプリにユーザーの位置情報へのアクセス許可を与えていない場合は、**設定**アプリの **[位置情報のプライバシー設定]** へのリンクを用意することをお勧めします。 この例では、ハイパーリンク コントロールを使って、`ms-settings:privacy-location` という URI に移動します。

```xml
<!--Set Visibility to Visible when access to the user's location is denied. -->  
<TextBlock x:Name="LocationDisabledMessage" FontStyle="Italic"
                 Visibility="Collapsed" Margin="0,15,0,0" TextWrapping="Wrap" >
          <Run Text="This app is not able to access Location. Go to " />
              <Hyperlink NavigateUri="ms-settings:privacy-location">
                  <Run Text="Settings" />
              </Hyperlink>
          <Run Text=" to check the location privacy settings."/>
</TextBlock>
```

また、アプリで [**LaunchUriAsync**](https://docs.microsoft.com/uwp/api/windows.system.launcher.launchuriasync) メソッドを呼び出し、コードで**設定**アプリを起動することもできます。 詳しくは、「[Windows 設定アプリの起動](https://docs.microsoft.com/windows/uwp/launch-resume/launch-settings-app)」をご覧ください。

```csharp
using Windows.System;
...
bool result = await Launcher.LaunchUriAsync(new Uri("ms-settings:privacy-location"));
```

## <a name="test-and-debug-your-app"></a>アプリのテストとデバッグ


ジオフェンス アプリはデバイスの位置に依存しているため、そのテストとデバッグは容易ではありません。 ここでは、フォアグラウンドとバックグラウンドのジオフェンスの両方をテストするいくつかの方法について概略を示します。

**Geofencing 機能アプリをデバッグするには**

1.  デバイスを新しい位置に物理的に移動します。
2.  現在の物理的な位置を含むジオフェンス領域を作成して、ジオフェンスへの進入をテストします。ジオフェンスの内部に既にいるため、"ジオフェンス進入" イベントが直ちにトリガーされます。
3.  Microsoft Visual Studio エミュレーターを使って、デバイスの位置をシミュレートします。

### <a name="test-and-debug-a-geofencing-app-that-is-running-in-the-foreground"></a>フォアグラウンドで実行中のジオフェンス アプリのテストとデバッグ

**前景色を実行している geofencing 機能アプリをテストするには**

1.  Visual Studio でアプリをビルドします。
2.  Visual Studio エミュレーターでアプリを起動します。
3.  これらのツールを使って、ジオフェンス領域の内外のさまざまな位置をシミュレートします。 [  **DwellTime**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.dwelltime) プロパティで指定した時間が経過してイベントがトリガーされるまで、十分な時間、待ってください。 アプリに位置情報のアクセス許可を与えるというメッセージに同意する必要があります。 位置のシミュレーションについて詳しくは、「シミュレーターでの Windows ストア アプリの実行」の「[デバイスのシミュレートされる地理上の位置を設定する](https://go.microsoft.com/fwlink/p/?LinkID=325245)」をご覧ください。
4.  また、さまざまな速度での検出に必要なおおよそのジオフェンスのサイズとドウェル時間を見積もるためにエミュレーターを使うこともできます。

### <a name="test-and-debug-a-geofencing-app-that-is-running-in-the-background"></a>バックグラウンドで実行中のジオフェンス アプリのテストとデバッグ

**バック グラウンドを実行している geofencing 機能アプリをテストするには**

1.  Visual Studio でアプリをビルドします。 アプリでバックグラウンド タスクの種類を **Location** に設定する必要があります。
2.  最初に、アプリをローカルに展開します。
3.  ローカルで実行中のアプリを閉じます。
4.  Visual Studio エミュレーターでアプリを起動します。 バックグラウンドのジオフェンス シミュレーションは、エミュレーター内では一度に 1 つのアプリでしかサポートされていません。 エミュレーター内で複数のジオフェンス アプリを起動しないでください。
5.  エミュレーターから、ジオフェンス領域の内外のさまざまな位置をシミュレートします。 [  **DwellTime**](https://docs.microsoft.com/uwp/api/windows.devices.geolocation.geofencing.geofence.dwelltime) の時間が経過してイベントがトリガーされるまで、十分な時間、待ってください。 アプリに位置情報のアクセス許可を与えるというメッセージに同意する必要があります。
6.  Visual Studio を使って、位置情報バックグラウンド タスクをトリガーします。 Visual Studio でのバックグラウンド タスクのトリガーについて詳しくは、「[Visual Studio で Windows ストア アプリの中断イベント、再開イベント、およびバックグラウンド イベントをトリガーする方法](https://go.microsoft.com/fwlink/p/?LinkID=325378)」をご覧ください。

## <a name="troubleshoot-your-app"></a>アプリのトラブルシューティング


アプリが位置情報にアクセスする前に、デバイスで **[位置情報]** を有効にする必要があります。 **設定**アプリで、次の**位置情報に関するプライバシー設定**がオンになっていることを確認します。

-   **このデバイスの場所.** なって**で**(Windows 10 Mobile には適用されません)
-   位置情報サービス設定の **[位置情報]** が **オン** になっている
-   **[位置情報を使うことができるアプリを選ぶ]** で、アプリが **オン** になっている

## <a name="related-topics"></a>関連トピック

* [UWP の位置情報のサンプル](https://go.microsoft.com/fwlink/p/?linkid=533278)
* [Geofencing 機能の設計ガイドライン](https://docs.microsoft.com/windows/uwp/maps-and-location/guidelines-for-geofencing)
* [位置認識アプリの設計ガイドライン](https://docs.microsoft.com/windows/uwp/maps-and-location/guidelines-and-checklist-for-detecting-location)
