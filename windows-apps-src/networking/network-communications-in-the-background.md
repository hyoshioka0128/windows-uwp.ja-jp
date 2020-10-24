---
description: バックグラウンドでないときにネットワーク通信を続けるため、アプリはバックグラウンド タスクを使うことができます。ソケット ブローカーまたはコントロール チャネルがトリガーされます。
title: バックグラウンドでのネットワーク通信
ms.assetid: 537F8E16-9972-435D-85A5-56D5764D3AC2
ms.date: 06/14/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: e352e5c60290252694a913a32ffc360a74aa67f8
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89174916"
---
# <a name="network-communications-in-the-background"></a>バックグラウンドでのネットワーク通信

> [!NOTE]
> **一部の情報はリリース前の製品に関する事項であり、正式版がリリースされるまでに大幅に変更される可能性があります。ここに記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。**

フォアグラウンドでないときにネットワーク通信を続けるため、アプリはバックグラウンド タスクと次のいずれかのオプションを使うことができます。
- ソケット ブローカー: 長期的な接続にソケットを使うアプリは、フォアグラウンドから離れるときにソケットの所有権をシステムのソケット ブローカーに委任できます。 ブローカーは、トラフィックがソケットに到着したときにアプリをアクティブ化して所有権をアプリに戻し、その後にアプリが着信トラフィックを処理します。
- コントロール チャネル トリガー。 

## <a name="performing-network-operations-in-background-tasks"></a>バックグラウンド タスクでのネットワーク操作の実行
- パケットを受信し、有効期間が短いタスクを実行する必要がある場合は、[SocketActivityTrigger](/uwp/api/windows.applicationmodel.background.socketactivitytrigger) を使用して、バックグラウンド タスクをアクティブにします。 タスクを実行すると、電力を節約するためにバックグラウンド タスクが終了します。
- パケットを受信し、有効期間が長いタスクを実行する必要がある場合は、[ControlChannelTrigger](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) を使用して、バックグラウンド タスクをアクティブにします。

**ネットワーク関連の条件とフラグ**

- バックグラウンド タスク [BackgroundTaskBuilder.AddCondition](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) に **InternetAvailable** 条件を追加して、ネットワーク スタックが実行されるまで、バックグラウンド タスクのトリガーを遅らせます。 この条件では、ネットワークが起動するまでバックグラウンド タスクが実行されないため、電力が節約されます。 この条件では、リアルタイムのアクティブ化は行われません。

使用するトリガーに関係なく、バックグラウンド タスクで [IsNetworkRequested](/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder) を設定すると、バックグラウンド タスクが実行されている間、ネットワークは稼働状態のままになります。 これによって、デバイスがコネクト スタンバイ モードに入っている場合でも、タスクの実行中はネットワークを稼働状態に保つようにバックグラウンド タスク インフラストラクチャに指示されます。 バックグラウンド タスクが **IsNetworkRequested** を使用しない場合、そのバックグラウンド タスクはコネクト スタンバイ モードのとき (たとえば電話の画面がオフになっているとき) にネットワークにアクセスできません。

## <a name="socket-broker-and-the-socketactivitytrigger"></a>ソケット ブローカーと SocketActivityTrigger
アプリが [**DatagramSocket**](/uwp/api/Windows.Networking.Sockets.DatagramSocket)、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket)、または [**StreamSocketListener**](/uwp/api/Windows.Networking.Sockets.StreamSocketListener) 接続を使う場合、[**SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) とソケット ブローカーを使って、フォアグラウンドでないときにトラフィックがアプリに到着したという通知を受け取る必要があります。

アプリがアクティブでないときにソケットでデータを受け取って処理するには、アプリは起動時に 1 回限りのセットアップをいくつか実行した後、アクティブでない状態に移行するときにソケットの所有権をソケット ブローカーに転送する必要があります。

1 回限りのセットアップ手順では、次のようにトリガーを作成し、そのトリガーのバックグラウンド タスクを登録し、ソケット ブローカーのソケットを有効します。
  - **SocketActivityTrigger** を作成し、TaskEntryPoint パラメーターを受信パケットを処理するためのコードに設定してトリガーのバックグラウンド タスクを登録します。
```csharp
            var socketTaskBuilder = new BackgroundTaskBuilder();
            socketTaskBuilder.Name = _backgroundTaskName;
            socketTaskBuilder.TaskEntryPoint = _backgroundTaskEntryPoint;
            var trigger = new SocketActivityTrigger();
            socketTaskBuilder.SetTrigger(trigger);
            _task = socketTaskBuilder.Register();
```
  - ソケットをバインドする前に、ソケットで **EnableTransferOwnership** を呼び出します。
```csharp
           _tcpListener = new StreamSocketListener();

           // Note that EnableTransferOwnership() should be called before bind,
           // so that tcpip keeps required state for the socket to enable connected
           // standby action. Background task Id is taken as a parameter to tie wake pattern
           // to a specific background task.  
           _tcpListener. EnableTransferOwnership(_task.TaskId,SocketActivityConnectedStandbyAction.Wake);
           _tcpListener.ConnectionReceived += OnConnectionReceived;
           await _tcpListener.BindServiceNameAsync("my-service-name");
```

