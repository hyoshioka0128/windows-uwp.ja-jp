---
description: ネットワーク機能要素の追加、認証の提供、セキュリティで保護された接続の提供により、アプリでネットワークを使用できるようにする方法について説明します。
title: ネットワークの基本
ms.assetid: 1F47D33B-6F00-4F74-A52D-538851FD38BE
ms.date: 06/01/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 42c82b8cfdfca3287b8943760ef0b47180425af4
ms.sourcegitcommit: 5481bb34def681bc60fbfa42d9779053febec468
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304594"
---
# <a name="networking-basics"></a>ネットワークの基本
ネットワーク対応アプリで実行する必要がある事柄について説明します。

## <a name="capabilities"></a>機能
ネットワークを使うには、アプリ マニフェストに適切な機能要素を追加する必要があります。 アプリ マニフェストにネットワーク機能が指定されていない場合、アプリはネットワーク機能を持たないため、ネットワークへの接続は失敗します。

最もよく使われるネットワーク機能を次に示します。

| 機能 | 説明 |
|------------|-------------|
| **internetClient** | インターネットや、公共の場所のネットワーク (空港、喫茶店など) への出力方向のアクセスを提供します。 インターネットにアクセスする必要があるほとんどのアプリは、この機能を使います。 |
| **internetClientServer** | インターネットや、公共の場所のネットワーク (空港、喫茶店など) からの入力方向と出力方向のネットワーク アクセスをアプリに提供します。 |
| **privateNetworkClientServer** | ユーザーの信頼する場所 (自宅、職場など) において、入力方向と出力方向のネットワーク アクセスをアプリに提供します。 |

特定の状況では、上記以外の機能がアプリで必要になることがあります。

| 機能 | 説明 |
|------------|-------------|
| **enterpriseAuthentication** | ドメイン資格情報を必要とするネットワーク リソースにアプリが接続できるようにします。 たとえば、プライベート イントラネットの SharePoint サーバーからデータを取得するアプリが該当します。 この機能を使うと、資格情報を必要とするネットワーク上のリソースに、自分の資格情報を使ってアクセスすることができます。 この機能を持ったアプリは、ネットワーク上でユーザーを偽装することができます。 認証プロキシ経由でのインターネットへのアクセスをアプリに許可する手段として、この機能は必要ありません。<br/><br/>詳細については、[制限付き機能](../packaging/app-capability-declarations.md#restricted-capabilities)の *Enterprise* 機能のシナリオについてのドキュメントを参照してください。 |
| **proximity** | コンピューターときわめて近い場所にあるデバイスとの近距離近接通信で必要となります。 近距離近接通信は、近くのデバイス上のアプリケーションに接続したりデータを送ったりするときに使われます。 <br/><br/> この機能を有効にすると、アプリは、ユーザーの同意に基づいて相手を招待したり招待に応じたりしながら、ネットワークにアクセスし、きわめて近い場所にあるデバイスに接続することができます。 |
| **sharedUserCertificates** | ソフトウェア証明書とハードウェア証明書 (スマート カード証明書など) にアプリがアクセスできるようにします。 この機能が実行時に呼び出されると、ユーザーは、カードの挿入や証明書の選択などの行動をとる必要があります。 <br/><br/> この機能では、ソフトウェア証明書やハードウェア証明書、スマート カードが、アプリでの身分証明に使われます。 この機能は、企業や銀行、行政サービスで身分証明に使うことができます。 |

## <a name="communicating-when-your-app-is-not-in-the-foreground"></a>アプリがフォア グラウンドにないときの通信
「[バックグラウンド タスクによるアプリのサポート](../launch-resume/support-your-app-with-background-tasks.md)」には、アプリがフォアグラウンドでないときにバックグラウンド タスクを使って処理を実行する方法に関する一般的な情報が含まれています。 具体的には、アプリがフォアグラウンド アプリでないときにネットワーク経由でそのアプリのデータが到着した場合は、到着通知を受け取るための特別な手順のコードを実行する必要があります。 Windows 8 では、このためにコントロール チャネル トリガーを使っていました。これらのトリガーは、Windows 10 でも引き続きサポートされます。 コントロール チャネル トリガーの使い方について詳しくは[**ここ**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger)をご覧ください。 Windows 10 の新しいテクノロジでは、プッシュ対応ストリーム ソケットなどのいくつかのシナリオでオーバーヘッドが小さい優れた機能であるソケット ブローカーとソケット アクティビティ トリガーを利用できます。

アプリで [**DatagramSocket**](/uwp/api/Windows.Networking.Sockets.DatagramSocket)、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket)、または [**StreamSocketListener**](/uwp/api/Windows.Networking.Sockets.StreamSocketListener) を使っている場合は、開いているソケットの所有権をシステムが提供するソケット ブローカーに移譲した後、フォアグラウンドから離れるか、アプリを終了できます。 移譲されたソケットで接続が行われるか、そのソケットでトラフィックが到着すると、アプリまたは指定されたバックグラウンド タスクがアクティブ化します。 アプリが実行されていない場合は、開始されます。 その後、ソケット ブローカーは、[**SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) を使って、新しいトラフィックが到着していることをアプリに通知します。 アプリは、ソケット ブローカーからソケットを取り戻し、そのソケットのトラフィックを処理します。 つまり、アプリがネットワーク トラフィックをアクティブに処理していないときに消費するシステム リソースが非常に少なくなります。

