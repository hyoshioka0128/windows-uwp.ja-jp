---
description: ユーザーがアプリを無料で使うことができる試用期間を設け、その期間中は一部の機能を除外または制限することで、アプリを通常版にアップグレードするようユーザーに促すことができます。
title: 試用版での機能の除外または制限
ms.assetid: 1B62318F-9EF5-432A-8593-F3E095CA7056
keywords: Windows 10, UWP, 試用, アプリ内購入, IAP, Windows.ApplicationModel.Store
ms.date: 08/25/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 701769386f9637574cfb7f38f7458a1434796730
ms.sourcegitcommit: a3bbd3dd13be5d2f8a2793717adf4276840ee17d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93033975"
---
# <a name="exclude-or-limit-features-in-a-trial-version"></a>試用版での機能の除外または制限

ユーザーがアプリを無料で使うことができる試用期間を設け、その期間中は一部の機能を除外または制限することで、アプリを通常版にアップグレードするようユーザーに促すことができます。 どのような機能を制限するかをコーディング開始前に決め、完全なライセンスが購入されたときにだけその機能が正しく動作するようにアプリを設定します。 また、ユーザーがアプリを購入する前の試用期間中にだけバナーや透かしなどを表示する機能を有効にすることもできます。

> [!IMPORTANT]
> この記事では、[Windows.ApplicationModel.Store](/uwp/api/windows.applicationmodel.store) 名前空間のメンバーを使って、試用版機能を実装する方法について説明します。 この名前空間は更新されなくなり、新機能も追加されないため、代わりに [Windows.Services.Store](/uwp/api/windows.services.store) 名前空間を使用することをお勧めします。 **Windows** では、ストアで管理されているアドオンやサブスクリプションなど、最新のアドオンの種類がサポートされており、パートナーセンターとストアでサポートされる将来の種類の製品や機能と互換性があるように設計されています。 **Windows.Services.Store** 名前空間は、Windows 10 バージョン 1607 で導入され、Visual Studio で、 **Windows 10 Anniversary Edition (10.0、ビルド 14393)** 以降のリリースをターゲットとするプロジェクトでのみ使用できます。 **Windows.Services.Store** 名前空間を使用した試用版機能の実装について詳しくは、 [この記事](implement-a-trial-version-of-your-app.md)をご覧ください。

## <a name="prerequisites"></a>前提条件

ユーザーが購入できる機能を追加する Windows アプリ。

## <a name="step-1-pick-the-features-you-want-to-enable-or-disable-during-the-trial-period"></a>手順 1: 試用期間中に有効または無効にする機能を選ぶ

アプリの現時点でのライセンスの状態は、[LicenseInformation](/uwp/api/Windows.ApplicationModel.Store.LicenseInformation) クラスのプロパティとして保存されています。 通常は、次の手順で説明するように、ライセンスの状態に依存する関数を条件ブロック内に記述します。 このような機能について検討するときには、ライセンスがどの状態であっても動作するように実装できることを確認してください。

また、アプリの実行中にライセンスが変更された場合の処理方法を決めておきます。 試用版のアプリでもすべての機能を使うことができるようにしながら、購入版では表示されない広告バナーを表示することができます。 また、試用版アプリでは一部の機能を無効にしたり、ユーザーに購入を勧めるメッセージを表示したりすることもできます。

アプリの性質を考慮して、それに適した試用や有効期限の戦略を立ててください。 ゲームの試用版の場合は、ユーザーが遊べるゲーム コンテンツの量を制限するのが良い戦略でしょう。 ユーティリティの試用版の場合は、有効期限日の設定や、ユーザーが使いたがるような機能の制限を検討するとよいでしょう。

ゲーム以外の多くのアプリでは、ユーザーにアプリ全体を理解してもらうために、有効期限日を設定するのが適しています。 ここでは、有効期限に関するいくつかの一般的なシナリオと、その処理方法について説明します。

-   **アプリの実行中に試用ライセンスが期限切れになった**

    アプリの実行中に試用ライセンスが期限切れになった場合は、次の対処方法があります。

    -   何もしない。
    -   ユーザーにメッセージを表示する。
    -   惜しいです。
    -   ユーザーにアプリの購入を促す。

    お勧めするのは、アプリの購入を促すメッセージを表示することです。ユーザーがアプリを購入したら、すべての機能を有効にして、そのまま使うことができるようにします。 購入しなかった場合は、アプリを閉じるか、アプリの購入が必要なことを一定の間隔で通知します。

-   **アプリの起動前に試用ライセンスが期限切れになった**

    ユーザーがアプリを起動する前に試用ライセンスが期限切れになった場合、アプリは起動しません。 ユーザーには、ストアからそのアプリを購入できることを伝えるダイアログ ボックスが表示されます。

-   **アプリの実行中にユーザーがアプリを購入した**

    アプリの実行中にユーザーがアプリを購入した場合は、次の対処方法があります。

    -   何もせず、アプリが再起動されるまでは試用モードを続ける。
    -   購入に対するお礼をする、またはメッセージを表示する。
    -   完全なライセンスがある場合に使うことができる機能を、通知なしで有効にする (または、試用版であることを示す表示を消す)。

ライセンスの変更を検出して、アプリで対応する場合は、次の手順で説明するように、そのためのイベント ハンドラーを追加する必要があります。

## <a name="step-2-initialize-the-license-info"></a>手順 2: ライセンス情報を初期化する