ソケットが正しくセットアップされたら、アプリが中断する直前に、ソケットで **TransferOwnership** を呼び出してソケット ブローカーに転送します。 ブローカーはソケットを監視し、データが受信されたらバックグラウンド タスクをアクティブにします。 次の例には、**StreamSocketListener** ソケットの転送を実行する **TransferOwnership** ユーティリティ関数が含まれています (さまざまな種類の各ソケットに独自の **TransferOwnership** メソッドがあるため、転送する所有権を持つソケットに適したメソッドを呼び出す必要があります。 **OnSuspending** コードの読みやすさを維持するため、コードにはオーバーロードされた **TransferOwnership** ヘルパーを含め、使用するソケットの種類ごとに 1 つずつ実装することをお勧めします)。

アプリは、次のうち適切なメソッドを使って、ソケットの所有権をソケット ブローカーに転送し、バックグラウンド タスクの ID を渡します。
-   [  **DatagramSocket**](/uwp/api/Windows.Networking.Sockets.DatagramSocket) の [**TransferOwnership**](/uwp/api/windows.networking.sockets.datagramsocket.transferownership) メソッドのいずれか
-   [  **StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) の [**TransferOwnership**](/uwp/api/windows.networking.sockets.streamsocket.transferownership) メソッドのいずれか
-   [  **StreamSocketListener**](/uwp/api/Windows.Networking.Sockets.StreamSocketListener) の [**TransferOwnership**](/uwp/api/windows.networking.sockets.streamsocketlistener.transferownership) メソッドのいずれか

```csharp

// declare int _transferOwnershipCount as a field.

private void TransferOwnership(StreamSocketListener tcpListener)
{
    await tcpListener.CancelIOAsync();

    var dataWriter = new DataWriter();
    ++_transferOwnershipCount;
    dataWriter.WriteInt32(transferOwnershipCount);
    var context = new SocketActivityContext(dataWriter.DetachBuffer());
    tcpListener.TransferOwnership(_socketId, context);
}

private void OnSuspending(object sender, SuspendingEventArgs e)
{
    var deferral = e.SuspendingOperation.GetDeferral();

    TransferOwnership(_tcpListener);
    deferral.Complete();
}
```
バックグラウンド タスクのイベント ハンドラーで、次の作業を行います。
   -  まず、非同期メソッドを使ってイベントを処理できるように、バックグラウンド タスクの保留を取得します。
```csharp
var deferral = taskInstance.GetDeferral();
```
   -  次に、イベント引数から SocketActivityTriggerDetails を抽出し、イベントが発生した理由を調べます。
```csharp
var details = taskInstance.TriggerDetails as SocketActivityTriggerDetails;
    var socketInformation = details.SocketInformation;
    switch (details.Reason)
```
   -   ソケット アクティビティが原因でイベントが発生した場合、ソケットに DataReader を作成してリーダーを非同期で読み込み、アプリのデザインに従ってデータを使います。 ソケット アクティビティの通知を再度受け取るには、ソケットの所有権をソケット ブローカーに戻す必要がある点に注意してください。

   次の例では、ソケットで受け取ったテキストがトーストに表示されます。

```csharp
case SocketActivityTriggerReason.SocketActivity:
            var socket = socketInformation.StreamSocket;
            DataReader reader = new DataReader(socket.InputStream);
            reader.InputStreamOptions = InputStreamOptions.Partial;
            await reader.LoadAsync(250);
            var dataString = reader.ReadString(reader.UnconsumedBufferLength);
            ShowToast(dataString);
            socket.TransferOwnership(socketInformation.Id); /* Important! */
            break;
```

   -   キープアライブ タイマーの有効期限が切れたためにイベントが発生した場合、ソケットをライブに維持してキープアライブ タイマーを再開するには、コードがソケット経由でデータを送信する必要があります。 繰り返しになりますが、イベント通知を今後も受け取るには、ソケットの所有権をソケット ブローカーに戻す必要があります。

```csharp
case SocketActivityTriggerReason.KeepAliveTimerExpired:
            socket = socketInformation.StreamSocket;
            DataWriter writer = new DataWriter(socket.OutputStream);
            writer.WriteBytes(Encoding.UTF8.GetBytes("Keep alive"));
            await writer.StoreAsync();
            writer.DetachStream();
            writer.Dispose();
            socket.TransferOwnership(socketInformation.Id); /* Important! */
            break;
```

   -   ソケットが閉じられたためにイベントが発生した場合、ソケットを再確立します。新しいソケットを作成した後、必ずその所有権をソケット ブローカーに転送します。 次のサンプルでは、新しいソケット接続の確立に使うことができるようにホスト名とポートがローカル設定に保存されています。

```csharp
case SocketActivityTriggerReason.SocketClosed:
            socket = new StreamSocket();
            socket.EnableTransferOwnership(taskInstance.Task.TaskId, SocketActivityConnectedStandbyAction.Wake);
            if (ApplicationData.Current.LocalSettings.Values["hostname"] == null)
            {
                break;
            }
            var hostname = (String)ApplicationData.Current.LocalSettings.Values["hostname"];
            var port = (String)ApplicationData.Current.LocalSettings.Values["port"];
            await socket.ConnectAsync(new HostName(hostname), port);
            socket.TransferOwnership(socketId);
            break;
```

   -   イベント通知の処理を完了したら、必ず保留を終了してください。

