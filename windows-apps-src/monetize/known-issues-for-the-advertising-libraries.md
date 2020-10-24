---
ms.assetid: 9ca1f880-2ced-46b4-8ea7-aba43d2ff863
description: Microsoft Advertising SDK の現在のリリースにおける既知の問題について説明します。
title: アプリ内広告の既知の問題とトラブルシューティング
ms.date: 02/18/2020
ms.topic: article
keywords: Windows 10, UWP, 広告, Advertising, 既知の問題, トラブルシューティング
ms.localizationpriority: medium
ms.openlocfilehash: c69c61cc1db0796edbaedb2f8e2970e1100c5774
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89158536"
---
# <a name="known-issues-and-troubleshooting-for-ads-in-apps"></a>アプリ内広告の既知の問題とトラブルシューティング

>[!WARNING]
> 2020年6月1日から、Microsoft Ad 収益化 platform for Windows UWP アプリがシャットダウンされます。 [詳細を表示](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/db8d44cb-1381-47f7-94d3-c6ded3fea36f/microsoft-ad-monetization-platform-shutting-down-june-1st?forum=aiamgr)

このトピックでは、Microsoft Advertising SDK の現在のリリースにおける既知の問題を示します。 トラブルシューティングのガイダンスについては、以下のトピックを参照してください。

* [HTML と JavaScript のトラブルシューティング ガイド](html-and-javascript-troubleshooting-guide.md)
* [XAML と C# のトラブルシューティング ガイド](xaml-and-c-troubleshooting-guide.md)

## <a name="adcontrol-interface-unknown-in-xaml"></a>XAML での不明な AdControl インターフェイス

[AdControl](/uwp/api/microsoft.advertising.winrt.ui.adcontrol) の XAML マークアップに、そのインターフェイスが不明であることを示す青い破線が表示される場合があります。 これは、x86 をターゲットとして設定している場合にのみ発生するもので、無視してかまいません。

## <a name="lasterror-from-previous-ad-request"></a>以前の広告要求からの lastError

以前の広告要求の **lastError** が残っている場合、次の広告呼び出し中にこのイベントが 2 回を発生する可能性があります。 その一方で新しい広告要求が行われ、有効な広告が生成されると、この動作によって混乱が生じる可能性があります。

## <a name="interstitial-ads-and-navigation-buttons-on-phones"></a>スポット広告と電話のナビゲーション ボタン

ハードウェア ボタンの代わりにソフトウェア ボタンの **"戻る"**、**"スタート"**、**"検索"** を備えた電話 (またはエミュレーター) では、スポット広告用のカウントダウン タイマー ボタンとクリックスルー ボタンが隠れる場合があります。

## <a name="recently-created-ads-are-not-being-served-to-your-app"></a>最近作成した広告がアプリに提供されない

その広告が最近 (1 日以内) 作成された広告の場合は、すぐに利用可能にならない場合があります。 編集コンテンツに関する承認が済んでいる場合、広告は、広告サーバーによって処理され、インベントリとして利用可能になった時点で提供されるようになります。

## <a name="no-ads-are-shown-in-your-app"></a>アプリに広告が表示されない

広告が表示されない場合、ネットワーク エラーを含むさまざまな理由があります。 次の理由も考えられます。

* アプリのコード内の **Adcontrol** のサイズより大きいか小さいサイズのパートナーセンターの広告ユニットを選択します。

* 広告ユニット ID に[テスト モードの値](set-up-ad-units-in-your-app.md#test-ad-units)を使ってライブ アプリを実行した場合、広告は表示されません。

* 新しい広告ユニット ID の作成を行ったのがこの 30 分以内の場合、サーバーによってシステムに新しいデータが伝達されるまで、広告は表示されません。 広告が表示されていた既存の ID を使用すると、広告はすぐに表示されます。

アプリにテスト広告が表示される場合は、コードが正常に動作していて広告を表示できることを示します。 問題が発生した場合は、[製品サポート](https://developer.microsoft.com/windows/support)にお問い合わせください。 このページで、[ **お問い合わせ**] を選択します。

[フォーラム](https://social.msdn.microsoft.com/forums/windowsapps/en-US/home?category=windowsapps)に質問を投稿することもできます。

## <a name="test-ads-are-showing-in-your-app-instead-of-live-ads"></a>ライブ広告ではなくテスト広告がアプリに表示される

ライブ広告が想定されているときでもテスト広告が表示される場合があります。 これは、次の状況で発生することがあります。

* ストアで使用されているライブ アプリケーション ID を広告プラットフォームが確認または検出できない。 この場合、広告ユニットがユーザーによって作成されたとき、その状態は "ライブ" (非テスト) として開始されますが、最初の広告要求が行われてから 6 時間以内にテスト状態に移行します。 その状態は、10 日間テスト アプリからの要求がない場合に "ライブ" に戻ります。

* サイドローディングされたアプリやエミュレーターで実行されているアプリには、ライブ広告は表示されません。

ライブ ad ユニットがテスト広告にサービスを提供している場合、ad ユニットの状態は [アクティブ] と表示され、パートナーセンターの **テスト広告を提供** します。 現時点で、これは、電話アプリには適用されません。


<span id="reference_errors"/>

## <a name="reference-errors-caused-by-targeting-any-cpu-in-your-project"></a>プロジェクトのターゲットを "任意の CPU" に設定すると参照エラーが発生する

Microsoft Advertising SDK を使う場合、プロジェクトで**任意の CPU** をターゲットにすることはできません。 プロジェクトのターゲットを **Any CPU** プラットフォームに設定した場合、次のような参照を追加した後で警告が表示される場合があります。

![referenceerror \- solutionexplorer](images/13-19629921-023c-42ec-b8f5-bc0b63d5a191.jpg)

この警告を解決するには、アーキテクチャ固有のビルド出力 (たとえば、**x86**) を使用するようにプロジェクトを更新します。 デバッグおよびリリース用の構成のプラットフォームのターゲットを設定するには、**Configuration Manager** を使用します。

![configurationmanagerwin10](images/13-87074274-c10d-4dbd-9a06-453b7184f8de.png)

(次の図に示すように) ストアに申請するアプリ パッケージを作成するときは、ターゲットのアーキテクチャを必ず指定してください。 x64 OS で x86 ビルドを実行する場合は、x64 をスキップしてもかまいません。

![projectstorecreateapppackages](images/13-a99b05a4-8917-4c53-822e-2548fadf828a.png)

![createapppackages](images/13-16280cb1-a838-42b9-9256-eac7f33f5603.png)

## <a name="z-order-in-javascripthtml-apps"></a>JavaScript/HTML アプリでの Z オーダー

JavaScript/HTML アプリでは、z オーダーの予約済みの MAX-10 の範囲に要素を配置しないでください。 この唯一の例外として、Skype アプリの着信通知などの割り込みオーバーレイがあります。

<span id="bkmk-ui"/>

## <a name="do-not-use-borders"></a>境界線を使わない

**AdControl** によってその親クラスから継承される境界線に関連するプロパティを設定すると、広告の配置に関して問題が発生します。

## <a name="more-information"></a>詳細情報

最新の既知の問題についての詳細を調べたり、Microsoft Advertising SDK に関連する質問を投稿したりするには、[フォーラム](https://social.msdn.microsoft.com/forums/windowsapps/en-US/home?category=windowsapps)をご利用ください。

 

 