ソケット ブローカーはコントロール チャネル トリガーと同じ機能を少ない制限と小さなメモリ使用量で提供するため、ソケット ブローカーの目的は、適切な場所でコントロール チャネル トリガーと交代することです。 ソケット ブローカーは、ロック画面に表示するアプリ以外のアプリで使うことができ、電話でも他のデバイスと同じように使うことができます。 ソケット ブローカーによってアクティブ化するために、トラフィックの到着時にアプリが実行されている必要はありません。 さらに、ソケット ブローカーは、TCP ソケットでのリッスンをサポートします。これはコントロール チャネル トリガーではサポートされていません。

### <a name="choosing-a-network-trigger"></a>ネットワーク トリガーの選択
どちらの種類のトリガーが適しているかを判断するいくつかのシナリオがあります。 アプリで使うトリガーの種類を選択するときは、次のアドバイスを検討してください。

-   [  **IXMLHTTPRequest2**](/previous-versions/windows/desktop/api/msxml6/nn-msxml6-ixmlhttprequest2)、[**System.Net.Http.HttpClient**](/uwp/api/Windows.Web.Http.HttpClient)、または [System.Net.Http.HttpClientHandler](/dotnet/api/system.net.http.httpclienthandler) を使う場合は、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) を使う必要があります。
-   プッシュ対応 **StreamSockets** を使っている場合、コントロール チャネル トリガーを使うことができますが、[**SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) をお勧めします。 後者を選ぶと、接続がアクティブに使われていない場合は、システムによってメモリが解放され、電力要件が低減されます。
-   アプリがネットワーク要求をアクティブに処理していないときのメモリ使用量をできる限り少なくする場合は、可能な限り [**SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) をお勧めします。
-   システムがコネクト スタンバイ モードにあるときにアプリがデータを受信できるようにする場合は、[**SocketActivityTrigger**](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger) を使います。

ソケット ブローカーの使い方の説明と例については、「[バックグラウンドでのネットワーク通信](network-communications-in-the-background.md)」をご覧ください。

## <a name="secured-connections"></a>セキュリティ保護された接続
Secure Sockets Layer (SSL) とより新しいトランスポート層セキュリティ (TLS) は、ネットワーク通信の認証と暗号化を実現するように設計された暗号化プロトコルです。 これらのプロトコルは、ネットワーク データの送受信時に傍受や改ざんを防ぐように設計されています。 これらのプロトコルでは、クライアント/サーバー モデルを使ってプロトコル交換が行われます。 また、デジタル証明書と証明機関を使って、サーバーが本物であることが確認されます。

### <a name="creating-secure-socket-connections"></a>セキュリティが確保されたソケット接続の作成
[  **StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) オブジェクトは、クライアントとサーバー間の通信に SSL/TLS を使うように構成できます。 この SSL/TLS のサポートは、SSL/TLS ネゴシエーションで **StreamSocket** オブジェクトをクライアントとして使うことに制限されます。 サーバーとしての SSL/TLS ネゴシエーションは **StreamSocket** クラスで実装されていないため、着信接続を受信したときに [**StreamSocketListener**](/uwp/api/Windows.Networking.Sockets.StreamSocketListener) によって作成された **StreamSocket** と共に SSL/TLS を使うことはできません。

[  **StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) 接続のセキュリティを確保するには 2 つの方法があります。

-   [**ConnectAsync**](/uwp/api/windows.networking.sockets.streamsocket.connectasync) - ネットワーク サービスへの最初の接続を確立してすぐに、すべての通信で SSL/TLS を使うようにネゴシエートします。
-   [**UpgradeToSslAsync**](/uwp/api/windows.networking.sockets.streamsocket.upgradetosslasync) - 最初に暗号化なしでネットワーク サービスに接続します。 アプリでデータが送受信される場合があります。 その後、以降のすべての通信で SSL/TLS を使うように接続をアップグレードします。

