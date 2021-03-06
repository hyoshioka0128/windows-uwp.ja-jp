---
ms.assetid: B0AD0B8E-867E-4403-9CF6-43C81F3C30CA
description: Microsoft Store 送信 API でこのメソッドを使用して、パートナー センター アカウントに登録されているアプリのパッケージのフライト情報を取得します。
title: アプリのパッケージ フライトの取得
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, フライト, パッケージ フライト
ms.localizationpriority: medium
ms.openlocfilehash: 66e64f2c499835a345bb9563fd005b86a926a4d2
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372014"
---
# <a name="get-package-flights-for-an-app"></a>アプリのパッケージ フライトの取得

Microsoft Store 送信 API でこのメソッドを使用して、パートナー センター アカウントに登録されているアプリのパッケージのフライトを一覧表示します。 パッケージ フライトについて詳しくは、「[パッケージ フライト](https://docs.microsoft.com/windows/uwp/publish/package-flights)」をご覧ください。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| メソッド | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/listflights` |


### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

|  名前  |  種類  |  説明  |  必須  |
|------|------|------|------|
|  applicationId  |  string  |  パッケージ フライトを取得するアプリのストア ID です。 ストア ID について詳しくは、「[アプリ ID の詳細の表示](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)」をご覧ください。  |  〇  |
|  top  |  int  |  要求で返される項目の数 (つまり、返されるパッケージ フライトの数)。 クエリで指定した値よりアカウントのパッケージ フライトの数が多い場合、応答本文には、データの次のページを要求するためにメソッド URI に追加できる相対 URI パスが含まれます。  |  X  |
|  skip  |  int  |  残りの項目を返す前にクエリでバイパスする項目の数。 データ セットを操作するには、このパラメーターを使用します。 たとえば、top = 10 と skip = 0 は、1 から 10 の項目を取得し、top=10 と skip=10 は 11 から 20 の項目を取得するという具合です。  |  X  |


### <a name="request-body"></a>要求本文

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、アプリのすべてのパッケージ フライトを一覧表示する方法を示しています。

```json
GET https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/listflights HTTP/1.1
Authorization: Bearer <your access token>
```

次の例は、アプリの 1 番目のパッケージ フライトを表示する方法を示しています。

```json
GET https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315/listflights?top=1 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

次の例は、合計 3 個のパッケージ フライトがあるアプリの、1 番目のパッケージ フライトに対する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
  "value": [
    {
      "flightId": "7bfc11d5-f710-47c5-8a98-e04bb5aad310",
      "friendlyName": "myflight",
      "lastPublishedFlightSubmission": {
        "id": "1152921504621086517",
        "resourceLocation": "flights/7bfc11d5-f710-47c5-8a98-e04bb5aad310/submissions/1152921504621086517"
      },
      "pendingFlightSubmission": {
        "id": "1152921504621215786",
        "resourceLocation": "flights/7bfc11d5-f710-47c5-8a98-e04bb5aad310/submissions/1152921504621215786"
      },
      "groupIds": [
        "1152921504606962205"
      ],
      "rankHigherThan": "Non-flighted submission"
    }
  ],
  "totalCount": 3
}
```

### <a name="response-body"></a>応答本文

| Value      | 種類   | 説明       |
|------------|--------|---------------------|
| @nextLink  | string | データの追加ページが存在する場合、この文字列には、データの次のページを要求するために、ベースとなる `https://manage.devcenter.microsoft.com/v1.0/my/` 要求 URI に追加できる相対パスが含まれます。 たとえば、最初の要求本文の *top* パラメーターが 2 に設定されていて、アプリには 4 個のパッケージ フライトが存在する場合、応答本文には、`applications/{applicationid}/listflights/?skip=2&top=2` という @nextLink 値が含まれます。これは、次の 2 個のパッケージ フライトを要求するために、`https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationid}/listflights/?skip=2&top=2` を呼び出すことができることを示しています。 |
| value      | array  | 指定されたアプリのパッケージ フライトに関する情報を提供するオブジェクトの配列。 各オブジェクトのデータについて詳しくは、「[フライト リソース](get-app-data.md#flight-object)」をご覧ください。               |
| totalCount | int    | クエリのデータ結果の行の合計数 (つまり、指定されたアプリのパッケージ フライトの合計数)。   |


## <a name="error-codes"></a>エラー コード

要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。

| エラー コード |  説明   |
|--------|------------------|
| 404  | パッケージ フライトは見つかりませんでした。 |
| 409  | アプリはパートナー センター機能を使用する[現在サポートされていません、Microsoft Store 送信 API](create-and-manage-submissions-using-windows-store-services.md#not_supported)します。  |


## <a name="related-topics"></a>関連トピック

* [作成し、Microsoft Store サービスを使用して送信の管理](create-and-manage-submissions-using-windows-store-services.md)
* [すべてのアプリを入手します。](get-all-apps.md)
* [アプリを取得します。](get-an-app.md)
* [アプリのアドオンを入手します。](get-add-ons-for-an-app.md)