```csharp
  deferral.Complete();
```

[  **SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) とソケット ブローカーの使い方を示す詳しいサンプルについては、[SocketActivityStreamSocket のサンプルに関するページ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SocketActivityStreamSocket)をご覧ください。 Scenario1\_Connect.xaml.cs ではソケットの初期化が実行され、SocketActivityTask.cs ではバックグラウンド タスクが実装されます。

サンプルを見ると、新しいソケットが作成されるか、既存のソケットが取得されると、すぐに **TransferOwnership** が呼び出されることがわかります。このトピックで説明したように **OnSuspending** イベント ハンドラーを使って行われるのではありません。 これは、このサンプルが [**SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) の使い方を示すことに重点を置いており、実行中に他のアクティビティにソケットを使っていないためです。 実際のアプリはより複雑と思われるため、**OnSuspending** を使って **TransferOwnership** を呼び出すタイミングを判断してください。

## <a name="control-channel-triggers"></a>コントロール チャネル トリガー
まず、コントロール チャネル トリガー (CCT) を適切に使っていることを確認します。 [**DatagramSocket**](/uwp/api/Windows.Networking.Sockets.DatagramSocket)、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket)、または [**StreamSocketListener**](/uwp/api/Windows.Networking.Sockets.StreamSocketListener) 接続を使っている場合は、[**SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) を使うことをお勧めします。 **StreamSocket** には CCT を使うことができますが、リソースを多く使うため、コネクト スタンバイ モードでは動作しない可能性があります。

WebSocket、[**IXMLHTTPRequest2**](/previous-versions/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2)、[**System.Net.Http.HttpClient**](/uwp/api/Windows.Web.Http.HttpClient)、または [**Windows.Web.Http.HttpClient**](/uwp/api/windows.web.http.httpclient) を使っている場合は、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) を使う必要があります。

## <a name="controlchanneltrigger-with-websockets"></a>ControlChannelTrigger と WebSocket

> [!IMPORTANT]
> このセクションで説明される機能 (**ControlChannelTrigger と WebSockets**) は、10.0.15063.0 およびそれ以前のバージョンの SDK でサポートされています。 また、これはプレリリース バージョンの [Windows 10 Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewSDK) でもサポートされています。

[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket) または [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) を使う場合は、特別な注意事項がいくつかあります。 **ControlChannelTrigger** で **MessageWebSocket** または **StreamWebSocket** を使う際には、トランスポート固有の使用パターンとベスト プラクティスに従う必要があります。 また、**StreamWebSocket** でパケットを受け取る要求の処理方法にも、これらの注意事項が関係します。 **MessageWebSocket** でパケットを受け取るための要求には影響しません。

[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket) または [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) を使う際に従う必要のある使用パターンとベスト プラクティスを次に示します。

-   未処理のソケット受信は、常にポストされ続ける必要があります。 これは、プッシュ通知タスクの実行を許可するために必要です。
-   WebSocket プロトコルで、キープアライブ メッセージの標準モデルを定義します。 [  **WebSocketKeepAlive**](/uwp/api/Windows.Networking.Sockets.WebSocketKeepAlive) クラスは、クライアント側から開始される WebSocket プロトコルのキープアライブ メッセージをサーバーに送信することができます。 **WebSocketKeepAlive** クラスは、アプリによって KeepAliveTrigger の TaskEntryPoint として登録される必要があります。

いくつかの特別な注意事項は、[**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) でパケットを受け取る要求の処理方法にかかわってきます。 特に、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で **StreamWebSocket** を使うアプリは、読み取り処理に、**await** モデル (C# と VB.NET) やタスク (C++) ではなく、生の非同期パターンを使う必要があります。 生の非同期パターンは、このセクションで後述するサンプル コードに示しています。

生の非同期パターンを使うことによって、Windows は、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) のバックグラウンド タスクの [**IBackgroundTask.Run**](/uwp/api/windows.applicationmodel.background.ibackgroundtask.run) メソッドを、受信完了コールバックの戻りと同期させることができます。 **Run** メソッドは、完了コールバックから制御が戻った後に呼び出されます。 これによって、**Run** メソッドが呼び出される前に、アプリはデータ/エラーを確実に受け取ることができます。

アプリは、完了コールバックから制御を戻す前に別の読み取りをポストしなければならない点に注意してください。 また、[**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket) または [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) トランスポートで [**DataReader**](/uwp/api/Windows.Storage.Streams.DataReader) を直接使うことはできません。上で説明した同期に支障をきたします。 トランスポートで直接 [**DataReader.LoadAsync**](/uwp/api/windows.storage.streams.datareader.loadasync) メソッドを使うことはサポートされません。 別の方法として、[**StreamWebSocket.InputStream**](/uwp/api/windows.networking.sockets.streamwebsocket.inputstream) プロパティの [**IInputStream.ReadAsync**](/uwp/api/windows.storage.streams.iinputstream.readasync) メソッドから返された [**IBuffer**](/uwp/api/Windows.Storage.Streams.IBuffer) を後で [**DataReader.FromBuffer**](/uwp/api/windows.storage.streams.datareader.frombuffer) メソッドに渡して処理することはできます。