SocketProtectionLevel は、アプリが接続を確立またはアップグレードする際に必要なソケット保護レベルを指定します。 ただし、確立される接続の最終的な保護レベルは接続の両方のエンドポイント間のネゴシエーション プロセスで決まります。 指定した保護レベルは、相手のエンドポイントでより低いレベルが要求されている場合、より低くなることがあります。 

 非同期操作が正常に完了した後、[**ConnectAsync**](/uwp/api/windows.networking.sockets.streamsocket.connectasync) または [**UpgradeToSslAsync**](/uwp/api/windows.networking.sockets.streamsocket.upgradetosslasync) の呼び出しで要求された保護レベルは、[**StreamSocketinformation.ProtectionLevel**](/uwp/api/windows.networking.sockets.streamsocketinformation.protectionlevel) プロパティで取得できます。 ただし、これは接続で実際に使用されている保護レベルを反映していません。

> [!NOTE]
> コードでは、特定の保護レベルの使用に暗黙的に依存しないように、つまり特定のセキュリティ レベルの既定での使用を前提にしないようにしてください。 セキュリティ環境は変わり続けており、プロトコルと既定の保護レベルは、既知の弱点のあるプロトコルの使用を避けるように、刻々と変更されています。 既定値は、個々のコンピューターの構成、つまりインストールされているソフトウェアや適用されているパッチによって異なることがあります。 アプリが特定のセキュリティ レベルの使用に依存する場合は、明示的にそのレベルを指定したうえで、実際にそのレベルを使って接続が確立されたことを確認する必要があります。

### <a name="use-connectasync"></a>ConnectAsync の使用
[**ConnectAsync**](/uwp/api/windows.networking.sockets.streamsocket.connectasync) は、ネットワーク サービスへの最初の接続を確立して、すぐにすべての通信で SSL/TLS を使うようにネゴシエートするのに使えます。 *protectionLevel* パラメーターを渡すことができる **ConnectAsync** メソッドは 2 つあります。

-   [**ConnectAsync(EndpointPair, SocketProtectionLevel)** ](/uwp/api/windows.networking.sockets.streamsocket.connectasync) - [**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) オブジェクトで、[**EndpointPair**](/uwp/api/Windows.Networking.EndpointPair) オブジェクトと [**SocketProtectionLevel**](/uwp/api/Windows.Networking.Sockets.SocketProtectionLevel) で指定したリモート ネットワークの宛先に接続する非同期操作を開始します。
-   [**ConnectAsync(HostName, String, SocketProtectionLevel)** ](/uwp/api/windows.networking.sockets.streamsocket.connectasync) - [**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) オブジェクトで、リモート ホスト名、リモート サービス名、[**SocketProtectionLevel**](/uwp/api/Windows.Networking.Sockets.SocketProtectionLevel) で指定したリモートの宛先に接続する非同期操作を開始します。

先ほどのいずれかの [**ConnectAsync**](/uwp/api/windows.networking.sockets.streamsocket.connectasync) メソッドを呼び出すときに *protectionLevel* パラメーターが **Windows.Networking.Sockets.SocketProtectionLevel.Ssl** に設定されていると、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) による通信の暗号化に SSL/TLS を使う必要があります。 この値を指定すると暗号化が必要になり、NULL 暗号を使うことはできません。

これらの [**ConnectAsync**](/uwp/api/windows.networking.sockets.streamsocket.connectasync) メソッドで使う一般的な手順は同じです。

-   [  **StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) を作成します。
-   ソケットの詳細オプションが必要な場合は、[**StreamSocket.Control**](/uwp/api/windows.networking.sockets.streamsocket.control) プロパティを使って、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) オブジェクトに関連付けられている [**StreamSocketControl**](/uwp/api/Windows.Networking.Sockets.StreamSocketControl) インスタンスを取得します。 **StreamSocketControl** のプロパティを設定します。
-   上記のいずれかの [**ConnectAsync**](/uwp/api/windows.networking.sockets.streamsocket.connectasync) メソッドを呼び出し、リモートの宛先に接続する操作を開始してすぐに、SSL/TLS の使用をネゴシエートします。
-   [  **ConnectAsync**](/uwp/api/windows.networking.sockets.streamsocket.connectasync) を使って実際にネゴシエートされる SSL の強度は、非同期操作の成功後に取得される [**StreamSocketinformation.ProtectionLevel**](/uwp/api/windows.networking.sockets.streamsocketinformation.protectionlevel) プロパティによって決まります。

