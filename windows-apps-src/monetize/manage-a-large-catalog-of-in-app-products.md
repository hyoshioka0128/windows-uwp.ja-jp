---
ms.assetid: 5E722AFF-539D-456E-8C4A-ADE90CF7674A
description: アプリ内製品のカタログが大きくなる場合、カタログを管理するためにこのトピックで説明するプロセスを採用できます。
title: アプリ内製品の大規模なカタログの管理
ms.date: 08/25/2017
ms.topic: article
keywords: Windows 10, UWP, アプリ内購入, IAP, アドオン, カタログ, Windows.ApplicationModel.Store
ms.localizationpriority: medium
ms.openlocfilehash: e3eb35e2fccede9dc6f0412a3762d3d6245847c0
ms.sourcegitcommit: c3ca68e87eb06971826087af59adb33e490ce7da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364095"
---
# <a name="manage-a-large-catalog-of-in-app-products"></a>アプリ内製品の大規模なカタログの管理

アプリ内製品のカタログが大きくなる場合、カタログを管理するためにこのトピックで説明するプロセスを採用できます。 Windows 10 より前のリリースでは、開発者アカウントごとに 200 製品の表示制限があり、このトピックで説明するプロセスを使ってこの制限を回避できます。 Windows 10 以降では、開発者アカウントごとに表示されるストアの製品数に制限がないため、この記事で説明されているプロセスは必要ありません。

> [!IMPORTANT]
> この記事では、[Windows.ApplicationModel.Store](/uwp/api/windows.applicationmodel.store) 名前空間のメンバーの使用方法について説明します。 この名前空間は更新されなくなり、新機能も追加されないため、代わりに [Windows.Services.Store](/uwp/api/windows.services.store) 名前空間を使用することをお勧めします。 **Windows**では、ストアで管理されているアドオンやサブスクリプションなど、最新のアドオンの種類がサポートされており、パートナーセンターとストアでサポートされる将来の種類の製品や機能と互換性があるように設計されています。 **Windows.Services.Store** 名前空間は、Windows 10 バージョン 1607 で導入され、Visual Studio で、**Windows 10 Anniversary Edition (10.0、ビルド 14393)** 以降のリリースをターゲットとするプロジェクトでのみ使用できます。 詳しくは、「[アプリ内購入と試用版](in-app-purchases-and-trials.md)」をご覧ください。

この機能を有効にするには、特定の価格帯に対して少数の製品エントリを作成し、個々のエントリで、カタログ内の多数の製品を表します。 [RequestProductPurchaseAsync](/uwp/api/windows.applicationmodel.store.currentapp.requestproductpurchaseasync) メソッドのオーバーロードを使って、ストアに掲載されたアプリ内購入製品に関連する、アプリで定義された販売を指定します。 呼び出し中に販売と製品の関連付けを指定することに加えて、アプリでは、大規模なカタログ販売の詳細を格納する [ProductPurchaseDisplayProperties](/uwp/api/Windows.ApplicationModel.Store.ProductPurchaseDisplayProperties) オブジェクトも渡す必要があります。 これらの詳細が指定されていない場合、一覧に掲載された製品の詳細が代わりに使われます。

ストアでは、結果の [PurchaseResults](/uwp/api/Windows.ApplicationModel.Store.PurchaseResults) で、購入要求からの *offerId* のみを使います。 このプロセスは、[ストアにアプリ内製品を掲載した](../publish/add-on-submissions.md)ときに最初に提供された情報を直接変更するわけではありません。

## <a name="prerequisites"></a>前提条件

