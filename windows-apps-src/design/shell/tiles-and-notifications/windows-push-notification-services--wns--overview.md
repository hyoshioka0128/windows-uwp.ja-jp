---
description: Windows プッシュ通知サービス (WNS) を利用することで、サード パーティの開発者が独自のクラウド サービスからトースト更新、タイル更新、バッジ更新、直接更新を送ることができます。 これにより、新しい更新を電力効率に優れた信頼できる方法でユーザーに配信するためのメカニズムが提供されます。
title: Windows プッシュ通知サービス (WNS) の概要
ms.assetid: 2125B09F-DB90-4515-9AA6-516C7E9ACCCD
template: detail.hbs
ms.date: 09/28/2020
ms.topic: article
ms.custom: contperfq1
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: e2fc69f49308164307bc3c6c23479aae991d0ff7
ms.sourcegitcommit: f46edb85d523a4a1f5006787d357cdc9d090aefe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "91414852"
---
# <a name="windows-push-notification-services-wns-overview"></a>Windows プッシュ通知サービス (WNS) の概要 

Windows プッシュ Notification Services (WNS) を使用すると、サードパーティの開発者は、独自のクラウドサービスからトースト、タイル、バッジ、生の更新プログラムを送信できます。 これにより、新しい更新を電力効率に優れた信頼できる方法でユーザーに配信するためのメカニズムが提供されます。

## <a name="how-it-works"></a>しくみ

次の図に、プッシュ通知を送るときの全体のデータ フローを示します。 以下のステップが関係します。

1.  アプリは WNS からプッシュ通知チャネルを要求します。
2.  Windows が、通知チャネルを作成するように WNS に要求します。 このチャネルは、Uniform Resource Identifier (URI) の形式で呼び出し元のデバイスに返されます。
3.  通知チャネル URI は WNS によってアプリに返されます。
4.  アプリから独自のクラウド サービスに URI を送ります。 その後で、URI をユーザー独自のクラウド サービスに保存し、通知を送るときに URI にアクセスできるようにします。 この URI は、独自のアプリと独自のサービスの間のインターフェイスです。このインターフェイスは、セキュリティで保護された安全な Web 標準に従って実装する必要があります。
5.  送られる更新情報がクラウド サービスにある場合、チャネルの URI を使って WNS に通知されます。 この処理では、通知ペイロードを含む HTTP POST 要求が Secure Sockets Layer (SSL) 経由で発行されます。 この手順では認証が必要になります。
6.  WNS が要求を受け取り、適切なデバイスに通知をルーティングします。

![プッシュ通知の WNS データ フローの図](images/wns-diagram-01.jpg)

## <a name="registering-your-app-and-receiving-the-credentials-for-your-cloud-service"></a>アプリの登録とクラウド サービスの資格情報の取得