次のサンプルでは、[**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) の読み取りを生の非同期パターンを使って処理しています。

```csharp
void PostSocketRead(int length)
{
    try
    {
        var readBuf = new Windows.Storage.Streams.Buffer((uint)length);
        var readOp = socket.InputStream.ReadAsync(readBuf, (uint)length, InputStreamOptions.Partial);
        readOp.Completed = (IAsyncOperationWithProgress<IBuffer, uint>
            asyncAction, AsyncStatus asyncStatus) =>
        {
            switch (asyncStatus)
            {
                case AsyncStatus.Completed:
                case AsyncStatus.Error:
                    try
                    {
                        // GetResults in AsyncStatus::Error is called as it throws a user friendly error string.
                        IBuffer localBuf = asyncAction.GetResults();
                        uint bytesRead = localBuf.Length;
                        readPacket = DataReader.FromBuffer(localBuf);
                        OnDataReadCompletion(bytesRead, readPacket);
                    }
                    catch (Exception exp)
                    {
                        Diag.DebugPrint("Read operation failed:  " + exp.Message);
                    }
                    break;
                case AsyncStatus.Canceled:

                    // Read is not cancelled in this sample.
                    break;
           }
       };
   }
   catch (Exception exp)
   {
       Diag.DebugPrint("failed to post a read failed with error:  " + exp.Message);
   }
}
```

[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) のバックグラウンド タスクの [**IBackgroundTask.Run**](/uwp/api/windows.applicationmodel.background.ibackgroundtask.run) メソッドが呼び出される前に確実に読み取り完了ハンドラーが呼び出されます。 Windows は、読み取り完了コールバックからのアプリの復帰を待機する内部的な同期機構を備えています。 通常、アプリは、[**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket) または [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) からのデータやエラーを読み取り完了コールバックですぐに処理します。 メッセージそのものは、**IBackgroundTask.Run** メソッドのコンテキスト内で処理されます。 以下のサンプルでは、この点をメッセージ キューを使って示しています。メッセージは、読み取り完了ハンドラーによってメッセージ キューに挿入され、バックグラウンド タスクによって後から処理されます。

次のサンプルは、[**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) の読み取りを処理するための生の非同期パターンで使う読み取り完了ハンドラーを示しています。

```csharp
public void OnDataReadCompletion(uint bytesRead, DataReader readPacket)
{
    if (readPacket == null)
    {
        Diag.DebugPrint("DataReader is null");

        // Ideally when read completion returns error,
        // apps should be resilient and try to
        // recover if there is an error by posting another recv
        // after creating a new transport, if required.
        return;
    }
    uint buffLen = readPacket.UnconsumedBufferLength;
    Diag.DebugPrint("bytesRead: " + bytesRead + ", unconsumedbufflength: " + buffLen);

    // check if buffLen is 0 and treat that as fatal error.
    if (buffLen == 0)
    {
        Diag.DebugPrint("Received zero bytes from the socket. Server must have closed the connection.");
        Diag.DebugPrint("Try disconnecting and reconnecting to the server");
        return;
    }

    // Perform minimal processing in the completion
    string message = readPacket.ReadString(buffLen);
    Diag.DebugPrint("Received Buffer : " + message);

    // Enqueue the message received to a queue that the push notify
    // task will pick up.
    AppContext.messageQueue.Enqueue(message);

    // Post another receive to ensure future push notifications.
    PostSocketRead(MAX_BUFFER_LENGTH);
}
```

WebSocket に関連して、キープアライブ ハンドラーについても詳しく説明します。 WebSocket プロトコルで、キープアライブ メッセージの標準モデルを定義します。

[  **MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket) または [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) を使う場合、アプリの中断状態を解除し、キープアライブ メッセージをサーバー (リモート エンドポイント) に定期的に送信するためには、[**WebSocketKeepAlive**](/uwp/api/Windows.Networking.Sockets.WebSocketKeepAlive) クラス インスタンスを KeepAliveTrigger の [**TaskEntryPoint**](/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.taskentrypoint) として登録する必要があります。 これは、アプリのバックグラウンド登録コードとパッケージ マニフェストで行う必要があります。

[  **Windows.Sockets.WebSocketKeepAlive**](/uwp/api/Windows.Networking.Sockets.WebSocketKeepAlive) のタスク エントリ ポイントは、次の 2 か所で指定する必要があります。

-   ソース コードで KeepAliveTrigger トリガーを作成する部分 (以下の例を参照)。
-   キープアライブのバックグラウンド タスクが宣言されているアプリ パッケージ マニフェスト。

次のサンプルでは、アプリ マニフェストの &lt;Application&gt; 要素の下に、ネットワーク トリガー通知とキープアライブ トリガーを追加しています。

