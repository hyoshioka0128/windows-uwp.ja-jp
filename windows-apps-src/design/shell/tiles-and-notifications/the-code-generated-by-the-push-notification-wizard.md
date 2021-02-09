---
description: Visual Studio でウィザードを使うことで、Azure のモバイル サービスで作成されたモバイル サービスからプッシュ通知を生成できます。
title: プッシュ通知ウィザードにより生成されるコード
ms.assetid: 340F55C1-0DDF-4233-A8E4-C15EF9030785
template: detail.hbs
ms.date: 09/24/2020
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: f9af0301dcf8944127ab814155466335940642f0
ms.sourcegitcommit: a3bbd3dd13be5d2f8a2793717adf4276840ee17d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93034445"
---
# <a name="code-generated-by-the-push-notification-wizard"></a>プッシュ通知ウィザードにより生成されるコード
 

Visual Studio でウィザードを使うことで、Azure のモバイル サービスで作成されたモバイル サービスからプッシュ通知を生成できます。 Visual Studio ウィザードにより、この作業に役立つコードが生成されます。 このトピックでは、ウィザードによるプロジェクトの変更内容、生成されたコードによる実行内容、このコードを使う方法、プッシュ通知を最大限に活用するために次に行うことができる作業について説明します。 「[Windows プッシュ通知サービス (WNS) の概要](windows-push-notification-services--wns--overview.md)」をご覧ください。

## <a name="how-the-wizard-modifies-your-project"></a>ウィザードによるプロジェクトの変更内容


プッシュ通知ウィザードは、次のようにプロジェクトを変更します。

-   モバイル サービスの管理されたクライアントへの参照を追加します (MobileServicesManagedClient.dll)。 JavaScript プロジェクトには当てはまりません。
-   サービスの下にあるサブフォルダーにファイルを追加し、ファイルに push.register.cs、push.register.vb、push.register.cpp、または push.register.js という名前を付けます。
-   モバイル サービスのデータベース サーバーでチャネル テーブルを作成します。 テーブルには、アプリ インスタンスにプッシュ通知を送るために必要な情報が格納されます。
-   4 つの機能 (削除、挿入、読み取り、更新) のスクリプトを作成します。
-   カスタム API を含むスクリプト notifyallusers.js を作成します。この API は、すべてのクライアントにプッシュ通知を送ります。
-   App.xaml.cs、App.xaml.vb、または App.xaml.cpp ファイルに宣言を追加したり、JavaScript プロジェクトの新しいファイルである service.js に宣言を追加したりします。 宣言では、モバイル サービスへの接続に必要な情報を含む MobileServiceClient オブジェクトが宣言されます。 App. *MyServiceName* Client という名前を使って、アプリ内のどのページからでも *MyServiceName* Client という名前のこの MobileServiceClient オブジェクトにアクセスできます。

services.js ファイルには、次のコードが含まれています。

```js
var <mobile-service-name>Client = new Microsoft.WindowsAzure.MobileServices.MobileServiceClient(
                "https://<mobile-service-name>.azure-mobile.net/",
                "<your client secret>");
```

## <a name="registration-for-push-notifications"></a>プッシュ通知への登録


Push. register. では \* 、UploadChannel メソッドによってデバイスが登録され、プッシュ通知が受信されます。 ストアは、アプリのインストールされたインスタンスを追跡し、プッシュ通知チャネルを提供します。 「 [**PushNotificationChannelManager**](/uwp/api/Windows.Networking.PushNotifications.PushNotificationChannelManager)」をご覧ください。

クライアント コードは、JavaScript のバックエンドと .NET のバックエンドの両方に似ています。 既定では、JavaScript バックエンド サービスのプッシュ通知を追加すると、notifyAllUsers カスタム API のサンプル呼び出しが UploadChannel メソッドに挿入されます。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;
using Microsoft.WindowsAzure.MobileServices;
using Newtonsoft.Json.Linq;

namespace App2
{
    internal class mymobileservice1234Push
    {
        public async static void UploadChannel()
        {
            var channel = await Windows.Networking.PushNotifications.PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            try
            {
                await App.mymobileservice1234Client.GetPush().RegisterNativeAsync(channel.Uri);
                await App.mymobileservice1234Client.InvokeApiAsync("notifyAllUsers");
            }
            catch (Exception exception)
            {
                HandleRegisterException(exception);
            }
        }

        private static void HandleRegisterException(Exception exception)
        {
            
        }
    }
}
```

```vb
Imports Microsoft.WindowsAzure.MobileServices
Imports Newtonsoft.Json.Linq

