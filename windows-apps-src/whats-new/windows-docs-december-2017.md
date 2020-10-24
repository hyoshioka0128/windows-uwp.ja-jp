---
title: Windows ドキュメントの最新情報、2017 年 12 月 - UWP アプリの開発
description: 2017 年 12 月版の Windows 10 開発者向けドキュメントには、新しい機能、ビデオ、開発者向けガイダンスが追加されました
keywords: 最新情報, 更新, 機能, 開発者向けガイダンス, Windows 10, 12 月
ms.date: 12/14/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 8d58fe1662c5ba13c2952fbd96414ab201f5ba27
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89174386"
---
# <a name="whats-new-in-the-windows-developer-docs-in-december-2017"></a>Windows 開発者向けドキュメントの最新情報、2017 年 12 月

Windows 開発者向けドキュメントは、Windows プラットフォームで開発者に提供される新機能の情報を反映して継続的に更新されています。 ここに示す機能概要、開発者向けガイダンス、サンプルは Fall Creators Update のリリース後に公開されたもので、Windows 開発者向けの新しい情報や更新情報を含んでいます。

Windows 10 の[ツールと SDK をインストール](https://developer.microsoft.com/windows/downloads#_blank)すると、[新しいユニバーサル Windows アプリを作成](../get-started/create-uwp-apps.md)したり、[Windows の既存のアプリ コード](../porting/index.md)がどのように使えるかを試したりすることができます。

## <a name="features"></a>機能

### <a name="windows-mixed-reality-enthusiasts-guide"></a>Windows Mixed Reality: 技術者向けガイド

Mixed Reality の世界に入ろうとしている技術者を対象とした[技術者向けガイド](/windows/mixed-reality/enthusiast-guide/)では、Windows Mixed Reality に関してよくある質問の回答を示しています。 

このガイドの内容は次のとおりです。 
- 購入前の FAQ 
- PC の互換性を確認する方法 
- セットアップ手順 
- ヘッドセットとコントローラーを使う方法 
- イマーシブ ゲーム、360°動画、2D アプリ、WebVR、SteamVR をダウンロードしてプレイする方法 
- 問題のトラブルシューティング方法など

![Windows Mixed Reality ヘッドセット ユーザーとモーション コントローラー](images/BeforeYouBegin-tile.jpg)

### <a name="keyboard-interactions"></a>キーボード操作

更新された[キーボード操作](../design/input/keyboard-interactions.md)によって、アクセシビリティ対応エクスペリエンスとパワー ユーザー向け機能の両方が提供される UWP アプリを設計し、最適化できます。 Fall Creators Update で追加されたこれらの操作に対する新しい機能強化が反映されるように、推奨事項とガイダンスが更新されました。

アプリのキーボード機能を拡張するには、「[キーボード アクセラレータ](../design/input/keyboard-accelerators.md)」と、[カスタムのキーボード操作](../design/input/focus-navigation.md)に関するページをご覧ください。

タッチ操作をサポートするデバイスで、「[タッチ キーボードの表示への応答](../design/input/respond-to-the-presence-of-the-touch-keyboard.md)」と「[入力値の種類を使ったタッチ キーボードの変更](../design/input/use-input-scope-to-change-the-touch-keyboard.md)」を使ってキーボード機能を追加します。

### <a name="microsoft-collaborate"></a>Microsoft Collaborate

Microsoft Collaborate ポータルには、エンジニアリング システムの作業項目 (バグ、機能に関するご要望など) の共有とコンテンツ (ビルド、ドキュメント、仕様) の配布を可能にすることで、Microsoft エコシステム内でのエンジニアリング コラボレーションを簡素化するツールとサービスが用意されています。 [詳しくはこちらをご覧ください](/collaborate/)。

![パートナー センターでの Microsoft Collaborate](images/microsoft_collaborate_screenshot.PNG)

### <a name="package-desktop-applications-with-uwp-projects"></a>UWP プロジェクトを使ってデスクトップ アプリケーションをパッケージ化する

Visual Studio 2017 バージョン 15.5 では、**Windows アプリケーション パッケージ プロジェクト** テンプレートが更新されており、UWP プロジェクトがかなり追加しやすくなっています。 JavaScript ベースのパッケージ プロジェクトを使い、パッケージ マニフェストを手動で調整する必要がなくなりました。  

この新しいテンプレートを使ってデスクトップ アプリケーションをパッケージ化する方法については、[Visual Studio を使ったアプリのパッケージ化](/windows/msix/desktop/desktop-to-uwp-packaging-dot-net)に関するページをご覧ください。

UWP プロジェクトをパッケージに追加する方法については、[最新の UWP コンポーネントによるデスクトップ アプリケーションの拡張](/windows/apps/desktop/modernize/desktop-to-uwp-extend)に関するページをご覧ください。

### <a name="subscription-add-ons-are-now-available-to-developers-in-the-windows-dev-center-insider-program"></a>サブスクリプション アドオンを Windows デベロッパー センター Insider program の開発者が利用できるようになりました

デベロッパー センター Insider プログラムに参加しているすべての開発者は、サブスクリプション アドオンを使うことにより、定期的な自動の課金期間を設定してアプリ内でデジタル製品 (アプリの機能やデジタル コンテンツなど) を販売できるようになりました。 詳しくは、「[アプリのサブスクリプション アドオンの有効化](../monetize/enable-subscription-add-ons-for-your-app.md)」をご覧ください。

## <a name="developer-guidance"></a>開発者ガイド

### <a name="color"></a>色

最良のユーザー エクスペリエンスを実現するため、アプリで色を使う方法に関する新しいガイダンスが追加されました。 これには、API の使用シナリオに加えて、UI デザインとアクセシビリティに関する一般的なガイダンスが含まれます。 また、Xbox で利用できるユーザー アクセント カラーの一覧も更新されました。 [更新された「色」の記事をこちらからご覧ください。](../design/style/color.md)

![ユニバーサル windows カラー パレット](../design/basics/images/colors.png)

### <a name="data-access-guides"></a>データ アクセス ガイド

アプリが SQL Server データベースに直接アクセスする方法を示す、[SQL Server ガイド](../data-access/sql-server-databases.md)が追加されました。 必要なサービス レイヤーはありません。

さらに、[SQLite ガイド](../data-access/sqlite-databases.md)がまったく新しくなり、よりすっきりとした外観になりました。また、ユーザー デバイスの軽量なデータベースにデータを保存して取得するための最新のベスト プラクティスが追加されました。

### <a name="forms"></a>フォーム

ユーザーからデータを収集して送信するための[フォームをアプリに作成する方法](../design/controls-and-patterns/forms.md)に関する新しい記事が追加されました。 これには、フォームの実装に関する具体的な情報と、フォームを使うタイミングと場所に関する一般的なガイダンスが含まれます。

### <a name="intro-to-app-design"></a>アプリ設計の概要

ユニバーサル Windows プラットフォーム (UWP) の設計ガイダンスは、美しく洗練されたアプリを設計および構築するのに役立つリソースです。 [新しい手順](../design/basics/design-and-ui-intro.md)では、あらゆる UWP アプリに含まれているユニバーサル デザイン機能の概要と、ドキュメントを使ってさまざまなデバイス間で美しくスケーリングされるユーザー インターフェイス (UI) を構築する方法について説明します。


### <a name="request-ratings-and-reviews"></a>評価とレビューを求める

[アプリの評価とレビューを求める](../monetize/request-ratings-and-reviews.md)方法について説明する新しい記事が追加されました。 アプリのコンテキストで評価とレビュー ダイアログを表示したり、Store でアプリの評価とレビュー ページを開いたりすることができます。

## <a name="samples"></a>サンプル

### <a name="customer-orders"></a>顧客の注文

[顧客注文データベース](https://github.com/Microsoft/Windows-appsample-customers-orders-database) サンプルが更新され、リポジトリ パターンの使用や複数のデータ ソース (Sqlite、SQL Azure、REST サービスなど) に接続する方法のような、データ アクセスに関するベスト プラクティスが示されるようになりました。

## <a name="videos"></a>ビデオ

### <a name="package-a-net-app-in-visual-studio"></a>Visual Studio で .NET アプリをパッケージ化する

デスクトップ アプリをこれまで以上に簡単にユニバーサル Windows プラットフォームに移行できます。 [ビデオ](https://www.youtube.com/watch?v=fJkbYPyd08w)で、配布用の .NET アプリをパッケージ化する方法をご覧ください。その後、[このページで詳細情報を確認](/windows/msix/desktop/desktop-to-uwp-packaging-dot-net)してください。