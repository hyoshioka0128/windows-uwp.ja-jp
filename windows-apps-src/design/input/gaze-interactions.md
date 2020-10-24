---
title: 視線の操作
Description: Windows アプリを設計および最適化して、視線とヘッドのトラッカーからの入力を見つめているユーザーに最適なエクスペリエンスを提供する方法について説明します。
label: Gaze interactions
template: detail.hbs
keywords: 視線, 視線追跡, 頭の追跡, 視線ポイント, 入力, ユーザーの操作, アクセシビリティ, ユーザビリティ
ms.date: 09/24/2020
ms.topic: article
pm-contact: Jake Cohen
dev-contact: Austin Hodges
doc-status: Draft
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: fa08cb65afc46069e48263344270e1e3b1a3d5f5
ms.sourcegitcommit: eda7bbe9caa9d61126e11f0f1a98b12183df794d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91217025"
---
# <a name="gaze-interactions-and-eye-tracking-in-windows-apps"></a>Windows アプリでの対話と視線の追跡

![視線追跡ヒーロー](images/gaze/eyecontrolbanner1.png)

ユーザーの視線、注意、および場所とユーザーの目の動きに基づくプレゼンスを追跡するためのサポートを提供します。

> [!NOTE]
> [Windows Mixed Reality](/windows/mixed-reality/) での視線入力については、「[視線](/windows/mixed-reality/gaze)」を参照してください。

**重要な API**: [Windows.Devices.Input.Preview](/uwp/api/windows.devices.input.preview)、[GazeDevicePreview](/uwp/api/windows.devices.input.preview.gazedevicepreview)、[GazePointPreview](/uwp/api/windows.devices.input.preview.gazepointpreview)、[GazeInputSourcePreview](/uwp/api/windows.devices.input.preview.gazeinputsourcepreview)

## <a name="overview"></a>概要

Neuro を使用すると、Windows アプリケーションを操作して使用するための強力な手段となります。これは特に、muscular 病名 (ALS など) や、障害のある筋肉またはの機能を伴う他の障碍を持つユーザーのための補助技術として役に立ちます。

さらに、視線入力は、ゲーム (ターゲット把握や追跡を含む) や従来の生産性向上アプリケーション、キオスクだけでなく、従来の入力デバイス (キーボード、マウス、タッチ) が使用できないか、ユーザーの両手を他のタスク (買い袋を持つなど) のために開放することが便利である可能性のあるその他の対話型シナリオで、同様に魅力的な機会をもたらします。

