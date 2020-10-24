---
description: この REST URI を使用して、特定の日付範囲とその他のオプションのフィルターを使用して、デスクトップアプリケーションの集計インストールデータを取得します。
title: デスクトップ アプリケーションのインストール数の取得
ms.date: 03/01/2018
ms.topic: article
keywords: windows 10、デスクトップアプリのインストール、Windows デスクトップアプリケーションプログラム
localizationpriority: medium
ms.openlocfilehash: 1c4f7aaffc9e623d4863bee4de44daa75ae05852
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89175026"
---
# <a name="get-desktop-application-installs"></a>デスクトップ アプリケーションのインストール数の取得


この REST URI を使用して、 [Windows デスクトップアプリケーションプログラム](/windows/desktop/appxpkg/windows-desktop-application-program)に追加したデスクトップアプリケーションの JSON 形式で集計インストールデータを取得します。 この URI を使用すると、指定された日付範囲とその他のオプションのフィルターの間にデータをインストールできます。 この情報は、パートナーセンターのデスクトップアプリケーションの [インストールレポート](/windows/desktop/appxpkg/windows-desktop-application-program) でも確認できます。

## <a name="prerequisites"></a>前提条件


このメソッドを使うには、最初に次の作業を行う必要があります。

* Microsoft Store 分析 API に関するすべての[前提条件](access-analytics-data-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

## <a name="request"></a>Request


### <a name="request-syntax"></a>要求の構文

| 認証方法 | 要求 URI       |
|--------|----------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/installbasedaily```|


### <a name="request-header"></a>要求ヘッダー

| Header        | Type   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| 承認 | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |


### <a name="request-parameters"></a>要求パラメーター

| パラメーター        | Type   |  説明      |  必須  
|---------------|--------|---------------|------|
| applicationId | string | インストールデータを取得するデスクトップアプリケーションの製品 ID。 デスクトップアプリケーションの製品 ID を取得するには、パートナーセンター (**インストールレポート**など)[でデスクトップアプリケーションの分析レポート](/windows/desktop/appxpkg/windows-desktop-application-program)を開き、URL から製品 id を取得します。 |  はい  |
| startDate | 日付 | 取得するインストール データの日付範囲の開始日です。 既定値は、現在の日付の90日前です。 |  いいえ  |
| endDate | 日付 | 取得するインストール データの日付範囲の終了日です。 既定値は現在の日付です。 |  いいえ  |
| top | int | 要求で返すデータの行数です。 最大値および指定しない場合の既定値は 10000 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。 |  いいえ  |
| skip | int | クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=10000 と skip=0 を指定すると、データの最初の 10,000 行が取得され、top=10000 と skip=10000 を指定すると、データの次の 10,000 行が取得されます。 |  いいえ  |
| filter | string  | 応答内の行をフィルター処理する 1 つまたは複数のステートメントです。 各ステートメントには、応答本文からのフィールド名、および **eq** 演算子または **ne** 演算子と関連付けられる値が含まれており、**and** や **or** を使用してステートメントを組み合わせることができます。 *filter* パラメーターでは、文字列値を単一引用符で囲む必要があります。 応答本文から次のフィールドを指定することができます。<p/><ul><li><strong>applicationVersion</strong></li><li><strong>deviceType</strong></li><li><strong>マーケティング</strong></li><li><strong>osVersion</strong></li><li><strong>osRelease</strong></li></ul> | いいえ   |
| orderby | string | 各インストールの結果データ値の順序を指定するステートメントです。 構文は <em>orderby=field [order],field [order],...</em> です。<em>field</em> パラメーターには、応答本文から次のフィールドのいずれかを指定できます。<p/><ul><li><strong>同様</strong></li><li><strong>date</strong><li><strong>applicationVersion</strong></li><li><strong>deviceType</strong></li><li><strong>マーケティング</strong></li><li><strong>osVersion</strong></li><li><strong>osRelease</strong></li><li><strong>installBase</strong></li></ul><p><em>order</em> パラメーターは省略可能であり、<strong>asc</strong> または <strong>desc</strong> を指定して、各フィールドを昇順または降順にすることができます。 既定値は <strong>asc</strong>です。</p><p><em>orderby</em> 文字列の例: <em>orderby=date,market</em></p> |  いいえ  |
| groupby | string | 指定したフィールドのみにデータ集計を適用するステートメントです。 応答本文から次のフィールドを指定することができます。<p/><ul><li><strong>applicationVersion</strong></li><li><strong>deviceType</strong></li><li><strong>マーケティング</strong></li><li><strong>osVersion</strong></li><li><strong>osRelease</strong></li></ul><p>返されるデータ行には、<em>groupby</em> パラメーターに指定したフィールドと次の値が含まれます。</p><ul><li><strong>applicationId</strong></li><li><strong>date</strong></li><li><strong>同様</strong></li><li><strong>installBase</strong></li></ul></p> |  いいえ  |


### <a name="request-example"></a>要求の例

次の例は、デスクトップアプリケーションのインストールデータを取得するためのいくつかの要求を示しています。 *ApplicationId*の値を、デスクトップアプリケーションの製品 ID に置き換えます。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/installbasedaily?applicationId=1234567890&startDate=2018-01-01&endDate=2018-02-01&top=10&skip=0 HTTP/1.1
Authorization: Bearer <your access token>

GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/desktop/installbasedaily?applicationId=1234567890&startDate=2018-01-01&endDate=2018-02-01&filter=market eq 'US' and deviceType eq 'PC' HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]


### <a name="response-body"></a>応答本文

| 値      | Type   | 説明                  |
|------------|--------|-------------------------------------------------------|
| 値      | array  | 集計インストール データが含まれるオブジェクトの配列です。 各オブジェクトのデータの詳細については、以下の表を参照してください。 |
| @nextLink  | string | データの追加ページがある場合、この文字列には、データの次のページを要求するために使用できる URI が含まれます。 たとえば、要求の **top** パラメーターを 10000 に設定した場合、クエリに適合するインストール データが 10,000 行を超えると、この値が返されます。 |
| TotalCount | INT    | クエリの結果データ内の行の総数です。 |


*Value* 配列の要素には、次の値が含まれます。

| 値               | Type   | 説明                           |
|---------------------|--------|-------------------------------------------|
| date                | string | インストールのベース値に関連付けられた日付。 |
| applicationId       | string | インストールデータを取得したデスクトップアプリケーションの製品 ID。 |
| productName         | string | デスクトップ アプリケーションの表示名です。アプリケーションに関連付けられている実行可能ファイルのメタデータから取得されます。 |
| applicationVersion  | string | インストールされたアプリケーション実行可能ファイルのバージョン。 |
| deviceType          | string | デスクトップアプリケーションがインストールされているデバイスの種類を指定する次のいずれかの文字列。<p/><ul><li><strong>PC</strong></li><li><strong>サーバー</strong></li><li><strong>タブレット</strong></li><li><strong>Unknown</strong></li></ul> |
| market              | string | デスクトップアプリケーションがインストールされている市場の ISO 3166 国コード。 |
| osVersion           | string | デスクトップ アプリケーションがインストールされている OS のバージョンを示す、以下のいずれかの文字列です。<p/><ul><li><strong>Windows 7</strong></li><li><strong>Windows 8.1</strong></li><li><strong>Windows 10</strong></li><li><strong>Windows Server 2016</strong></li><li><strong>Windows Server 1709</strong></li><li><strong>Unknown</strong></li></ul>   |
| osRelease           | string | デスクトップ アプリケーションがインストールされている OS リリースまたはフライティング リングを (OS バージョン内のサブグループとして) 指定する、以下のいずれかの文字列です。<p/><p>Windows 10 の場合:</p><ul><li><strong>バージョン1507</strong></li><li><strong>バージョン1511</strong></li><li><strong>バージョン1607</strong></li><li><strong>バージョン1703</strong></li><li><strong>バージョン1709</strong></li><li><strong>リリース プレビュー</strong></li><li><strong>Insider Fast</strong></li><li><strong>Insider Slow</strong></li></ul><p/><p>Windows Server 1709 の場合:</p><ul><li><strong>リリース</strong></li></ul><p>Windows Server 2016 の場合:</p><ul><li><strong>バージョン1607</strong></li></ul><p>Windows 8.1 の場合:</p><ul><li><strong>Update 1</strong></li></ul><p>Windows 7 の場合:</p><ul><li><strong>Service Pack 1</strong></li></ul><p>OS リリースまたはフライティング リングが不明な場合、このフィールドは値 <strong>Unknown</strong> になります。</p> |
| installBase         | number | 指定した集計レベルで製品がインストールされていた個別のデバイスの数。 |


### <a name="response-example"></a>応答の例

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
    {
      "date": "2018-01-24",
      "applicationId": "123456789",
      "productName": "Contoso Demo",
      "applicationVersion": "1.0.0.0",
      "deviceType": "PC",
      "market": "All",
      "osVersion": "Windows 10",
      "osRelease": "Version 1709",
      "installBase": 348218.0
    }
  ],
  "@nextLink": "desktop/installbasedaily?applicationId=123456789&startDate=2018-01-01&endDate=2018-02-01&top=10000&skip=10000&groupby=applicationVersion,deviceType,osVersion,osRelease",
  "TotalCount": 23012
}
```

## <a name="related-topics"></a>関連トピック

* [Windows デスクトップアプリケーションプログラム](/windows/desktop/appxpkg/windows-desktop-application-program)