---
ms.assetid: C7428551-4B31-4259-93CD-EE229007C4B8
description: Microsoft Store 送信 API でこれらのメソッドを使用して、パートナーセンターアカウントに登録されているアプリの送信を管理します。
title: アプリの申請の管理
ms.date: 04/30/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, アプリの申請
ms.localizationpriority: medium
ms.openlocfilehash: 00820f00360575f0a335d37aa0859b94648709e3
ms.sourcegitcommit: 7e8dfd83b181fe720b4074cb42adc908e1ba5e44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98811279"
---
# <a name="manage-app-submissions"></a>アプリの申請の管理

Microsoft Store 申請 API には、段階的なパッケージのロールアウトなど、アプリの申請を管理するために使用できるメソッドが用意されています。 Microsoft Store 申請 API の概要については、「[Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)」をご覧ください。この API を使用するための前提条件などの情報があります。

> [!IMPORTANT]
> Microsoft Store 送信 API を使用してアプリの送信を作成する場合は、パートナーセンターではなく、API のみを使用して、送信に対してさらに変更を加えるようにしてください。 API を使用して最初に作成した送信をパートナーセンターを使用して変更した場合、API を使用してその送信を変更またはコミットすることはできなくなります。 場合によっては、申請がエラー状態のままになり、申請プロセスを進めることができなくなります。 この場合、申請を削除して新しい申請を作成する必要があります。

> [!IMPORTANT]
> この API を使って、[ビジネス向け Microsoft Store や教育機関向け Microsoft Store でのボリューム購入](../publish/organizational-licensing.md)の申請を公開したり、[LOB アプリ](../publish/distribute-lob-apps-to-enterprises.md)の申請を直接企業に発行したりすることはできません。 どちらのシナリオでも、パートナーセンターを使用して送信を発行する必要があります。


<span id="methods-for-app-submissions" />

## <a name="methods-for-managing-app-submissions"></a>アプリの申請を管理するためのメソッド

アプリの申請を取得、作成、更新、コミット、または削除するには、次のメソッドを使用します。 これらの方法を使用する前に、アプリケーションがパートナーセンターアカウントに既に存在している必要があります。最初に、パートナーセンターでアプリの送信を1つ作成する必要があります。 詳細については、[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を参照してください。

<table>
<colgroup>
<col width="10%" />
<col width="30%" />
<col width="60%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">認証方法</th>
<th align="left">URI</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}</td>
<td align="left"><a href="get-an-app-submission.md">既存のアプリの申請を取得します</a></td>
</tr>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/status</td>
<td align="left"><a href="get-status-for-an-app-submission.md">既存のアプリの申請の状態を取得します</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions</td>
<td align="left"><a href="create-an-app-submission.md">新しいアプリの申請を作成します</a></td>
</tr>
<tr>
<td align="left">PUT</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}</td>
<td align="left"><a href="update-an-app-submission.md">既存のアプリの申請を更新します</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/commit</td>
<td align="left"><a href="commit-an-app-submission.md">新しいアプリの申請または更新されたアプリの申請をコミットします</a></td>
</tr>
<tr>
<td align="left">DELETE</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}</td>
<td align="left"><a href="delete-an-app-submission.md">アプリの申請の削除</a></td>
</tr>
</tbody>
</table>

<span id="create-an-app-submission">

### <a name="create-an-app-submission"></a>アプリの申請の作成

アプリの申請を作成するには、次のプロセスに従います。

