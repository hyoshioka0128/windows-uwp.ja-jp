---
ms.assetid: 79C284CA-C53A-4C24-807E-6D4CE1A29BFA
description: このセクションでは、以前の Windows 8.1 から、Windows 10 バージョンに加えられた変更をサポートするために、PlayReady Web アプリを変更する方法について説明します。
title: PlayReady の Encrypted Media Extension
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: e5ac10a1cc4e9feee609a56e5db6285284c41b98
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89163696"
---
# <a name="playready-encrypted-media-extension"></a>PlayReady の Encrypted Media Extension



このセクションでは、以前の Windows 8.1 から、Windows 10 バージョンに加えられた変更をサポートするために、PlayReady Web アプリを変更する方法について説明します。

Internet Explorer で PlayReady メディア要素を使うと、開発者はコンテンツ プロバイダーが定義したアクセス ルールを適用しながら、ユーザーに PlayReady コンテンツを提供することのできる Web アプリを作成することができます。 ここでは、HTML5 と JavaScript のみを使って、既存の Web アプリに PlayReady メディア要素を追加する方法について説明します。

## <a name="whats-new-in-playready-encrypted-media-extension"></a>PlayReady の Encrypted Media Extension の新機能

このセクションでは、Windows 10 で PlayReady コンテンツ保護を有効にするために PlayReady Encrypted Media Extension (EME) に加えられた変更を示します。

次に、Windows 10 の PlayReady Encrypted Media Extension に関する新機能や変更点について説明します。

-   追加されたハードウェア デジタル著作権管理 (DRM)。

    ハードウェア ベースのコンテンツ保護により、複数のデバイス プラットフォーム上で、高解像度 (HD) と超高解像度 (UHD) のコンテンツを安全に再生できます。 キー マテリアル (秘密キー、コンテンツ キー、これらのキーを派生またはロック解除するために使われるその他のキー マテリアルを含みます)、および暗号化解除された圧縮および非圧縮ビデオ サンプルは、ハードウェア セキュリティを利用して保護されます。

-   永続的でないライセンスの事前の取得を提供します。
-   1 つのメッセージで複数のライセンスを取得できるようにします。

    Windows 8.1 のように PlayReady オブジェクトと複数のキー識別子 (KeyID) を使うか、[Content Decryption Model データ (CDMData)](/previous-versions/windows/apps/dn457361(v=ieb.10)) と複数の KeyID を使うことができます。

    > [!NOTE]
    > Windows 10 では、複数のキー識別子が CDMData の &lt;KeyID&gt; でサポートされます。

-   リアルタイムの有効期限のサポートや期間限定ライセンス (LDL) が追加されました。

    ライセンスに対してリアルタイムの有効期限を設定することができます。

-   HDCP Type 1 (バージョン 2.2) ポリシーのサポートを追加しました。
-   Miracast が暗黙的な出力となりました。
-   セキュア ストップが追加されました。

    セキュア ストップによって、特定のコンテンツについてのメディア再生が停止したメディア ストリーミング サービスに対して、PlayReady デバイスが確実にアサートするための手段が提供されます。

-   オーディオとビデオに関するライセンスの分離が追加されました。

    トラックを分離することによって、ビデオがオーディオにデコードされるのを防ぐことができます。これにより、さらに強力なコンテンツ保護が可能になります。 最新の標準では、オーディオ トラックと映像トラックに対して別々のキーが必要になります。

-   MaxResDecode が追加されました。

    この機能は、コンテンツの再生を最大解像度に制限するために追加されました (ライセンスではなく、より強力なキーを所有している場合にも制限を受けます)。 これは、複数のストリーム サイズが 1 つのキーでエンコードされる状況をサポートします。

## <a name="encrypted-media-extension-support-in-playready"></a>PlayReady の Encrypted Media Extension のサポート

このセクションでは、PlayReady でサポートされている W3C 暗号化メディア拡張機能のバージョンについて説明します。

