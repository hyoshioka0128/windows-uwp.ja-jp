---
Description: 名前を予約してアプリを作成したら、そのアプリを公開するための作業を開始できます。 まず、申請を作成します。
title: アプリの申請
ms.assetid: 363BB9E4-4437-4238-A80F-ABDFC70D96E4
keywords: チェックリスト, windows, uwp, 申請, 提出, ゲーム, アプリ, 送信
ms.date: 10/31/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 1359fb530dec1a35b2ab2994442b65ec441cc0ac
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89158066"
---
# <a name="app-submissions"></a>アプリの申請


[名前を予約してアプリを作成](create-your-app-by-reserving-a-name.md)したら、そのアプリを公開するための作業を開始できます。 最初の手順では、 **送信**を作成します。

申請は、アプリが完成して公開する準備ができたときに開始できます。または、1 行のコードを記述する前でも情報を入力し始めることができます。 提出物に対して行った更新は保存されるので、準備ができたらいつでも戻って作業することができます。

> [!NOTE]
> Microsoft Store にアプリを送信するには、[パートナーセンター](https://partner.microsoft.com/dashboard)にアクティブな[開発者アカウント](https://developer.microsoft.com/store/register)が必要です。

アプリが発行されたら、パートナーセンターで別の送信を作成して、更新されたバージョンを発行できます。 新しい申請を作成すると、新しいパッケージをアップロードするときでも、価格やカテゴリなどの情報を変更するだけのときでも、必要な変更を加えて公開することができます。 発行されたアプリの新しい送信を作成するには、[**概要**] ページに表示されている最新の送信の横にある [**更新**] をクリックします。 また、必要に応じて [ストアからアプリを削除](guidance-for-app-package-management.md#removing-an-app-from-the-store) することもできます (必要に応じて、後で再度使用できるようにします)。

> [!NOTE]
> ドキュメントのこのセクションでは、パートナーセンターでアプリの送信を作成する方法について説明します。 ここで説明する方法以外に、[Microsoft Store 申請 API](../monetize/create-and-manage-submissions-using-windows-store-services.md) を使用してアプリ申請を自動化することもできます。

> [!IMPORTANT]
> Windows Phone 8. x SDK を使用してビルドされた新しい XAP パッケージをアップロードすることはできなくなりました。 既に XAP パッケージと共にストアに格納されているアプリは、引き続き Windows 10 Mobile デバイスで動作します。 詳細については、こちらの [ブログ投稿](https://blogs.windows.com/windowsdeveloper/2018/08/20/important-dates-regarding-apps-with-windows-phone-8-x-and-earlier-and-windows-8-8-1-packages-submitted-to-microsoft-store)を参照してください。

## <a name="app-submission-checklist"></a>アプリの申請用チェック リスト

ここでは、アプリの申請を作成するときに提供できる詳細情報と、それぞれの詳細へのリンクを示します。

提供または指定する情報には、必須のものと 省略可能なものがあります。提供されている既定値は必要に応じて変更できます。 これらのセクションについて、記載されている順序で作業する必要はありません。

### <a name="pricing-and-availability-page"></a>[価格と使用可能状況] ページ
| フィールド名                    | Notes                                       | 詳しい情報                                                             |
|-------------------------------|---------------------------------------------|---------------------------------------------------------------------------|
| **市場**                   | 既定値: 対象となるすべての市場  | [価格と市場の選択の定義](./define-market-selection.md)         |
| **対象ユーザー**                | 既定値: パブリック対象ユーザー | [対象ユーザー](choose-visibility-options.md#audience) |
| **Discoverability (探索可能性)**                | 既定値: この製品を Microsoft Store で提供し、検索可能にします | [Discoverability (探索可能性)](choose-visibility-options.md#discoverability) |
| **[スケジュール]**                  | 既定値: 最短でリリース        | [正確なリリース スケジュールの構成](configure-precise-release-scheduling.md) |
| **基本価格**                | 必須                                    | [アプリの価格の設定とスケジュール](set-and-schedule-app-pricing.md)              |
| **無料試用版**                | 既定値: 無料の試用版なし                      | [無料試用版](set-app-pricing-and-availability.md#free-trial)              |
| **セール価格**              | オプション                                    | [アプリとアドオンの販売](put-apps-and-add-ons-on-sale.md)           |
| **組織のライセンス**    | 既定値: 組織単位でのボリューム購入を許可する | [組織のライセンス オプション](organizational-licensing.md)        |
      |


### <a name="properties-page"></a>[プロパティ] ページ

| フィールド名                    | Notes                                       | 詳しい情報                                                             |
|-------------------------------|---------------------------------------------|---------------------------------------------------------------------------|
| **[カテゴリとサブカテゴリ]**  | 必須                                    | [カテゴリとサブカテゴリの一覧](category-and-subcategory-table.md)       |
| **[プライバシー ポリシーの URL]**            | 多くのアプリでは必須。 「[アプリ開発者契約](/legal/windows/agreements/app-developer-agreement)」と「[Microsoft Store ポリシー](store-policies.md#105-personal-information)」をご覧ください | [[プライバシー ポリシーの URL]](enter-app-properties.md#privacy-policy-url)        |
| **Web サイト**                   | オプション                                    | [Web サイト](enter-app-properties.md#website)                   |
| **サポートの問い合わせ先情報**      | 製品が Xbox で使用可能な場合は必須。それ以外の場合は省略可能 (ただし推奨)                                   | [サポートの問い合わせ先情報](enter-app-properties.md#support-contact-info)              |
| **ゲーム設定**             | 省略可能 (ゲームにのみ適用)         | [ゲーム設定](enter-app-properties.md#game-settings) |
| **表示モード**             | オプション                   | [表示モード](enter-app-properties.md#display-mode) |
| **製品の宣言**          | 既定値: ユーザーは、代替ドライブやリムーバブル ストレージにこのアプリをインストールできます。Windows はこのアプリのデータを OneDrive に自動的にバックアップできます | [製品の宣言](./product-declarations.md) |
| **システム要件**      | オプション                                    | [システム要件](enter-app-properties.md#system-requirements)      |

<span/>

### <a name="age-ratings-page"></a>[年齢区分] ページ

| フィールド名                    | Notes                                       | 詳しい情報                          |
|-------------------------------|---------------------------------------------|----------------------------------------|
| **年齢区分**               | 必須                                    | [年齢区分](age-ratings.md)          |

<span/>

### <a name="packages-page"></a>[パッケージ] ページ

| フィールド名                    | Notes                                  | 詳しい情報                          |
|-------------------------------|----------------------------------------|----------------------------------------|
| **パッケージのアップロード制御**    | 必須 (パッケージが 1 つ以上)        | [アプリ パッケージのアップロード](upload-app-packages.md) |
| **デバイス ファミリの利用可否** | 既定値: パッケージに基づく       | [デバイス ファミリの利用可否](device-family-availability.md) |
| **段階的なパッケージのロールアウト**   | 省略可能 (更新プログラムのみ)            | [段階的なパッケージのロールアウト](gradual-package-rollout.md) |
| **必須の更新プログラム**          | 省略可能 (更新プログラムのみ)            | [必須の更新プログラム](upload-app-packages.md#mandatory-update)


### <a name="store-listings"></a>ストア登録情報

必須情報のすべてを、アプリでサポートする言語のうち、少なくとも 1 つの言語で用意する必要があります。 [Store 登録情報](create-app-store-listings.md)は、アプリでサポートするすべての言語で用意することをお勧めします。また[追加の言語で Store 登録情報を用意](create-app-store-listings.md#store-listing-languages)することもできます。 同じ製品の複数の登録情報を管理しやすくするため、[Store 登録情報をインポートおよびエクスポート](import-and-export-store-listings.md)することができます。

| フィールド名                    | Notes                                       | 詳しい情報                                                     |
|-------------------------------|---------------------------------------------|-------------------------------------------------------------------|
| **説明**               | 必須                                    | [人の心をつかむアプリの説明を書く](write-a-great-app-description.md) |
| **このバージョンの新機能**   | オプション                                 | [リリース ノート](create-app-store-listings.md#whats-new-in-this-version)       |
| **アプリの機能**              | オプション                                    | [製品の機能](create-app-store-listings.md#product-features)         |
| **スクリーンショット**               | 必須 (スクリーンショット 1 つ以上。4 つ以上を推奨)          | [スクリーンショット](app-screenshots-and-images.md#screenshots)          |
| **ストア ロゴ**               | 推奨。一部の OS バージョンで必須 | [ストア ロゴ](app-screenshots-and-images.md#store-logos)             |
| **予告編**                  | オプション                                    | [予告編](app-screenshots-and-images.md#trailers)                | 
| **Windows 10 と Xbox の画像 (16:9 スーパー ヒーロー アート)**     | 推奨        | [Windows 10 と Xbox の画像 (16:9 スーパー ヒーロー アート)](app-screenshots-and-images.md#windows-10-and-xbox-image-169-super-hero-art) |
| **Xbox 画像**     | Xbox に発行した場合に適切に表示するために必要です        | [Xbox 画像](app-screenshots-and-images.md#xbox-images) |
| **補足フィールド**  | オプション                                    | [補足フィールド](create-app-store-listings.md#supplemental-fields) 
| **検索語句**              | オプション                                    | [検索語句](create-app-store-listings.md#search-terms)         |
| **著作権と商標の情報** | オプション                                 | [著作権と商標の情報](create-app-store-listings.md#copyright-and-trademark-info) |
| **追加のライセンス条項**  | オプション                                    | [追加のライセンス条項](create-app-store-listings.md#additional-license-terms) |
| **開発者**              | オプション                                    | [開発者](create-app-store-listings.md#developed-by)                   |


<span/>

### <a name="submission-options-page"></a>申請オプション ページ

| フィールド名                    | Notes                                       | 詳しい情報                                                     |
|-------------------------------|---------------------------------------------|-------------------------------------------------------------------|
| **公開の保留オプション**     | 既定: この申請が認定されたら、すぐに申請を公開します (または [スケジュール] セクションで選択した各日付で公開します)      | [公開の保留オプション](manage-submission-options.md#publishing-hold-options)    
| **[認定の注意書き]**     | 推奨          | [[認定の注意書き]](notes-for-certification.md)             |
| **制限付き機能**     | 製品で制限された[機能](../packaging/app-capability-declarations.md#restricted-capabilities)を宣言する場合は必須    | [制限付き機能](manage-submission-options.md#publishing-hold-options)       

<span/>

> [!NOTE]
> 基幹業務 (LOB) アプリを企業に直接公開する方法については、「[LOB アプリの企業への配布](distribute-lob-apps-to-enterprises.md)」をご覧ください。