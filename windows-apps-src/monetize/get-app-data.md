---
ms.assetid: 8D4AE532-22EF-4743-9555-A828B24B8F16
description: Microsoft Store 送信 API でこれらのメソッドを使用して、パートナーセンターアカウントに登録されているアプリのデータを取得します。
title: アプリ データの入手
ms.date: 02/28/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, アプリ データ
ms.localizationpriority: medium
ms.openlocfilehash: 120cb4d20299a8690f3d3814a8e937e763de1e7a
ms.sourcegitcommit: 80ea62d6c0ee25d73750437fe1e37df5224d5797
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2021
ms.locfileid: "105619608"
---
# <a name="get-app-data"></a>アプリ データの入手

Microsoft Store 送信 API で次のメソッドを使用して、パートナーセンターアカウントの既存のアプリのデータを取得します。 Microsoft Store 申請 API の概要については、「[Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)」をご覧ください。この API を使用するための前提条件などの情報があります。

これらの方法を使用する前に、アプリケーションがパートナーセンターアカウントに既に存在している必要があります。 アプリの提出を作成または管理する方法については、「[アプリ提出の管理](manage-app-submissions.md)」のメソッドを参照してください。

| 認証方法 | URI                                                                                             | 説明                                                 |
|------- |------------------------------------------------------------------------------------------------ |------------------------------------------------------------ |
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/applications`                                   | [全アプリのデータの取得](get-all-apps.md)               |
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}`                   | [特定アプリのデータの取得](get-an-app.md)                |
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/listinappproducts` | [アプリのアドオンの取得](get-add-ons-for-an-app.md)         |
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/listflights`       | [アプリのパッケージ フライトの取得](get-flights-for-an-app.md) |

## <a name="prerequisites"></a>前提条件

Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="data-resources"></a>データ リソース

アプリ データを取得するための Microsoft Store 申請 API のメソッドでは、次の JSON データ リソースが使われます。

<span id="application_object" />

### <a name="application-resource"></a>アプリケーション リソース

このリソースは、アカウントに登録されているアプリを表します。

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
  "hasAdvancedListingPermission": true
}
```

このリソースには、次の値があります。

| 値           | Type    | 説明       |
|-----------------|---------|---------------------|
| id            | string  | アプリケーションのストア ID です。 ストア ID について詳しくは、「[アプリ ID の詳細の表示](../publish/view-app-identity-details.md)」をご覧ください。   |
| primaryName   | string  | アプリのプライマリ名です。      |
| packageFamilyName | string  | アプリのパッケージ ファミリ名です。      |
| packageIdentityName          | string  | アプリのパッケージ ID 名です。                       |
| publisherName       | string  | アプリに関連付けられている Windows 発行元 ID です。 これは、パートナーセンターのアプリの [[アプリ id](../publish/view-app-identity-details.md) ] ページに表示される **パッケージ/Id/発行元** の値に対応しています。       |
| firstPublishedDate      | string  | アプリが最初に発行された日付 (ISO 8601 形式)。   |
| lastPublishedApplicationSubmission       | object | アプリの最後に公開された申請に関する情報を提供する[申請のリソース](#submission_object)。    |
| pendingApplicationSubmission        | object  |  アプリの現在保留中の申請に関する情報を提供する[申請のリソース](#submission_object)。   |   
| hasAdvancedListingPermission        | boolean  |  アプリの申請用に [gamingOptions](manage-app-submissions.md#gaming-options-object) または[トレーラー](manage-app-submissions.md#trailer-object)を構成できるかどうかを示します。 2017 年 5 月以降に作成された申請では、この値は true になります。 |

<span id="add-on-object" />

### <a name="add-on-resource"></a>アドオン リソース

このリソースは、アドオンに関する情報を提供します。

```json
{
    "inAppProductId": "9WZDNCRD7DLK"
}
```

このリソースには、次の値があります。

| 値           | Type    | 説明         |
|-----------------|---------|----------------------|
| inAppProductId            | string  | アドオンのストア ID です。 この値は、ストアによって提供されます。 ストア ID の例は 9NBLGGH4TNMP です。   |


<span id="flight-object" />

### <a name="flight-resource"></a>フライト リソース

このリソースは、アプリのパッケージ フライトに関する情報を提供します。

```json
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
```

このリソースには、次の値があります。

| 値           | Type    | 説明           |
|-----------------|---------|------------------------|
| flightId            | string  | パッケージ フライトの ID。 この値は、パートナーセンターによって指定されます。  |
| friendlyName           | string  | 開発者によって指定されているパッケージ フライトの名前。   |
| lastPublishedFlightSubmission       | object | パッケージ フライトの最後に公開された申請に関する情報を提供する[申請のリソース](#submission_object)。   |
| pendingFlightSubmission        | object  |  パッケージ フライトの現在保留中の申請に関する情報を提供する[申請のリソース](#submission_object)。  |    
| groupIds           | array  | パッケージ フライトに関連付けられているフライト グループの ID を含む文字列の配列。 フライト グループについて詳しくは、「[パッケージ フライト](../publish/package-flights.md)」をご覧ください。   |
| rankHigherThan           | string  | 現在のパッケージ フライトの次に低位のパッケージ フライトのフレンドリ名。 フライト グループのランク付けについて詳しくは、「[パッケージ フライト](../publish/package-flights.md)」をご覧ください。  |


<span id="submission_object" />

### <a name="submission-resource"></a>申請のリソース

このリソースは、申請に関する情報を提供します。 次の例は、このリソースの書式設定を示しています。

```json
{
  "pendingApplicationSubmission": {
    "id": "1152921504621243487",
    "resourceLocation": "applications/9WZDNCRD9MMD/submissions/1152921504621243487"
  }
}
```

このリソースには、次の値があります。

| 値              | Type   | 説明               |
|--------------------|--------|---------------------------|
| id                 | string | 申請 ID。 |
| resourceLocation   | string | 申請の完全なデータを取得するために基本 ```https://manage.devcenter.microsoft.com/v1.0/my/``` 要求 URI に付加できる相対パス。 |

 
## <a name="related-topics"></a>関連トピック

* [Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)
* [Microsoft Store 申請 API を使用したアプリの申請の管理](manage-app-submissions.md)
* [すべてのアプリの取得](get-all-apps.md)
* [アプリの入手](get-an-app.md)
* [アプリのアドオンの取得](get-add-ons-for-an-app.md)
* [アプリのパッケージ フライトの取得](get-flights-for-an-app.md)