---
description: Xbox Live の実績データを取得するには、Microsoft Store 分析 API の以下のメソッドを使います。
title: Xbox Live の実績データの取得
ms.date: 06/04/2018
ms.topic: article
keywords: Windows 10, UWP, Store サービス, Microsoft Store 分析 API, Xbox Live 分析, 実績
ms.localizationpriority: medium
ms.openlocfilehash: 422024445be4662aab0a47b5527369c8b7091446
ms.sourcegitcommit: 6f32604876ed480e8238c86101366a8d106c7d4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2019
ms.locfileid: "67317769"
---
# <a name="get-xbox-live-achievements-data"></a>Xbox Live の実績データの取得

[Xbox Live 対応ゲーム](https://docs.microsoft.com/gaming/xbox-live/index.md)の各実績のロックを解除したユーザーの数を取得するには、Microsoft Store 分析 API の以下のメソッドを使います。実績データがある直近の日付、その日から過去 30 日間、およびゲームのリリースからその日までの期間のデータを取得できます。 この情報も記載されて、 [Xbox analytics レポート](../publish/xbox-analytics-report.md)パートナー センターでします。

> [!IMPORTANT]
> このメソッドは、Xbox のゲームまたは Xbox Live サービスを使用するゲームのみサポートします。 これらのゲームは、[概念の承認プロセス](../gaming/concept-approval.md)を完了する必要があります。これには、[Microsoft パートナー](https://docs.microsoft.com/gaming/xbox-live/developer-program-overview.md#microsoft-partners)が発行したゲームと [ID@Xbox プログラム](https://docs.microsoft.com/gaming/xbox-live/developer-program-overview.md#id)を介して申請されたゲームが含まれます。 このメソッドでは、[Xbox Live クリエーターズ プログラム](https://docs.microsoft.com/gaming/xbox-live/get-started-with-creators/get-started-with-xbox-live-creators.md)を介して発行されたゲームは現在サポートされていません。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 分析 API に関するすべての[前提条件](access-analytics-data-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>要求


### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI       |
|--------|----------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/gameanalytics``` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター


| パラメーター        | 種類   |  説明      |  必須  
|---------------|--------|---------------|------|
| applicationId | string | Xbox Live の実績データを取得するゲームの [Store ID](in-app-purchases-and-trials.md#store-ids) です。  |  〇  |
| metricType | string | 取得する Xbox Live 分析データの種類を指定する文字列です。 このメソッドでは、値 **achievements** を指定します。  |  〇  |
| top | int | 要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |  X  |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=10000 と skip=0 を指定すると、データの最初の 10,000 行が取得され、top=10000 と skip=10000 を指定すると、データの次の 10,000 行が取得されます。 |  X  |


### <a name="request-example"></a>要求の例

次の例では、Xbox Live 対応ゲームで最初の 10 個の実績のロックを解除したユーザーの実績データを取得する要求を示します。 *applicationId* の値は、ゲームの Store ID に置き換えてください。


```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/gameanalytics?applicationId=9NBLGGGZ5QDR&metrictype=achievements&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

| Value      | 種類   | 説明                  |
|------------|--------|-------------------------------------------------------|
| Value      | array  | 対象ゲームの各実績のデータを含むオブジェクトの配列です。 各オブジェクトのデータの詳細については、以下の表を参照してください。                                                                                                                      |
| @nextLink  | string | データの追加ページがある場合、この文字列には、データの次のページを要求するために使用できる URI が含まれます。 たとえば、要求の **top** パラメーターが 100 に設定されていたとき、クエリに対して 100 行を超えるデータが一致すると、この値が返されます。 |
| TotalCount | int    | クエリの結果データ内の行の総数です。  |


*Value* 配列の要素には、次の値が含まれます。

| Value               | 種類   | 説明                           |
|---------------------|--------|-------------------------------------------|
| applicationId       | string | 実績データを取得しているゲームの Store ID です。     |
| reportDateTime     | string |  実績データの日付です。    |
| achievementId          | number |  実績の ID です。 |
| achievementName           | string | 実績の名前です。  |
| gamerscore           | number |  実績のゲーマースコア リワードです。  |
| dailyUnlocks           | number |  *reportDateTime* で指定された日付に実績のロックを解除したユーザーの数です。  |
| monthlyUnlocks              | number |  *reportDateTime* で指定された日付から過去 30 日間に実績のロックを解除したユーザーの数です。   |
| totalUnlocks | number |  ゲームのリリースから *reportDateTime* で指定された日付までの期間に実績のロックを解除したユーザーの数です。   |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
    {
      "applicationId": "9NBLGGGZ5QDR",
      "reportDateTime": "2018-01-30T00:00:00",
      "achievementId": 6,
      "achievementName": "Yoink!",
      "gamerscore": 10,
      "dailyUnlocks": 0,
      "monthlyUnlocks": 10310,
      "totalUnlocks": 1215360
    },
    {
      "applicationId": "9NBLGGGZ5QDR",
      "reportDateTime": "2018-01-30T00:00:00",
      "achievementId": 7,
      "achievementName": "Ding!",
      "gamerscore": 10,
      "dailyUnlocks": 0,
      "monthlyUnlocks": 10897,
      "totalUnlocks": 1282524
    },
    {
      "applicationId": "9NBLGGGZ5QDR",
      "reportDateTime": "2018-01-30T00:00:00",
      "achievementId": 8,
      "achievementName": "End of the Beginning",
      "gamerscore": 30,
      "dailyUnlocks": 0,
      "monthlyUnlocks": 9848,
      "totalUnlocks": 1105074
    }
  ],
  "@nextLink": null,
  "TotalCount": 3
}
```

## <a name="related-topics"></a>関連トピック

* [Microsoft Store サービスを使用して分析データにアクセス](access-analytics-data-using-windows-store-services.md)
* [Xbox Live analytics データを取得します。](get-xbox-live-analytics.md)
* [Xbox Live の正常性データを取得します。](get-xbox-live-health-data.md)
* [Xbox Live Game ハブのデータを取得します。](get-xbox-live-game-hub-data.md)
* [Xbox Live クラブ活動用のデータを取得します。](get-xbox-live-club-data.md)
* [Xbox Live のマルチ プレーヤー データを取得します。](get-xbox-live-multiplayer-data.md)