```xml
  <Extensions>
    <Extension Category="windows.backgroundTasks"
         Executable="$targetnametoken$.exe"
         EntryPoint="Background.PushNotifyTask">
      <BackgroundTasks>
        <Task Type="controlChannel" />
      </BackgroundTasks>
    </Extension>
    <Extension Category="windows.backgroundTasks"
         Executable="$targetnametoken$.exe"
         EntryPoint="Windows.Networking.Sockets.WebSocketKeepAlive">
      <BackgroundTasks>
        <Task Type="controlChannel" />
      </BackgroundTasks>
    </Extension>
  </Extensions>
```

[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) と [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket)、[**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket)、または [**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) に対する非同期操作のコンテキストで **await** ステートメントを使う際には、特に注意する必要があります。 Task**Task&lt;bool&gt;** オブジェクトを使うと、プッシュ通知と WebSocket キープアライブの **ControlChannelTrigger** を **StreamWebSocket** に対して登録し、このトランスポートを接続できます。 この登録の一環として、**StreamWebSocket** トランスポートが **ControlChannelTrigger** のトランスポートとして設定され、読み取りがポストされます。 **Task.Result** は、タスクのすべてのステップが実行されてメッセージ本文でステートメントが返されるまで現在のスレッドをブロックします。 タスクは、このメソッドが true または false を返すまで解決されません。 これにより、メソッド全体が実行されることが保証されます。 **Task** には、**Task** によって保護される **await** ステートメントを複数含めることができます。 **ControlChannelTrigger** オブジェクトで **StreamWebSocket** または **MessageWebSocket** をトランスポートとして使う場合はこのパターンを使う必要があります。 完了までに長時間かかる可能性がある操作 (一般的な非同期読み取り操作など) に対しては、既に説明した生の非同期パターンを使う必要があります。

次のサンプルは、プッシュ通知と WebSocket キープアライブの [**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) を [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) に対して登録します。

```csharp
private bool RegisterWithControlChannelTrigger(string serverUri)
{
    // Make sure the objects are created in a system thread
    // Demonstrate the core registration path
    // Wait for the entire operation to complete before returning from this method.
    // The transport setup routine can be triggered by user control, by network state change
    // or by keepalive task
    Task<bool> registerTask = RegisterWithCCTHelper(serverUri);
    return registerTask.Result;
}

async Task<bool> RegisterWithCCTHelper(string serverUri)
{
    bool result = false;
    socket = new StreamWebSocket();

    // Specify the keepalive interval expected by the server for this app
    // in order of minutes.
    const int serverKeepAliveInterval = 30;

    // Specify the channelId string to differentiate this
    // channel instance from any other channel instance.
    // When background task fires, the channel object is provided
    // as context and the channel id can be used to adapt the behavior
    // of the app as required.
    const string channelId = "channelOne";

    // For websockets, the system does the keepalive on behalf of the app
    // But the app still needs to specify this well known keepalive task.
    // This should be done here in the background registration as well
    // as in the package manifest.
    const string WebSocketKeepAliveTask = "Windows.Networking.Sockets.WebSocketKeepAlive";

    // Try creating the controlchanneltrigger if this has not been already
    // created and stored in the property bag.
    ControlChannelTriggerStatus status;

    // Create the ControlChannelTrigger object and request a hardware slot for this app.
    // If the app is not on LockScreen, then the ControlChannelTrigger constructor will
    // fail right away.
    try
    {
        channel = new ControlChannelTrigger(channelId, serverKeepAliveInterval,
                                   ControlChannelTriggerResourceType.RequestHardwareSlot);
    }
    catch (UnauthorizedAccessException exp)
    {
        Diag.DebugPrint("Is the app on lockscreen? " + exp.Message);
        return result;
    }

    Uri serverUriInstance;
    try
    {
        serverUriInstance = new Uri(serverUri);
    }
    catch (Exception exp)
    {
        Diag.DebugPrint("Error creating URI: " + exp.Message);
        return result;
    }

    // Register the apps background task with the trigger for keepalive.
    var keepAliveBuilder = new BackgroundTaskBuilder();
    keepAliveBuilder.Name = "KeepaliveTaskForChannelOne";
    keepAliveBuilder.TaskEntryPoint = WebSocketKeepAliveTask;
    keepAliveBuilder.SetTrigger(channel.KeepAliveTrigger);
    keepAliveBuilder.Register();

    // Register the apps background task with the trigger for push notification task.
    var pushNotifyBuilder = new BackgroundTaskBuilder();
    pushNotifyBuilder.Name = "PushNotificationTaskForChannelOne";
    pushNotifyBuilder.TaskEntryPoint = "Background.PushNotifyTask";
    pushNotifyBuilder.SetTrigger(channel.PushNotificationTrigger);
    pushNotifyBuilder.Register();

    // Tie the transport method to the ControlChannelTrigger object to push enable it.
    // Note that if the transport' s TCP connection is broken at a later point of time,
    // the ControlChannelTrigger object can be reused to plug in a new transport by
    // calling UsingTransport API again.
    try
    {
        channel.UsingTransport(socket);

        // Connect the socket
        //
        // If connect fails or times out it will throw exception.
        // ConnectAsync can also fail if hardware slot was requested
        // but none are available
        await socket.ConnectAsync(serverUriInstance);

        // Call WaitForPushEnabled API to make sure the TCP connection has
        // been established, which will mean that the OS will have allocated
        // any hardware slot for this TCP connection.
        //
        // In this sample, the ControlChannelTrigger object was created by
        // explicitly requesting a hardware slot.
        //
        // On systems that without connected standby, if app requests hardware slot as above,
        // the system will fallback to a software slot automatically.
        //
        // On systems that support connected standby,, if no hardware slot is available, then app
        // can request a software slot by re-creating the ControlChannelTrigger object.
        status = channel.WaitForPushEnabled();
        if (status != ControlChannelTriggerStatus.HardwareSlotAllocated
            && status != ControlChannelTriggerStatus.SoftwareSlotAllocated)
        {
            throw new Exception(string.Format("Neither hardware nor software slot could be allocated. ChannelStatus is {0}", status.ToString()));
        }

        // Store the objects created in the property bag for later use.
        CoreApplication.Properties.Remove(channel.ControlChannelTriggerId);

        var appContext = new AppContext(this, socket, channel, channel.ControlChannelTriggerId);
        ((IDictionary<string, object>)CoreApplication.Properties).Add(channel.ControlChannelTriggerId, appContext);
        result = true;

        // Almost done. Post a read since we are using streamwebsocket
        // to allow push notifications to be received.
        PostSocketRead(MAX_BUFFER_LENGTH);
    }
    catch (Exception exp)
    {
         Diag.DebugPrint("RegisterWithCCTHelper Task failed with: " + exp.Message);

         // Exceptions may be thrown for example if the application has not
         // registered the background task class id for using real time communications
         // broker in the package manifest.
    }
    return result
}
```

