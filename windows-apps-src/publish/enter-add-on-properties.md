---
description: アドオンを提出するとき、[プロパティ] ページのオプションは、ユーザーに提供される場合のアドオン動作を決めるのに役立ちます。
title: アドオン プロパティの入力
ms.assetid: 26D2139F-66FD-479E-940B-7491238ADCAE
ms.date: 10/31/2018
ms.topic: article
keywords: windows 10, uwp, アドオン, プロパティ, サブスクリプション期間, 製品の有効期間, コンテンツの種類, iap, アプリ内購入, アプリ内製品
ms.localizationpriority: medium
ms.openlocfilehash: d9e43529d9a54cc014e1a9596e766de9ebe89d00
ms.sourcegitcommit: a3bbd3dd13be5d2f8a2793717adf4276840ee17d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93030505"
---
# <a name="enter-add-on-properties"></a>アドオン プロパティの入力

アドオンを提出するとき、 **[プロパティ]** ページのオプションは、ユーザーに提供される場合のアドオン動作を決めるのに役立ちます。

## <a name="product-type"></a>製品の種類

最初に[アドオンを作成する](set-your-add-on-product-id.md)ときに、製品の種類を選びます。 ここには、選んだ製品の種類が表示されますが、変更することはできません。

> [!TIP]
> アドオンを公開しておらず、別の製品の種類を選ぶ必要がある場合は、申請を削除して、もう一度選ぶことができます。

このページに表示されるフィールドは、アドオンの製品の種類に応じて変化します。


## <a name="product-lifetime"></a>製品の有効期限

製品の種類として **[永続的]** を選んだ場合、 **[製品の有効期限]** がここに表示されます。 永続的なアドオンの **[製品の有効期限]** の既定値は、 **[無期限]** です。つまり、アドオンの期限は切れません。 必要に応じて、設定した期間の後にアドオンが期限切れになるように **製品の有効期間** を変更することができます (オプションは1-365 日)。


## <a name="quantity"></a>Quantity

製品の種類に **[ストアで管理されるコンシューマブル]** を選択した場合、 **[数量]** がここに表示されます。 1 ~ 1000000 の範囲の数値を入力する必要があります。 顧客が対象アドオンを入手するときにこの数量が付与されます。顧客によるアドオンの消費がアプリによって報告されるたびに、ストアが残量を追跡します。


## <a name="subscription-period"></a>サブスクリプション期間

製品の種類として **[サブスクリプション]** を選んだ場合、 **[サブスクリプション期間]** がここに表示されます。 サブスクリプション料を課金する頻度を指定するオプションを選びす。 既定のオプションは **月単位** ですが、 **3 か月** 、 **6 か月** 、 **1 年、** または **24 か月** を選択することもできます。

> [!IMPORTANT]
> アドオンが公開されると、 **[サブスクリプション期間]** の指定は変更できません。


## <a name="free-trial"></a>無料試用版

製品の種類として **[サブスクリプション]** を選んだ場合、 **[無料試用版]** もここに表示されます。 既定のオプションは **[無料の試用版なし]** です。 必要に応じて、一定の期間アドオンを無料でユーザーが使えるようにすることもできます ( **[1 週間]** または **[1 か月]** )。 

> [!IMPORTANT]
> アドオンが公開されると、 **[無料試用版]** の指定は変更できません。


## <a name="content-type"></a>Content type

アドオンの製品の種類に関係なく、提供するコンテンツの種類を指定する必要があります。 ほとんどのアドオンでは、コンテンツの種類は **[ソフトウェアのダウンロード]** になります。 一覧の別のオプションがアドオンの説明としてより適している場合 (たとえば、音楽のダウンロードや電子書籍を提供している場合) は、代わりにそのオプションを選びます。

アドオンのコンテンツの種類として利用可能なオプションを次に示します。

-   ソフトウェアのダウンロード
-   電子書籍
-   電子雑誌 1 冊
-   電子新聞 1 部
-   ミュージックのダウンロード
-   ミュージックのストリーミング
-   オンライン データ ストレージ/サービス
-   サービスとしてのソフトウェア
-   ビデオのダウンロード
-   ビデオのストリーミング


## <a name="additional-properties"></a>追加のプロパティ

これらのフィールドは、どのアドオンの種類でも省略可能です。

<span id="keywords" />

### <a name="keywords"></a>Keywords

提出するアドオンごとに、それぞれ 30 文字以内のキーワードを最大 10 個指定するオプションがあります。 そうすると、アプリはキーワードと一致するアドオンを照会できます。 この機能を利用すると、アプリのコードで製品 ID を直接指定しなくても、アドオンを読み込むことができる画面をアプリで構築できるようになります。 その場合、アプリでコードを変更したり、アプリをもう一度提出したりしなくても、いつでもアドオンのキーワードを変更することができます。

このフィールドを照会するには、[Windows.Services.Store 名前空間](/uwp/api/Windows.Services.Store)の [StoreProduct.Keywords](/uwp/api/windows.services.store.storeproduct.Keywords) プロパティを使用します  (または、[Windows.ApplicationModel.Store 名前空間](/uwp/api/Windows.ApplicationModel.Store)を使用している場合は、[ProductListing.Keywords](/uwp/api/windows.applicationmodel.store.productlisting.Keywords) プロパティを使用します)。

> [!NOTE]
> キーワードは、Windows 8 と Windows 8.1 を対象とするパッケージでは使うことができません。

<span id="custom-developer-data" />

### <a name="custom-developer-data"></a>カスタムの開発者データ

**[カスタムの開発者データ]** フィールド (以前は **タグ** と呼ばれていました) に最大 3,000 文字を入力して、アプリ内製品について追加のコンテキストを指定できます。 通常、これは XML 文字列の形式ですが、このフィールドには任意の内容を入力できます。 これで、アプリはこのフィールドを照会して内容を読み取ることができます (ただし、アプリからデータを編集したり、変更を書き戻したりすることはできません)。

たとえば、ゲームのアドオンとして、ユーザーが上のレベルにアクセスできるようになる金貨入りの袋を販売するとします。 **[カスタムの開発者データ]** フィールドを使うと、このアドオンをユーザーが所有している場合、どのレベルを利用できるかをアプリから照会できます。 値 (ここでは、設定されているレベル) は、アプリのコードを変更したり、アプリをもう一度提出したりしなくても、アドオンの **[カスタムの開発者データ]** フィールドで情報を更新し、アドオンの更新された申請を公開することでいつでも調整できます。

このフィールドを照会するには、[Windows.Services.Store 名前空間](/uwp/api/Windows.Services.Store)の [StoreSku.CustomDeveloperData](/uwp/api/windows.services.store.storesku.customdeveloperdata#Windows_Services_Store_StoreSku_CustomDeveloperData) プロパティを使用します  (または、[Windows.ApplicationModel.Store 名前空間](/uwp/api/Windows.ApplicationModel.Store)を使用している場合は、[ProductListing.Tag](/uwp/api/windows.applicationmodel.store.productlisting.tag#Windows_ApplicationModel_Store_ProductListing_Tag) プロパティを使用します)。

> [!NOTE]
> **[カスタムの開発者データ]** フィールドは、Windows 8 と Windows 8.1 を対象とするパッケージでは使うことができません。

 

 

 
