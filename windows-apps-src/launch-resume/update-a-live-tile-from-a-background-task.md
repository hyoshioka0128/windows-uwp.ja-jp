---
title: バックグラウンド タスクのライブ タイルの更新
description: アプリのライブ タイルを新しいコンテンツで更新するには、バックグラウンド タスクを使います。
Search.SourceType: Video
ms.assetid: 9237A5BD-F9DE-4B8C-B689-601201BA8B9A
ms.date: 01/11/2018
ms.topic: article
keywords: windows 10、uwp、バックグラウンドタスク
ms.localizationpriority: medium
ms.openlocfilehash: 50ed0246941645824ee0705582a9efbf2b193dc9
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89155776"
---
# <a name="update-a-live-tile-from-a-background-task"></a>バックグラウンド タスクのライブ タイルの更新

**重要な API**

-   [**IBackgroundTask**](/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask)
-   [**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder)

アプリのライブ タイルを新しいコンテンツで更新するには、バックグラウンド タスクを使います。

アプリにライブ タイルを追加する方法について説明するビデオをご覧ください。

<iframe src="https://channel9.msdn.com/Blogs/One-Dev-Minute/Updating-a-live-tile-from-a-background-task/player" width="720" height="405" allowFullScreen="true" frameBorder="0"></iframe>

## <a name="create-the-background-task-project"></a>バックグラウンド タスク プロジェクトを作る  

アプリのライブタイルを有効にするには、新しい Windows ランタイムコンポーネントプロジェクトをソリューションに追加します。 このプロジェクトは個別のアセンブリです。ユーザーがアプリをインストールするとき、OS ではこのプロジェクトがバックグラウンドで読み込まれ、実行されます。