次の例では、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) を作り、ネットワーク サービスへの接続を確立してすぐに、SSL/TLS を使うようにネゴシエートします。 ネゴシエーションに成功すると、クライアントとネットワーク サーバー間で **StreamSocket** を使うすべてのネットワーク通信が暗号化されます。

```csharp
using Windows.Networking;
using Windows.Networking.Sockets;

    // Define some variables and set values
    StreamSocket clientSocket = new StreamSocket();
     
    HostName serverHost = new HostName("www.contoso.com");
    string serverServiceName = "https";
    
    // For simplicity, the sample omits implementation of the
    // NotifyUser method used to display status and error messages 
    
    // Try to connect to contoso using HTTPS (port 443)
    try {

        // Call ConnectAsync method with SSL
        await clientSocket.ConnectAsync(serverHost, serverServiceName, SocketProtectionLevel.Ssl);

        NotifyUser("Connected");
    }
    catch (Exception exception) {
        // If this is an unknown status it means that the error is fatal and retry will likely fail.
        if (SocketError.GetStatus(exception.HResult) == SocketErrorStatus.Unknown) {
            throw;
        }
        
        NotifyUser("Connect failed with error: " + exception.Message);
        // Could retry the connection, but for this simple example
        // just close the socket.
        
        clientSocket.Dispose();
        clientSocket = null; 
    }
           
    // Add code to send and receive data using the clientSocket
    // and then close the clientSocket
```

```cppwinrt
#include <winrt/Windows.Networking.Sockets.h>

using namespace winrt;
...
    // Define some variables, and set values.
    Windows::Networking::Sockets::StreamSocket clientSocket;

    Windows::Networking::HostName serverHost{ L"www.contoso.com" };
    winrt::hstring serverServiceName{ L"https" };

    // For simplicity, the sample omits implementation of the
    // NotifyUser method used to display status and error messages.

    // Try to connect to the server using HTTPS and SSL (port 443).
    try
    {
        co_await clientSocket.ConnectAsync(serverHost, serverServiceName, Windows::Networking::Sockets::SocketProtectionLevel::Tls12);
        NotifyUser(L"Connected");
    }
    catch (winrt::hresult_error const& exception)
    {
        NotifyUser(L"Connect failed with error: " + exception.message());
        clientSocket = nullptr;
    }
    // Add code to send and receive data using the clientSocket,
    // then set the clientSocket to nullptr when done to close it.
```

```cpp
using Windows::Networking;
using Windows::Networking::Sockets;

    // Define some variables and set values
    StreamSocket^ clientSocket = new ref StreamSocket();
 
    HostName^ serverHost = new ref HostName("www.contoso.com");
    String serverServiceName = "https";

    // For simplicity, the sample omits implementation of the
    // NotifyUser method used to display status and error messages 

    // Try to connect to the server using HTTPS and SSL (port 443)
    task<void>(clientSocket->ConnectAsync(serverHost, serverServiceName, SocketProtectionLevel::SSL)).then([this] (task<void> previousTask) {
        try
        {
            // Try getting all exceptions from the continuation chain above this point.
            previousTask.Get();
            NotifyUser("Connected");
        }
        catch (Exception^ exception)
        {
            NotifyUser("Connect failed with error: " + exception->Message);
            
            clientSocket.Close();
            clientSocket = null;
        }
    });
    // Add code to send and receive data using the clientSocket
    // Then close the clientSocket when done
```

### <a name="use-upgradetosslasync"></a>UpgradeToSslAsync の使用
コードで [**UpgradeToSslAsync**](/uwp/api/windows.networking.sockets.streamsocket.upgradetosslasync) を使うときは、ネットワーク サービスへの最初の接続を暗号化なしで確立します。 アプリでデータが送受信される可能性があるため、以降のすべての通信で SSL/TLS を使うように接続をアップグレードします。

[  **UpgradeToSslAsync**](/uwp/api/windows.networking.sockets.streamsocket.upgradetosslasync) メソッドは 2 つのパラメーターを受け取ります。 *protectionLevel* パラメーターは、目的の保護レベルを示します。 *validationHostName* パラメーターは、SSL へのアップグレード時の検証に使われるリモート ネットワークの宛先のホスト名です。 通常、*validationHostName* は、アプリが最初に接続を確立するときに使ったホスト名と同じです。 **UpgradeToSslAsync** を呼び出すときに *protectionLevel* パラメーターが **Windows.System.Socket.SocketProtectionLevel.Ssl** に設定されていると、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) による以降の通信の暗号化に SSL/TLS を使う必要があります。 この値を指定すると暗号化が必要になり、NULL 暗号を使うことはできません。