> [!NOTE]
> 視線追跡ハードウェアのサポートは、**Windows 10 Fall Creators Update** で[視線制御](https://support.microsoft.com/help/4043921/windows-10-get-started-eye-control)と共に導入されました。視線制御は、ユーザーが目を使用して画面上のポインターを制御し、スクリーン キーボードで入力し、音声合成を使用して人々とやり取りすることができる組み込み機能です。 視線追跡ハードウェアと対話できるアプリケーションを構築するための一連の Windows ランタイム Api ([windows](/uwp/api/windows.devices.input.preview)) は、 **Windows 10 April 2018 Update (バージョン1803、ビルド 17134)** 以降で使用できます。

## <a name="privacy"></a>プライバシー

視線追跡デバイスによって収集された機密性の高い個人データにより、 `gazeInput` アプリケーションのアプリマニフェストで機能を宣言する必要があります (次の **セットアップ** セクションを参照してください)。 宣言すると、アプリが最初に実行されたときに Windows によって自動的にユーザーに同意ダイアログ ボックスが表示されます。ここでは、ユーザーはアプリが視線追跡デバイスと通信して、このデータにアクセスできるようにアクセス許可を付与する必要があります。

さらに、アプリが視線追跡データを収集、保存、転送する場合は、アプリのプライバシーに関する声明でこれを宣言し、[Microsoft Store ポリシー](/legal/windows/agreements/store-policies)と[アプリ開発者契約](/legal/windows/agreements/app-developer-agreement)の**個人情報**のその他すべての要件に従う必要があります。

## <a name="setup"></a>セットアップ

Windows アプリで宝石入力 Api を使用するには、次のことを行う必要があります。 

- アプリ マニフェストで `gazeInput` 機能を指定します。

    Visual Studio マニフェスト デザイナーで **Package.appxmanifest** ファイルを開くか、または手動で **[コードの表示]** を選択し、次の `DeviceCapability` を `Capabilities` ノードに挿入することで機能を追加します。

    ```xaml
    <Capabilities>
       <DeviceCapability Name="gazeInput" />
    </Capabilities>
    ```

- Windows と互換性のある視線追跡デバイスがシステム (組み込みまたは外付け) に接続され、オンになりました。

    サポートされる視線追跡デバイスの一覧については、「[Windows 10 の視線制御の概要](https://support.microsoft.com/help/4043921/windows-10-get-started-eye-control#supported-devices )」を参照してください。

## <a name="basic-eye-tracking"></a>基本的な視線追跡

この例では、Windows アプリ内でユーザーの宝石を追跡し、タイミング関数と基本的なヒットテストを使用して、特定の要素に対してどの程度のフォーカスを維持できるかを示す方法を示します。

小さな楕円を使用して視線のポイントがアプリケーションのビューポート内のどこにあるかを示しますが、[Windows コミュニティ ツールキット](/windows/communitytoolkit/)の [RadialProgressBar](/windows/communitytoolkit/controls/radialprogressbar) はキャンバス上でランダムに配置されます。 進行状況バーで注視フォーカスが検出されると、タイマーが開始し、進行状況バーが 100% に達したときに、キャンバスで、進行状況バーがランダムに移動します。

![タイマーのサンプルを使用した視線追跡](images/gaze/gaze-input-timed2.gif)

*タイマーのサンプルを使用した視線追跡*

**このサンプルは、 [「宝石入力のサンプル (基本)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-gazeinput-basic.zip) 」からダウンロードしてください。**

1. まず、UI を設定します (MainPage.xaml)。

    ```xaml
    <Page
        x:Class="gazeinput.MainPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:gazeinput"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"    
        mc:Ignorable="d">
    
        <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
            <Grid x:Name="containerGrid">
                <Grid.RowDefinitions>
                    <RowDefinition Height="Auto"/>
                    <RowDefinition Height="*"/>
                </Grid.RowDefinitions>
                <StackPanel x:Name="HeaderPanel" 
                        Orientation="Horizontal" 
                        Grid.Row="0">
                    <StackPanel.Transitions>
                        <TransitionCollection>
                            <AddDeleteThemeTransition/>
                        </TransitionCollection>
                    </StackPanel.Transitions>
                    <TextBlock x:Name="Header" 
                           Text="Gaze tracking sample" 
                           Style="{ThemeResource HeaderTextBlockStyle}" 
                           Margin="10,0,0,0" />
                    <TextBlock x:Name="TrackerCounterLabel"
                           VerticalAlignment="Center"                 
                           Style="{ThemeResource BodyTextBlockStyle}"
                           Text="Number of trackers: " 
                           Margin="50,0,0,0"/>
                    <TextBlock x:Name="TrackerCounter"
                           VerticalAlignment="Center"                 
                           Style="{ThemeResource BodyTextBlockStyle}"
                           Text="0" 
                           Margin="10,0,0,0"/>
                    <TextBlock x:Name="TrackerStateLabel"
                           VerticalAlignment="Center"                 
                           Style="{ThemeResource BodyTextBlockStyle}"
                           Text="State: " 
                           Margin="50,0,0,0"/>
                    <TextBlock x:Name="TrackerState"
                           VerticalAlignment="Center"                 
                           Style="{ThemeResource BodyTextBlockStyle}"
                           Text="n/a" 
                           Margin="10,0,0,0"/>
                </StackPanel>
                <Canvas x:Name="gazePositionCanvas" Grid.Row="1">
                    <controls:RadialProgressBar
                        x:Name="GazeRadialProgressBar" 
                        Value="0"
                        Foreground="Blue" 
                        Background="White"
                        Thickness="4"
                        Minimum="0"
                        Maximum="100"
                        Width="100"
                        Height="100"
                        Outline="Gray"
                        Visibility="Collapsed"/>
                    <Ellipse 
                        x:Name="eyeGazePositionEllipse"
                        Width="20" Height="20"
                        Fill="Blue" 
                        Opacity="0.5" 
                        Visibility="Collapsed">
                    </Ellipse>
                </Canvas>
            </Grid>
        </Grid>
    </Page>
    ```

2. 次に、アプリを初期化します。

    このスニペットでは、グローバル オブジェクトを宣言し、[OnNavigatedTo](/uwp/api/windows.ui.xaml.controls.page.onnavigatedto) ページ イベントを上書きして[視線デバイス ウォッチャー](/uwp/api/windows.devices.input.preview.gazedevicewatcherpreview)を開始し、[OnNavigatedFrom](/uwp/api/windows.ui.xaml.controls.page.onnavigatedfrom) ページ イベントを上書きして[視線デバイス ウォッチャー](/uwp/api/windows.devices.input.preview.gazedevicewatcherpreview)を停止します。

    ```csharp
    using System;
    using Windows.Devices.Input.Preview;
    using Windows.UI.Xaml.Controls;
    using Windows.UI.Xaml;
    using Windows.Foundation;
    using System.Collections.Generic;
    using Windows.UI.Xaml.Media;
    using Windows.UI.Xaml.Navigation;
    
    namespace gazeinput
    {
        public sealed partial class MainPage : Page
        {
            /// <summary>
            /// Reference to the user's eyes and head as detected
            /// by the eye-tracking device.
            /// </summary>
            private GazeInputSourcePreview gazeInputSource;
    
            /// <summary>
            /// Dynamic store of eye-tracking devices.
            /// </summary>
            /// <remarks>
            /// Receives event notifications when a device is added, removed, 
            /// or updated after the initial enumeration.
            /// </remarks>
            private GazeDeviceWatcherPreview gazeDeviceWatcher;
    
            /// <summary>
            /// Eye-tracking device counter.
            /// </summary>
            private int deviceCounter = 0;
    
            /// <summary>
            /// Timer for gaze focus on RadialProgressBar.
            /// </summary>
            DispatcherTimer timerGaze = new DispatcherTimer();
    
            /// <summary>
            /// Tracker used to prevent gaze timer restarts.
            /// </summary>
            bool timerStarted = false;
    
            /// <summary>
            /// Initialize the app.
            /// </summary>
            public MainPage()
            {
                InitializeComponent();
            }

            /// <summary>
            /// Override of OnNavigatedTo page event starts GazeDeviceWatcher.
            /// </summary>
            /// <param name="e">Event args for the NavigatedTo event</param>
            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
                // Start listening for device events on navigation to eye-tracking page.
                StartGazeDeviceWatcher();
            }
    
            /// <summary>
            /// Override of OnNavigatedFrom page event stops GazeDeviceWatcher.
            /// </summary>
            /// <param name="e">Event args for the NavigatedFrom event</param>
            protected override void OnNavigatedFrom(NavigationEventArgs e)
            {
                // Stop listening for device events on navigation from eye-tracking page.
                StopGazeDeviceWatcher();
            }
        }
    }
    ```

3. 次に、視線デバイス ウォッチャーのメソッドを追加します。 
    
    `StartGazeDeviceWatcher` で、[CreateWatcher](/uwp/api/windows.devices.input.preview.gazeinputsourcepreview.createwatcher) を呼び出し、視線追跡デバイスのイベント リスナー ([DeviceAdded](/uwp/api/windows.devices.input.preview.gazedevicewatcherpreview.added)、[DeviceUpdated](/uwp/api/windows.devices.input.preview.gazedevicewatcherpreview.updated)、[DeviceRemoved](/uwp/api/windows.devices.input.preview.gazedevicewatcherpreview.removed)) を宣言します。

    `DeviceAdded` で、視線追跡デバイスの状態を確認します。 実行可能なデバイスで、デバイス カウントをインクリメントし、視線追跡を有効にします。 詳細については、次の手順を参照してください。

    `DeviceUpdated` では、デバイスが再調整された場合にこのイベントがトリガーされたときにも視線追跡を有効にします。

    `DeviceRemoved` では、デバイス カウンターをデクリメントし、デバイスのイベント ハンドラーを削除します。

    `StopGazeDeviceWatcher` で、視線デバイス ウォッチャーをシャットダウンします。 

```csharp
    /// <summary>
    /// Start gaze watcher and declare watcher event handlers.
    /// </summary>
    private void StartGazeDeviceWatcher()
    {
        if (gazeDeviceWatcher == null)
        {
            gazeDeviceWatcher = GazeInputSourcePreview.CreateWatcher();
            gazeDeviceWatcher.Added += this.DeviceAdded;
            gazeDeviceWatcher.Updated += this.DeviceUpdated;
            gazeDeviceWatcher.Removed += this.DeviceRemoved;
            gazeDeviceWatcher.Start();
        }
    }

    /// <summary>
    /// Shut down gaze watcher and stop listening for events.
    /// </summary>
    private void StopGazeDeviceWatcher()
    {
        if (gazeDeviceWatcher != null)
        {
            gazeDeviceWatcher.Stop();
            gazeDeviceWatcher.Added -= this.DeviceAdded;
            gazeDeviceWatcher.Updated -= this.DeviceUpdated;
            gazeDeviceWatcher.Removed -= this.DeviceRemoved;
            gazeDeviceWatcher = null;
        }
    }

    /// <summary>
    /// Eye-tracking device connected (added, or available when watcher is initialized).
    /// </summary>
    /// <param name="sender">Source of the device added event</param>
    /// <param name="e">Event args for the device added event</param>
    private void DeviceAdded(GazeDeviceWatcherPreview source, 
        GazeDeviceWatcherAddedPreviewEventArgs args)
    {
        if (IsSupportedDevice(args.Device))
        {
            deviceCounter++;
            TrackerCounter.Text = deviceCounter.ToString();
        }
        // Set up gaze tracking.
        TryEnableGazeTrackingAsync(args.Device);
    }

    /// <summary>
    /// Initial device state might be uncalibrated, 
    /// but device was subsequently calibrated.
    /// </summary>
    /// <param name="sender">Source of the device updated event</param>
    /// <param name="e">Event args for the device updated event</param>
    private void DeviceUpdated(GazeDeviceWatcherPreview source,
        GazeDeviceWatcherUpdatedPreviewEventArgs args)
    {
        // Set up gaze tracking.
        TryEnableGazeTrackingAsync(args.Device);
    }

    /// <summary>
    /// Handles disconnection of eye-tracking devices.
    /// </summary>
    /// <param name="sender">Source of the device removed event</param>
    /// <param name="e">Event args for the device removed event</param>
    private void DeviceRemoved(GazeDeviceWatcherPreview source,
        GazeDeviceWatcherRemovedPreviewEventArgs args)
    {
        // Decrement gaze device counter and remove event handlers.
        if (IsSupportedDevice(args.Device))
        {
            deviceCounter--;
            TrackerCounter.Text = deviceCounter.ToString();

            if (deviceCounter == 0)
            {
                gazeInputSource.GazeEntered -= this.GazeEntered;
                gazeInputSource.GazeMoved -= this.GazeMoved;
                gazeInputSource.GazeExited -= this.GazeExited;
            }
        }
    }
```

4. ここでは、デバイスが `IsSupportedDevice` で実行可能であるかどうかを確認し、実行可能であれば、`TryEnableGazeTrackingAsync` で視線追跡を有効にすることを試みます。

    `TryEnableGazeTrackingAsync` では、視線のイベント ハンドラーを宣言し、[GazeInputSourcePreview.GetForCurrentView()](/uwp/api/windows.devices.input.preview.gazeinputsourcepreview.getforcurrentview) を呼び出して入力ソースへの参照を取得します (これは UI スレッドで呼び出す必要があります。「[UI スレッドの応答性の確保](../../debug-test-perf/keep-the-ui-thread-responsive.md)」を参照してください)。

    > [!NOTE]
    > [GazeInputSourcePreview.GetForCurrentView()](/uwp/api/windows.devices.input.preview.gazeinputsourcepreview.getforcurrentview) は、互換性のある視線追跡デバイスが接続され、アプリケーションで必要な場合にのみ呼び出す必要があります。 それ以外の場合、同意ダイアログ ボックスは不要です。

```csharp
    /// <summary>
    /// Initialize gaze tracking.
    /// </summary>
    /// <param name="gazeDevice"></param>
    private async void TryEnableGazeTrackingAsync(GazeDevicePreview gazeDevice)
    {
        // If eye-tracking device is ready, declare event handlers and start tracking.
        if (IsSupportedDevice(gazeDevice))
        {
            timerGaze.Interval = new TimeSpan(0, 0, 0, 0, 20);
            timerGaze.Tick += TimerGaze_Tick;

            SetGazeTargetLocation();

            // This must be called from the UI thread.
            gazeInputSource = GazeInputSourcePreview.GetForCurrentView();

            gazeInputSource.GazeEntered += GazeEntered;
            gazeInputSource.GazeMoved += GazeMoved;
            gazeInputSource.GazeExited += GazeExited;
        }
        // Notify if device calibration required.
        else if (gazeDevice.ConfigurationState ==
                    GazeDeviceConfigurationStatePreview.UserCalibrationNeeded ||
                    gazeDevice.ConfigurationState ==
                    GazeDeviceConfigurationStatePreview.ScreenSetupNeeded)
        {
            // Device isn't calibrated, so invoke the calibration handler.
            System.Diagnostics.Debug.WriteLine(
                "Your device needs to calibrate. Please wait for it to finish.");
            await gazeDevice.RequestCalibrationAsync();
        }
        // Notify if device calibration underway.
        else if (gazeDevice.ConfigurationState == 
            GazeDeviceConfigurationStatePreview.Configuring)
        {
            // Device is currently undergoing calibration.  
            // A device update is sent when calibration complete.
            System.Diagnostics.Debug.WriteLine(
                "Your device is being configured. Please wait for it to finish"); 
        }
        // Device is not viable.
        else if (gazeDevice.ConfigurationState == GazeDeviceConfigurationStatePreview.Unknown)
        {
            // Notify if device is in unknown state.  
            // Reconfigure/recalbirate the device.  
            System.Diagnostics.Debug.WriteLine(
                "Your device is not ready. Please set up your device or reconfigure it."); 
        }
    }

    /// <summary>
    /// Check if eye-tracking device is viable.
    /// </summary>
    /// <param name="gazeDevice">Reference to eye-tracking device.</param>
    /// <returns>True, if device is viable; otherwise, false.</returns>
    private bool IsSupportedDevice(GazeDevicePreview gazeDevice)
    {
        TrackerState.Text = gazeDevice.ConfigurationState.ToString();
        return (gazeDevice.CanTrackEyes &&
                    gazeDevice.ConfigurationState == 
                    GazeDeviceConfigurationStatePreview.Ready);
    }
```

5. 次に、視線のイベント ハンドラーを設定します。

    視線追跡の楕円を `GazeEntered` で表示し、`GazeExited` で非表示にします。

    `GazeMoved` では、[GazeEnteredPreviewEventArgs](/uwp/api/windows.devices.input.preview.gazeenteredprevieweventargs) の [CurrentPoint](/uwp/api/windows.devices.input.preview.gazeenteredprevieweventargs.currentpoint) で提供される [EyeGazePosition](/uwp/api/windows.devices.input.preview.gazepointpreview.eyegazeposition) に基づいて視線追跡の楕円を移動します。 また、[RadialProgressBar](/windows/communitytoolkit/controls/radialprogressbar) で視線フォーカスのタイマーを管理します。これにより進行状況バーの位置変更がトリガーされます。 詳細については、次の手順を参照してください。

    ```csharp
    /// <summary>
    /// GazeEntered handler.
    /// </summary>
    /// <param name="sender">Source of the gaze entered event</param>
    /// <param name="e">Event args for the gaze entered event</param>
    private void GazeEntered(
        GazeInputSourcePreview sender, 
        GazeEnteredPreviewEventArgs args)
    {
        // Show ellipse representing gaze point.
        eyeGazePositionEllipse.Visibility = Visibility.Visible;

        // Mark the event handled.
        args.Handled = true;
    }

    /// <summary>
    /// GazeExited handler.
    /// Call DisplayRequest.RequestRelease to conclude the 
    /// RequestActive called in GazeEntered.
    /// </summary>
    /// <param name="sender">Source of the gaze exited event</param>
    /// <param name="e">Event args for the gaze exited event</param>
    private void GazeExited(
        GazeInputSourcePreview sender, 
        GazeExitedPreviewEventArgs args)
    {
        // Hide gaze tracking ellipse.
        eyeGazePositionEllipse.Visibility = Visibility.Collapsed;

        // Mark the event handled.
        args.Handled = true;
    }

    /// <summary>
    /// GazeMoved handler translates the ellipse on the canvas to reflect gaze point.
    /// </summary>
    /// <param name="sender">Source of the gaze moved event</param>
    /// <param name="e">Event args for the gaze moved event</param>
    private void GazeMoved(GazeInputSourcePreview sender, GazeMovedPreviewEventArgs args)
    {
        // Update the position of the ellipse corresponding to gaze point.
        if (args.CurrentPoint.EyeGazePosition != null)
        {
            double gazePointX = args.CurrentPoint.EyeGazePosition.Value.X;
            double gazePointY = args.CurrentPoint.EyeGazePosition.Value.Y;

            double ellipseLeft = 
                gazePointX - 
                (eyeGazePositionEllipse.Width / 2.0f);
            double ellipseTop = 
                gazePointY - 
                (eyeGazePositionEllipse.Height / 2.0f) - 
                (int)Header.ActualHeight;

            // Translate transform for moving gaze ellipse.
            TranslateTransform translateEllipse = new TranslateTransform
            {
                X = ellipseLeft,
                Y = ellipseTop
            };

            eyeGazePositionEllipse.RenderTransform = translateEllipse;

            // The gaze point screen location.
            Point gazePoint = new Point(gazePointX, gazePointY);

            // Basic hit test to determine if gaze point is on progress bar.
            bool hitRadialProgressBar = 
                DoesElementContainPoint(
                    gazePoint, 
                    GazeRadialProgressBar.Name, 
                    GazeRadialProgressBar); 

            // Use progress bar thickness for visual feedback.
            if (hitRadialProgressBar)
            {
                GazeRadialProgressBar.Thickness = 10;
            }
            else
            {
                GazeRadialProgressBar.Thickness = 4;
            }

            // Mark the event handled.
            args.Handled = true;
        }
    }
    ```
6. 最後に、このアプリの視線フォーカス タイマーを管理するために使用する方法を示します。

    `DoesElementContainPoint` 見つめポインターがプログレスバーの上にあるかどうかを確認します。 超えている場合は、視線タイマーを開始し、それぞれの視線タイマー ティックで進行状況バーをインクリメントします。

    `SetGazeTargetLocation` 進行状況バーの初期位置を設定します。進行状況バーが完了した場合は、進行状況バーがランダムな場所に移動します。

    ```csharp
    /// <summary>
    /// Return whether the gaze point is over the progress bar.
    /// </summary>
    /// <param name="gazePoint">The gaze point screen location</param>
    /// <param name="elementName">The progress bar name</param>
    /// <param name="uiElement">The progress bar UI element</param>
    /// <returns></returns>
    private bool DoesElementContainPoint(
        Point gazePoint, string elementName, UIElement uiElement)
    {
        // Use entire visual tree of progress bar.
        IEnumerable<UIElement> elementStack = 
            VisualTreeHelper.FindElementsInHostCoordinates(gazePoint, uiElement, true);
        foreach (UIElement item in elementStack)
        {
            //Cast to FrameworkElement and get element name.
            if (item is FrameworkElement feItem)
            {
                if (feItem.Name.Equals(elementName))
                {
                    if (!timerStarted)
                    {
                        // Start gaze timer if gaze over element.
                        timerGaze.Start();
                        timerStarted = true;
                    }
                    return true;
                }
            }
        }

        // Stop gaze timer and reset progress bar if gaze leaves element.
        timerGaze.Stop();
        GazeRadialProgressBar.Value = 0;
        timerStarted = false;
        return false;
    }

    /// <summary>
    /// Tick handler for gaze focus timer.
    /// </summary>
    /// <param name="sender">Source of the gaze entered event</param>
    /// <param name="e">Event args for the gaze entered event</param>
    private void TimerGaze_Tick(object sender, object e)
    {
        // Increment progress bar.
        GazeRadialProgressBar.Value += 1;

        // If progress bar reaches maximum value, reset and relocate.
        if (GazeRadialProgressBar.Value == 100)
        {
            SetGazeTargetLocation();
        }
    }

    /// <summary>
    /// Set/reset the screen location of the progress bar.
    /// </summary>
    private void SetGazeTargetLocation()
    {
        // Ensure the gaze timer restarts on new progress bar location.
        timerGaze.Stop();
        timerStarted = false;

        // Get the bounding rectangle of the app window.
        Rect appBounds = Windows.UI.ViewManagement.ApplicationView.GetForCurrentView().VisibleBounds;

        // Translate transform for moving progress bar.
        TranslateTransform translateTarget = new TranslateTransform();

        // Calculate random location within gaze canvas.
            Random random = new Random();
            int randomX = 
                random.Next(
                    0, 
                    (int)appBounds.Width - (int)GazeRadialProgressBar.Width);
            int randomY = 
                random.Next(
                    0, 
                    (int)appBounds.Height - (int)GazeRadialProgressBar.Height - (int)Header.ActualHeight);

        translateTarget.X = randomX;
        translateTarget.Y = randomY;

        GazeRadialProgressBar.RenderTransform = translateTarget;

        // Show progress bar.
        GazeRadialProgressBar.Visibility = Visibility.Visible;
        GazeRadialProgressBar.Value = 0;
    }
    ```

## <a name="see-also"></a>関連項目

### <a name="resources"></a>リソース

- [Windows コミュニティ ツールキットの視線ライブラリ](/windows/communitytoolkit/gaze/gazeinteractionlibrary)

### <a name="topic-samples"></a>トピックのサンプル

- [視線のサンプル (基本) (C#)](https://github.com/MicrosoftDocs/windows-topic-specific-samples/archive/uwp-gazeinput-basic.zip)