アプリを初期化するときに、この例で示されているように、アプリの [LicenseInformation](/uwp/api/Windows.ApplicationModel.Store.LicenseInformation) オブジェクトを取得してください。 **licenseInformation** は、 **LicenseInformation** 型のグローバル変数またはフィールドと仮定します。

ここでは、[CurrentApp](/uwp/api/Windows.ApplicationModel.Store.CurrentApp) ではなく [CurrentAppSimulator](/uwp/api/Windows.ApplicationModel.Store.CurrentAppSimulator) を使って、シミュレートされたライセンス情報を取得します。 アプリのリリース バージョンを **ストア** に提出する前に、コード内のすべての **CurrentAppSimulator** の参照を **CurrentApp** と置き換える必要があります。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/InAppPurchasesAndLicenses/cs/TrialVersion.cs" id="InitializeLicenseTest":::

次に、アプリの実行中にライセンスが変更されたときに通知を受け取るイベント ハンドラーを追加します。 アプリのライセンスが変更されるのは、たとえば、試用期間が終了したときや、ユーザーがストアを通じてアプリを購入したときです。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/InAppPurchasesAndLicenses/cs/TrialVersion.cs" id="InitializeLicenseTestWithEvent":::

## <a name="step-3-code-the-features-in-conditional-blocks"></a>手順 3: 条件ブロック内に機能のコードを記述する

ライセンスの変更のイベントが発生したときに、アプリはライセンス API を呼び出して試用の状態が変わったかどうかを判定する必要があります。 この手順のコードは、このイベントのハンドラーを構造化する方法を示しています。 この時点で、ユーザーがアプリを購入したら、ライセンスの状態が変わったことをユーザーに知らせることをお勧めします。 コーディングの方法上、必要であれば、ユーザーにアプリを再起動してもらわなければならないこともあります。 ただし、この移行は可能な限りスムーズで違和感のないようにする必要があります。

この例は、アプリの機能を必要に応じて有効にしたり、無効にしたりできるように、アプリのライセンス状態を判断する方法を示したものです。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/InAppPurchasesAndLicenses/cs/TrialVersion.cs" id="ReloadLicense":::

## <a name="step-4-get-an-apps-trial-expiration-date"></a>手順 4: アプリの試用有効期限日を取得する

アプリの試用有効期限日を取得するコードを含めます。

この例のコードは、アプリの試用有効期限日を取得する関数を定義しています。 ライセンスがまだ有効であれば、試用期限が切れるまでの日数で有効期限を表示します。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/InAppPurchasesAndLicenses/cs/TrialVersion.cs" id="DisplayTrialVersionExpirationTime":::

## <a name="step-5-test-the-features-using-simulated-calls-to-the-license-api"></a>手順 5: シミュレートされたライセンス API 呼び出しで機能をテストする

シミュレートされたデータを使用してアプリをテストします。 **Currentappsimulator** は WindowsStoreProxy.xml という名前の XML ファイルからテスト固有のライセンス情報を取得します。このファイルは、% UserProfile% \\ AppData \\ ローカル \\ パッケージの \\ &lt; パッケージ名 &gt; \\ localstate \\ Microsoft \\ Windows Store \\ apidata にあります。 WindowsStoreProxy.xml を編集して、アプリや機能のシミュレートされた有効期限日を変更できます。 すべてが意図したとおりに動作するように、想定されるすべての有効期限とライセンスの構成をテストします。 詳しくは、「[CurrentAppSimulator での WindowsStoreProxy.xml ファイルの使用](in-app-purchases-and-trials-using-the-windows-applicationmodel-store-namespace.md#proxy)」をご覧ください。

このパスとファイルがない場合は、インストール時か実行時にそれらを作る必要があります。 WindowsStoreProxy.xml が所定の場所にない状態で [CurrentAppSimulator.LicenseInformation](/uwp/api/windows.applicationmodel.store.currentappsimulator.licenseinformation) プロパティにアクセスしようとすると、エラーになります。

## <a name="step-6-replace-the-simulated-license-api-methods-with-the-actual-api"></a>手順 6: シミュレートされたライセンス API メソッドを実際の API に置き換える

シミュレートされたライセンス サーバーでアプリをテストした後、認定用にストアにアプリを提出する前に、 **CurrentAppSimulator** を **CurrentApp** に置き換えます (次のコード例を参照)。

> [!IMPORTANT]
> アプリはストアへの提出時に **CurrentApp** オブジェクトを使っている必要があり、そうでない場合は認定が不合格になります。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/InAppPurchasesAndLicenses/cs/TrialVersion.cs" id="InitializeLicenseRetailWithEvent":::

## <a name="step-7-describe-how-the-free-trial-works-to-your-customers"></a>手順 7: 無料の試用版についてユーザーに説明する

アプリの動作でユーザーが驚くことがないように、無料試用版のアプリが試用期間中にどのように機能し、期間が過ぎるとどのようになるかを必ず説明してください。

アプリの説明について詳しくは、「[アプリの説明の作成](../publish/create-app-store-listings.md)」をご覧ください。

## <a name="related-topics"></a>関連トピック

* [ストア サンプル (試用版とアプリ内購入のデモンストレーション)](https://github.com/Microsoft/Windows-universal-samples/tree/win10-1507/Samples/Store)
* [アプリの価格と使用可能状況の設定](../publish/set-app-pricing-and-availability.md)
* [CurrentApp](/uwp/api/Windows.ApplicationModel.Store.CurrentApp)
* [CurrentAppSimulator](/uwp/api/Windows.ApplicationModel.Store.CurrentAppSimulator)
 

 