[  **UpgradeToSslAsync**](/uwp/api/windows.networking.sockets.streamsocket.upgradetosslasync) メソッドで使う一般的な手順は次のとおりです。

-   [  **StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) を作成します。
-   ソケットの詳細オプションが必要な場合は、[**StreamSocket.Control**](/uwp/api/windows.networking.sockets.streamsocket.control) プロパティを使って、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) オブジェクトに関連付けられている [**StreamSocketControl**](/uwp/api/Windows.Networking.Sockets.StreamSocketControl) インスタンスを取得します。 **StreamSocketControl** のプロパティを設定します。
-   データを暗号化せずに送受信する必要がある場合は、ここで送信します。
-   [  **UpgradeToSslAsync**](/uwp/api/windows.networking.sockets.streamsocket.upgradetosslasync) メソッドを呼び出して、SSL/TLS を使うように接続をアップグレードする操作を開始します。
-   [  **UpgradeToSslAsync**](/uwp/api/windows.networking.sockets.streamsocket.upgradetosslasync) を使って実際にネゴシエートされる SSL の強度は、非同期操作の成功後に取得される [**StreamSocketinformation.ProtectionLevel**](/uwp/api/windows.networking.sockets.streamsocketinformation.protectionlevel) プロパティによって決まります。

次の例では、[**StreamSocket**](/uwp/api/Windows.Networking.Sockets.StreamSocket) を作り、ネットワーク サービスへの接続を確立して最初のデータを送って、SSL/TLS を使うようにネゴシエートします。 ネゴシエーションに成功すると、クライアントとネットワーク サーバー間で **StreamSocket** を使うすべてのネットワーク通信が暗号化されます。

```csharp
using Windows.Networking;
using Windows.Networking.Sockets;
using Windows.Storage.Streams;

    // Define some variables and set values
    StreamSocket clientSocket = new StreamSocket();
 
    HostName serverHost = new HostName("www.contoso.com");
    string serverServiceName = "http";

    // For simplicity, the sample omits implementation of the
    // NotifyUser method used to display status and error messages 

    // Try to connect to contoso using HTTP (port 80)
    try {
        // Call ConnectAsync method with a plain socket
        await clientSocket.ConnectAsync(serverHost, serverServiceName, SocketProtectionLevel.PlainSocket);

        NotifyUser("Connected");

    }
    catch (Exception exception) {
        // If this is an unknown status it means that the error is fatal and retry will likely fail.
        if (SocketError.GetStatus(exception.HResult) == SocketErrorStatus.Unknown) {
            throw;
        }

        NotifyUser("Connect failed with error: " + exception.Message, NotifyType.ErrorMessage);
        // Could retry the connection, but for this simple example
        // just close the socket.

        clientSocket.Dispose();
        clientSocket = null; 
        return;
    }

    // Now try to send some data
    DataWriter writer = new DataWriter(clientSocket.OutputStream);
    string hello = "Hello, World! ☺ ";
    Int32 len = (int) writer.MeasureString(hello); // Gets the UTF-8 string length.
    writer.WriteInt32(len);
    writer.WriteString(hello);
    NotifyUser("Client: sending hello");

    try {
        // Call StoreAsync method to store the hello message
        await writer.StoreAsync();

        NotifyUser("Client: sent data");

        writer.DetachStream(); // Detach stream, if not, DataWriter destructor will close it.
    }
    catch (Exception exception) {
        NotifyUser("Store failed with error: " + exception.Message);
        // Could retry the store, but for this simple example
            // just close the socket.

            clientSocket.Dispose();
            clientSocket = null; 
            return;
    }

    // Now upgrade the client to use SSL
    try {
        // Try to upgrade to SSL
        await clientSocket.UpgradeToSslAsync(SocketProtectionLevel.Ssl, serverHost);

        NotifyUser("Client: upgrade to SSL completed");
           
        // Add code to send and receive data 
        // The close clientSocket when done
    }
    catch (Exception exception) {
        // If this is an unknown status it means that the error is fatal and retry will likely fail.
        if (SocketError.GetStatus(exception.HResult) == SocketErrorStatus.Unknown) {
            throw;
        }

        NotifyUser("Upgrade to SSL failed with error: " + exception.Message);

        clientSocket.Dispose();
        clientSocket = null; 
        return;
    }
```

