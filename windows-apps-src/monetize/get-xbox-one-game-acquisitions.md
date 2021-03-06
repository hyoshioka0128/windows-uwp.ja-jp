---
ms.assetid: C1E42E8B-B97D-4B09-9326-25E968680A0F
description: 日付範囲やその他のオプション フィルターを指定して、Xbox One ゲームに関する集計入手データを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。
title: Xbox One ゲームの入手数の取得
ms.date: 10/18/2018
ms.topic: article
keywords: Windows 10, UWP, Store サービス, Microsoft Store 分析 API, Xbox One ゲームの入手数
ms.localizationpriority: medium
ms.openlocfilehash: 0fbb9a5c33cfb218bc3dc51ddf217ddf9735a2b6
ms.sourcegitcommit: e63fbd7a63a7e8c03c52f4219f34513f4b2bb411
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "57822897"
---
# <a name="get-xbox-one-game-acquisitions"></a>Xbox One ゲームの入手数の取得

このメソッドを使用して、Microsoft Store analytics API 取得の集計データを取得する JSON 形式で、Xbox One ゲーム Xbox 開発者ポータル (XDP) を取り込んだして XDP Analytics ダッシュ ボードで使用できます。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 分析 API に関するすべての[前提条件](access-analytics-data-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>要求


### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI       |
|--------|----------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/acquisitions``` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

| パラメーター        | 種類   |  説明      |  必須  
|---------------|--------|---------------|------|
| applicationId | string | 入手データを取得する Xbox One ゲームの製品 ID です。 これが Store ID と XDP 製品 ID ではないことに注意してください。 ゲームの製品 ID を取得するには、XDP 分析プログラムでゲームに移動し、URL から、製品 ID を取得します。 または、パートナー センターの分析レポートから買収データをダウンロードする場合は、.tsv ファイルで製品 ID が含まれます。  |  〇  |
| startDate | date | 取得する入手データの日付範囲の開始日です。 既定値は現在の日付です。 |  X  |
| endDate | date | 取得する入手データの日付範囲終了日です。 既定値は現在の日付です。 |  X  |
| top | int | 返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |  X  |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=10000 と skip=0 を指定すると、データの最初の 10,000 行が取得され、top=10000 と skip=10000 を指定すると、データの次の 10,000 行が取得されます。 |  X  |
| filter | string  | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各ステートメントには、応答本文からのフィールド名、および **eq** 演算子または **ne** 演算子と関連付けられる値が含まれており、**and** や **or** を使用してステートメントを組み合わせることができます。 *filter* パラメーターでは、文字列値を単一引用符で囲む必要があります。 たとえば、「*filter=market eq 'US' and gender eq 'm'*」のように指定します。 <p/><p/>応答本文から次のフィールドを指定することができます。<p/><ul><li><strong>acquisitionType</strong></li><li><strong>経過時間</strong></li><li><strong>storeClient</strong></li><li><strong>性別</strong></li><li><strong>market</strong></li><li><strong>osVersion</strong></li><li><strong>deviceType</strong></li><li><strong>sandboxId</strong></li></ul> | X   |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。<strong>day</strong>、<strong>week</strong>、または <strong>month</strong>。 指定しない場合、既定値は <strong>day</strong> です。 | X |
| orderby | string | それぞれの入手数について結果データ値の順序を指定するステートメントです。 構文は <em>orderby=field [order],field [order],...</em> です。<em>field</em> パラメーターには、次のいずれかの文字列を指定できます。<ul><li><strong>date</strong></li><li><strong>acquisitionType</strong></li><li><strong>経過時間</strong></li><li><strong>storeClient</strong></li><li><strong>性別</strong></li><li><strong>market</strong></li><li><strong>osVersion</strong></li><li><strong>deviceType</strong></li><li><strong>paymentInstrumentType</strong></li><li><strong>sandboxId</strong></li><li><strong>xboxTitleIdHex</strong></li></ul><p><em>order</em> パラメーターは省略可能であり、<strong>asc</strong> または <strong>desc</strong> を指定して、各フィールドを昇順または降順にすることができます。 既定値は <strong>asc</strong> です。</p><p><em>orderby</em> 文字列の例: <em>orderby=date,market</em></p> |  X  |
| groupby | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 次のフィールドを指定できます。<ul><li><strong>date</strong></li><li><strong>applicationName</strong></li><li><strong>acquisitionType</strong></li><li><strong>ageGroup</strong></li><li><strong>storeClient</strong></li><li><strong>性別</strong></li><li><strong>market</strong></li><li><strong>osVersion</strong></li><li><strong>deviceType</strong></li><li><strong>paymentInstrumentType</strong></li><li><strong>sandboxId</strong></li><li><strong>xboxTitleIdHex</strong></li></ul><p>返されるデータ行には、<em>groupby</em> パラメーターに指定したフィールドと次の値が含まれます。</p><ul><li><strong>date</strong></li><li><strong>applicationId</strong></li><li><strong>acquisitionQuantity</strong></li></ul><p><em>groupby</em> パラメーターは、<em>aggregationLevel</em> パラメーターと同時に使用できます。 例: <em>&amp;groupby=ageGroup,market&amp;aggregationLevel=week</em></p> |  X  |


### <a name="request-example"></a>要求の例

Xbox One ゲームの入手データを取得するための要求の例を、いくつか次に示します。 置換、 *applicationId*ゲームの製品 ID を持つ値。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/acquisitions?applicationId=BRRT4NJ9B3D1&startDate=1/1/2017&endDate=2/1/2017&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>

GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/xbox/acquisitions?applicationId=BRRT4NJ9B3D1&startDate=8/1/2017&endDate=8/31/2017&skip=0&filter=market eq 'US' and gender eq 'm' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答


### <a name="response-body"></a>応答本文

| Value      | 種類   | 説明                  |
|------------|--------|-------------------------------------------------------|
| Value      | array  | ゲームに関する集計入手データを含むオブジェクトの配列です。 各オブジェクト内のデータについて詳しくは、後の「[入手値](#acquisition-values)」セクションをご覧ください。                                                                                                                      |
| @nextLink  | string | データの追加ページがある場合、この文字列には、データの次のページを要求するために使用できる URI が含まれます。 たとえば、要求の **top** パラメーターが 10000 に設定されたが、クエリの入手データに 10,000 を超える行が含まれている場合に、この値が返されます。 |
| TotalCount | int    | クエリの結果データ内の行の総数です。              |


### <a name="acquisition-values"></a>入手値

*Value* 配列の要素には、次の値が含まれます。

| Value               | 種類   | 説明                           |
|---------------------|--------|-------------------------------------------|
| date                | string | 入手データの日付範囲の最初の日付です。 要求に日付を指定した場合、この値はその日付になります。 要求に週、月、またはその他の日付範囲を指定した場合、この値はその日付範囲の最初の日付になります。 |
| applicationId       | string | 入手データを取得する Xbox One ゲームの製品 ID です。 これが Store ID と XDP 製品 ID ではないことに注意してください。  |
| applicationName     | string | ゲームの表示名です。       |
| acquisitionType     | string | 入手の種類を示す、以下のいずれかの文字列です。<ul><li><strong>無料</strong></li><li><strong>試用版</strong></li><li><strong>有料</strong></li><li><strong>プロモーション コード</strong></li><li><strong>Iap</strong></li><li><strong>サブスクリプション Iap</strong></li><li><strong>プライベートの対象ユーザー</strong></li><li><strong>前の順序</strong></li><li><strong>Xbox Game Pass</strong> (または、2018 年 3 月 23 日より前のデータを照会した場合は <strong>Game Pass</strong>)</li><li><strong>Disk</strong></li><li><strong>前払いコード</strong></li><li><strong>課金の事前注文</strong></li><li><strong>前の取り消された順序</strong></li><li><strong>障害が発生した以前の注文</strong></li></ul>    |
| age                 | string | 入手したユーザーの年齢グループを示す、以下のいずれかの文字列です。<ul><li><strong>小さい 13</strong></li><li><strong>13-17</strong></li><li><strong>18-24</strong></li><li><strong>25-34</strong></li><li><strong>35-44</strong></li><li><strong>44-55</strong></li><li><strong>55 より大きい</strong></li><li><strong>Unknown</strong></li></ul>     |
| deviceType          | string | 入手が完了したデバイスの種類を指定する、以下のいずれかの文字列です。<ul><li><strong>PC</strong></li><li><strong>Phone</strong></li><li><strong>Console</strong></li><li><strong>IoT</strong></li><li><strong>[サーバー]</strong></li><li><strong>タブレット</strong></li><li><strong>Holographic</strong></li><li><strong>Unknown</strong></li></ul>  |
| gender              | string | 入手したユーザーの性別を指定する、以下のいずれかの文字列です。<ul><li><strong>m</strong></li><li><strong>f</strong></li><li><strong>Unknown</strong></li></ul>     |
| market              | string | 入手が発生した市場の ISO 3166 国コードです。  |
| osVersion           | string | 入手が発生した OS のバージョンです。 このメソッドでは、この値は常に **Windows 10** になります。</li></ul>    |
| paymentInstrumentType           | string | 入手に使われた支払い方法を示す、以下のいずれかの文字列です。<ul><li><strong>クレジット_カード</strong></li><li><strong>直接デビット カード</strong></li><li><strong>推論による発注</strong></li><li><strong>MS 分散</strong></li><li><strong>通信事業者</strong></li><li><strong>オンライン銀行振込</strong></li><li><strong>PayPal</strong></li><li><strong>分割されたトランザクション</strong></li><li><strong>トークンの引き換え</strong></li><li><strong>0 個の支払額</strong></li><li><strong>eWallet</strong></li><li><strong>Unknown</strong></li></ul>    |
| sandboxId              | string | ゲーム用に作成されたサンドボックス ID です。 これは値 **RETAIL** か、またはプライベート サンドボックスの ID になります。  |
| storeClient         | string | 入手が発生した Store のバージョンを示す、以下のいずれかの文字列です。<ul><li>**Windows Phone ストア (クライアント)**</li><li>**Microsoft Store (client)** (または、2018 年 3 月 23 日より前のデータを照会した場合は **Windows Store (client)**)</li><li>**Microsoft Store (web)** (または、2018 年 3 月 23 日より前のデータを照会した場合は **Windows Store (web)**)</li><li>**組織でボリューム購入**</li><li>**その他**</li></ul>                             |
| xboxTitleIdHex              | string | Xbox デベロッパー ポータル (XDP) によって Xbox Live 対応ゲームに割り当てられた Xbox Live タイトル ID (16 進数表記) です。  |
| acquisitionQuantity | number | 指定された集計レベルで発生した入手の数です。     |
| purchasePriceUSDAmount | number | 入手時にユーザーが支払った金額を、月ごとの為替レートを使って米国ドルに換算した値です。    |
| taxUSDAmount     | number | 入手時に適用された税額を米国ドルに換算した値です。 |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
    {
      "date": "2017-02-01",
      "applicationId": "BRRT4NJ9B3D1 ",
      "applicationName": "Contoso Game",
      "acquisitionType": "Paid",
      "age": "35-49",
      "deviceType": "Console",
      "gender": "m",
      "market": "US",
      "osVersion": "Windows 10",
      "PaymentInstrumentType": "Credit Card ",
      "sandboxId": "RETAIL",
      "storeClient": "Windows Store (web)",
      "xboxTitleIdHex": "",
      "acquisitionQuantity": 1,
      "purchasePriceUSDAmount": 29.99,
      "taxUSDAmount": 2.99
    }
  ],
  "@nextLink": "xbox/acquisitions?applicationId=BRRT4NJ9B3D1&aggregationLevel=day&startDate=2017/02/01&endDate=2017/03/01&top=1&skip=1&orderby=date desc",
  "TotalCount": 39812
}
```

## <a name="related-topics"></a>関連トピック

* [Microsoft Store サービスを使用して分析データにアクセス](access-analytics-data-using-windows-store-services.md)
