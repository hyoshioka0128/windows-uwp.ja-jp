---
ms.assetid: DAF92881-6AF6-44C7-B466-215F5226AE04
description: Microsoft Store 送信 API でこのメソッドを使用して、パートナーセンターアカウントに登録されている特定のアプリに関する情報を取得します。
title: アプリの入手
ms.date: 02/28/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, アプリ
ms.localizationpriority: medium
ms.openlocfilehash: 29f4b7fdb196e1463f4e738618694363094933f0
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89171476"
---
# <a name="get-an-app"></a>アプリの入手

Microsoft Store 送信 API でこのメソッドを使用して、パートナーセンターアカウントに登録されている特定のアプリに関する情報を取得します。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| 認証方法 | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}` |


### <a name="request-header"></a>要求ヘッダー

| Header        | Type   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 承認 | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

| 名前        | Type   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| applicationId | string | 必須。 取得するアプリのストア ID。 ストア ID について詳しくは、「[アプリ ID の詳細の表示](../publish/view-app-identity-details.md)」をご覧ください。  |


### <a name="request-body"></a>[要求本文]

このメソッドでは要求本文を指定しないでください。

### <a name="request-example"></a>要求の例

次の例は、Store ID 値が 9NBLGGH4R315 であるアプリに関する情報を取得する方法を示しています。

```json
GET https://manage.devcenter.microsoft.com/v1.0/my/applications/9NBLGGH4R315 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

次の例は、このメソッドが正常に呼び出された場合の JSON 応答本文を示しています。 応答の本文内の値について詳しくは、[アプリケーションのリソース](get-app-data.md#application_object)をご覧ください。

```json
{
  "id": "9NBLGGH4R315",
  "primaryName": "ApiTestApp",
  "packageFamilyName": "30481DevCenterAPITester.ApiTestAppForDevbox_ng6try80pwt52",
  "packageIdentityName": "30481DevCenterAPITester.ApiTestAppForDevbox",
  "publisherName": "CN=…",
  "firstPublishedDate": "1601-01-01T00:00:00Z",
  "lastPublishedApplicationSubmission": {
    "id": "1152921504621086517",
    "resourceLocation": "applications/9NBLGGH4R315/submissions/1152921504621086517"
  },
  "pendingApplicationSubmission": {
    "id": "1152921504621243487",
    "resourceLocation": "applications/9NBLGGH4R315/submissions/1152921504621243487"
  },
  "hasAdvancedListingPermission": false
}
```

## <a name="error-codes"></a>エラー コード

要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。

| エラー コード |  説明   |
|--------|------------------|
| 404  | 指定したアプリは見つかりませんでした。 |
| 409  | このアプリでは、 [Microsoft Store 送信 API で現在サポート](create-and-manage-submissions-using-windows-store-services.md#not_supported)されていないパートナーセンター機能を使用しています。  |


## <a name="related-topics"></a>関連トピック

* [Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)
* [すべてのアプリの取得](get-all-apps.md)
* [アプリのパッケージ フライトの取得](get-flights-for-an-app.md)
* [アプリのアドオンの取得](get-add-ons-for-an-app.md)