```cppwinrt
#include <winrt/Windows.Networking.Sockets.h>
#include <winrt/Windows.Storage.Streams.h>

using namespace winrt;
using namespace Windows::Storage::Streams;
...
    // Define some variables, and set values.
    Windows::Networking::Sockets::StreamSocket clientSocket;

    Windows::Networking::HostName serverHost{ L"www.contoso.com" };
    winrt::hstring serverServiceName{ L"https" };

    // For simplicity, the sample omits implementation of the
    // NotifyUser method used to display status and error messages. 

    // Try to connect to the server using HTTP (port 80).
    try
    {
        co_await clientSocket.ConnectAsync(serverHost, serverServiceName, Windows::Networking::Sockets::SocketProtectionLevel::PlainSocket);
        NotifyUser(L"Connected");
    }
    catch (winrt::hresult_error const& exception)
    {
        NotifyUser(L"Connect failed with error: " + exception.message());
        clientSocket = nullptr;
    }

    // Now, try to send some data.
    DataWriter writer{ clientSocket.OutputStream() };
    winrt::hstring hello{ L"Hello, World! ☺ " };
    uint32_t len{ writer.MeasureString(hello) }; // Gets the size of the string, in bytes.
    writer.WriteInt32(len);
    writer.WriteString(hello);
    NotifyUser(L"Client: sending hello");

    try
    {
        co_await writer.StoreAsync();
        NotifyUser(L"Client: sent hello");

        writer.DetachStream(); // Detach the stream when you want to continue using it; otherwise, the DataWriter destructor closes it.
    }
    catch (winrt::hresult_error const& exception)
    {
        NotifyUser(L"Store failed with error: " + exception.message());
        // We could retry the store operation. But, for this simple example, just close the socket by setting it to nullptr.
        clientSocket = nullptr;
        co_return;
    }

    // Now, upgrade the client to use SSL.
    try
    {
        co_await clientSocket.UpgradeToSslAsync(Windows::Networking::Sockets::SocketProtectionLevel::Tls12, serverHost);
        NotifyUser(L"Client: upgrade to SSL completed");

        // Add code to send and receive data using the clientSocket,
        // then set the clientSocket to nullptr when done to close it.
    }
    catch (winrt::hresult_error const& exception)
    {
        // If this is an unknown status, then the error is fatal and retry will likely fail.
        Windows::Networking::Sockets::SocketErrorStatus socketErrorStatus{ Windows::Networking::Sockets::SocketError::GetStatus(exception.to_abi()) };
        if (socketErrorStatus == Windows::Networking::Sockets::SocketErrorStatus::Unknown)
        {
            throw;
        }

        NotifyUser(L"Upgrade to SSL failed with error: " + exception.message());
        // We could retry the store operation. But for this simple example, just close the socket by setting it to nullptr.
        clientSocket = nullptr;
        co_return;
    }
```

```cpp
using Windows::Networking;
using Windows::Networking::Sockets;
using Windows::Storage::Streams;

    // Define some variables and set values
    StreamSocket^ clientSocket = new ref StreamSocket();
 
    Hostname^ serverHost = new ref HostName("www.contoso.com");
    String serverServiceName = "http";

    // For simplicity, the sample omits implementation of the
    // NotifyUser method used to display status and error messages 

    // Try to connect to contoso using HTTP (port 80)
    task<void>(clientSocket->ConnectAsync(serverHost, serverServiceName, SocketProtectionLevel::PlainSocket)).then([this] (task<void> previousTask) {
        try
        {
            // Try getting all exceptions from the continuation chain above this point.
            previousTask.Get();
            NotifyUser("Connected");
        }
        catch (Exception^ exception)
        {
            NotifyUser("Connect failed with error: " + exception->Message);
 
            clientSocket->Close();
            clientSocket = null;
        }
    });
       
    // Now try to send some data
    DataWriter^ writer = new ref DataWriter(clientSocket.OutputStream);
    String hello = "Hello, World! ☺ ";
    Int32 len = (int) writer->MeasureString(hello); // Gets the UTF-8 string length.
    writer->writeInt32(len);
    writer->writeString(hello);
    NotifyUser("Client: sending hello");

    task<void>(writer->StoreAsync()).then([this] (task<void> previousTask) {
        try {
            // Try getting all exceptions from the continuation chain above this point.
            previousTask.Get();

            NotifyUser("Client: sent hello");

            writer->DetachStream(); // Detach stream, if not, DataWriter destructor will close it.
       }
       catch (Exception^ exception) {
               NotifyUser("Store failed with error: " + exception->Message);
               // Could retry the store, but for this simple example
               // just close the socket.
 
               clientSocket->Close();
               clientSocket = null;
               return
       }
    });

    // Now upgrade the client to use SSL
    task<void>(clientSocket->UpgradeToSslAsync(clientSocket.SocketProtectionLevel.Ssl, serverHost)).then([this] (task<void> previousTask) {
        try {
            // Try getting all exceptions from the continuation chain above this point.
            previousTask.Get();

           NotifyUser("Client: upgrade to SSL completed");
           
           // Add code to send and receive data 
           // Then close clientSocket when done
        }
        catch (Exception^ exception) {
            // If this is an unknown status it means that the error is fatal and retry will likely fail.
            if (SocketError.GetStatus(exception.HResult) == SocketErrorStatus.Unknown) {
                throw;
            }

            NotifyUser("Upgrade to SSL failed with error: " + exception.Message);

            clientSocket->Close();
            clientSocket = null; 
            return;
        }
    });
```