1.  ソリューション エクスプローラーで該当ソリューションを右クリックして **[追加]** をクリックし、 **[新しいプロジェクト]** をクリックします。
2.  **[新しいプロジェクトの追加]** ダイアログ ボックスで、**[インストール済み] &gt; [他の言語] &gt; [Visual C#] &gt; [Windows ユニバーサル]** セクションで、**[Windows ランタイム コンポーネント]** テンプレートを選びます。
3.  プロジェクトに BackgroundTasks という名前を付け、**[OK]** をクリックまたはタップします。 Microsoft Visual Studio によって、新しいプロジェクトがソリューションに追加されます。
4.  メイン プロジェクトで、BackgroundTasks プロジェクトへの参照を追加します。

## <a name="implement-the-background-task"></a>バックグラウンド タスクの実装


[**IBackgroundTask**](/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask) インターフェイスを実装して、アプリのライブ タイルを更新するクラスを作ります。 バックグラウンドの作業は、Run メソッドで実行されます。 この場合、タスクによって MSDN ブログの配信フィードが取得されます。 非同期コードの実行中にタスクが途中で終了するのを防ぐには、保留を取得します。

1.  ソリューション エクスプローラーで、自動的に生成されたファイルである Class1.cs の名前を BlogFeedBackgroundTask.cs に変更します。
2.  BlogFeedBackgroundTask.cs を開き、自動的に生成されたコードを、**BlogFeedBackgroundTask** クラスのスタブ コードに置き換えます。
3.  Run メソッドの実装で、**GetMSDNBlogFeed** メソッドと **UpdateTile** のメソッドのコードを追加します。

```cs
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

// Added during quickstart
using Windows.ApplicationModel.Background;
using Windows.Data.Xml.Dom;
using Windows.UI.Notifications;
using Windows.Web.Syndication;

namespace BackgroundTasks
{
    public sealed class BlogFeedBackgroundTask  : IBackgroundTask
    {
        public async void Run( IBackgroundTaskInstance taskInstance )
        {
            // Get a deferral, to prevent the task from closing prematurely
            // while asynchronous code is still running.
            BackgroundTaskDeferral deferral = taskInstance.GetDeferral();

            // Download the feed.
            var feed = await GetMSDNBlogFeed();

            // Update the live tile with the feed items.
            UpdateTile( feed );

            // Inform the system that the task is finished.
            deferral.Complete();
        }

        private static async Task<SyndicationFeed> GetMSDNBlogFeed()
        {
            SyndicationFeed feed = null;

            try
            {
                // Create a syndication client that downloads the feed.  
                SyndicationClient client = new SyndicationClient();
                client.BypassCacheOnRetrieve = true;
                client.SetRequestHeader( customHeaderName, customHeaderValue );

                // Download the feed.
                feed = await client.RetrieveFeedAsync( new Uri( feedUrl ) );
            }
            catch( Exception ex )
            {
                Debug.WriteLine( ex.ToString() );
            }

            return feed;
        }

        private static void UpdateTile( SyndicationFeed feed )
        {
            // Create a tile update manager for the specified syndication feed.
            var updater = TileUpdateManager.CreateTileUpdaterForApplication();
            updater.EnableNotificationQueue( true );
            updater.Clear();

            // Keep track of the number feed items that get tile notifications.
            int itemCount = 0;

            // Create a tile notification for each feed item.
            foreach( var item in feed.Items )
            {
                XmlDocument tileXml = TileUpdateManager.GetTemplateContent( TileTemplateType.TileWide310x150Text03 );

                var title = item.Title;
                string titleText = title.Text == null ? String.Empty : title.Text;
                tileXml.GetElementsByTagName( textElementName )[0].InnerText = titleText;

                // Create a new tile notification.
                updater.Update( new TileNotification( tileXml ) );

                // Don't create more than 5 notifications.
                if( itemCount++ > 5 ) break;
            }
        }

        // Although most HTTP servers do not require User-Agent header, others will reject the request or return
        // a different response if this header is missing. Use SetRequestHeader() to add custom headers.
        static string customHeaderName = "User-Agent";
        static string customHeaderValue = "Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)";

        static string textElementName = "text";
        static string feedUrl = @"http://blogs.msdn.com/b/MainFeed.aspx?Type=BlogsOnly";
    }
}
```

## <a name="set-up-the-package-manifest"></a>パッケージ マニフェストの設定


パッケージ マニフェストを設定するには、そのマニフェストを開き、新しいバックグラウンド タスクの宣言を追加します。 タスクのエントリ ポイントを設定します。このエントリ ポイントには、名前空間を含めてクラスの名前を指定します。

1.  ソリューション エクスプローラーで、Package.appxmanifest を開きます。
2.  **[宣言]** タブをタップまたはクリックします。
3.  **[使用可能な宣言]** で、**[BackgroundTasks]** を選び、**[追加]** をクリックします。 Visual Studio で、**[サポートされる宣言]** の下に **[BackgroundTasks]** が追加されます。
4.  **[サポートされるタスクの種類]** で、**[タイマー]** がオンになっていることを確認します。
5.  **[アプリの設定]** で、エントリ ポイントを **[BackgroundTasks.BlogFeedBackgroundTask]** に設定します。
6.  **[アプリケーション UI]** タブをクリックまたはタップします。
7.  **[ロック画面通知]** を **[バッジとタイル テキスト]** に設定します。
8.  **[バッジ ロゴ]** フィールドに、24x24 ピクセルのアイコンへのパスを設定します。
    **重要**   このアイコンは、モノクロおよび透明ピクセルのみを使用する必要があります。
9.  **[小さいロゴ]** フィールドに、30x30 ピクセルのアイコンへのパスを設定します。
10. **[ワイド ロゴ]** フィールドに、310x150 ピクセルのアイコンへのパスを設定します。

## <a name="register-the-background-task"></a>バックグラウンド タスクの登録


[**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) を作って、タスクを登録します。

> **メモ**   Windows 8.1 以降では、バックグラウンドタスクの登録パラメーターが登録時に検証されます。 いずれかの登録パラメーターが有効でない場合は、エラーが返されます。 アプリは、バックグラウンド タスクの登録が失敗するシナリオを処理できる必要があります。たとえば、条件ステートメントを使って登録エラーを確認し、失敗した登録は別のパラメーター値を使ってやり直してみます。
 

アプリのメイン ページで、**RegisterBackgroundTask** メソッドを追加し、このメソッドを **OnNavigatedTo** イベント ハンドラーで呼び出します。

```cs
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading.Tasks;
using Windows.ApplicationModel.Background;
using Windows.Data.Xml.Dom;
using Windows.Foundation;
using Windows.Foundation.Collections;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Primitives;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Navigation;
using Windows.Web.Syndication;

// The Blank Page item template is documented at https://go.microsoft.com/fwlink/p/?LinkID=234238

namespace ContosoApp
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        public MainPage()
        {
            this.InitializeComponent();
        }

        /// <summary>
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.  The Parameter
        /// property is typically used to configure the page.</param>
        protected override void OnNavigatedTo( NavigationEventArgs e )
        {
            this.RegisterBackgroundTask();
        }


        private async void RegisterBackgroundTask()
        {
            var backgroundAccessStatus = await BackgroundExecutionManager.RequestAccessAsync();
            if( backgroundAccessStatus == BackgroundAccessStatus.AllowedSubjectToSystemPolicy ||
                backgroundAccessStatus == BackgroundAccessStatus.AlwaysAllowed )
            {
                foreach( var task in BackgroundTaskRegistration.AllTasks )
                {
                    if( task.Value.Name == taskName )
                    {
                        task.Value.Unregister( true );
                    }
                }

                BackgroundTaskBuilder taskBuilder = new BackgroundTaskBuilder();
                taskBuilder.Name = taskName;
                taskBuilder.TaskEntryPoint = taskEntryPoint;
                taskBuilder.SetTrigger( new TimeTrigger( 15, false ) );
                var registration = taskBuilder.Register();
            }
        }

        private const string taskName = "BlogFeedBackgroundTask";
        private const string taskEntryPoint = "BackgroundTasks.BlogFeedBackgroundTask";
    }
}
```

## <a name="debug-the-background-task"></a>バックグラウンド タスクのデバッグ


バックグラウンド タスクをデバッグするには、タスクの Run メソッドにブレークポイントを設定します。 **[デバッグの場所]** ツール バーで、バックグラウンド タスクを選びます。 この操作によって、システムで Run メソッドがすぐに呼び出されます。

1.  タスクの Run メソッドにブレークポイントを設定します。
2.  F5 キーを押すか、[デバッグ] [ ** &gt; デバッグの開始** ] の順にタップして、アプリをデプロイして実行します。
3.  アプリを起動した後で、Visual Studio に戻ります。
4.  **[デバッグの場所]** ツール バーが表示されていることを確認します。 これは、[ ** &gt; ツールバーの表示** ] メニューにあります。
5.  **[デバッグの場所]** ツール バーで、**[中断]** ドロップダウンをクリックし、**[BlogFeedBackgroundTask]** を選びます。
6.  Visual Studio では、ブレークポイントで実行が中断します。
7.  F5 キーを押すか、[ **デバッグ &gt; 続行** するには、アプリの実行を続行します。
8.  Shift キーを押しながら F5 キーを押すか、[デバッグの ** &gt; 停止** デバッグを停止してデバッグを停止します。
9.  スタート画面にあるアプリのタイルに戻ります。 数秒後、アプリのタイルにタイル通知が表示されます。

## <a name="related-topics"></a>関連トピック


* [**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder)
* [**TileUpdateManager**](/uwp/api/Windows.UI.Notifications.TileUpdateManager)
* [**TileNotification**](/uwp/api/Windows.UI.Notifications.TileNotification)
* [バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)
* [タイルとバッジのガイドラインとチェック リスト](../design/shell/tiles-and-notifications/creating-tiles.md)

 

 