---
ms.assetid: bb105fbe-bbbd-4d78-899b-345af2757720
description: アプリをストアに送信する前に、パートナーセンターからアプリにアプリケーション ID と ad ユニット ID の値を追加する方法について説明します。
title: アプリの広告ユニットをセットアップする
ms.date: 02/18/2020
ms.topic: article
keywords: Windows 10, UWP, 広告, Advertising, 広告ユニット, テスト
ms.localizationpriority: medium
ms.openlocfilehash: c7bafdc7d21814a03d6f7da7132d8017d7f238e5
ms.sourcegitcommit: c2e4bbe46c7b37be1390cdf3fa0f56670f9d34e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92253631"
---
# <a name="set-up-ad-units-in-your-app"></a>アプリの広告ユニットをセットアップする

>[!WARNING]
> 2020年6月1日から、Microsoft Ad 収益化 platform for Windows UWP アプリがシャットダウンされます。 [詳細情報](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/db8d44cb-1381-47f7-94d3-c6ded3fea36f/microsoft-ad-monetization-platform-shutting-down-june-1st?forum=aiamgr)

ユニバーサル Windows プラットフォーム (UWP) アプリ内の各広告コントロールには、対応する*広告ユニット*があります。広告ユニットは、コントロールに広告を提供するためにサービスで使用されます。 各広告ユニットは、*広告ユニット ID* と*アプリケーション ID* があり、これらをアプリ内でコードに割り当てる必要があります。

テスト中にテスト広告がアプリに表示されていることを確認するために使用できる[テスト広告ユニット値](#test-ad-units)が用意されています。 これらのテスト値は、テスト バージョンのアプリでのみ使用できます。 いったん公開したアプリでテスト用の値を使うと、ライブ アプリで広告は表示されません。

UWP アプリのテストを完了し、パートナーセンターに送信する準備ができたら、パートナーセンターの [[アプリ内広告](../publish/in-app-ads.md)] ページから[ライブ ad ユニットを作成](#live-ad-units)し、この AD ユニットのアプリケーション ID と ad ユニット ID の値を使用するようにアプリコードを更新する必要があります。

アプリケーション ID と広告ユニット ID の値をアプリのコードに割り当てる方法の詳細については、次の記事を参照してください。
* [XAML および .NET の AdControl](adcontrol-in-xaml-and--net.md)
* [HTML 5 および Javascript での AdControl](adcontrol-in-html-5-and-javascript.md)
* [スポット広告](../monetize/interstitial-ads.md)
* [ネイティブ広告](../monetize/native-ads.md)

<span id="test-ad-units" />

## <a name="test-ad-units"></a>広告ユニットをテストする

アプリを開発しているときには、このセクションに示されているテスト用のアプリケーション ID と広告ユニット ID の値を使って、テスト時にアプリでどのように広告がレンダリングされるかを確認します。

### <a name="banner-ads-using-the-adcontrol-class"></a>バナー広告 (AdControl クラスを使用)

* Ad ユニット ID: ```test```
* アプリケーション ID:  ```3f83fe91-d6be-434d-a0ae-7351c5a997f1```

    > [!IMPORTANT]
    > **AdControl** では、ライブ広告のサイズは **Width** プロパティと **Height** プロパティによって定義されます。 最善の結果を得るには、コード内の **Width** プロパティと **Height** プロパティが、[バナー広告でサポートされている広告サイズ](supported-ad-sizes-for-banner-ads.md)のいずれかであることを確認します。 **Width** プロパティと **Height** プロパティは、ライブ広告のサイズに基づいて変更されません。

### <a name="interstitial-ads-and-native-ads"></a>スポット広告やネイティブ広告

* Ad ユニット ID: ```test```
* アプリケーション ID:  ```d25517cb-12d4-4699-8bdc-52040c712cab```

<span id="live-ad-units" />

## <a name="live-ad-units"></a>ライブ広告ユニット

パートナーセンターからライブ ad ユニットを取得し、アプリで使用するには、次のようにします。

1.  パートナーセンターの**アプリ内広告**ページで[広告ユニットを作成](../publish/in-app-ads.md#create-ad-unit)します。 アプリで使用している広告コントロールに合わせて、適切な種類の広告ユニットを指定してください。
    > [!NOTE]
    > 必要に応じて、[[仲介設定]](../publish/in-app-ads.md#mediation) セクションで設定を構成することで、広告ユニットの広告仲介を有効にできます。 広告仲介を使うと、複数の広告ネットワークから広告を表示して、広告収益とアプリ プロモーションの機能を最大限に引き出すことができます。表示される広告には、他の有料広告ネットワークからの広告や、Microsoft のアプリ プロモーション キャンペーン用の広告などが含まれます。 既定では、アプリがサポートする市場全体で広告の収益を最大化できるように、機械学習アルゴリズムを使った仲介設定が自動的に構成されますが、必要に応じて仲介設定を手動で構成することができます。

2.  新しい広告ユニットを作成したら、**[収益化]** &gt; **[アプリ内広告]** ページにある利用可能な広告ユニットの表で、作成した広告ユニットの**アプリケーション ID** と**広告ユニット ID** を取得します。
    > [!NOTE]
    > テスト広告ユニットとライブ UWP 広告ユニットでは、アプリケーション ID の値の形式が異なります。 テスト アプリケーション ID の値は GUID です。 パートナーセンターでライブ UWP ad ユニットを作成すると、ad ユニットの [アプリケーション ID] の値は、常にアプリのストア ID と一致します (たとえば、ストア ID 値は9NBLGGH4R315 のようになります)。

3.  アプリのコードで、アプリケーション ID と広告ユニット ID の値を割り当てます。 詳細については、以下の記事を参照してください。
    * [XAML および .NET の AdControl](adcontrol-in-xaml-and--net.md)
    * [HTML 5 および Javascript での AdControl](adcontrol-in-html-5-and-javascript.md)
    * [スポット広告](../monetize/interstitial-ads.md)
    * [ネイティブ広告](../monetize/native-ads.md)

<span id="manage" />

## <a name="manage-ad-units-for-multiple-ad-controls-in-your-app"></a>アプリで複数の広告コントロールの広告ユニットを管理する

1 つのアプリに複数のバナー広告コントロール、スポット広告コントロール、ネイティブ広告コントロールを使用できます。 このシナリオでは、各コントロールに異なる広告ユニットを割り当てることをお勧めします。 各コントロールに異なる広告ユニットを使用することで、別々に[仲介の設定を構成](../publish/in-app-ads.md#mediation)して、個別の[報告データ](../publish/advertising-performance-report.md)を取得することが可能です。 また、これにより、Microsoft のサービスはアプリに提供する広告を最適化できます。

> [!IMPORTANT]
> 各広告ユニットは 1 つのアプリのみで使用できます。 同じ広告ユニットを複数のアプリで使うと、その広告ユニットには広告が配信されません。

## <a name="related-topics"></a>関連トピック

* [XAML および .NET の AdControl](adcontrol-in-xaml-and--net.md)
* [HTML 5 および Javascript での AdControl](adcontrol-in-html-5-and-javascript.md)
* [スポット広告](interstitial-ads.md)
* [ネイティブ広告](native-ads.md)


 

 