-   このトピックでは、ストアの一覧に表示される 1 つのアプリ内購入製品を使って複数のアプリ内販売を表現することに対する、ストアのサポートについて説明します。 アプリ内購入に詳しくない場合は、「[アプリ内製品購入の有効化](enable-in-app-product-purchases.md)」を読んで、ライセンス情報と、ストアでアプリ内購入を適切に一覧表示する方法を確かめてください。
-   新しいアプリ内販売のコード記述やテストを初めて行うときは、[CurrentApp](/uwp/api/Windows.ApplicationModel.Store.CurrentApp) オブジェクトではなく、[CurrentAppSimulator](/uwp/api/Windows.ApplicationModel.Store.CurrentAppSimulator) オブジェクトを使う必要があります。 そうすることで、実稼働サーバーを呼び出すのではなく、ライセンス サーバーへのシミュレートされた呼び出しを使って、ライセンス ロジックを検証できます。 これを行うには、% userprofile% \\ AppData \\ ローカル \\ パッケージの \\ &lt; パッケージ名 &gt; \\ localstate \\ Microsoft \\ Windows Store \\ apidata で WindowsStoreProxy.xml という名前のファイルをカスタマイズする必要があります。 このファイルは、アプリを初めて実行するときに Microsoft Visual Studio シミュレーターによって作られます。カスタマイズされたファイルを実行時に読み込むこともできます。 詳しくは、「[CurrentAppSimulator での WindowsStoreProxy.xml ファイルの使用](in-app-purchases-and-trials-using-the-windows-applicationmodel-store-namespace.md#proxy)」をご覧ください。
-   このトピックでは、[ストア サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/win10-1507/Samples/Store)で提供されているコード例も参照します。 このサンプルを利用すると、ユニバーサル Windows プラットフォーム (UWP) アプリに提供されるさまざまな収益化オプションを体験できます。

## <a name="make-the-purchase-request-for-the-in-app-product"></a>アプリ内製品に対する購入要求

大規模なカタログ内の特定の製品に対する購入要求は、他のアプリ内購入要求とほとんど同様に処理されます。 アプリが新しい [RequestProductPurchaseAsync](/uwp/api/windows.applicationmodel.store.currentapp.requestproductpurchaseasync) メソッドのオーバーロードを呼び出すときに、アプリは *OfferId* と、アプリ内製品の名前が設定された [ProductPurchaseDisplayProperties](/uwp/api/windows.applicationmodel.store.productpurchasedisplayproperties) オブジェクトの両方を提供します。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/InAppPurchasesAndLicenses/cs/ManageCatalog.cs" id="MakePurchaseRequest":::

## <a name="report-fulfillment-of-the-in-app-offer"></a>アプリ内販売のフルフィルメントの報告

アプリでは、販売のローカルのフルフィルメントが完了したらすぐに、ストアに製品フルフィルメントを報告する必要があります。 大規模なカタログのシナリオでは、アプリで販売のフルフィルメントを報告しなかった場合、ユーザーは、その同じストアの製品一覧を使ってアプリ内販売を購入できなくなります。

前に説明したように、ストアでは提供された販売情報のみを使って [PurchaseResults](/uwp/api/Windows.ApplicationModel.Store.PurchaseResults) を設定し、大規模なカタログ販売とストアの製品一覧の間に永続的な関連付けは作成しません。 その結果、製品に対するユーザーの権限を追跡し、製品固有のコンテキスト (購入される項目の名前やその詳細など) を [RequestProductPurchaseAsync](/uwp/api/windows.applicationmodel.store.currentapp.requestproductpurchaseasync) 操作の外部でユーザーに提供します。

次のコードは、フルフィルメントの呼び出しと、特定の販売情報が挿入される UI メッセージング パターンを示しています。 この特定の製品情報がない場合、この例では製品の [ListingInformation](/uwp/api/Windows.ApplicationModel.Store.ListingInformation) からの情報を使います。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/InAppPurchasesAndLicenses/cs/ManageCatalog.cs" id="ReportFulfillment":::

## <a name="related-topics"></a>関連トピック

* [アプリ内製品購入の有効化](enable-in-app-product-purchases.md)
* [コンシューマブルなアプリ内製品購入の有効化](enable-consumable-in-app-product-purchases.md)
* [ストア サンプル (試用版とアプリ内購入のデモンストレーション)](https://github.com/Microsoft/Windows-universal-samples/tree/win10-1507/Samples/Store)
* [RequestProductPurchaseAsync](/uwp/api/windows.applicationmodel.store.currentapp.requestproductpurchaseasync)
* [ProductPurchaseDisplayProperties](/uwp/api/Windows.ApplicationModel.Store.ProductPurchaseDisplayProperties)
