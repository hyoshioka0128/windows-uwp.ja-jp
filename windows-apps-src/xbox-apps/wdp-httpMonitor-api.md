---
title: Device Portal の HTTP モニター API のリファレンス
description: /Ext/httpmonitor/sessions Xbox デバイスポータル REST API を使用して、Xbox 上のフォーカスのあるアプリからリアルタイムの HTTP トラフィックにアクセスする方法について説明します。
ms.localizationpriority: medium
ms.topic: article
ms.date: 02/08/2017
ms.openlocfilehash: 6ea53f6356aa89a83f3b267a65f65b32aad5749d
ms.sourcegitcommit: 5481bb34def681bc60fbfa42d9779053febec468
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304534"
---
# <a name="http-monitor-api-reference"></a>HTTP モニター API のリファレンス   
Dev Home のチェック ボックスをオンにすることにより Xbox 本体で HTTP モニターが有効になっている場合、この API を使用してフォーカスのあるアプリのリアルタイム HTTP トラフィックにアクセスできます。

## <a name="get-if-the-http-monitor-is-enabled"></a>HTTP モニターが有効かどうかを取得

**Request**

Dev Home で HTTP モニターが有効になっているかどうかを取得できます。

Method      | 要求 URI
:------     | :-----
GET | /ext/httpmonitor/sessions

**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**   
次のフィールドを含む JSON オブジェクト。

* Enabled - (ブール値) Dev Home でチェック ボックスをオンにすることにより Xbox 本体で HTTP モニターが有効になっているかどうか。

**status code**

この API では次の状態コードが返される可能性があります。

HTTP 状態コード      | 説明
:------     | :-----
200 | 要求は成功しました
4XX | エラー コード
5XX | エラー コード

## <a name="get-http-traffic-from-the-focused-app"></a>フォーカスのあるアプリから HTTP トラフィックを取得します。

**Request**

Dev Home で HTTP モニターが有効になっている場合は、Xbox のフォーカスのあるアプリ (システム アプリでない限り) からリアルタイムで HTTP トラフィックを取得します。

Method      | 要求 URI
:------     | :-----
WebSocket | /ext/httpmonitor/sessions

**URI パラメーター**

- なし

**要求ヘッダー**

- なし

**要求本文**

- なし

**応答**   
次のフィールドを含む JSON オブジェクト。

* セッション
    * RequestHeaders - (JSON オブジェクト) HTTP 要求からの要求ヘッダー。
    * RequestContentHeaders - (JSON オブジェクト) HTTP 要求からの要求コンテンツ ヘッダー。
    * RequestURL - (文字列) 要求 URL。
    * RequestMethod - (文字列) 要求メソッド。
    * RequestMessage - (文字列) 要求メッセージは、現在のところ JSON およびテキスト コンテンツのみをサポートしています。
    * ResponseHeaders - (JSON オブジェクト) HTTP 応答からの応答ヘッダー。
    * ResponseContentHeaders - (JSON オブジェクト) HTTP 応答からの応答コンテンツ ヘッダー。
    * StatusCode - (数値) 応答状態コード。
    * ReasponsePhrase - (文字列) 応答理由フレーズ。
    * ResponseMessage - (文字列) 応答メッセージは、現在のところ JSON およびテキスト コンテンツのみをサポートしています。

**status code**

この API では次の状態コードが返される可能性があります。

HTTP 状態コード      | 説明
:------     | :-----
200 | 要求は成功しました
4XX | エラー コード
403 | HTTP モニターが無効になっています。Dev Home で有効にする必要があります。
5XX | エラー コード


**利用可能なデバイス ファミリ**

* Windows Xbox