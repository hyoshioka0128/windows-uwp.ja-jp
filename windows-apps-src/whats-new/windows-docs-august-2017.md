---
title: Windows ドキュメントの最新情報、2017 年 8 月 - UWP アプリの開発
description: 2017 年 8 月版の Windows 10 開発者向けドキュメントには、新しい機能、ビデオ、開発者向けガイダンスが追加されました
keywords: 最新情報, 更新, 機能, 開発者向けガイダンス, Windows 10, 1708
ms.date: 08/03/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: cbaf2726e8f3e517fd0664c3d00b9a82ca018fbc
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89174416"
---
# <a name="whats-new-in-the-windows-developer-docs-in-august-2017"></a>Windows 開発者向けドキュメントの最新情報、2017 年 8 月

Windows 開発者向けドキュメントは、Windows プラットフォームで開発者に提供される新機能の情報を反映して継続的に更新されています。 ここに示す機能概要、開発者向けガイダンス、ビデオは最近公開されたもので、Windows 開発者向けの新しい情報や更新情報を含んでいます。

Windows 10 の[ツールと SDK をインストール](https://developer.microsoft.com/windows/downloads#_blank)すると、[新しいユニバーサル Windows アプリを作成](../get-started/your-first-app.md)したり、[Windows の既存のアプリ コード](../porting/index.md)がどのように使えるかを試したりすることができます。

## <a name="features"></a>機能

### <a name="windows-template-studio"></a>Windows Template Studio

Visual Studio 2019 用の新しい [Windows Template Studio](https://marketplace.visualstudio.com/items?itemName=WASTeamAccount.WindowsTemplateStudio) 拡張機能を使うと、必要なページ、フレームワーク、機能が組み込まれた UWP アプリをすばやく作成できます。 このウィザード ベースのエクスペリエンスには、実証済みのパターンとベスト プラクティスが実装されています。これにより、アプリに機能を追加するときにかかる時間を短縮し、よくある問題を避けることができます。

![Windows Template Studio](images/template-studio.png)

### <a name="conditional-xaml"></a>条件付き XAML

[バージョン アダプティブ アプリ](../debug-test-perf/version-adaptive-apps.md)の作成を可能にする[条件付き XAML](../debug-test-perf/conditional-xaml.md) をプレビューできるようになりました。 条件付き XAML では、XAML マークアップで ApiInformation.IsApiContractPresent メソッドを使用できるため、分離コードを使わなくても、API の有無に基づいてマークアップでプロパティの設定やオブジェクトのインスタンス化を行うことができます。

### <a name="game-mode"></a>ゲーム モード

ユニバーサル Windows プラットフォーム (UWP) 用の[ゲーム モード](/previous-versions/windows/desktop/gamemode/game-mode-portal) API では、Windows 10 のゲーム モードを利用することで最適化されたゲーム エクスペリエンスを実現できます。 これらの API は **&lt;expandedresources.h&gt;** ヘッダーに含まれています。

![ゲーム モード](images/game-mode.png)

### <a name="submission-api-supports-video-trailers-and-gaming-options"></a>申請 API でのビデオ トレーラーとゲーム オプションのサポート

[Microsoft Store 申請 API](../monetize/create-and-manage-submissions-using-windows-store-services.md) で、アプリの申請に[ビデオ トレーラー](../monetize/manage-app-submissions.md#trailer-object)や[ゲーム オプション](../monetize/manage-app-submissions.md#gaming-options-object)を含めることができるようになりました。


## <a name="developer-guidance"></a>開発者ガイド

### <a name="data-schemas-for-store-products"></a>Store 製品のデータ スキーマ

記事「[ストア製品のデータ スキーマ](../monetize/data-schemas-for-store-products.md)」が追加されました。 この記事では、[StoreProduct](/uwp/api/windows.services.store.storeproduct) や [StoreAppLicense](/uwp/api/windows.services.store.storeapplicense) など、[Windows.Services.Store](/uwp/api/windows.services.store) 名前空間のいくつかのオブジェクトで利用できるストア関連のデータ用のスキーマを示します。

### <a name="desktop-bridge"></a>デスクトップ ブリッジ

Windows 10 ユーザーの利便性を高める最新のエクスペリエンスを実装するために役立つ 2 つのガイドが追加されました。

「[Windows 10 向けのデスクトップ アプリを強化する](/windows/apps/desktop/modernize/desktop-to-uwp-enhance)」では、適切なファイルを見つけて参照し、Windows 10 ユーザーの UWP エクスペリエンスを向上させるコードを記述する方法について説明します。  

「[最新の UWP コンポーネントによるデスクトップ アプリケーションの拡張](/windows/apps/desktop/modernize/desktop-to-uwp-extend)」では、UWP アプリ コンテナーで実行される最新の XAML UI やその他の UWP エクスペリエンスを組み込む方法について説明します。

### <a name="getting-started-with-point-of-service"></a>POS (店舗販売時点管理) の概要

[POS (店舗販売時点管理) サービス](../devices-sensors/pos-get-started.md)を利用する場合に役立つ新しいガイドが追加されました。 このガイドでは、デバイスの列挙、デバイス機能の確認、デバイスの要求、デバイスの共有といったトピックについて説明します。 

### <a name="xbox-live"></a>Xbox Live

Xbox Live 開発者向けに、UWP ゲームと Xbox 開発キット (XDK) のゲームの両方に関するドキュメントが追加されました。

「[Xbox Live 開発者向けガイド](//gaming/xbox-live/index)」では、Xbox Live API を使ってゲームを Xbox Live ソーシャル ゲーミング ネットワークに接続する方法について説明します。

[Xbox Live クリエーターズ プログラム](//gaming/xbox-live/get-started-with-creators/get-started-with-xbox-live-creators)を利用すると、UWP ゲーム開発者はだれでも、PC と Xbox One の両方で Xbox Live 対応ゲームを開発して公開できます。

Xbox Live 開発者向けに提供されているプログラムと機能については、「[Xbox Live 開発者プログラムの概要](//gaming/xbox-live/developer-program-overview)」をご覧ください。

## <a name="videos"></a>ビデオ

### <a name="mixed-reality"></a>Mixed Reality

[Microsoft HoloLens Course 250](https://developer.microsoft.com/windows/mixed-reality/mixed_reality_250) 向けに一連のチュートリアル ビデオが公開されました。 既にツールをインストールしていて、Mixed Reality の開発の基本を理解している場合は、これらのビデオ コースをチェックして、Mixed Reality デバイス間で共通のエクスペリエンスを作成する方法をご覧ください。

### <a name="narrator-and-dev-mode"></a>ナレーターと開発者モード

[ナレーター](https://support.microsoft.com/help/22798/windows-10-complete-guide-to-narrator)を使うと、アプリの読み上げをテストできます。 ナレーターには開発者モードもあり、このモードでは、ナレーターに公開されている情報が視覚的にわかりやすく表示されます。 [ビデオ](https://channel9.msdn.com/Blogs/One-Dev-Minute/Using-Narrator-and-Dev-Mode)をご覧になってから、[ナレーター開発者モード](https://channel9.msdn.com/Blogs/One-Dev-Minute/Using-Narrator-and-Dev-Mode)の詳細を確認してください。

### <a name="windows-template-studio"></a>Windows Template Studio

[このビデオ](https://channel9.msdn.com/Blogs/One-Dev-Minute/Getting-Started-with-Windows-Template-Studio)では、Windows Template Studio の概要について詳しく紹介しています。 準備ができたら、[拡張機能をインストール](https://marketplace.visualstudio.com/items?itemName=WASTeamAccount.WindowsTemplateStudio)することも、[ソース コードとドキュメントを確認](https://marketplace.visualstudio.com/items?itemName=WASTeamAccount.WindowsTemplateStudio)することもできます。