Friend Class mymobileservice1234Push
    Public Shared Async Sub UploadChannel()
        Dim channel = Await Windows.Networking.PushNotifications.PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync()

        Try
            Await App.mymobileservice1234Client.GetPush().RegisterNativeAsync(channel.Uri)
            Await App.mymobileservice1234Client.GetPush().RegisterNativeAsync(channel.Uri, New String() {"tag1", "tag2"})
            Await App.mymobileservice1234Client.InvokeApiAsync("notifyAllUsers")
        Catch exception As Exception
            HandleRegisterException(exception)
        End Try
    End Sub

    Private Shared Sub HandleRegisterException(exception As Exception)

    End Sub
End Class
```

```c++
#include "pch.h"
#include "services\mobile services\mymobileservice1234\mymobileservice1234Push.h"

using namespace AzureMobileHelper;

using namespace web;
using namespace concurrency;

using namespace Windows::Networking::PushNotifications;

void mymobileservice1234Push::UploadChannel()
{
    create_task(PushNotificationChannelManager::CreatePushNotificationChannelForApplicationAsync()).
    then([] (PushNotificationChannel^ newChannel) 
    {
        return mymobileservice1234MobileService::GetClient().get_push().register_native(newChannel->Uri->Data());
    }).then([]()
    {
        return mymobileservice1234MobileService::GetClient().invoke_api(L"notifyAllUsers");
    }).then([](task<json::value> result)
    {
        try
        {
            result.wait();
        }
        catch(...)
        {
            HandleExceptionsComingFromTheServer();
        }
    });
}

void mymobileservice1234Push::HandleExceptionsComingFromTheServer()
{
}
```

```js
(function () {
    "use strict";

    var app = WinJS.Application;
    var activation = Windows.ApplicationModel.Activation;

    app.addEventListener("activated", function (args) {
        if (args.detail.kind == activation.ActivationKind.launch) {
            Windows.Networking.PushNotifications.PushNotificationChannelManager.createPushNotificationChannelForApplicationAsync()
                .then(function (channel) {
                    mymobileserviceclient1234Client.push.registerNative(channel.Uri, new Array("tag1", "tag2"))
                    return mymobileservice1234Client.push.registerNative(channel.uri);
                })
                .done(function (registration) {
                    return mymobileservice1234Client.invokeApi("notifyAllUsers");
                }, function (error) {
                    // Error

                });
        }
    });
})();
```

プッシュ通知のタグがクライアントのサブセットへの通知を制限する方法を提供します。 registerNative メソッド (または RegisterNativeAsync) メソッドを使って、タグを指定せずにすべてのプッシュ通知に登録するか、2 番目の引数としてタグの配列を指定することによって、タグを指定して登録できます。 1 つまたは複数のタグを登録すると、タグに一致する通知のみを受け取ります。

## <a name="server-side-scripts-javascript-backend-only"></a>サーバー側のスクリプト (JavaScript バックエンドのみ)


JavaScript バックエンドを使うモバイル サービスの場合、サーバー側のスクリプトは、削除、挿入、読み取り、または更新操作が行われたときに実行されます。 スクリプトにはこれらの操作が実装されていませんが、クライアントから Windows モバイルの REST API への呼び出しによってこれらのイベントがトリガーされると実行されます。 次に、スクリプトは request.execute または request.respond を呼び出して呼び出し元コンテキストに応答を発行することで、コントロールを操作自体に渡します。 「[Azure のモバイル サービスの REST API リファレンス](/previous-versions/azure/reference/jj710108(v=azure.100))」をご覧ください。

サーバー側のスクリプトでは、さまざまな関数を使うことができます。 「[Azure のモバイル サービスでのテーブル操作の登録](https://msdn.microsoft.com/library/azure/dn167708.aspx)」をご覧ください。 使用できる関数のリファレンスについては、「[Mobile Services サーバーのスクリプトのリファレンス](/previous-versions/azure/reference/jj554226(v=azure.100))」をご覧ください。

また、Notifyallusers.js に次のカスタム API コードが作成されます。

```js
exports.post = function(request, response) {
    response.send(statusCodes.OK,{ message : 'Hello World!' })
    
    // The following call is for illustration purpose only
    // The call and function body should be moved to a script in your app
    // where you want to send a notification
    sendNotifications(request);
};

