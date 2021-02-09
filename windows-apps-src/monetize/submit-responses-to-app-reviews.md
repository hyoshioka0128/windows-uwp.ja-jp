---
ms.assetid: 038903d6-efab-4da6-96b5-046c7431e6e7
description: アプリのレビューに返信を送るには、Microsoft Store レビュー API の以下のメソッドを使います。
title: レビューに対する返信の送信
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, Store サービス, Microsoft Store レビュー API, アドオンの入手数
ms.localizationpriority: medium
ms.openlocfilehash: 9cf62f5f619eba0431f1398a391eef03b47bb13d
ms.sourcegitcommit: 140bbbab0f863a7a1febee85f736b0412bff1ae7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91984638"
---
# <a name="submit-responses-to-reviews"></a>レビューに対する返信の送信


アプリのレビューにプログラムで返信するには、Microsoft Store レビュー API の以下のメソッドを使います。 このメソッドを呼び出すときは、返信するレビューの ID を指定する必要があります。 レビュー ID は、Microsoft Store 分析 API の[アプリのレビューの取得](get-app-reviews.md)メソッドの応答データ、および[レビュー レポート](../publish/reviews-report.md)の[オフライン ダウンロード](../publish/download-analytic-reports.md)で取得できます。

顧客はレビューを送信するときに、レビューへの返信を受け取らないことを選択できます。 顧客が返信を受け取らないように指定しているレビューに返信すると、このメソッドの返信の本文には、返信ができなかったことが示されます。 このメソッドを呼び出す前に、任意で、[アプリのレビューへの返信情報の取得](get-response-info-for-app-reviews.md)メソッドを使用して、特定のレビューへの返信が許可されているかどうかを確認できます。

> [!NOTE]
> この方法を使用して、プログラムでレビューに応答するだけでなく、 [パートナーセンターを使用して](../publish/respond-to-customer-reviews.md)レビューに応答することもできます。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store レビュー API に関するすべての[前提条件](respond-to-reviews-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](respond-to-reviews-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。
* 返信するレビューの ID を取得します。 レビュー ID は、Microsoft Store 分析 API の[アプリのレビューの取得](get-app-reviews.md)メソッドの応答データ、および[レビュー レポート](../publish/reviews-report.md)の[オフライン ダウンロード](../publish/download-analytic-reports.md)で取得できます。

## <a name="request"></a>Request

### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| POST    | ```https://manage.devcenter.microsoft.com/v1.0/my/reviews/responses``` |


### <a name="request-header"></a>要求ヘッダー

| Header        | Type   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 承認 | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

このメソッドには要求パラメーターはありません。


### <a name="request-body"></a>要求本文

要求本文には次の値が含まれます。

| 値        | Type   | 説明                                                                 |
|---------------|--------|-----------------------------------------|
| 応答 | array | 提出する返信を含むオブジェクトの配列です。 各オブジェクトのデータの詳細については、以下の表を参照してください。 |


*Responses* 配列内の各オブジェクトには、次の値が保持されています。

| 値        | Type   | 説明           |  必須  |
|---------------|--------|-----------------------------|-----|
| ApplicationId | string |  返信対象のレビューがあるアプリのストア ID です。 ストア ID は、パートナーセンターの [ [アプリ id] ページ](../publish/view-app-identity-details.md) で使用できます。 ストア ID は、たとえば 9WZDNCRFJ3Q8 のような文字列です。   |  はい  |
| ReviewId | string |  返信するレビューの ID です (これは GUID です)。 レビュー ID は、Microsoft Store 分析 API の[アプリのレビューの取得](get-app-reviews.md)メソッドの応答データ、および[レビュー レポート](../publish/reviews-report.md)の[オフライン ダウンロード](../publish/download-analytic-reports.md)で取得できます。   |  はい  |
| ResponseText | string | 提出する返信です。 返信は、[こちらのガイドライン](../publish/respond-to-customer-reviews.md#guidelines-for-responses)に従う必要があります。   |  はい  |
| SupportEmail | string | アプリのサポート メール アドレスです。顧客はこのアドレスを使用して、直接連絡できます。 したがって、有効なメール アドレスである必要があります。     |  はい  |
| IsPublic | Boolean |  **True**を指定すると、お客様のアプリのストアの一覧に、顧客のレビューのすぐ下に応答が表示され、すべてのお客様に表示されます。 **False**を指定し、ユーザーが電子メールによる応答を受信していない場合は、電子メールで顧客に返信が送信され、アプリのストアの一覧にある他の顧客には表示されません。 **False**を指定し、ユーザーが電子メールの応答を受信しない場合は、エラーが返されます。   |  はい  |


### <a name="request-example"></a>要求の例

次の例は、このメソッドを使用して、いくつかのレビューに返信を提出する方法を示しています。

```json
POST https://manage.devcenter.microsoft.com/v1.0/my/reviews/responses HTTP/1.1
Authorization: Bearer <your access token>
Content-Type: application/json
{
  "Responses": [
    {
      "ApplicationId": "9WZDNCRFJ3Q8",
      "ReviewId": "6be543ff-1c9c-4534-aced-af8b4fbe0316",
      "ResponseText": "Thank you for pointing out this bug. I fixed it and published an update, you should have the fix soon",
      "SupportEmail": "support@contoso.com",
      "IsPublic": true
    },
    {
      "ApplicationId": "9NBLGGH1RP08",
      "ReviewId": "80c9671a-96c2-4278-bcbc-be0ce5a32a7c",
      "ResponseText": "Thank you for submitting your review. Can you tell more about what you were doing in the app when it froze? Thanks very much for your help.",
      "SupportEmail": "support@contoso.com",
      "IsPublic": false
    }
  ]
}
```

## <a name="response"></a>[応答]

### <a name="response-body"></a>応答本文

| 値        | Type   | 説明            |
|---------------|--------|---------------------|
| 結果 | array | 提出した各返信についてのデータを保持するオブジェクトの配列です。 各オブジェクトのデータの詳細については、以下の表を参照してください。  |


*Result* 配列内の各オブジェクトには、次の値が保持されています。

| 値        | Type   | 説明                                                                 |
|---------------|--------|-----------------------------------------------|
| ApplicationId | string |  返信対象のレビューがあるアプリのストア ID です。 ストア ID は、たとえば 9WZDNCRFJ3Q8 のような文字列です。   |
| ReviewId | string |  返信するレビューの ID です。 これは GUID です。   |
| 成功 | string | 値が **true** の場合、返信が正常に送信されたことを示します。 値が **false** の場合、返信は提出できなかったことを示します。    |
| FailureReason | string | **Successful** が **false** の場合、この値には失敗の理由が含まれます。 **Successful** が **true** の場合、この値は空です。      |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Result": [
    {
      "ApplicationId": "9WZDNCRFJ3Q8",
      "ReviewId": "6be543ff-1c9c-4534-aced-af8b4fbe0316",
      "Successful": "true",
      "FailureReason": ""
    },
    {
      "ApplicationId": "9NBLGGH1RP08",
      "ReviewId": "80c9671a-96c2-4278-bcbc-be0ce5a32a7c",
      "Successful": "false",
      "FailureReason": "No Permission"
    }
  ]
}
```

## <a name="related-topics"></a>関連トピック

* [パートナーセンターを使用した顧客レビューへの対応](../publish/respond-to-customer-reviews.md)
* [Microsoft Store サービスを使ってレビューに返信する](respond-to-reviews-using-windows-store-services.md)
* [アプリのレビューへの返信情報の取得](get-response-info-for-app-reviews.md)
* [アプリのレビューの取得](get-app-reviews.md)
