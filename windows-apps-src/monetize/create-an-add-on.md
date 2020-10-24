---
ms.assetid: 5BD650D2-AA26-4DE9-8243-374FDB7D932B
description: Microsoft Store 送信 API でこのメソッドを使用して、PartnerCenter アカウントに登録されているアプリのアドオンを作成します。
title: アドオンの作成
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, アドオンの作成, アプリ内製品, IAP
ms.localizationpriority: medium
ms.openlocfilehash: a54ad4bcdb0c6fd652d56c767aa8362073b07875
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89167726"
---
# <a name="create-an-add-on"></a>アドオンの作成

Microsoft Store 送信 API でこのメソッドを使用して、パートナーセンターアカウントに登録されているアプリのアドオン (アプリ内製品または IAP とも呼ばれます) を作成します。

> [!NOTE]
> このメソッドは、申請なしでアドオンを作成します。 アドオンの申請を作成する方法については、「[アドオンの申請の管理](manage-add-on-submissions.md)」のメソッドをご覧ください。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| 認証方法 | 要求 URI                                                      |
|--------|------------------------------------------------------------------|
| POST    | `https://manage.devcenter.microsoft.com/v1.0/my/inappproducts` |


### <a name="request-header"></a>要求ヘッダー

| Header        | Type   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 承認 | string | 必須。 ベアラートークン形式の Azure AD アクセストークン**Bearer** &lt; *token* &gt; 。 |


### <a name="request-body"></a>要求本文

要求本文には次のパラメーターがあります。

|  パラメーター  |  Type  |  説明  |  必須  |
|------|------|------|------|
|  applicationIds  |  array  |  このアドオンが関連付けられるアプリのストア ID を含む配列です。 この配列でサポートされる項目は 1 つのみです。   |  はい  |
|  productId  |  string  |  アドオンの製品 ID です。 これは、アドオンを参照する、コード内で使用できる識別子です。 詳しくは、「[IAP の製品の種類と製品 ID を設定する](../publish/set-your-add-on-product-id.md)」をご覧ください。  |  はい  |
|  productType  |  string  |  アドオンの製品の種類です。 値 **Durable** と **Consumable** がサポートされています。  |  はい  |


### <a name="request-example"></a>要求の例

次の例は、アプリの新しいコンシューマブルなアドオンを作成する方法を示しています。

```json
POST https://manage.devcenter.microsoft.com/v1.0/my/inappproducts HTTP/1.1
Authorization: Bearer eyJ0eXAiOiJKV1Q...
Content-Type: application/json
{
    "applicationIds": [  "9NBLGGH4R315"  ],
    "productId": "my-new-add-on",
    "productType": "Consumable",
}
```

## <a name="response"></a>応答

次の例は、このメソッドが正常に呼び出された場合の JSON 応答本文を示しています。 応答の本文内の値について詳しくは、[アドオンのリソース](manage-add-ons.md#add-on-object)をご覧ください。

```json
{
  "applications": {
    "value": [
      {
        "id": "9NBLGGH4R315",
        "resourceLocation": "applications/9NBLGGH4R315"
      }
    ],
    "totalCount": 1
  },
  "id": "9NBLGGH4TNMP",
  "productId": "my-new-add-on",
  "productType": "Consumable",
}
```

## <a name="error-codes"></a>エラー コード

要求を正常に完了できない場合、次の HTTP エラー コードのいずれかが応答に含まれます。

| エラー コード |  説明                                                                                                                                                                           |
|--------|------------------|
| 400  | 要求が無効です。 |
| 409  | 現在の状態によりアドオンを作成できませんでした。またはアドオンが、 [現在 Microsoft Store 送信 API でサポート](create-and-manage-submissions-using-windows-store-services.md#not_supported)されていないパートナーセンターの機能を使用しています。 |   


## <a name="related-topics"></a>関連トピック

* [Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)
* [アドオンの申請の管理](manage-add-on-submissions.md)
* [すべてのアドオンの入手](get-all-add-ons.md)
* [アドオンの入手](get-an-add-on.md)
* [アドオンの削除](delete-an-add-on.md)