1. Microsoft Store 申請 API に関するすべての[前提条件](create-and-manage-submissions-using-windows-store-services.md#prerequisites)を満たします (前提条件がまだ満たされていない場合)。
    > [!NOTE]
    > [年齢区分](../publish/age-ratings.md)の情報を含む 1 つ以上の申請がアプリで既に完了していることを確認します。

2. [Azure AD のアクセス トークンを取得します](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token)。 このアクセス トークンを Microsoft Store 申請 API のメソッドに渡す必要があります。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

3. Microsoft Store 申請 API の次のメソッドを実行して、[アプリの申請を作成](create-an-app-submission.md)します。 このメソッドによって、新しい申請が作成され、審査中になります。これは、前回発行した申請のコピーです。

    ```json
    POST https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions
    ```

    応答本文 [には、](#app-submission-object) 新しい送信の ID、送信用の関連ファイルを Azure Blob Storage にアップロードするための shared access SIGNATURE (SAS) URI (アプリパッケージ、一覧画像、トレーラーファイルなど)、および新しい送信用のすべてのデータ (一覧や価格情報など) が含まれています。

    > [!NOTE]
    > SAS URI では、アカウント キーを必要とせずに、Azure Storage 内のセキュリティで保護されたリソースにアクセスできます。 SAS Uri と Azure Blob Storage の使用に関する背景情報については、「 [Shared Access signature、第1部: sas モデル](/azure/storage/common/storage-sas-overview) と Shared access signature について」 [、「パート 2: Blob ストレージでの sas の作成と使用](/azure/storage/common/storage-sas-overview)」を参照してください。

4. 申請用に新しいパッケージ、登録情報の画像、またはトレーラー ファイルを追加する場合は、[アプリのパッケージを準備](../publish/app-package-requirements.md)し、[アプリのスクリーンショット、画像、およびトレーラーを準備](../publish/app-screenshots-and-images.md)します。 これらのファイルをすべてまとめて ZIP アーカイブに追加します。

5. 新しい申請用に必要な変更を行って[アプリの申請](#app-submission-object)データを修正し、次のメソッドを実行して[アプリの申請を更新](update-an-app-submission.md)します。

    ```json
    PUT https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}
    ```
      > [!NOTE]
      > 申請用に新しいファイルを追加する場合、ZIP アーカイブ内の新しいファイルの名前と相対パスを参照するように、申請データを更新してください。

4. 新しいパッケージを追加する場合、イメージを一覧表示している場合、または送信用にトレーラーファイルを追加する場合は、前に呼び出した POST メソッドの応答本文に指定された SAS URI を使用して、 [Azure Blob Storage](/azure/storage/storage-introduction#blob-storage) に ZIP アーカイブをアップロードします。 さまざまなプラットフォームでこれを行うために使用できる、次のようなさまざまな Azure ライブラリがあります。

    * [.NET 用 Azure Storage クライアントライブラリ](/azure/storage/storage-dotnet-how-to-use-blobs)
    * [Azure Storage SDK for Java](/azure/storage/storage-java-how-to-use-blob-storage)
    * [Azure Storage SDK for Python](/azure/storage/storage-python-how-to-use-blob-storage)

    次の C# コード例は、.NET 用 Azure Storage クライアントライブラリの [Cloudblockblob](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob) クラスを使用して AZURE BLOB STORAGE に ZIP アーカイブをアップロードする方法を示しています。 この例では、ZIP アーカイブが既にストリーム オブジェクトに書き込まれていることを前提としています。

    ```csharp
    string sasUrl = "https://productingestionbin1.blob.core.windows.net/ingestion/26920f66-b592-4439-9a9d-fb0f014902ec?sv=2014-02-14&sr=b&sig=usAN0kNFNnYE2tGQBI%2BARQWejX1Guiz7hdFtRhyK%2Bog%3D&se=2016-06-17T20:45:51Z&sp=rwl";
    Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob blockBob =
        new Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob(new System.Uri(sasUrl));
    await blockBob.UploadFromStreamAsync(stream);
    ```

5. 次のメソッドを実行して、[アプリの申請をコミット](commit-an-app-submission.md)します。 これにより、送信が完了したことがパートナーセンターに通知され、更新プログラムがアカウントに適用されるようになります。

    ```json
    POST https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/commit
    ```

6. 次のメソッドを実行して[アプリの申請の状態を取得](get-status-for-an-app-submission.md)して、コミット状態を確認します。

    ```json
    GET https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/status
    ```

    申請の状態を確認するには、応答本文の *status* の値を確認します。 この値が **CommitStarted** から **PreProcessing** (要求が成功した場合) または **CommitFailed** (要求でエラーが発生した場合) に変わっています。 エラーがある場合は、*statusDetails* フィールドにエラーについての詳細情報が含まれています。

7. コミットが正常に処理されると、インジェストのために申請がストアに送信されます。 前の方法を使用するか、パートナーセンターにアクセスして、送信の進行状況を引き続き監視することができます。

<span id="manage-gradual-package-rollout">

## <a name="methods-for-managing-a-gradual-package-rollout"></a>段階的なパッケージのロールアウトを管理するためのメソッド

アプリの申請で更新されたパッケージを、アプリの Windows 10 のユーザーの一部に、段階的にロールアウトできます。 これにより、更新に確信が持てるよう、特定のパッケージのフィードバックと分析データを監視してから、より広くロールアウトできます。 新しい申請を作成することなく、公開された申請のロールアウトの割合を変更する (または更新を停止する) ことができます。 パートナーセンターで段階的なパッケージのロールアウトを有効化および管理する手順など、詳細については、こちらの [記事](../publish/gradual-package-rollout.md)を参照してください。

アプリの申請の段階的なパッケージのロールアウトをプログラムによって有効化するには、Microsoft Store 申請 API のメソッドを使用して、次の手順に従います。

  1. [アプリの申請を作成する](create-an-app-submission.md)か、[既存のアプリの申請を取得](get-an-app-submission.md)します。
  2. 応答データで、[packageRollout](#package-rollout-object) リソースを探し、*[isPackageRollout]* フィールドを **[true]** に設定し、*[packageRolloutPercentage]* フィールドに、アプリのユーザーが更新されたパッケージを取得する割合を設定します。
  3. [アプリの申請の更新](update-an-app-submission.md)のメソッドに、更新されたアプリの申請データを渡します。

アプリの申請の段階的なパッケージのロールアウトが有効化された後、段階的なロールアウトをプログラムで取得、更新、停止、または完了するには、次のメソッドを使用できます。

<table>
<colgroup>
<col width="10%" />
<col width="30%" />
<col width="60%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">認証方法</th>
<th align="left">URI</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/packagerollout</td>
<td align="left"><a href="get-package-rollout-info-for-an-app-submission.md">アプリの申請の段階的なロールアウトの情報を取得します</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/updatepackagerolloutpercentage</td>
<td align="left"><a href="update-the-package-rollout-percentage-for-an-app-submission.md">アプリの申請の段階的なロールアウトの割合を更新します</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/haltpackagerollout</td>
<td align="left"><a href="halt-the-package-rollout-for-an-app-submission.md">アプリの申請の段階的なロールアウトを停止します</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/finalizepackagerollout</td>
<td align="left"><a href="finalize-the-package-rollout-for-an-app-submission.md">アプリの申請の段階的なロールアウトを完了します</a></td>
</tr>
</tbody>
</table>


## <a name="code-examples-for-managing-app-submissions"></a>アプリの申請を管理するためのコード例

次の記事では、さまざまなプログラミング言語でアプリの申請を作成する方法を説明する詳しいコード例を紹介します。

* [C# のコード例: アプリ、アドオン、およびフライトの申請](csharp-code-examples-for-the-windows-store-submission-api.md)
* [C# のコード例: ゲーム オプションおよびトレーラーを含むアプリの申請](csharp-code-examples-for-submissions-game-options-and-trailers.md)
* [Java のコード例: アプリ、アドオン、およびフライトの申請](java-code-examples-for-the-windows-store-submission-api.md)
* [Java のコード例: ゲーム オプションおよびトレーラーを含むアプリの申請](java-code-examples-for-submissions-game-options-and-trailers.md)
* [Python のコード例: アプリ、アドオン、およびフライトの申請](python-code-examples-for-the-windows-store-submission-api.md)
* [Python のコード例: ゲーム オプションおよびトレーラーを含むアプリの申請](python-code-examples-for-submissions-game-options-and-trailers.md)

## <a name="storebroker-powershell-module"></a>StoreBroker PowerShell モジュール

Microsoft Store 申請 API を直接呼び出す代わりに、API の上にコマンド ライン インターフェイスを実装するオープンソースの PowerShell モジュールも用意されています。 このモジュールは、[StoreBroker](https://github.com/Microsoft/StoreBroker) と呼ばれています。 このモジュールを使うと、Microsoft Store 申請 API を直接呼び出さずに、コマンド ラインからアプリ、フライト、アドオンの申請を管理できます。また、ソースを参照して、この API を呼び出す方法の例を確認することもできます。 StoreBroker モジュールは、多くのファースト パーティ アプリケーションをストアに申請する主要な方法として Microsoft 内で積極的に使っています。

詳しくは、[GitHub の StoreBroker に関するページ](https://github.com/Microsoft/StoreBroker)をご覧ください。

<span/>

## <a name="data-resources"></a>データ リソース
アプリの申請を管理するための Microsoft Store 申請 API のメソッドでは、次の JSON データ リソースが使われます。

<span id="app-submission-object" />

### <a name="app-submission-resource"></a>アプリの申請のリソース

このリソースは、アプリの申請を記述しています。

```json
{
  "id": "1152921504621243540",
  "applicationCategory": "BooksAndReference_EReader",
  "pricing": {
    "trialPeriod": "FifteenDays",
    "marketSpecificPricings": {},
    "sales": [],
    "priceId": "Tier2",
    "isAdvancedPricingModel": true
  },
  "visibility": "Public",
  "targetPublishMode": "Manual",
  "targetPublishDate": "1601-01-01T00:00:00Z",
  "listings": {
    "en-us": {
      "baseListing": {
        "copyrightAndTrademarkInfo": "",
        "keywords": [
          "epub"
        ],
        "licenseTerms": "",
        "privacyPolicy": "",
        "supportContact": "",
        "websiteUrl": "",
        "description": "Description",
        "features": [
          "Free ebook reader"
        ],
        "releaseNotes": "",
        "images": [
          {
            "fileName": "contoso.png",
            "fileStatus": "Uploaded",
            "id": "1152921504672272757",
            "description": "Main page",
            "imageType": "Screenshot"
          }
        ],
        "recommendedHardware": [],
        "title": "Contoso ebook reader"
      },
      "platformOverrides": {
        "Windows81": {
          "description": "Ebook reader for Windows 8.1"
        }
      }
    }
  },
  "hardwarePreferences": [
    "Touch"
  ],
  "automaticBackupEnabled": false,
  "canInstallOnRemovableMedia": true,
  "isGameDvrEnabled": false,
  "gamingOptions": [],
  "hasExternalInAppProducts": false,
  "meetAccessibilityGuidelines": true,
  "notesForCertification": "",
  "status": "PendingCommit",
  "statusDetails": {
    "errors": [],
    "warnings": [],
    "certificationReports": []
  },
  "fileUploadUrl": "https://productingestionbin1.blob.core.windows.net/ingestion/387a9ea8-a412-43a9-8fb3-a38d03eb483d?sv=2014-02-14&sr=b&sig=sdd12JmoaT6BhvC%2BZUrwRweA%2Fkvj%2BEBCY09C2SZZowg%3D&se=2016-06-17T18:32:26Z&sp=rwl",
  "applicationPackages": [
    {
      "fileName": "contoso_app.appx",
      "fileStatus": "Uploaded",
      "id": "1152921504620138797",
      "version": "1.0.0.0",
      "architecture": "ARM",
      "languages": [
        "en-US"
      ],
      "capabilities": [
        "ID_RESOLUTION_HD720P",
        "ID_RESOLUTION_WVGA",
        "ID_RESOLUTION_WXGA"
      ],
      "minimumDirectXVersion": "None",
      "minimumSystemRam": "None",
      "targetDeviceFamilies": [
        "Windows.Mobile min version 10.0.10240.0"
      ]
    }
  ],
  "packageDeliveryOptions": {
    "packageRollout": {
        "isPackageRollout": false,
        "packageRolloutPercentage": 0.0,
        "packageRolloutStatus": "PackageRolloutNotStarted",
        "fallbackSubmissionId": "0"
    },
    "isMandatoryUpdate": false,
    "mandatoryUpdateEffectiveDate": "1601-01-01T00:00:00.0000000Z"
  },
  "enterpriseLicensing": "Online",
  "allowMicrosoftDecideAppAvailabilityToFutureDeviceFamilies": true,
  "allowTargetFutureDeviceFamilies": {
    "Desktop": false,
    "Mobile": true,
    "Holographic": true,
    "Xbox": false,
    "Team": true
  },
  "friendlyName": "Submission 2",
  "trailers": []
}
```

このリソースには、次の値があります。

| 値      | Type   | 説明      |
|------------|--------|-------------------|
| id            | string  | 申請 ID。 この ID は、[アプリの申請の作成](create-an-app-submission.md)要求、[すべてのアプリの取得](get-all-apps.md)要求、[アプリの取得](get-an-app.md)要求に対する応答データで確認できます。 パートナーセンターで作成された送信の場合、この ID はパートナーセンターの [送信] ページの URL でも利用できます。  |
| applicationCategory           | string  |   アプリの[カテゴリとサブカテゴリ](../publish/category-and-subcategory-table.md)を指定する文字列です。 カテゴリとサブカテゴリは、アンダースコア "_" で 1 つの文字列に連結します (例: **BooksAndReference_EReader**)。      |  
| 価格           |  object  | アプリの価格設定情報が保持される[価格リソース](#pricing-object)です。        |   
| 参照可能範囲           |  string  |  アプリの可視性です。 次のいずれかの値を指定できます。 <ul><li>[非表示]</li><li>パブリック</li><li>プライベート</li><li>NotSet</li></ul>       |   
| targetPublishMode           | string  | 申請の公開モードです。 次のいずれかの値を指定できます。 <ul><li>即時</li><li>マニュアル</li><li>SpecificDate</li></ul> |
| targetPublishDate           | string  | *targetPublishMode* が SpecificDate に設定されている場合、ISO 8601 形式での申請の公開日です。  |  
| listings           |   object  |  キーと値のペアのディクショナリです。各キーは国コード、各値はアプリの登録情報を含む[登録情報リソース](#listing-object) オブジェクトです。       |   
| hardwarePreferences           |  array  |   アプリの[ハードウェアの基本設定](../publish/enter-app-properties.md)を定義する文字列の配列です。 次のいずれかの値を指定できます。 <ul><li>Touch</li><li>キーボード</li><li>マウス</li><li>カメラ</li><li>NfcHce</li><li>Nfc</li><li>BluetoothLE</li><li>テレフォニー</li></ul>     |   
| automaticBackupEnabled           |  boolean  |   OneDrive への自動バックアップにアプリのデータを含めることができるかどうかを示します。 詳しくは、「[アプリの宣言](../publish/product-declarations.md)」をご覧ください。   |   
| canInstallOnRemovableMedia           |  boolean  |   ユーザーがアプリをリムーバブル記憶域にインストールできるかどうかを示します。 詳しくは、「[アプリの宣言](../publish/product-declarations.md)」をご覧ください。     |   
| isGameDvrEnabled           |  boolean |   アプリのゲーム録画が有効になっているかどうかを示します。    |   
| gamingOptions           |  array |   アプリのゲーム関連の設定を定義する 1 つの[ゲーム オプション リソース](#gaming-options-object)を格納する配列です。     |   
| hasExternalInAppProducts           |     boolean          |   ユーザーが Microsoft Store コマース システムを使わないで購入することをアプリが許可するかどうかを示します。 詳しくは、「[アプリの宣言](../publish/product-declarations.md)」をご覧ください。     |   
| meetAccessibilityGuidelines           |    boolean           |  アプリがアクセシビリティ ガイドラインを満たことをテストされているかどうかを示します。 詳しくは、「[アプリの宣言](../publish/product-declarations.md)」をご覧ください。      |   
| notesForCertification           |  string  |   アプリの[認定の注意書き](../publish/notes-for-certification.md)が含まれます。    |    
| status           |   string  |  申請の状態。 次のいずれかの値を指定できます。 <ul><li>なし</li><li>Canceled</li><li>PendingCommit</li><li>CommitStarted</li><li>CommitFailed</li><li>PendingPublication</li><li>発行</li><li>公開済み</li><li>PublishFailed</li><li>PreProcessing</li><li>PreProcessingFailed</li><li>認定</li><li>CertificationFailed</li><li>Release</li><li>ReleaseFailed</li></ul>      |    
| statusDetails           |   object  | エラーに関する情報など、申請のステータスに関する追加情報が保持される[ステータスの詳細に関するリソース](#status-details-object)です。       |    
| fileUploadUrl           |   string  | 申請のパッケージのアップロードに使用する共有アクセス署名 (SAS) URI です。 申請用に新しいパッケージ、登録情報の画像、またはトレーラー ファイルを追加する場合は、パッケージと画像を含む ZIP アーカイブをこの URI にアップロードします。 詳しくは、「[アプリの申請の作成](#create-an-app-submission)」をご覧ください。       |    
| applicationPackages           |   array  | 申請の各パッケージに関する詳細を提供する[アプリケーション パッケージ リソース](#application-package-object)の配列です。 |    
| packageDeliveryOptions    | object  | 申請の段階的なパッケージのロールアウトと必須の更新の設定が含まれた[パッケージ配布オプション リソース](#package-delivery-options-object)です。  |
| enterpriseLicensing           |  string  |  アプリのエンタープライズ ライセンス動作を示す[エンタープライズ ライセンス値](#enterprise-licensing)のいずれかです。  |    
| allowMicrosoftDecideAppAvailabilityToFutureDeviceFamilies           |  boolean   |  [アプリを将来の Windows 10 デバイス ファミリで利用できるようにする](../publish/set-app-pricing-and-availability.md)ことを Microsoft が許可されているかどうかを示すします。    |    
| allowTargetFutureDeviceFamilies           | object   |  キーと値のペアのディクショナリです。各キーは [Windows 10 デバイス ファミリ](../publish/set-app-pricing-and-availability.md) を表し、各値は指定されたデバイス ファミリをアプリがターゲットにできるかどうかを示すブール値です。     |    
| friendlyName           |   string  |  パートナーセンターに表示される送信のフレンドリ名。 この値は、申請を作成するときに生成されます。       |  
| trailers           |  array |   アプリの登録情報用のビデオ トレーラーを表す[トレーラー リソース](#trailer-object)を 15 個まで格納する配列です。<br/><br/>   |  


<span id="pricing-object" />

### <a name="pricing-resource"></a>価格リソース

このリソースにはアプリの価格設定情報が保持されます。 このリソースには、次の値があります。

| 値           | Type    | 説明        |
|-----------------|---------|------|
|  trialPeriod               |    string     |  アプリの試用期間を示す文字列です。 次のいずれかの値を指定できます。 <ul><li>NoFreeTrial</li><li>OneDay</li><li>TrialNeverExpires</li><li>SevenDays</li><li>FifteenDays</li><li>ThirtyDays</li></ul>    |
|  marketSpecificPricings               |    object     |  キーと値のペアのディクショナリです。各キーは 2 文字の ISO 3166-1 alpha-2 の国コードで、各値は[価格帯](#price-tiers)です。 これらの項目は、[特定の市場でのアプリのカスタム価格](../publish/define-market-selection.md)を表します。 このディクショナリに含まれる項目は、指定された市場の *priceId* の値によって指定されている基本価格を上書きします。      |     
|  営業               |   array      |  **非推奨** です。 アプリの販売情報が保持される[販売リソース](#sale-object)の配列です。   |     
|  priceId               |   string      |  アプリの[基本価格](../publish/define-market-selection.md)を規定する[価格帯](#price-tiers)です。   |     
|  isAdvancedPricingModel               |   boolean      |  **true** の場合、開発者アカウントは 0.99 USD ～ 1999.99 USD の拡張された価格セットにアクセスできます。 **false** の場合、開発者アカウントは 0.99 USD ～ 999.99 USD の元の価格帯セットにアクセスできます。 各種価格帯について詳しくは、「[価格帯](#price-tiers)」をご覧ください。<br/><br/> &nbsp; メモ &nbsp;このフィールドは読み取り専用です。   |


<span id="sale-object" />

### <a name="sale-resource"></a>セール リソース

このリソースにはアプリのセール情報が保持されます。

> [!IMPORTANT]
> **セール** リソースはサポートを終了しました。現在、Microsoft Store 申請 API を使ってアプリの申請の販売データを取得または変更することはできません。 将来的には、Microsoft Store 申請 API を更新して、アプリの申請のセール情報にプログラムでアクセスする新しい方法を導入する予定です。
>    * [アプリの申請を取得する GET メソッド](get-an-app-submission.md)を呼び出すと、*セール* リソースは空になります。 引き続きパートナーセンターを使用して、アプリの送信に関する売上データを取得できます。
>    * [アプリの申請を更新する PUT メソッド](update-an-app-submission.md)を呼び出すとき、*セール* の値に含まれた情報は無視されます。 引き続きパートナーセンターを使用して、アプリの送信用に販売データを変更することができます。

このリソースには、次の値があります。

| 値           | Type    | 説明    |
|-----------------|---------|------|
|  name               |    string     |   セールの名前です。    |     
|  basePriceId               |   string      |  セールの基本価格として使用する[価格帯](#price-tiers)です。    |     
|  startDate               |   string      |   ISO 8601 形式で表したセールの開始日です。  |     
|  endDate               |   string      |  ISO 8601 形式で表したセールの終了日です。      |     
|  marketSpecificPricings               |   object      |   キーと値のペアのディクショナリです。各キーは 2 文字の ISO 3166-1 alpha-2 の国コードで、各値は[価格帯](#price-tiers)です。 これらの項目は、[特定の市場でのアプリのカスタム価格](../publish/define-market-selection.md)を表します。 このディクショナリに含まれる項目は、指定された市場の *basePriceId* の値によって指定されている基本価格を上書きします。    |


<span id="listing-object" />

### <a name="listing-resource"></a>登録情報リソース

このリソースにはアプリの登録情報が保持されます。 このリソースには、次の値があります。

| 値           | Type    | 説明                  |
|-----------------|---------|------|
|  baseListing               |   object      |  アプリの[基本の登録情報](#base-listing-object)です。これはすべてのプラットフォームで既定の登録情報となります。   |     
|  platformOverrides               | object |   キーと値のペアのディクショナリです。各キーは、登録情報を上書きするプラットフォームを示す文字列を表し、各値は、指定されたプラットフォームで上書きする登録情報を示す[基本の登録情報](#base-listing-object)リソース (description から title までの値のみが保持されています) を表します。 キーには次の値を設定できます。 <ul><li>Unknown</li><li>Windows80</li><li>Windows81</li><li>WindowsPhone71</li><li>WindowsPhone80</li><li>WindowsPhone81</li></ul>     |      |     

<span id="base-listing-object" />

### <a name="base-listing-resource"></a>基本の登録情報リソース

このリソースにはアプリの基本の登録情報が保持されます。 このリソースには、次の値があります。

| 値           | Type    | 説明       |
|-----------------|---------|------|
|  copyrightAndTrademarkInfo                |   string      |  (省略可能) [著作権や商標の情報](../publish/create-app-store-listings.md)です。  |
|  keywords                |  array       |  結果にアプリが表示される確率を高める[キーワード](../publish/create-app-store-listings.md)の配列です。    |
|  licenseTerms                |    string     | アプリの[ライセンス条項](../publish/create-app-store-listings.md) (省略可能) です。     |
|  privacyPolicy                |   string      |   この値は今後は使用しません。 アプリのプライバシーポリシーの URL を設定または変更するには、パートナーセンターの [ [プロパティ](../publish/enter-app-properties.md#privacy-policy-url) ] ページでこれを行う必要があります。 この値は、申請 API の呼び出しから省略することができます。 この値を設定しても無視されます。       |
|  supportContact                |   string      |  この値は今後は使用しません。 アプリのサポート担当者の URL または電子メールアドレスを設定または変更するには、パートナーセンターの [  [プロパティ](../publish/enter-app-properties.md#support-contact-info) ] ページでこの操作を行う必要があります。 この値は、申請 API の呼び出しから省略することができます。 この値を設定しても無視されます。        |
|  websiteUrl                |   string      |  この値は今後は使用しません。 アプリの web ページの URL を設定または変更するには、パートナーセンターの [  [プロパティ](../publish/enter-app-properties.md#website) ] ページでこれを行う必要があります。 この値は、申請 API の呼び出しから省略することができます。 この値を設定しても無視されます。      |    
|  description               |    string     |   アプリの登録情報の[説明](../publish/create-app-store-listings.md)です。   |     
|  features               |    array     |  アプリの[機能](../publish/create-app-store-listings.md)を示す最大 20 個の文字列の配列です。     |
|  releaseNotes               |  string       |  アプリの[リリース ノート](../publish/create-app-store-listings.md)です。    |
|  images               |   array      |  アプリの登録情報の[画像とアイコン](#image-object)のリソースの配列です。  |
|  recommendedHardware               |   array      |  アプリの[推奨されるハードウェア構成](../publish/create-app-store-listings.md#additional-information)を示す最大 11 個の文字列の配列です。     |
|  minimumHardware               |     string    |  アプリの[最小ハードウェア構成](../publish/create-app-store-listings.md#additional-information)を示す最大 11 個の文字列の配列です。    |  
|  title               |     string    |   アプリの登録情報のタイトルです。   |  
|  shortDescription               |     string    |  ゲームにのみ使用されます。 この説明は、Xbox One の Game Hub の **情報** セクションに表示され、お客様のゲームの詳細を理解するのに役立ちます。   |  
|  shortTitle               |     string    |  製品の名前の短いバージョン。 指定した場合、Xbox One のさまざまな場所 (インストール時や [実績] など) で製品のフル タイトルの代わりにこの短い名前が表示されることがあります。    |  
|  sortTitle               |     string    |   製品のアルファベット表記が複数ある場合、ここに別のバージョンを入力できます。 これにより、ユーザーが検索したときに製品がすばやく見つかるようになる可能性があります。    |  
|  voiceTitle               |     string    |   Kinect やヘッドセットを使うときに Xbox One のオーディオ エクスペリエンスで使われる、製品の代替名 (ある場合)。    |  
|  devStudio               |     string    |   登録情報に **[Developed by] (開発元)** フィールドを含める必要がある場合はこの値を指定します  (*devStudio* 値の指定とは関係なく、**[公開元]** フィールドにはアカウントに関連付けられた発行者の表示名が示されます)。    |  

<span id="image-object" />

### <a name="image-resource"></a>画像リソース

このリソースにはアプリの登録情報の画像とアイコンのデータが保持されます。 アプリの登録情報の画像とアイコンについて詳しくは、「[アプリのスクリーンショットと画像](../publish/app-screenshots-and-images.md)」をご覧ください。 このリソースには、次の値があります。

| 値           | Type    | 説明           |
|-----------------|---------|------|
|  fileName               |    string     |   申請用にアップロードした ZIP アーカイブに含まれている画像ファイルの名前です。    |     
|  fileStatus               |   string      |  画像ファイルの状態です。 次のいずれかの値を指定できます。 <ul><li>なし</li><li>PendingUpload</li><li>アップロード完了</li><li>PendingDelete</li></ul>   |
|  id  |  string  | 画像の ID です。 この値は、パートナーセンターによって指定されます。  |
|  description  |  string  | 画像の説明です。  |
|  imageType  |  string  | 画像の種類を示します。 現在サポートされている文字列は次のとおりです。 <p/>[スクリーン ショット画像](../publish/app-screenshots-and-images.md#screenshots): <ul><li>Screenshot (デスクトップのスクリーンショットにはこの値を使用します)</li><li>MobileScreenshot</li><li>XboxScreenshot</li><li>SurfaceHubScreenshot</li><li>HoloLensScreenshot</li></ul><p/>[ストアロゴ](../publish/app-screenshots-and-images.md#store-logos):<ul><li>StoreLogo9x16 </li><li>StoreLogoSquare</li><li>Icon (1:1 の 300 x 300 ピクセルのロゴにはこの値を使用します)</li></ul><p/>[プロモーションイメージ](../publish/app-screenshots-and-images.md#promotional-images): <ul><li>PromotionalArt16x9</li><li>PromotionalArtwork2400X1200</li></ul><p/>[Xbox イメージ](../publish/app-screenshots-and-images.md#xbox-images): <ul><li>XboxBrandedKeyArt</li><li>XboxTitledHeroArt</li><li>XboxFeaturedPromotionalArt</li></ul><p/>[オプションのプロモーションイメージ](../publish/app-screenshots-and-images.md#optional-promotional-images): <ul><li>SquareIcon358X358</li><li>BackgroundImage1000X800</li><li>PromotionalArtwork414X180</li></ul><p/> <!-- The following strings are also recognized for this field, but they correspond to image types that are no longer for listings in the Store.<ul><li>PromotionalArtwork846X468</li><li>PromotionalArtwork558X756</li><li>PromotionalArtwork414X468</li><li>PromotionalArtwork558X558</li><li>WideIcon358X173</li><li>Unknown</li></ul> -->   |


<span id="gaming-options-object" />

### <a name="gaming-options-resource"></a>ゲーム オプション リソース

このリソースにはアプリのゲーム関連の設定が保持されます。 このリソースの値は、パートナーセンターでの送信の [ゲーム設定](../publish/enter-app-properties.md#game-settings) に対応しています。

```json
{
  "gamingOptions": [
    {
      "genres": [
        "Games_ActionAndAdventure",
        "Games_Casino"
      ],
      "isLocalMultiplayer": true,
      "isLocalCooperative": true,
      "isOnlineMultiplayer": false,
      "isOnlineCooperative": false,
      "localMultiplayerMinPlayers": 2,
      "localMultiplayerMaxPlayers": 12,
      "localCooperativeMinPlayers": 2,
      "localCooperativeMaxPlayers": 12,
      "isBroadcastingPrivilegeGranted": true,
      "isCrossPlayEnabled": false,
      "kinectDataForExternal": "Enabled"
    }
  ],
}
```

このリソースには、次の値があります。

| 値           | Type    | 説明        |
|-----------------|---------|------|
|  ジャンル               |    array     |  ゲームのジャンルを説明する次の 1 つ以上の文字列の配列です。 <ul><li>Games_ActionAndAdventure</li><li>Games_CardAndBoard</li><li>Games_Casino</li><li>Games_Educational</li><li>Games_FamilyAndKids</li><li>Games_Fighting</li><li>Games_Music</li><li>Games_Platformer</li><li>Games_PuzzleAndTrivia</li><li>Games_RacingAndFlying</li><li>Games_RolePlaying</li><li>Games_Shooter</li><li>Games_Simulation</li><li>Games_Sports</li><li>Games_Strategy</li><li>Games_Word</li></ul>    |
|  isLocalMultiplayer               |    boolean     |  ゲームでローカル マルチプレイヤーがサポートされているかどうかを示します。      |     
|  isLocalCooperative               |   boolean      |  ゲームでローカル協力プレイがサポートされているかどうかを示します。    |     
|  isOnlineMultiplayer               |   boolean      |  ゲームでオンライン マルチプレイヤーがサポートされているかどうかを示します。    |     
|  isOnlineCooperative               |   boolean      |  ゲームでオンライン協力プレイがサポートされているかどうかを示します。    |     
|  localMultiplayerMinPlayers               |   INT      |   ゲームでサポートされるローカル マルチプレイヤーの最小プレイヤー数を指定します。   |     
|  localMultiplayerMaxPlayers               |   INT      |   ゲームでサポートされるローカル マルチプレイヤーの最大プレイヤー数を指定します。  |     
|  localCooperativeMinPlayers               |   INT      |   ゲームでサポートされるローカル協力プレイの最小プレイヤー数を指定します。  |     
|  localCooperativeMaxPlayers               |   INT      |   ゲームでサポートされるローカル協力プレイの最大プレイヤー数を指定します。  |     
|  isBroadcastingPrivilegeGranted               |   boolean      |  ゲームでブロードキャストがサポートされているかどうかを示します。   |     
|  isCrossPlayEnabled               |   boolean      |   ゲームで Windows 10 PC と Xbox のプレイヤー間でのマルチプレイヤー セッションがサポートされているかどうかを示します。  |     
|  kinectDataForExternal               |   string      |  次の各文字列値は、ゲームで Kinect データを収集し、外部サービスに送信できるかどうかを示します。 <ul><li>NotSet</li><li>Unknown</li><li>Enabled</li><li>無効</li></ul>   |

> [!NOTE]
> *gamingOptions* リソースは、Microsoft Store 申請 API が開発者向けに最初にリリースされた後、2017 年 5 月に追加されました。 このリソースが導入される前に申請 API を通じててアプリの申請を作成し、その申請がまだ審査中の場合、申請を正常にコミットするか削除するまで、アプリの申請に対するこのリソースは null になります。 アプリの申請で *gamingOptions* リソースが利用できない場合、[アプリの取得](get-an-app.md)メソッドから返される [アプリケーション リソース](get-app-data.md#application_object)の *hasAdvancedListingPermission* フィールドは false になります。

<span id="status-details-object" />

### <a name="status-details-resource"></a>ステータスの詳細に関するリソース

このリソースには、申請の状態についての追加情報が保持されます。 このリソースには、次の値があります。

| 値           | Type    | 説明         |
|-----------------|---------|------|
|  エラー               |    object     |   申請のエラーの詳細が保持される[ステータスの詳細リソース](#status-detail-object)の配列です。    |     
|  warnings               |   object      | 申請の警告の詳細が保持される[ステータスの詳細リソース](#status-detail-object)の配列です。      |
|  certificationReports               |     object    |   申請の認定レポート データへのアクセスを提供する[認定レポート リソース](#certification-report-object)です。 認定されなかった場合に、これらのレポートから詳しい情報を知ることができます。   |  


<span id="status-detail-object" />

### <a name="status-detail-resource"></a>ステータスの詳細に関するリソース

このリソースには、申請に関連するエラーや警告についての追加情報が保持されます。 このリソースには、次の値があります。

| 値           | Type    | 説明        |
|-----------------|---------|------|
|  code               |    string     |   エラーや警告の種類を説明する[申請ステータス コード](#submission-status-code)です。   |     
|  details               |     string    |  問題についての詳細が含まれるメッセージです。     |


<span id="application-package-object" />

### <a name="application-package-resource"></a>アプリケーション パッケージ リソース

このリソースには、申請のアプリ パッケージについての情報が保持されます。

```json
{
  "applicationPackages": [
    {
      "fileName": "contoso_app.appx",
      "fileStatus": "Uploaded",
      "id": "1152921504620138797",
      "version": "1.0.0.0",
      "architecture": "ARM",
      "languages": [
        "en-US"
      ],
      "capabilities": [
        "ID_RESOLUTION_HD720P",
        "ID_RESOLUTION_WVGA",
        "ID_RESOLUTION_WXGA"
      ],
      "minimumDirectXVersion": "None",
      "minimumSystemRam": "None",
      "targetDeviceFamilies": [
        "Windows.Mobile min version 10.0.10240.0"
      ]
    }
  ],
}
```

このリソースには、次の値があります。  

> [!NOTE]
> [アプリの申請の更新](update-an-app-submission.md)のメソッドを呼び出す場合、要求本文に必要なのは、このオブジェクトの *fileName*、*fileStatus*、*minimumDirectXVersion*、*minimumSystemRam* の値のみです。 その他の値は、パートナーセンターによって設定されます。

| 値           | Type    | 説明                   |
|-----------------|---------|------|
| fileName   |   string      |  パッケージの名前です。    |  
| fileStatus    | string    |  パッケージの状態です。 次のいずれかの値を指定できます。 <ul><li>なし</li><li>PendingUpload</li><li>アップロード完了</li><li>PendingDelete</li></ul>    |  
| id    |  string   |  パッケージを一意に識別する ID です。 この値は、パートナーセンターによって提供されます。   |     
| version    |  string   |  アプリ パッケージのバージョンです。 詳しくは、「[パッケージ バージョンの番号付け](../publish/package-version-numbering.md)」をご覧ください。   |   
| アーキテクチャ    |  string   |  パッケージのアーキテクチャ (ARM など) です。   |     
| languages    | array    |  アプリがサポートする言語の言語コードの配列です。 詳細については、[サポートされている言語](../publish/supported-languages.md)に関するページを参照してください。    |     
| capabilities    |  array   |  パッケージに必要な機能の配列です。 機能について詳しくは、「[アプリ機能の宣言](../packaging/app-capability-declarations.md)」をご覧ください。   |     
| minimumDirectXVersion    |  string   |  アプリ パッケージによってサポートされる DirectX の最小バージョンです。 Windows 8.x をターゲットとするアプリでのみ設定できます。 その他の OS バージョンをターゲットとするアプリの場合、[アプリの申請の更新](update-an-app-submission.md)メソッドの呼び出し時にはこの値が存在している必要がありますが、指定した値は無視されます。 次のいずれかの値を指定できます。 <ul><li>なし</li><li>DirectX93</li><li>DirectX100</li></ul>   |     
| minimumSystemRam    | string    |  アプリ パッケージに必要な RAM の最小サイズです。 Windows 8.x をターゲットとするアプリでのみ設定できます。 その他の OS バージョンをターゲットとするアプリの場合、[アプリの申請の更新](update-an-app-submission.md)メソッドの呼び出し時にはこの値が存在している必要がありますが、指定した値は無視されます。 次のいずれかの値を指定できます。 <ul><li>なし</li><li>Memory2GB</li></ul>   |       
| targetDeviceFamilies    | array    |  パッケージがターゲットにするデバイス ファミリを表す文字列の配列です。 この値は Windows 10 をターゲットにするパッケージにしか使用できません。以前のリリースをターゲットにするパッケージでは、この値は **None** になります。 次のデバイスファミリ文字列は、現在、Windows 10 パッケージでサポートされています *{0}* 。は、10.0.10240.0、10.0.10586.0、10.0.14393.0 などの windows 10 のバージョン文字列です。 <ul><li>Windows ユニバーサル最小バージョン *{0}*</li><li>Windows. Desktop の最小バージョン *{0}*</li><li>Windows Mobile の最小バージョン *{0}*</li><li>Windows. Xbox の最小バージョン *{0}*</li><li>Holographic の最小バージョン *{0}*</li></ul>   |    

<span/>

<span id="certification-report-object" />

### <a name="certification-report-resource"></a>認定レポート リソース

このリソースは、申請の認定レポート データへのアクセスを提供します。 このリソースには、次の値があります。

| 値           | Type    | 説明             |
|-----------------|---------|------|
|     date            |    string     |  レポートが生成された日付と時刻 (ISO 8601 形式)。    |
|     reportUrl            |    string     |  レポートにアクセスできる URL です。    |


<span id="package-delivery-options-object" />

### <a name="package-delivery-options-resource"></a>パッケージの配信オプション リソース

このリソースには、申請の段階的なパッケージのロールアウトと必須の更新の設定が含まれています。

```json
{
  "packageDeliveryOptions": {
    "packageRollout": {
        "isPackageRollout": false,
        "packageRolloutPercentage": 0,
        "packageRolloutStatus": "PackageRolloutNotStarted",
        "fallbackSubmissionId": "0"
    },
    "isMandatoryUpdate": false,
    "mandatoryUpdateEffectiveDate": "1601-01-01T00:00:00.0000000Z"
  },
}
```

このリソースには、次の値があります。

| 値           | Type    | 説明        |
|-----------------|---------|------|
| packageRollout   |   object      |  申請の段階的なパッケージのロールアウトの設定が含まれた[パッケージのロールアウトのリソース](#package-rollout-object)です。   |  
| isMandatoryUpdate    | boolean    |  この申請のパッケージを自己インストールのアプリの更新のために必須として扱うかどうかを指定します。 自己インストールのアプリの更新のために必須なパッケージについて詳しくは、「[アプリのパッケージの更新をダウンロードしてインストールする](../packaging/self-install-package-updates.md)」をご覧ください。    |  
| mandatoryUpdateEffectiveDate    |  date   |  この申請のパッケージが必須となる日時 (ISO 8601 形式、UTC タイムゾーン)。   |        

<span id="package-rollout-object" />

### <a name="package-rollout-resource"></a>パッケージのロールアウトのリソース

このリソースには、申請の段階的な[パッケージのロールアウトの設定](#manage-gradual-package-rollout)が含まれています。 このリソースには、次の値があります。

| 値           | Type    | 説明        |
|-----------------|---------|------|
| isPackageRollout   |   boolean      |  申請の段階的なパッケージのロールアウトが有効化されているかどうかを示します。    |  
| packageRolloutPercentage    | float    |  段階的なロールアウトでパッケージを受信するユーザーの割合。    |  
| packageRolloutStatus    |  string   |  段階的なパッケージのロールアウトの状態を示す、次の文字列のいずれかです。 <ul><li>PackageRolloutNotStarted</li><li>PackageRolloutInProgress</li><li>PackageRolloutComplete</li><li>PackageRolloutStopped</li></ul>  |  
| fallbackSubmissionId    |  string   |  段階的なロールアウトのパッケージを入手しないユーザーが受信する申請のID。   |          

> [!NOTE]
> *PackageRolloutStatus* と *fallbackの Id* 値はパートナーセンターによって割り当てられ、開発者が設定するものではありません。 これらの値を要求本文に含めると、これらの値は無視されます。

<span id="trailer-object" />

### <a name="trailers-resource"></a>トレーラー リソース

このリソースは、アプリの登録情報のビデオ トレーラーを表します。 このリソースの値は、パートナーセンターでの送信の [トレーラー](../publish/app-screenshots-and-images.md#trailers) オプションに対応しています。

[アプリの申請リソース](#app-submission-object)の *trailers* 配列には最大 15 個のトレーラー リソースを追加できます。 申請用のトレーラー ビデオ ファイルとサムネイル画像をアップロードするには、申請用のパッケージと登録情報の画像が含まれているものと同一の ZIP アーカイブにこれらのファイルを追加し、この ZIP アーカイブを申請用の共有アクセス署名 (SAS) URI にアップロードします。 ZIP アーカイブを SAS URI にアップロードする方法について詳しくは、「[アプリの申請の作成](#create-an-app-submission)」をご覧ください。

```json
{
  "trailers": [
    {
      "id": "1158943556954955699",
      "videoFileName": "Trailers\\ContosoGameTrailer.mp4",
      "videoFileId": "1159761554639123258",
      "trailerAssets": {
        "en-us": {
          "title": "Contoso Game",
          "imageList": [
            {
              "fileName": "Images\\ContosoGame-Thumbnail.png",
              "id": "1155546904097346923",
              "description": "This is a still image from the video."
            }
          ]
        }
      }
    }
  ]
}
```

このリソースには、次の値があります。

| 値           | Type    | 説明        |
|-----------------|---------|------|
|  id               |    string     |   トレーラーの ID です。 この値は、パートナーセンターによって提供されます。   |
|  videoFileName               |    string     |    申請用のファイルが含まれた ZIP アーカイブ内のトレーラー ビデオ ファイルの名前です。    |     
|  videoFileId               |   string      |  トレーラー ビデオ ファイルの ID です。 この値は、パートナーセンターによって提供されます。   |     
|  trailerAssets               |   object      |  キーと値のペアのディクショナリです。各キーは言語コードであり、各値はトレーラーの追加のロケール固有アセットを含む[トレーラー アセット リソース](#trailer-assets-object)です。 サポートされている言語コードについて詳しくは、「[サポートされている言語](../publish/supported-languages.md)」をご覧ください。    |     

> [!NOTE]
> *trailers* リソースは、Microsoft Store 申請 API が開発者向けに最初にリリースされた後、2017 年 5 月に追加されました。 このリソースが導入される前に申請 API を通じててアプリの申請を作成し、その申請がまだ審査中の場合、申請を正常にコミットするか削除するまで、アプリの申請に対するこのリソースは null になります。 アプリの申請で *trailers* リソースが利用できない場合、[アプリの取得](get-an-app.md)メソッドから返される [アプリケーション リソース](get-app-data.md#application_object)の *hasAdvancedListingPermission* フィールドは false になります。

<span id="trailer-assets-object" />

### <a name="trailer-assets-resource"></a>トレーラー アセット リソース

このリソースには、[トレーラー リソース](#trailer-object)で定義されているトレーラー用の追加のロケール固有アセットが保持されます。 このリソースには、次の値があります。

| 値           | Type    | 説明        |
|-----------------|---------|------|
| title   |   string      |  トレーラーのローカライズされたタイトルです。 タイトルは、ユーザーがトレーラーを全画面表示モードで再生すると表示されます。     |  
| imageList    | array    |   1 つの[画像](#image-for-trailer-object)リソースが含まれた配列で、トレーラーのサムネイル画像を提供します。 この配列には 1 つの[画像](#image-for-trailer-object)リソースのみを含めることができます。  |   


<span id="image-for-trailer-object" />

### <a name="image-resource-for-a-trailer"></a>画像リソース (トレーラー用)

このリソースは、トレーラーのサムネイル画像を記述しています。 このリソースには、次の値があります。

| 値           | Type    | 説明           |
|-----------------|---------|------|
|  fileName               |    string     |   申請用にアップロードした ZIP アーカイブに含まれているサムネイル画像ファイルの名前です。    |     
|  id  |  string  | サムネイル画像の ID です。 この値は、パートナーセンターによって提供されます。  |
|  description  |  string  | サムネイル画像の説明です。 この値はメタデータのみです。ユーザーには表示されません。   |

<span/>

## <a name="enums"></a>列挙型

これらのメソッドでは、次の列挙型が使用されます。

<span id="price-tiers" />

### <a name="price-tiers"></a>価格レベル

次の値は、[価格リソース](#pricing-object)における、アプリの申請に利用できる価格帯を表します。

| 値           | 説明        |
|-----------------|------|
|  ベース               |   価格帯が設定されていない場合、アプリの基本価格が使用されます。      |     
|  NotAvailable              |   アプリは指定された地域で提供されていません。    |     
|  Free              |   このアプリは無料です。    |    
|  Tier *xxx*               |   アプリの価格帯を指定する文字列 (**Tier <em>xxxx</em>** の形式)。 現在のところ、次の範囲の価格帯がサポートされています。<br/><br/><ul><li>[価格リソース](#pricing-object)の *isAdvancedPricingModel* 値が **true** の場合、アカウントで利用可能な価格帯値は **Tier1012** - **Tier1424** です。</li><li>[価格リソース](#pricing-object)の *isAdvancedPricingModel* 値が **false** の場合、アカウントで利用可能な価格帯値は **Tier2** - **Tier96** です。</li></ul>各レベルに関連付けられている市場固有の価格を含め、開発者アカウントで使用できる価格レベルの完全なテーブルを確認するには、パートナーセンターで任意のアプリの送信の [**価格と可用性**] ページにアクセスし、[**市場とカスタム価格** **] セクション** の [**テーブルの表示**] リンクをクリックします。    |


<span id="enterprise-licensing" />

### <a name="enterprise-licensing-values"></a>エンタープライズ ライセンス値

次の値は、アプリに対する組織のライセンス動作を表します。 これらのオプションについて詳しくは、「[組織のライセンス オプション](../publish/organizational-licensing.md)」をご覧ください。

> [!NOTE]
> アプリに対する組織のライセンス オプションは申請 API を通じて構成できますが、この API を使って[ビジネス向け Microsoft Store や教育機関向け Microsoft Store でのボリューム購入](../publish/organizational-licensing.md)の申請を公開することはできません。 教育のために Microsoft Store のビジネス向けおよび Microsoft Store に送信を発行するには、パートナーセンターを使用する必要があります。


| 値           |  説明      |
|-----------------|---------------|
| なし            |     ストアで管理される (オンラインの) ボリューム ライセンスがある企業に、アプリの利用を許可しません。         |     
| オンライン        |     ストアで管理される (オンラインの) ボリューム ライセンスがある企業に、アプリの利用を許可します。  |
| OnlineAndOffline | ストアで管理される (オンラインの) ボリューム ライセンスがある企業にアプリの利用を許可し、未接続状態 (オフライン) のライセンスのある企業にアプリの利用を許可します。 |


<span id="submission-status-code" />

### <a name="submission-status-code"></a>申請の状態コード

次の値は、申請の状態コードを表します。

| 値           |  説明      |
|-----------------|---------------|
| なし            |     コードが指定されていません。         |     
| InvalidArchive        |     パッケージが含まれる ZIP アーカイブは無効であるか、認識できないアーカイブ形式です。  |
| MissingFiles | ZIP アーカイブに、申請データで指定されているすべてのファイルが含まれていないか、ファイルのアーカイブ内の場所が正しくありません。 |
| PackageValidationFailed | 申請の 1 つ以上のパッケージを検証できませんでした。 |
| InvalidParameterValue | 要求本文に含まれるパラメーターの 1 つが無効です。 |
| InvalidOperation | 実行された操作は無効です。 |
| InvalidState | 実行された操作は、パッケージ フライトの現在の状態では無効です。 |
| ResourceNotFound | 指定されたパッケージ フライトは見つかりませんでした。 |
| ServiceError | 内部サービス エラーのため、要求を処理できませんでした。 もう一度要求を行ってください。 |
| ListingOptOutWarning | 開発者が以前の申請の登録情報を削除しているか、パッケージによってサポートされる登録情報を含めていませんでした。 |
| ListingOptInWarning  | 開発者が登録情報を追加しました。 |
| UpdateOnlyWarning | 開発者が、更新サポートしかないものを挿入しようとしています。 |
| その他  | 申請が非認識または未分類の状態です。 |
| PackageValidationWarning | パッケージ検証プロセスの結果、警告が生成されました。 |

<span/>

## <a name="related-topics"></a>関連トピック

* [Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)
* [Microsoft Store 申請 API を使用したアプリ データの取得](get-app-data.md)
* [パートナーセンターでのアプリの送信](../publish/app-submissions.md)