WNS を使用して通知を送信する前に、 [こちら](https://docs.microsoft.com/azure/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification)の説明に従って、アプリをストアダッシュボードに登録する必要があります。

## <a name="requesting-a-notification-channel"></a>通知チャネルの要求

プッシュ通知を受け取ることができるアプリを実行するときは、最初に [**CreatePushNotificationChannelForApplicationAsync**](/uwp/api/Windows.Networking.PushNotifications.PushNotificationChannelManager#Windows_Networking_PushNotifications_PushNotificationChannelManager_CreatePushNotificationChannelForApplicationAsync_System_String_) を使って通知チャネルを要求する必要があります。 詳しい説明とコード例については、「[通知チャネルを要求、作成、保存する方法](/previous-versions/windows/apps/hh465412(v=win.10))」をご覧ください。 この API から返されるチャネルの URI は、呼び出し元のアプリケーションとそのタイルに一意にリンクされます。これには送信可能なすべての種類の通知が使われます。

アプリでは、チャネルの URI の作成が正常に完了すると、その URI に関連付けられるアプリ固有のメタデータと一緒にクラウド サービスに送ります。

### <a name="important-notes"></a>重要

-   アプリの通知チャネルの URI は、常に同じであるとは限りません。 アプリを実行するたびに新しいチャネルを要求し、URI が変更されたらサービスを更新することをお勧めします。 チャネルの URI の文字列はブラック ボックスと見なし、変更しないようにしてください。 現時点で、チャネルの URI は 30 日が経過すると有効期限切れになります。 Windows 10 アプリのバックグラウンドでそのチャネルを定期的に更新する場合は、Windows 8.1 の[プッシュ通知と定期的な通知のサンプル](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Windows%208%20app%20samples/%5BC%23%5D-Windows%208%20app%20samples/C%23/Windows%208%20app%20samples/Push%20and%20periodic%20notifications%20client-side%20sample%20(Windows%208))をダウンロードし、紹介されているソース コードやパターンを再利用することができます。
-   クラウド サービスとクライアント アプリの間のインターフェイスは開発者が実装します。 独自のサービスに対するアプリの認証プロセスでは、データの送信に HTTPS などのセキュリティで保護されたプロトコルを使うことをお勧めします。
-   クラウド サービスでは、チャネルの URI で必ず "notify.windows.com" ドメインを使うことが重要です。 他のドメインのチャネルに通知をプッシュしないでください。 アプリのコールバックが侵害された場合、悪意のある攻撃者によってチャネルの URI が送信され、WNS がなりすまされるおそれがあります。 ドメインを検査しないと、クラウドサービスがこの攻撃者に知らずに情報を開示する可能性があります。
-   クラウド サービスが期限切れのチャネルに通知を配信しようとすると、WNS は[応答コード 410](/previous-versions/windows/apps/hh465435(v=win.10)) を返します。 このコードを受け取った後、サービスはその URI に対して通知を送らないようにする必要があります。

## <a name="authenticating-your-cloud-service"></a>クラウド サービスの認証

通知を送るには、クラウド サービスが WNS に認証される必要があります。 そのためには、まず、アプリを Microsoft Store のダッシュボードに登録します。 この登録プロセスで、アプリにパッケージ セキュリティ識別子 (SID) と秘密鍵が割り当てられます。 クラウド サービスでは、この情報を使って WNS に対する認証を行います。

WNS の認証方式は、[OAuth 2.0](https://tools.ietf.org/html/draft-ietf-oauth-v2-23) プロトコルのクライアント資格情報のプロファイルを使って実装されます。 資格情報 (パッケージ SID と秘密鍵) を指定して、WNS に対してクラウド サービスの認証を行うと、 アクセス トークンを受け取ります。 このアクセス トークンを使って、クラウド サービスで通知を送ることができます。 このトークンは、WNS に送るすべての通知要求で必要になります。

大まかな情報の流れを次に示します。

1.  クラウド サービスから WNS に、OAuth 2.0 プロトコルに従って HTTPS 経由で資格情報が送られます。 これにより、WNS でサービスが認証されます。
2.  認証に成功すると、WNS からアクセス トークンが返されます。 このアクセス トークンを、有効期限切れになるまで以降のすべての通知要求で使います。

![クラウド サービス認証の WNS の図](images/wns-diagram-02.jpg)

WNS に対する認証では、クラウド サービスからの HTTP 要求の送信に Secure Sockets Layer (SSL) を使います。 パラメーターの形式は "application/x-www-for-urlencoded" です。 次の例に示すように、[クライアント id] フィールドにパッケージ SID を指定し、 \_ [クライアントシークレット] フィールドに秘密キーを入力し \_ ます。 構文について詳しくは、[アクセス トークン要求](/previous-versions/windows/apps/hh465435(v=win.10))のリファレンスをご覧ください。

> [!NOTE]
> これはほんの一例です。独自のコードで正常に使用できる切り取りと貼り付けのコードではありません。 

``` http
 POST /accesstoken.srf HTTP/1.1
 Content-Type: application/x-www-form-urlencoded
 Host: https://login.live.com
 Content-Length: 211
 
 grant_type=client_credentials&client_id=ms-app%3a%2f%2fS-1-15-2-2972962901-2322836549-3722629029-1345238579-3987825745-2155616079-650196962&client_secret=Vex8L9WOFZuj95euaLrvSH7XyoDhLJc7&scope=notify.windows.com
```

WNS はクラウド サービスを認証し、成功した場合、"200 OK" という応答を送ります。 アクセス トークンは、"application/json" メディア タイプを使って、HTTP 応答の本文に含まれるパラメーターで返されます。 アクセス トークンを受け取ると、通知を送ることができるようになります。

次の例は、アクセス トークンを含む認証成功時の応答を示しています。 構文について詳しくは、「[プッシュ通知サービスの要求ヘッダーと応答ヘッダー](/previous-versions/windows/apps/hh465435(v=win.10))」をご覧ください。

``` http
 HTTP/1.1 200 OK   
 Cache-Control: no-store
 Content-Length: 422
 Content-Type: application/json
 
 {
     "access_token":"EgAcAQMAAAAALYAAY/c+Huwi3Fv4Ck10UrKNmtxRO6Njk2MgA=", 
     "token_type":"bearer"
 }
```

### <a name="important-notes"></a>重要

-   この手順でサポートされる OAuth 2.0 プロトコルは、草案の第 16 版に準拠したものです。
-   OAuth の Request for Comments (RFC) では、クラウド サービスのことを "クライアント" と表現しています。
-   この手順は、OAuth の草案が完成したときに変更される可能性があります。
-   アクセス トークンは、複数の通知要求に再利用できます。 そのため、クラウド サービスを 1 回認証するだけで、複数の通知を送ることができます。 ただし、アクセス トークンの有効期限が切れた場合は、認証をもう一度行って新しいアクセス トークンを受け取る必要があります。

## <a name="sending-a-notification"></a>通知の送信


クラウド サービスにユーザー向けの更新があるときは、チャネルの URI を使って通知を送ることができます。

既に説明したように、アクセス トークンは複数の通知要求に再利用できます。そのため、通知のたびに新しいアクセス トークンを要求する必要はありません。 アクセス トークンの有効期限が切れると、通知要求でエラーが返されます。 アクセス トークンが拒否されたときに通知の送信を何度も再試行しないようにしてください。 このエラーが発生した場合は、新しいアクセス トークンを要求して通知を再送する必要があります。 具体的なエラー コードについては、「[プッシュ通知の応答コード](/previous-versions/windows/apps/hh465435(v=win.10))」をご覧ください。

1.  クラウド サービスで、チャネルの URI に対する HTTP POST 要求を行います。 この要求は SSL 経由で行う必要があります。要求には、必要なヘッダーと通知のペイロードが含まれます。 承認用に取得したアクセス トークンを承認ヘッダーに含める必要があります。

    要求の例を次に示します。 構文について詳しくは、「[プッシュ通知の応答コード](/previous-versions/windows/apps/hh465435(v=win.10))」をご覧ください。

    通知のペイロードの構成について詳しくは、「[クイック スタート: プッシュ通知の送信](/previous-versions/windows/apps/hh868252(v=win.10))」をご覧ください。 タイル、トースト、またはバッジのプッシュ通知のペイロードは、それぞれの定義済み[アダプティブ タイル スキーマ](adaptive-tiles-schema.md)または[レガシ タイル スキーマ](/uwp/schemas/tiles/tiles-xml-schema-portal)に準拠した XML コンテンツとして提供されます。 直接通知のペイロードには、指定された構造体はありません。 これは、アプリによって厳密に定義されます。

    ``` http
     POST https://cloud.notify.windows.com/?token=AQE%bU%2fSjZOCvRjjpILow%3d%3d HTTP/1.1
     Content-Type: text/xml
     X-WNS-Type: wns/tile
     Authorization: Bearer EgAcAQMAAAAALYAAY/c+Huwi3Fv4Ck10UrKNmtxRO6Njk2MgA=
     Host: cloud.notify.windows.com
     Content-Length: 24

     <body>
     ....
    ```

2.  WNS から、受け取った通知を次回の配信時に送ることを示す応答を受け取ります。 ただし、WNS では、デバイスやアプリケーションで通知を受け取ったかどうかに関するエンド ツー エンドの確認は行われません。

次の図はデータ フローを示しています。

![通知送信の WNS の図](images/wns-diagram-03.jpg)

### <a name="important-notes"></a>重要

-   WNS では、通知の信頼性や待機時間については保証されません。
-   機密データや重要なデータは通知に含めないでください。
-   通知を送るには、事前に WNS に対してクラウド サービスを認証し、アクセス トークンを受け取る必要があります。
-   アクセス トークンを使用する場合、クラウド サービスはそのトークンが作成された単一のアプリに対してのみ通知を送信できます。 1 つのアクセス トークンで複数のアプリに通知を送ることはできません。 そのため、クラウド サービスで複数のアプリをサポートしている場合は、それぞれのチャネルの URI に通知をプッシュするときに、該当するアプリの正しいアクセス トークンを指定する必要があります。
-   デバイスがオフラインの場合、WNS では既定で、チャネル URI ごとに最大 5 つ (キューが有効になっていない場合は 1 つ) のタイル通知と 1 つのバッジ通知が保存されます。直接通知は保存されません。 この既定のキャッシュ処理は、[X-WNS-Cache-Policy ヘッダー](/previous-versions/windows/apps/hh465435(v=win.10))を使って変更することができます。 デバイスがオフラインである場合、トースト通知は保存されませんので注意してください。
-   通知の内容がユーザーごとに異なる場合、WNS では、クラウド サービスでそれらの更新を受け取ったら、それらを直ちに送るように推奨されています。 これには、たとえば、ソーシャル メディアのフィードの更新、即座の通知への招待、新しいメッセージの通知、アラートなどが該当します。 また、天気、株価情報、ニュースの更新など、多くのユーザーに同じ更新を頻繁に配信する場合もあります。 WNS のガイドラインでは、それらの更新頻度を 30 分に 1 回までにするように規定されています。 それよりも頻繁に更新を配信すると、エンド ユーザーや WNS に不正な通知と見なされる場合があります。
-   Windows Notification Platform は、ソケットをアクティブにして正常な状態に保つために、WNS との定期的なデータ接続を保持します。 通知チャネルを要求または使用するアプリケーションが存在しない場合、ソケットは作成されません。

## <a name="expiration-of-tile-and-badge-notifications"></a>タイル通知とバッジ通知の有効期限

既定では、タイル通知とバッジ通知は、ダウンロードされたときから 3 日後に有効期限切れになります。 通知の有効期限が切れると、タイルまたはキューからコンテンツが削除され、ユーザーに表示されなくなります。 すべてのタイル通知とバッジ通知には、アプリにとって適切な時間を使って有効期限を設定し、タイルのコンテンツの意味がなくなっても保持されないようにすることをお勧めします。 明示的な有効期限は、コンテンツの存続期間が決まっている場合に重要です。 また、クラウド サービスによる通知の送信が停止した場合や、ユーザーがネットワークに長時間接続していない場合に、古いコンテンツを確実に削除することができます。

クラウド サービスでは、送信後の通知が有効である時間を秒単位で指定する X-WNS-TTL HTTP ヘッダーを設定することで、通知ごとに有効期限を設定できます。 詳しくは、「[プッシュ通知サービスの要求ヘッダーと応答ヘッダー](/previous-versions/windows/apps/hh465435(v=win.10))」を参照してください。

たとえば、株式市場の取引が活発な日は、株価の更新の有効期限を送信間隔の有効期限の 2 倍に設定することをお勧めします (30 分ごとに通知を送っている場合は有効期限を受け取り後 1 時間にするなど)。 また、ニュース アプリの場合、毎日のニュースを表示するタイルの更新の有効期限は 1 日が適しています。

## <a name="push-notifications-and-battery-saver"></a>プッシュ通知とバッテリー セーバー

バッテリー セーバーは、デバイスでのバックグラウンド アクティビティを制限することでバッテリーの寿命を延ばします。 Windows 10 を使うと、バッテリーが指定されたしきい値を下回ったときに、ユーザーは自動的にバッテリー セーバーをオンになるように設定することができます。 バッテリー セーバーがオンのときは、電力を節約するため、プッシュ通知の受信は無効になります。 ただし、これにはいくつかの例外があります。 次の Windows 10 バッテリ セーバー設定 (**[設定]** アプリにあります) により、バッテリ セーバーがオンになっているときでも、プッシュ通知を受け取ることができます。

-   **[バッテリー節約機能がオンのときも、すべてのアプリケーションからのプッシュ通知を許可する]**: この設定では、バッテリー節約機能がオンになっているときでも、すべてのアプリがプッシュ通知を受け取ることができます。 この設定が適用されるのは、デスクトップ エディション (Home、Pro、Enterprise、Education の各エディション) 用 Windows 10 のみです。
-   **Always allowed**: この設定では、バッテリ セーバーがオンになっているときでも、プッシュ通知の受け取りを含めて、バックグラウンドで特定のアプリを実行できます。 この一覧は、ユーザーによって手動で管理されます。

これら 2 つの設定の状態を確認する方法はありませんが、バッテリ セーバーの状態を確認することはできます。 Windows 10 では、[**EnergySaverStatus**](/uwp/api/Windows.System.Power.PowerManager.EnergySaverStatus) プロパティを使って、バッテリ セーバーの状態を確認します。 アプリでは、[**EnergySaverStatusChanged**](/uwp/api/Windows.System.Power.PowerManager.EnergySaverStatusChanged) イベントを使って、バッテリ セーバーの変更をリッスンすることもできます。

アプリがプッシュ通知を多用している場合は、バッテリ セーバーがオンの時は通知を受け取らないことをユーザーに通知し、**バッテリ セーバーの設定**を簡単に調整できるようにすることをお勧めします。 Windows 10 でバッテリ セーバー設定の URI スキーム `ms-settings:batterysaver-settings` を使って、設定アプリへの便利なリンクを提供することができます。

> [!TIP]
> バッテリの節約設定についてユーザーに通知する場合は、今後メッセージを表示しないようにする方法を用意することをお勧めします。 たとえば、次の例の [`dontAskMeAgainBox`] チェックボックスは、[**LocalSettings**](/uwp/api/Windows.Storage.ApplicationData.LocalSettings) でユーザーの設定を保持します。

Windows 10 でバッテリ省が有効になっているかどうかを確認する方法の例を次に示します。 この例では、ユーザーに通知し、[設定] アプリを**バッテリ セーバー設定**で起動します。 `dontAskAgainSetting` により、ユーザーは再度通知を表示しないようにする場合に、メッセージを非表示にすることができます。

```csharp
using System;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;
using Windows.System;
using Windows.System.Power;
...
...
async public void CheckForEnergySaving()
{
   //Get reminder preference from LocalSettings
   bool dontAskAgain;
   var localSettings = Windows.Storage.ApplicationData.Current.LocalSettings;
   object dontAskSetting = localSettings.Values["dontAskAgainSetting"];
   if (dontAskSetting == null)
   {  // Setting does not exist
      dontAskAgain = false;
   }
   else
   {  // Retrieve setting value
      dontAskAgain = Convert.ToBoolean(dontAskSetting);
   }
   
   // Check if battery saver is on and that it's okay to raise dialog
   if ((PowerManager.EnergySaverStatus == EnergySaverStatus.On)
         && (dontAskAgain == false))
   {
      // Check dialog results
      ContentDialogResult dialogResult = await saveEnergyDialog.ShowAsync();
      if (dialogResult == ContentDialogResult.Primary)
      {
         // Launch battery saver settings (settings are available only when a battery is present)
         await Launcher.LaunchUriAsync(new Uri("ms-settings:batterysaver-settings"));
      }

      // Save reminder preference
      if (dontAskAgainBox.IsChecked == true)
      {  // Don't raise dialog again
         localSettings.Values["dontAskAgainSetting"] = "true";
      }
   }
}
```

```cppwinrt
#include <winrt/Windows.Foundation.h>
#include <winrt/Windows.Storage.h>
#include <winrt/Windows.System.h>
#include <winrt/Windows.System.Power.h>
#include <winrt/Windows.UI.Xaml.h>
#include <winrt/Windows.UI.Xaml.Controls.h>
#include <winrt/Windows.UI.Xaml.Navigation.h>
using namespace winrt;
using namespace winrt::Windows::Foundation;
using namespace winrt::Windows::Storage;
using namespace winrt::Windows::System;
using namespace winrt::Windows::System::Power;
using namespace winrt::Windows::UI::Xaml;
using namespace winrt::Windows::UI::Xaml::Controls;
using namespace winrt::Windows::UI::Xaml::Navigation;
...
winrt::fire_and_forget CheckForEnergySaving()
{
    // Get reminder preference from LocalSettings.
    bool dontAskAgain{ false };
    auto localSettings = ApplicationData::Current().LocalSettings();
    IInspectable dontAskSetting = localSettings.Values().Lookup(L"dontAskAgainSetting");
    if (!dontAskSetting)
    {
        // Setting doesn't exist.
        dontAskAgain = false;
    }
    else
    {
        // Retrieve setting value
        dontAskAgain = winrt::unbox_value<bool>(dontAskSetting);
    }

    // Check whether battery saver is on, and whether it's okay to raise dialog.
    if ((PowerManager::EnergySaverStatus() == EnergySaverStatus::On) && (!dontAskAgain))
    {
        // Check dialog results.
        ContentDialogResult dialogResult = co_await saveEnergyDialog().ShowAsync();
        if (dialogResult == ContentDialogResult::Primary)
        {
            // Launch battery saver settings
            // (settings are available only when a battery is present).
            co_await Launcher::LaunchUriAsync(Uri(L"ms-settings:batterysaver-settings"));
        }

        // Save reminder preference.
        if (dontAskAgainBox().IsChecked())
        {
            // Don't raise the dialog again.
            localSettings.Values().Insert(L"dontAskAgainSetting", winrt::box_value(true));
        }
    }
}
```

これは、次の例で使われている [**ContentDialog**](/uwp/api/Windows.UI.Xaml.Controls.ContentDialog) の XAML です。

```xaml
<ContentDialog x:Name="saveEnergyDialog"
               PrimaryButtonText="Open battery saver settings"
               SecondaryButtonText="Ignore"
               Title="Battery saver is on."> 
   <StackPanel>
      <TextBlock TextWrapping="WrapWholeWords">
         <LineBreak/><Run>Battery saver is on and you may 
          not receive push notifications.</Run><LineBreak/>
         <LineBreak/><Run>You can choose to allow this app to work normally
         while in battery saver, including receiving push notifications.</Run>
         <LineBreak/>
      </TextBlock>
      <CheckBox x:Name="dontAskAgainBox" Content="OK, got it."/>
   </StackPanel>
</ContentDialog>
```

## <a name="related-topics"></a>関連トピック

* [ローカル タイル通知の送信](sending-a-local-tile-notification.md)
* [クイック スタート: プッシュ通知の送信](/previous-versions/windows/apps/hh868252(v=win.10))
* [プッシュ通知を使用してバッジを更新する方法](/previous-versions/windows/apps/hh465450(v=win.10))
* [通知チャネルを要求、作成、保存する方法](/previous-versions/windows/apps/hh465412(v=win.10))
* [実行中のアプリの通知を中断する方法](/previous-versions/windows/apps/jj709907(v=win.10))
* [Windows プッシュ通知サービス (WNS) に対して認証する方法](/previous-versions/windows/apps/hh465407(v=win.10))
* [プッシュ通知サービスの要求ヘッダーと応答ヘッダー](/previous-versions/windows/apps/hh465435(v=win.10))
* [プッシュ通知のガイドラインとチェック リスト]()
* [直接通知](/previous-versions/windows/apps/hh761488(v=win.10))