Web アプリ用の PlayReady は、現在 [2013 年 5 月 10 日付けの W3C Encrypted Media Extension (EME) 草案](https://www.w3.org/TR/2013/WD-encrypted-media-20130510/)に準拠しています。 このサポートは、将来のバージョンの Windows では更新された EME 仕様に合わせて変更されます。

## <a name="use-hardware-drm"></a>ハードウェア DRM の使用

このセクションでは、Web アプリで PlayReady ハードウェア DRM を使う方法と、保護されたコンテンツがハードウェア DRM をサポートしていない場合にそれを無効にする方法について説明します。

PlayReady ハードウェア DRM を使うには、JavaScript Web アプリは、キー システム識別子 `com.microsoft.playready.hardware` と共に **isTypeSupported** EME メソッドを使って、ブラウザーから PlayReady ハードウェア DRM のサポートを照会する必要があります。

一部のコンテンツは、ハードウェア DRM ではサポートされない場合があります。 Cocktail コンテンツがハードウェア DRM でサポートされることはありません。Cocktail コンテンツを再生する場合は、ハードウェア DRM を除外する必要があります。 一部のハードウェア DRM は HEVC をサポートしますが、サポートしないものもあります。HEVC コンテンツを再生したいが、ハードウェア DRM がサポートしていない場合も、これを除外してください。

> [!NOTE]
> HEVC コンテンツがサポートされているかどうかを判断するには、`com.microsoft.playready` をインスタンス化した後で、[**PlayReadyStatics.CheckSupportedHardware**](/uwp/api/windows.media.protection.playready.playreadystatics.checksupportedhardware) メソッドを使います。

## <a name="add-secure-stop-to-your-web-app"></a>Web アプリにセキュア ストップを追加する

このセクションでは、Web アプリにセキュア ストップを追加する方法を説明します。

セキュア ストップによって、特定のコンテンツについてのメディア再生が停止したメディア ストリーミング サービスに対して、PlayReady デバイスが確実にアサートするための手段が提供されます。 この機能により、メディア ストリーミング サービスは、特定のアカウントのさまざまなデバイスに対する使用制限を正しく適用し報告することができるようになります。

セキュア ストップのチャレンジを送信する主なシナリオが 2 つあります。

-   コンテンツの最後に達したか、ユーザーがメディア プレゼンテーションを途中で停止したため、メディア プレゼンテーションが停止した場合。
-   (システムまたはアプリのクラッシュなどにより) 前回のセッションが予期せずに終了した場合。 アプリは、起動時またはシャットダウン時に、未処理のセキュア ストップ セッションについて照会し、その他のメディア再生とは別にチャレンジを送信する必要があります。

次の手順は、さまざまなシナリオでセキュア ストップを設定する方法について説明します。

プレゼンテーションの通常の終了時にセキュア ストップを設定するには

1.  再生が開始する前に **onEnded** イベントを登録します。
2.  **onEnded** イベント ハンドラーは、ビデオ/オーディオ要素のオブジェクトから `removeAttribute("src")` を呼び出し、ソースを **NULL** に設定する必要があります。これにより、メディア ファンデーションをトリガーしてトポロジを終了し、暗号化解除機能を破棄して、停止状態を設定します。
3.  ハンドラー内の CDM セッションのセキュア ストップを開始し、セキュア ストップ チャレンジをサーバーに送信して、現在は再生が停止したが、後でも実行できることを通知できます。

ユーザーがページから移動したか、タブまたはブラウザーを閉じた場合にセキュア ストップを設定するには

-   停止状態を記録するためにアプリの操作は必要ありません。自動的に記録されます。

カスタム ページ コントロールまたはユーザーの操作 (カスタム ナビゲーション ボタンや、現在のプレゼンテーションを完了する前に新しいプレゼンテーションを開始するなど) のセキュア ストップを設定するには

-   カスタム ユーザー アクションが発生すると、アプリは、ソースを **NULL** に設定する必要があります。これにより、メディア ファンデーションをトリガーして、トポロジを終了し、暗号化解除機能を破棄して、停止状態を設定します。

次の例は、Web アプリでのセキュア ストップの使い方を示しています。

```JavaScript
// JavaScript source code

var g_prkey = null;
var g_keySession = null;
var g_fUseSpecificSecureStopSessionID = false;
var g_encodedMeteringCert = 'Base64 encoded of your metering cert (aka publisher cert)';

// Note: g_encodedLASessionId is the CDM session ID of the proactive or reactive license acquisition 
//       that we want to initiate the secure stop process.
var g_encodedLASessionId = null;

function main()
{
    ...

    g_prkey = new MSMediaKeys("com.microsoft.playready");

    ...

    // add 'onended' event handler to the video element
    // Assume 'myvideo' is the ID of the video element
    var videoElement = document.getElementById("myvideo");
    videoElement.onended = function (e) { 

        //
        // Calling removeAttribute("src") will set the source to null
        // which will trigger the MF to tear down the topology, destroy the
        // decryptor(s) and set the stop state.  This is required in order
        // to set the stop state.
        //
        videoElement.removeAttribute("src");
        videoElement.load();

        onEndOfStream();
    };
}

function onEndOfStream()
{
    ...

    createSecureStopCDMSession();

    ...    
}

function createSecureStopCDMSession()
{
    try{    
        var targetMediaCodec = "video/mp4";
        var customData = "my custom data";

        var encodedSessionId = g_encodedLASessionId;
        if( !g_fUseSpecificSecureStopSessionID )
        {
            // Use "*" (wildcard) as the session ID to include all secure stop sessions
            // TODO: base64 encode "*" and place encoded result to encodedSessionId
        }

        var int8ArrayCDMdata = formatSecureStopCDMData( encodedSessionId, customData,  g_encodedMeteringCert );
        var emptyArrayofInitData = new Uint8Array();

        g_keySession = g_prkey.createSession(targetMediaCodec, emptyArrayofInitData, int8ArrayCDMdata);

        addPlayreadyKeyEventHandler();

    } catch( e )
    {
        // TODO: Handle exception
    }
}

function addPlayreadyKeyEventHandler()
{
    // add 'keymessage' eventhandler   
    g_keySession.addEventListener('mskeymessage', function (event) {

        // TODO: Get the keyMessage from event.message.buffer which contains the secure stop challenge
        //       The keyMessage format for the secure stop is similar to LA as below:
        //
        //            <PlayReadyKeyMessage type="SecureStop" >
        //              <SecureStop version="1.0" >
        //                <Challenge encoding="base64encoded">
        //                    secure stop challenge
        //                </Challenge>
        //                <HttpHeaders>
        //                    <HttpHeader>
        //                      <name>Content-Type</name>
        //                         <value>"content type data"</value>
        //                    </HttpHeader>
        //                    <HttpHeader>
        //                         <name>SOAPAction</name>
        //                         <value>soap action</value>
        //                     </HttpHeader>
        //                    ....
        //                </HttpHeaders>
        //              </SecureStop>
        //            </PlayReadyKeyMessage>
                
        // TODO: send the secure stop challenge to a server that handles the secure stop challenge

        // TODO: Receive and response and call event.target.Update() to proecess the response
    });
    
    // add 'keyerror' eventhandler
    g_keySession.addEventListener('mskeyerror', function (event) {
        var session = event.target;
        
        ...

        session.close();
    });
    
    // add 'keyadded' eventhandler
    g_keySession.addEventListener('mskeyadded', function (event) {
        
        var session = event.target;

        ...

        session.close();             
    });
}

/**
* desc@ formatSecureStopCDMData
*   generate playready CDMData
*   CDMData is in xml format:
*   <PlayReadyCDMData type="SecureStop">
*     <SecureStop version="1.0">
*       <SessionID>B64 encoded session ID</SessionID>
*       <CustomData>B64 encoded custom data</CustomData>
*       <ServerCert>B64 encoded server cert</ServerCert>
*     </SecureCert>
* </PlayReadyCDMData>        
*/
function formatSecureStopCDMData(encodedSessionId, customData, encodedPublisherCert) 
{
    var encodedCustomData = null;

    // TODO: base64 encode the custom data and place the encoded result to encodedCustomData

    var CDMDataStr = "<PlayReadyCDMData type=\"SecureStop\">" +
                     "<SecureStop version=\"1.0\" >" +
                     "<SessionID>" + encodedSessionId + "</SessionID>" +
                     "<CustomData>" + encodedCustomData + "</CustomData>" +
                     "<ServerCert>" + encodedPublisherCert + "</ServerCert>" +
                     "</SecureStop></PlayReadyCDMData>";
    
    var int8ArrayCDMdata = null

    // TODO: Convert CDMDataStr to Uint8 byte array and palce the converted result to int8ArrayCDMdata

    return int8ArrayCDMdata;
}
```

> [!NOTE]
> 上記のサンプルのセキュリティで保護された停止データは、 `<SessionID>B64 encoded session ID</SessionID>` アスタリスク () にすることができ \* ます。これは、記録されたすべてのセキュリティ停止セッションのワイルドカードです。 つまり、 **SessionID** タグは、特定のセッション、またはワイルドカード () を使用し \* て、すべてのセキュリティで保護された停止セッションを選択できます。

## <a name="programming-considerations-for-encrypted-media-extension"></a>Encrypted Media Extension のプログラミングについての考慮事項

このセクションでは、PlayReady 対応の Windows 10 用の Web アプリを作成するときに検討する必要があるプログラミングの考慮事項を示します。

アプリで作成した **MSMediaKeys** オブジェクトと **MSMediaKeySession** オブジェクトは、アプリが終了するまで有効なままである必要があります。 これらのオブジェクトが必ず有効な状態にとどまるようにする方法の 1 つは、それらをグローバル変数として割り当てることです (関数内でローカル変数宣言された場合、変数はスコープ外になり、ガベージ コレクションの対象になります)。 たとえば、次のサンプルでは、変数 *g \_ msmediakeys* と *g \_ mediakeysession* をグローバル変数として割り当てます。この変数は、関数の **msmediakeys** オブジェクトと **msmediakeysession** オブジェクトに割り当てられます。

``` syntax
var g_msMediaKeys;
var g_mediaKeySession;

function foo() {
  ...
  g_msMediaKeys = new MSMediaKeys("com.microsoft.playready");
  ...
  g_mediaKeySession = g_msMediaKeys.createSession("video/mp4", intiData, null);
  g_mediaKeySession.addEventListener(this.KEYMESSAGE_EVENT, function (e) 
  {
    ...
    downloadPlayReadyKey(url, keyMessage, function (data) 
    {
      g_mediaKeySession.update(data);
    });
  });
  g_mediaKeySession.addEventListener(this.KEYADDED_EVENT, function () 
  {
    ...
    g_mediaKeySession.close();
    g_mediaKeySession = null;
  });
}
```

詳しくは、[サンプル アプリケーション](https://github.com/microsoft/Windows-universal-samples/tree/master/Samples/PlayReady)をご覧ください。

## <a name="see-also"></a>関連項目
- [PlayReady DRM](playready-client-sdk.md)