### <a name="creating-secure-websocket-connections"></a>セキュリティが確保された WebSocket 接続の作成
従来のソケット接続と同様に、[**StreamWebSocket**](/uwp/api/Windows.Networking.Sockets.StreamWebSocket) と [**MessageWebSocket**](/uwp/api/Windows.Networking.Sockets.MessageWebSocket) の機能を UWP アプリで使う際に、トランスポート層セキュリティ (TLS)/Secure Sockets Layer (SSL) を使って WebSocket 接続を暗号化することもできます。 ほとんどの場合、WebSocket 接続にはセキュリティを確保する必要があります。 多くのプロキシは、暗号化されていない WebSocket 接続を拒否するため、接続の成功率が高くなります。

セキュリティが確保されたソケット接続を作成したりネットワーク サービスへとアップグレードする方法の例については、「[TLS/SSL を使って WebSocket 接続のセキュリティを確保する方法](/previous-versions/windows/apps/hh994399(v=win.10))」をご覧ください。

最初のハンドシェークを完了するために、サーバーでは TLS/SSL 暗号化だけでなく **Sec-WebSocket-Protocol** ヘッダー値を要求することもあります。 この値は [**StreamWebSocketInformation.Protocol**](/uwp/api/windows.networking.sockets.streamwebsocketinformation.protocol) プロパティと [**MessageWebSocketInformation.Protocol**](/uwp/api/windows.networking.sockets.messagewebsocketinformation.protocol) プロパティで表され、接続のプロトコル バージョンを示し、開いているハンドシェークとその後に交換されるデータをサーバーが正しく解釈できるようにします。 このプロトコル情報を使うと、サーバーが着信するデータを安全な方法で解釈できないような状況になったときに、接続を閉じることができます。

クライアントからの最初の要求にこの値が含まれていない場合、または含まれている値がサーバーで想定されるものと一致しない場合は、WebSocket ハンドシェーク エラーでサーバーから想定される値がクライアントに送信されます。

## <a name="authentication"></a>認証
ネットワーク経由で接続するときに、認証資格情報を提供する方法。

### <a name="providing-a-client-certificate-with-the-streamsocket-class"></a>StreamSocket クラスによるクライアント証明書の提供
[**Windows.Networking.Sockets.StreamSocket**](/uwp/api/windows.networking.sockets.streamsocket) クラスは、SSL/TLS を使ったアプリの接続先サーバーの認証をサポートします。 場合によっては、アプリは、TLS クライアント証明書を使って自身をサーバーに対して認証する必要があります。 Windows 10 では、クライアント証明書を [**StreamSocket.Control**](/uwp/api/Windows.Networking.Sockets.StreamSocketControl) オブジェクトに提供できます (これは TLS ハンドシェイクが開始される前に設定する必要があります)。 サーバーがクライアント証明書を要求した場合、Windows が提供された証明書を使って応答します。

これを実装する方法を示すコード スニペットを次に示します。

```csharp
var socket = new StreamSocket();
Windows.Security.Cryptography.Certificates.Certificate certificate = await GetClientCert();
socket.Control.ClientCertificate = certificate;
await socket.ConnectAsync(destination, SocketProtectionLevel.Tls12);
```

