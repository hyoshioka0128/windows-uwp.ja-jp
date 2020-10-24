---
ms.assetid: DD4F6BC4-67CD-4AEF-9444-F184353B0072
description: 日付範囲やその他のオプション フィルターを指定して集計評価データを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。
title: アプリの評価の取得
ms.date: 11/29/2017
ms.topic: article
keywords: Windows 10, UWP, Store サービス, Microsoft Store 分析 API, 評価
ms.localizationpriority: medium
ms.openlocfilehash: 228f567ecb0d89f2e5af0b53c7105aa9a9fca213
ms.sourcegitcommit: c1226b6b9ec5ed008a75a3d92abb0e50471bb988
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2020
ms.locfileid: "86492927"
---
# <a name="get-app-ratings"></a>アプリの評価の取得

日付範囲やその他のオプション フィルターを指定して、集計評価データを JSON 形式で取得するには、Microsoft Store 分析 API の以下のメソッドを使います。 この情報は、パートナーセンターの[レビューレポート](../publish/reviews-report.md)でも確認できます。

## <a name="prerequisites"></a>前提条件


このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 分析 API に関するすべての[前提条件](access-analytics-data-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。


## <a name="request"></a>Request


### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/ratings``` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 承認 | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

| パラメーター        | 種類   |  説明      |  必須  
|---------------|--------|---------------|------|
| applicationId | string | 評価データを取得するアプリの[ストア ID](in-app-purchases-and-trials.md#store-ids) 。  |  はい  |
| startDate | date | 取得する評価データの日付範囲の開始日です。 既定値は現在の日付です。 |  いいえ  |
| endDate | 日付 | 取得する評価データの日付範囲の終了日です。 既定値は現在の日付です。 |  いいえ  |
| top | INT | 要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |  いいえ  |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=10000 と skip=0 を指定すると、データの最初の 10,000 行が取得され、top=10000 と skip=10000 を指定すると、データの次の 10,000 行が取得されます。 |  いいえ  |
| filter | string  | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 詳しくは、次の「[フィルター フィールド](#filter-fields)」セクションをご覧ください。 | いいえ   |
| aggregationLevel | string | 集計データを取得する時間範囲を指定します。 次のいずれかの文字列を指定できます。<strong>day</strong>、<strong>week</strong>、または <strong>month</strong>。 指定しない場合、既定値は <strong>day</strong> です。 | いいえ |
| orderby | string | 各評価の結果データ値の順序を指定するステートメントです。 構文は <em>orderby=field [order],field [order],...</em> です。<em>field</em> パラメーターは次のいずれかの文字列になります。<ul><li><strong>date</strong></li><li><strong>osVersion</strong></li><li><strong>マーケティング</strong></li><li><strong>deviceType</strong></li><li><strong>isRevised</strong></li></ul><p><em>order</em> パラメーターは省略可能であり、<strong>asc</strong> または <strong>desc</strong> を指定して、各フィールドを昇順または降順にすることができます。 既定値は<strong>asc</strong>です。</p><p><em>orderby</em> 文字列の例: <em>orderby=date,market</em></p> |  いいえ  |
| groupby | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 次のフィールドを指定できます。<ul><li><strong>date</strong></li><li><strong>applicationName</strong></li><li><strong>マーケティング</strong></li><li><strong>osVersion</strong></li><li><strong>deviceType</strong></li><li><strong>isRevised</strong></li></ul><p>返されるデータ行には、<em>groupby</em> パラメーターに指定したフィールドと次の値が含まれます。</p><ul><li><strong>date</strong></li><li><strong>applicationId</strong></li><li><strong>fiveStars</strong></li><li><strong>fourStars</strong></li><li><strong>threeStars</strong></li><li><strong>twoStars</strong></li><li><strong>oneStar</strong></li></ul><p><em>groupby</em> パラメーターは、<em>aggregationLevel</em> パラメーターと同時に使用できます。 例: <em> &amp; Groupby = osVersion、market &amp; aggregationLevel = week</em></p> |  いいえ  |

 
### <a name="filter-fields"></a>フィルター フィールド

要求の *filter* パラメーターには、応答内の行をフィルター処理する 1 つまたは複数のステートメントが含まれます。 各ステートメントには **eq** 演算子または **ne** 演算子と関連付けられるフィールドと値が含まれ、**and** または **or** を使ってステートメントを組み合わせることができます。

*filter* 文字列の例は次のとおりです。*filter=market eq 'US' and deviceType eq 'phone' and isRevised eq true*

サポートされているフィールドの一覧については、次の表をご覧ください。 *filter* パラメーターでは、文字列値を単一引用符で囲む必要があります。

| フィールド        |  説明        |
|---------------|-----------------|
| market | アプリが評価された市場の ISO 3166 国コードを含む文字列です。 |
| osVersion | 次の文字列のいずれかです。<ul><li><strong>Windows Phone 7.5</strong></li><li><strong>Windows Phone 8</strong></li><li><strong>Windows Phone 8.1</strong></li><li><strong>Windows Phone 10</strong></li><li><strong>Windows 8</strong></li><li><strong>Windows 8.1</strong></li><li><strong>Windows 10</strong></li><li><strong>Unknown</strong></li></ul> |
| deviceType | 次の文字列のいずれかです。<ul><li><strong>PC</strong></li><li><strong>ダイヤル</strong></li><li><strong>コンソール-Xbox One</strong></li><li><strong>コンソール-Xbox シリーズ X</strong></li><li><strong>IoT</strong></li><li><strong>Holographic</strong></li><li><strong>Unknown</strong></li></ul> |
| isRevised | 更新されている評価をフィルター処理するには <strong>true</strong> を指定します。それ以外の場合は <strong>false</strong> を指定します。 |


### <a name="request-example"></a>要求の例

評価データを取得するためのいくつかの要求の例を次に示します。 *applicationId* 値を、目的のアプリのストア ID に置き換えてください。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/ratings?applicationId=9NBLGGGZ5QDR&startDate=1/1/2015&endDate=2/1/2015&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>

GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/ratings?applicationId=9NBLGGGZ5QDR&startDate=8/1/2015&endDate=8/31/2015&skip=0&filter=market eq 'US' and deviceType eq 'phone' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]


### <a name="response-body"></a>応答本文

| 値      | 種類   | 説明                                                                                                                                                                                                                                                                            |
|------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 値      | array  | 集計評価データが含まれるオブジェクトの配列です。 各オブジェクトのデータについて詳しくは、次の「[評価値](#rating-values)」セクションをご覧ください。                                                                                                                           |
| @nextLink  | string | データの追加ページがある場合、この文字列には、データの次のページを要求するために使用できる URI が含まれます。 たとえば、要求の **top** パラメーターを 10000 に設定した場合、クエリに適合する評価データが 10,000 行を超えると、この値が返されます。 |
| TotalCount | INT    | クエリの結果データ内の行の総数です。                               |


### <a name="rating-values"></a>評価値

*Value* 配列の要素には、次の値が含まれます。

| 値           | 種類    | 説明       |
|-----------------|---------|-------------------|
| date            | string  | 評価データの日付範囲の最初の日付です。 要求に日付を指定した場合、この値はその日付になります。 要求に週、月、またはその他の日付範囲を指定した場合、この値はその日付範囲の最初の日付になります。 |
| applicationId   | string  | 評価データを取得するアプリのストア ID です。         |
| applicationName | string  | アプリの表示名です。    |
| market          | string  | 評価が送信された市場の ISO 3166 国コードです。        |
| osVersion       | string  | 評価が送信された OS バージョンです。 サポートされる文字列の一覧については、前の「[フィルター フィールド](#filter-fields)」セクションをご覧ください。            |
| deviceType      | string  | 評価が送信されたデバイスの種類です。 サポートされる文字列の一覧については、前の「[フィルター フィールド](#filter-fields)」セクションをご覧ください。            |
| isRevised       | ブール値 | 値 **true** は、評価が更新済みであることを示します。それ以外の場合は **false** です。   |
| oneStar         | number  | 1 つ星評価の数です。        |
| twoStars        | number  | 2 つ星評価の数です。    |
| threeStars      | number  | 3 つ星評価の数です。   |
| fourStars       | number  | 4 つ星評価の数です。    |
| fiveStars       | number  | 5 つ星評価の数です。    |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
    {
      "date": "2015-02-13",
      "applicationId": "9NBLGGGZ5QDR",
      "applicationName": "Contoso demo",
      "market": "CN",
      "osVersion": "8.0.10517.0",
      "deviceType": "Phone",
      "isRevised": false,
      "oneStar": 0,
      "twoStars": 0,
      "threeStars": 0,
      "fourStars": 0,
      "fiveStars": 2
    }
  ],
  "@nextLink": "ratings?applicationId=9NBLGGGZ5QDR&aggregationLevel=day&startDate=2015/01/01&endDate=2016/02/01&top=1&skip=1",
  "TotalCount": 15242
}

```

## <a name="related-topics"></a>関連トピック

* [評価レポート](../publish/reviews-report.md)
* [Microsoft Store サービスを使った分析データへのアクセス](access-analytics-data-using-windows-store-services.md)
* [アプリの入手数の取得](get-app-acquisitions.md)
* [アドオンの入手数の取得](get-in-app-acquisitions.md)
* [エラー報告データの取得](get-error-reporting-data.md)
* [アプリのレビューの取得](get-app-reviews.md)
