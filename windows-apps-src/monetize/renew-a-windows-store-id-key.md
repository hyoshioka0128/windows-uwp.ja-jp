---
ms.assetid: 3569C505-8D8C-4D85-B383-4839F13B2466
description: Microsoft Store のキーを更新するには、以下のメソッドを使います。
title: Microsoft Store ID キーの更新
ms.date: 03/19/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store コレクション API, Microsoft Store 購入 API, Microsoft Store ID キー, 更新
ms.localizationpriority: medium
ms.openlocfilehash: fd4d7ce26e12f7ff939ced8d456390b97d0c8a0d
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57620487"
---
# <a name="renew-a-microsoft-store-id-key"></a>Microsoft Store ID キーの更新


Microsoft Store のキーを更新するには、以下のメソッドを使います。 [Microsoft Store ID キーを生成](view-and-grant-products-from-a-service.md#step-4)する場合、キーは 90 日間有効です。 キーの有効期限が切れた後で、有効期限が切れたキーとこのメソッドを使用して新しいキーを再ネゴシエートできます。

## <a name="prerequisites"></a>前提条件


このメソッドを使用するための要件:

* 対象ユーザー URI の値が `https://onestore.microsoft.com` の Azure AD アクセス トークン。
* [アプリのクライアント側コードから生成](view-and-grant-products-from-a-service.md#step-4)された有効期限切れの Microsoft Store ID キー。

詳しくは、「[サービスによる製品の権利の管理](view-and-grant-products-from-a-service.md)」をご覧ください。

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求の構文

| キーの種類    | メソッド | 要求 URI                                              |
|-------------|--------|----------------------------------------------------------|
| コレクション | POST   | ```https://collections.mp.microsoft.com/v6.0/b2b/keys/renew``` |
| 購入    | POST   | ```https://purchase.mp.microsoft.com/v6.0/b2b/keys/renew```    |


### <a name="request-header"></a>要求ヘッダー

| Header         | 種類   | 説明                                                                                           |
|----------------|--------|-------------------------------------------------------------------------------------------------------|
| Host           | string | **collections.mp.microsoft.com** または **purchase.mp.microsoft.com** の値に設定する必要があります。           |
| Content-Length | number | 要求の本文の長さ。                                                                       |
| Content-Type   | string | 要求と応答の種類を指定します。 現時点では、サポートされている唯一の値は **application/json** です。 |


### <a name="request-body"></a>要求本文

| パラメーター     | 種類   | 説明                       | 必須 |
|---------------|--------|-----------------------------------|----------|
| serviceTicket | string | Azure AD アクセス トークン。        | 〇      |
| key           | string | 有効期限が切れた Microsoft Store ID キー。 | 〇       |


### <a name="request-example"></a>要求の例

```syntax
POST https://collections.mp.microsoft.com/v6.0/b2b/keys/renew HTTP/1.1
Content-Length: 2774
Content-Type: application/json
Host: collections.mp.microsoft.com

{
    "serviceTicket": "eyJ0eXAiOiJKV1QiLCJhb….",
    "Key": "eyJ0eXAiOiJKV1QiLCJhbG…."
}
```

## <a name="response"></a>応答


### <a name="response-body"></a>応答本文

| パラメーター | 種類   | 説明                                                                                                            |
|-----------|--------|------------------------------------------------------------------------------------------------------------------------|
| key       | string | 以降の Microsoft Store コレクション API または Microsoft Store 購入 API の呼び出しで使用できる、更新された Microsoft Store のキー。 |


### <a name="response-example"></a>応答の例

```syntax
HTTP/1.1 200 OK
Content-Length: 1646
Content-Type: application/json
MS-CorrelationId: bfebe80c-ff89-4c4b-8897-67b45b916e47
MS-RequestId: 1b5fa630-d672-4971-b2c0-3713f4ea6c85
MS-CV: xu2HW6SrSkyfHyFh.0.0
MS-ServerId: 030011428
Date: Tue, 13 Sep 2015 07:31:12 GMT

{
    "key":"eyJ0eXAi….."
}
```

## <a name="error-codes"></a>エラー コード


| コード | エラー        | 内部エラー コード           | 説明   |
|------|--------------|----------------------------|---------------|
| 401  | 権限がありません | AuthenticationTokenInvalid | Azure AD アクセス トークンが無効です。 場合によっては、ServiceError の詳細に追加情報が含まれていることがあります (トークンの有効期限切れや *appid* 要求の欠落など)。 |
| 401  | 権限がありません | InconsistentClientId       | Microsoft Store ID キーの *clientId* 要求と Azure AD アクセス トークンの *appid* 要求が一致しません。                                                                     |


## <a name="related-topics"></a>関連トピック


* [サービスからの製品の利用資格を管理します。](view-and-grant-products-from-a-service.md)
* [製品のクエリ](query-for-products.md)
* [Fulfilled コンシューマブル製品をレポートします。](report-consumable-products-as-fulfilled.md)
* [無料の製品を付与します。](grant-free-products.md)