// The following code should be moved to appropriate script in your app where notification is sent
function sendNotifications(request) {
    var payload = '<?xml version="1.0" encoding="utf-8"?><toast><visual><binding template="ToastText01">' +
        '<text id="1">Sample Toast</text></binding></visual></toast>';
    var push = request.service.push; 
    push.wns.send(null,
        payload,
        'wns/toast', {
            success: function (pushResponse) {
                console.log("Sent push:", pushResponse);
            }
        });
}
```

sendNotifications 関数は、1 つの通知をトースト通知として送信します。 他の種類のプッシュ通知を使うこともできます。

**ヒント**  スクリプトの編集中にヘルプを表示する方法については、 [サーバー側の JavaScript で IntelliSense を有効にする方法](https://blogs.msdn.com/b/visualstudio/archive/2013/07/26/enabling-intellisense-for-mobile-services-javascript-in-visual-studio.aspx)に関するページをご覧ください。

 

## <a name="push-notification-types"></a>プッシュ通知の種類


Windows では、プッシュ通知ではない通知がサポートされています。 通知に関する一般情報については、「[通知配信方法の選択](choosing-a-notification-delivery-method.md)」をご覧ください。

トースト通知は使いやすく、自動的に生成されるチャネル テーブルの Insert.js コードで例を確認できます。 タイル通知かバッジ通知を使う予定の場合、タイルとバッジの XML テンプレートを作成し、テンプレートでパッケージ化された情報のエンコードを指定する必要があります。 「 [タイル、バッジ、およびトースト通知の操作](/previous-versions/windows/apps/hh868259(v=win.10))」を参照してください。

Windows は、プッシュ通知に応答するため、アプリが実行されていないときにこれらの通知のほとんどを処理できます。 たとえば、プッシュ通知は、ローカル メール アプリが実行されていないときでも新しいメール メッセージを受信したことをユーザーに知らせることができます。 Windows は、テキスト メッセージの先頭行のようなメッセージを表示することで、トースト通知を処理します。 Windows は、ライブ タイルを更新して新しいメール メッセージの数を反映することで、タイル通知またはバッジ通知を処理します。 このように、新しい情報をチェックするように促すプロンプトをアプリのユーザーに表示できます。 アプリは、実行中に直接通知を受け取ることができるため、直接通知を使ってアプリにデータを送ることができます。 アプリが実行されていない場合、プッシュ通知を監視するバックグラウンド タスクを設定できます。

Windows アプリのガイドラインに従ってプッシュ通知を使用する必要があります。これらの通知はユーザーのリソースを使用するため、超過した場合は邪魔になる可能性があるためです。 「[プッシュ通知のガイドラインとチェック リスト](./windows-push-notification-services--wns--overview.md)」をご覧ください。

プッシュ通知でライブ タイルを更新する場合は、「[タイルとバッジのガイドラインとチェック リスト](./creating-tiles.md)」のガイドラインにも従ってください。

## <a name="next-steps"></a>次のステップ


### <a name="using-the-windows-push-notification-services-wns"></a>Windows プッシュ通知サービス (WNS) の使用

Window Azure のモバイル サービスの柔軟性が不十分な場合、C# または Visual Basic でサーバー コードを記述する場合、または既にクラウド サービスを持っていてそこからプッシュ通知を送る場合は、Windows プッシュ通知サービス (WNS) を直接呼び出すこともできます。 WNS を直接呼び出すことで、データベースや他の Web サービスからのデータを監視するワーカーの役割など、独自のクラウド サービスからプッシュ通知を送ることができます。 クラウド サービスがプッシュ通知をアプリに送るには、WNS に対して認証する必要があります。 [Windows プッシュ通知サービスに対して認証する方法 (JavaScript)](/previous-versions/windows/apps/hh465407(v=win.10)) または [(C#/C++/VB)](/previous-versions/windows/apps/hh868206(v=win.10)) に関するページをご覧ください。

モバイル サービスでスケジュール済みタスクを実行して、プッシュ通知を送ることもできます。 「[Mobile Services での繰り返し発生するジョブのスケジュール](/azure/)」をご覧ください。

**警告**  プッシュ通知ウィザードは 1 回だけ実行してください。もう一度実行して、別のモバイル サービスの登録コードを追加しないようにしてください。 このウィザードをプロジェクトごとに複数回実行すると、生成されるコードで [**CreatePushNotificationChannelForApplicationAsync**](/uwp/api/Windows.Networking.PushNotifications.PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync) メソッドの呼び出しが重複し、ランタイムの例外が発生します。 複数のモバイル サービスのプッシュ通知を登録するには、ウィザードを 1 回だけ実行し、登録コードを上書きして、 **CreatePushNotificationChannelForApplicationAsync** の呼び出しが同時に実行されないようにしてください。 たとえば、ウィザードで生成されたコードを push. register \* で移動することで、これを実現できます。OnLaunched 上げイベントの外部にある **Createpushnotificationchannelforapplicationasync** の呼び出しを含めますが、その詳細はアプリのアーキテクチャによって異なります。

 

## <a name="related-topics"></a>関連トピック


* [Windows プッシュ通知サービス (WNS) の概要](windows-push-notification-services--wns--overview.md)
* [直接通知の概要](raw-notification-overview.md)
* [Window Azure のモバイル サービスへの接続 (JavaScript)](/previous-versions/windows/apps/dn263160(v=win.10))
* [Window Azure のモバイル サービスへの接続 (C#/C++/VB)](/previous-versions/windows/apps/dn263175(v=win.10))
* [クイック スタート: モバイル サービスでのプッシュ通知の追加 (JavaScript)](/previous-versions/windows/apps/dn263163(v=win.10))
 

 