### <a name="providing-authentication-credentials-to-a-web-service"></a>Web サービスへの認証資格情報の提供
Networking API は、セキュリティが確保された Web サービスとアプリが連携できるようにします。この API のそれぞれが、サーバーとプロキシの認証資格情報を使ってクライアントの初期化または要求ヘッダーの設定を行う独自のメソッドを提供します。 各メソッドは、[**PasswordCredential**](/uwp/api/Windows.Security.Credentials.PasswordCredential) オブジェクトを使って設定されます。このオブジェクトは、ユーザー名、パスワード、それぞれの資格情報が使われるリソースを示します。 次の表では、これらの API のマッピングについて説明します。

| **WebSocket** | [**MessageWebSocketControl.ServerCredential**](/uwp/api/windows.networking.sockets.messagewebsocketcontrol.servercredential) |
|-------------------------|----------------------------------------------------------------------------------------------------------|
|  | [**MessageWebSocketControl.ProxyCredential**](/uwp/api/windows.networking.sockets.messagewebsocketcontrol.proxycredential) |
|  | [**StreamWebSocketControl.ServerCredential**](/uwp/api/windows.networking.sockets.streamwebsocketcontrol.servercredential) |
|  | [**StreamWebSocketControl.ProxyCredential**](/uwp/api/windows.networking.sockets.streamwebsocketcontrol.proxycredential) |
| **バックグラウンド転送** | [**BackgroundDownloader.ServerCredential**](/uwp/api/windows.networking.backgroundtransfer.backgrounddownloader.servercredential) |
|  | [**BackgroundDownloader.ProxyCredential**](/uwp/api/windows.networking.backgroundtransfer.backgrounddownloader.proxycredential) |
|  | [**BackgroundUploader.ServerCredential**](/uwp/api/windows.networking.backgroundtransfer.backgrounduploader.servercredential) |
|  | [**BackgroundUploader.ProxyCredential**](/uwp/api/windows.networking.backgroundtransfer.backgrounduploader.proxycredential) |
| **配信** | [**SyndicationClient(PasswordCredential)** ](/uwp/api/windows.web.syndication.syndicationclient.-ctor#Windows_Web_Syndication_SyndicationClient__ctor_Windows_Security_Credentials_PasswordCredential_) |
|  | [**SyndicationClient.ServerCredential**](/uwp/api/windows.web.syndication.syndicationclient.servercredential) |
|  | [**SyndicationClient.ProxyCredential**](/uwp/api/windows.web.syndication.syndicationclient.proxycredential) |
| **AtomPub** | [**AtomPubClient(PasswordCredential)** ](/uwp/api/windows.web.atompub.atompubclient.-ctor#Windows_Web_AtomPub_AtomPubClient__ctor_Windows_Security_Credentials_PasswordCredential_) |
|  | [**AtomPubClient.ServerCredential**](/uwp/api/windows.web.atompub.atompubclient.servercredential) |
|  | [**AtomPubClient.ProxyCredential**](/uwp/api/windows.web.atompub.atompubclient.proxycredential) |

## <a name="handling-network-exceptions"></a>ネットワーク例外を処理する
ほとんどのプログラミング領域では、例外は、プログラムの不具合によって発生した重大な問題やエラーを示します。 ネットワーク プログラミングでは、さらに、ネットワークそのものとネットワーク通信の特性という、例外の発生源があります。 ネットワーク通信は、本質的に信頼性が低く、予期しない障害が発生する傾向があります。 アプリでネットワークを使う方法のそれぞれについて、状態情報を維持する必要があります。アプリのコードは、その状態情報を更新し、通信エラーが発生したときに接続を再び確立するか再試行する適切なロジックを開始することで、ネットワーク例外を処理する必要があります。

ユニバーサル Windows アプリで例外がスローされると、例外ハンドラーは例外の原因についての詳しい情報を取得することでエラーの内容を理解して適切な判断を下すことができます。

各言語のプロジェクションは、この詳しい情報にアクセスするためのメソッドをサポートしています。 例外は、ユニバーサル Windows アプリの **HRESULT** 値としてプロジェクションされます。 *Winerror.h* インクルード ファイルには、ネットワーク エラーを含む、出力される可能性がある **HRESULT** 値の大きなリストが格納されています。

Networking API は、例外の原因についての詳しい情報を取得するために、他のメソッドをサポートしています。

-   一部の API には、例外の **HRESULT** 値を列挙値に変換するヘルパー メソッドがあります。
-   その他の API には、実際の **HRESULT** 値を取得するメソッドがあります。

## <a name="related-topics"></a>関連トピック
* [Windows 10 での Networking API の機能強化](https://blogs.windows.com/buildingapps/2015/07/02/networking-api-improvements-in-windows-10/)