[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket) または [**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) を使う方法について詳しくは、[ControlChannelTrigger StreamWebSocket のサンプルに関するページ](https://github.com/microsoft/VCSamples/tree/master/VC2012Samples/Windows%208%20samples/C%2B%2B/Windows%208%20app%20samples/ControlChannelTrigger%20StreamSocket%20sample%20(Windows%208))をご覧ください。

## <a name="controlchanneltrigger-with-httpclient"></a>ControlChannelTrigger と HttpClient
[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [HttpClient](/dotnet/api/system.net.http.httpclient) を使う場合は、特別な注意事項がいくつかあります。 **ControlChannelTrigger** で [HttpClient](/dotnet/api/system.net.http.httpclient) を使う際には、トランスポート固有の使用パターンとベスト プラクティスに従う必要があります。 また、[HttpClient](/dotnet/api/system.net.http.httpclient) でパケットを受信する要求の処理方法にも、これらの注意事項が関係します。

**注**  SSL を使う   [HttpClient](/dotnet/api/system.net.http.httpclient) では、ネットワーク トリガー機能と [**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) の使用は現在サポートされていません。
 
[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [HttpClient](/dotnet/api/system.net.http.httpclient) を使う際に従う必要のある使用パターンとベスト プラクティスを次に示します。

-   アプリで、特定の URI に要求を送る前に、[System.Net.Http](/dotnet/api/system.net.http) 名前空間の [HttpClient](/dotnet/api/system.net.http.httpclient) オブジェクトまたは [HttpClientHandler](/dotnet/api/system.net.http.httpclienthandler) オブジェクトにさまざまなプロパティやヘッダーを設定する必要がある場合があります。
-   アプリには、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で使う [HttpClient](/dotnet/api/system.net.http.httpclient) トランスポートを作る前に、トランスポートをテストし、正しく設定するための初期要求が必要な場合があります。 トランスポートを正しく設定できることがアプリによって確認されると、[HttpClient](/dotnet/api/system.net.http.httpclient) オブジェクトを **ControlChannelTrigger** オブジェクトで使うトランスポート オブジェクトとして構成できます。 このプロセスは、一部のシナリオでトランスポートを使って確立された接続が中断されないようにするためのものです。 SSL と証明書を使う場合、アプリには、PIN 入力用、または選択する証明書が複数ある場合に表示されるダイアログが必要になる場合があります。 プロキシ認証とサーバー認証が必要になる場合があります。 プロキシ認証またはサーバー認証の期限が切れると、接続が閉じる場合があります。 これらの認証期限の問題に対処する 1 つの方法として、タイマーを設定できます。 HTTP リダイレクトが必要な場合、2 回目の接続は正しく確立できないことがあります。 初期テスト要求により、[HttpClient](/dotnet/api/system.net.http.httpclient) オブジェクトを **ControlChannelTrigger** オブジェクトでトランスポートとして使う前にアプリが最新のリダイレクト URL を使用できることが確認されます。

他のネットワーク トランスポートとは異なり、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) オブジェクトの [**UsingTransport**](/uwp/api/windows.networking.sockets.controlchanneltrigger.usingtransport) メソッドに直接 [HttpClient](/dotnet/api/system.net.http.httpclient) オブジェクトを渡すことはできません。 [HttpClient](/dotnet/api/system.net.http.httpclient) オブジェクトと **ControlChannelTrigger** 用に特別な方法で [HttpRequestMessage](/previous-versions/visualstudio/hh159020(v=vs.118)) オブジェクトを構築する必要があります。 [HttpRequestMessage](/previous-versions/visualstudio/hh159020(v=vs.118)) オブジェクトは、[RtcRequestFactory.Create](/dotnet/api/system.net.http.rtcrequestfactory.create) メソッドを使って作成します。 そのうえで、作成した [HttpRequestMessage](/previous-versions/visualstudio/hh159020(v=vs.118)) オブジェクトを **UsingTransport** メソッドに渡します。

次のサンプルでは、[HttpClient](/dotnet/api/system.net.http.httpclient) オブジェクトと [**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で使う [HttpRequestMessage](/previous-versions/visualstudio/hh159020(v=vs.118)) オブジェクトを構築しています。

```csharp
using System;
using System.Net;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;
using Windows.Networking.Sockets;

public HttpRequestMessage httpRequest;
public HttpClient httpClient;
public HttpRequestMessage httpRequest;
public ControlChannelTrigger channel;
public Uri serverUri;

private void SetupHttpRequestAndSendToHttpServer()
{
    try
    {
        // For HTTP based transports that use the RTC broker, whenever we send next request, we will abort the earlier
        // outstanding http request and start new one.
        // For example in case when http server is taking longer to reply, and keep alive trigger is fired in-between
        // then keep alive task will abort outstanding http request and start a new request which should be finished
        // before next keep alive task is triggered.
        if (httpRequest != null)
        {
            httpRequest.Dispose();
        }

        httpRequest = RtcRequestFactory.Create(HttpMethod.Get, serverUri);

        SendHttpRequest();
    }
        catch (Exception e)
    {
        Diag.DebugPrint("Connect failed with: " + e.ToString());
        throw;
    }
}
```

いくつかの特別な注意事項は、[HttpClient](/dotnet/api/system.net.http.httpclient) で HTTP 要求を送信して応答の受け取りを開始するための要求の処理方法にかかわってきます。 特に、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [HttpClient](/dotnet/api/system.net.http.httpclient) を使うアプリは、送信処理に、**await** モデルではなく、Task を使う必要があります。

[HttpClient](/dotnet/api/system.net.http.httpclient) を使った場合、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) のバックグラウンド タスクの [**IBackgroundTask.Run**](/uwp/api/windows.applicationmodel.background.ibackgroundtask.run) メソッドと、受信完了コールバックの戻りとの同期が生じません。 したがって、アプリは、ブロックする HttpResponseMessage を **Run** メソッドで使い、応答全体を受け取るまで待機するしかありません。

[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) での [HttpClient](/dotnet/api/system.net.http.httpclient) の使用は、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) や [**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket)、[**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) のトランスポートとは大きく異なります。 [HttpClient](/dotnet/api/system.net.http.httpclient) 受信コールバックは、[HttpClient](/dotnet/api/system.net.http.httpclient) コード以後、Task を介してアプリに送られます。 つまり、データまたはエラーがアプリにディスパッチされるとすぐに **ControlChannelTrigger** プッシュ通知タスクが作動します。 以下のサンプル コードは、[HttpClient.SendAsync](/dotnet/api/system.net.http.httpclient) メソッドから返された responseTask をグローバルなストレージに格納します。プッシュ通知タスクがそれを取り出し、インラインで処理します。

次のサンプルは、[HttpClient](/dotnet/api/system.net.http.httpclient) を [**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) と組み合わせて使い、送信要求を処理しています。

```csharp
using System;
using System.Net;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;
using Windows.Networking.Sockets;

private void SendHttpRequest()
{
    if (httpRequest == null)
    {
        throw new Exception("HttpRequest object is null");
    }

    // Tie the transport method to the controlchanneltrigger object to push enable it.
    // Note that if the transport' s TCP connection is broken at a later point of time,
    // the controlchanneltrigger object can be reused to plugin a new transport by
    // calling UsingTransport API again.
    channel.UsingTransport(httpRequest);

    // Call the SendAsync function to kick start the TCP connection establishment
    // process for this http request.
    Task<HttpResponseMessage> httpResponseTask = httpClient.SendAsync(httpRequest);

    // Call WaitForPushEnabled API to make sure the TCP connection has been established,
    // which will mean that the OS will have allocated any hardware slot for this TCP connection.
    ControlChannelTriggerStatus status = channel.WaitForPushEnabled();
    Diag.DebugPrint("WaitForPushEnabled() completed with status: " + status);
    if (status != ControlChannelTriggerStatus.HardwareSlotAllocated
        && status != ControlChannelTriggerStatus.SoftwareSlotAllocated)
    {
        throw new Exception("Hardware/Software slot not allocated");
    }

    // The HttpClient receive callback is delivered via a Task to the app.
    // The notification task will fire as soon as the data or error is dispatched
    // Enqueue the responseTask returned by httpClient.sendAsync
    // into a queue that the push notify task will pick up and process inline.
    AppContext.messageQueue.Enqueue(httpResponseTask);
}
```

次のサンプルは、[HttpClient](/dotnet/api/system.net.http.httpclient) を [**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) と組み合わせて使い、受け取った応答を読み取っています。

```csharp
using System.Net;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;

public string ReadResponse(Task<HttpResponseMessage> httpResponseTask)
{
    string message = null;
    try
    {
        if (httpResponseTask.IsCanceled || httpResponseTask.IsFaulted)
        {
            Diag.DebugPrint("Task is cancelled or has failed");
            return message;
        }
        // We' ll wait until we got the whole response.
        // This is the only supported scenario for HttpClient for ControlChannelTrigger.
        HttpResponseMessage httpResponse = httpResponseTask.Result;
        if (httpResponse == null || httpResponse.Content == null)
        {
            Diag.DebugPrint("Cannot read from httpresponse, as either httpResponse or its content is null. try to reset connection.");
        }
        else
        {
            // This is likely being processed in the context of a background task and so
            // synchronously read the Content' s results inline so that the Toast can be shown.
            // before we exit the Run method.
            message = httpResponse.Content.ReadAsStringAsync().Result;
        }
    }
    catch (Exception exp)
    {
        Diag.DebugPrint("Failed to read from httpresponse with error:  " + exp.ToString());
    }
    return message;
}
```

[HttpClient](/dotnet/api/system.net.http.httpclient) と [**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) を使う方法について詳しくは、[ControlChannelTrigger HttpClient のサンプルに関するページ](https://github.com/microsoft/VCSamples/tree/master/VC2012Samples/Windows%208%20samples/C%2B%2B/Windows%208%20app%20samples/ControlChannelTrigger%20XMLHTTPRequest%20sample%20(Windows%208))をご覧ください。

## <a name="controlchanneltrigger-with-ixmlhttprequest2"></a>ControlChannelTrigger と IXMLHttpRequest2
[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [**IXMLHTTPRequest2**](/previous-versions/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2) を使う場合は、特別な注意事項がいくつかあります。 **ControlChannelTrigger** で **IXMLHTTPRequest2** を使う際には、トランスポート固有の使用パターンとベスト プラクティスに従う必要があります。 **ControlChannelTrigger** の使用が、**IXMLHTTPRequest2** で HTTP 要求を送受信するための要求の処理方法に影響することはありません。

[  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で [**IXMLHTTPRequest2**](/previous-versions/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2) を使う際の使用パターンとベスト プラクティス

-   トランスポートとして使われる [**IXMLHTTPRequest2**](/previous-versions/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2) オブジェクトの有効期限は、1 つの要求/応答のみで構成されます。 [  **ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) オブジェクトと併用する場合は、**ControlChannelTrigger** オブジェクトを一度作って設定してから [**UsingTransport**](/uwp/api/windows.networking.sockets.controlchanneltrigger.usingtransport) メソッドを繰り返し呼び出して、そのたびに新しい **IXMLHTTPRequest2** オブジェクトを関連付けると便利です。 アプリは、新しい **IXMLHTTPRequest2** オブジェクトを提供する前に以前の **IXMLHTTPRequest2** オブジェクトを削除して、割り当てられたリソース制限を超えないようにする必要があります。
-   アプリは、[**Send**](/previous-versions/windows/desktop/api/msxml6/nf-msxml6-ixmlhttprequest2-send) メソッドを呼び出す前に、[**SetProperty**](/previous-versions/windows/desktop/api/msxml6/nf-msxml6-ixmlhttprequest2-setproperty) メソッドと [**SetRequestHeader**](/previous-versions/windows/desktop/api/msxml6/nf-msxml6-ixmlhttprequest2-setrequestheader) メソッドを呼び出して HTTP トランスポートを設定する必要がある場合があります。
-   アプリには、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) で使うトランスポートを作る前に、トランスポートをテストし、正しく設定するための初期 [**Send**](/previous-versions/windows/desktop/api/msxml6/nf-msxml6-ixmlhttprequest2-send) 要求が必要な場合があります。 アプリによってトランスポートが正しく設定されていることが確認されると、[**IXMLHTTPRequest2**](/previous-versions/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2) オブジェクトを **ControlChannelTrigger** で使うトランスポート オブジェクトとして構成できます。 このプロセスは、一部のシナリオでトランスポートを使って確立された接続が中断されないようにするためのものです。 SSL と証明書を使う場合、アプリには、PIN 入力用、または選択する証明書が複数ある場合に表示されるダイアログが必要になる場合があります。 プロキシ認証とサーバー認証が必要になる場合があります。 プロキシ認証またはサーバー認証の期限が切れると、接続が閉じる場合があります。 これらの認証期限の問題に対処する 1 つの方法として、タイマーを設定できます。 HTTP リダイレクトが必要な場合、2 回目の接続は正しく確立できないことがあります。 初期テスト要求により、**IXMLHTTPRequest2** オブジェクトを **ControlChannelTrigger** オブジェクトでトランスポートとして使う前にアプリが最新のリダイレクト URL を使用できることが確認されます。

[  **IXMLHTTPRequest2**](/previous-versions/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2) と [**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) を使う方法について詳しくは、[ControlChannelTrigger と IXMLHTTPRequest2 のサンプルに関するページ](https://github.com/microsoft/VCSamples/tree/master/VC2012Samples/Windows%208%20samples/C%2B%2B/Windows%208%20app%20samples/ControlChannelTrigger%20XMLHTTPRequest%20sample%20(Windows%208))をご覧ください。

## <a name="important-apis"></a>重要な API
* [SocketActivityTrigger](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger)
* [ControlChannelTrigger](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger)