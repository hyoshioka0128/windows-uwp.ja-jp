---
title: Xbox One の UWP
description: Xbox One でユニバーサル Windows プラットフォーム (UWP) アプリを構築する方法。
ms.date: 10/25/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 2d935f53-84db-4108-86dc-cb6a0749782f
ms.localizationpriority: medium
ms.openlocfilehash: 1fe3e4e23bc2be46d3ddb09d9ebf83b5fda5ce9d
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173716"
---
# <a name="uwp-on-xbox-one"></a>Xbox One の UWP

Xbox One でユニバーサル Windows プラットフォーム (UWP) 向けのアプリの構築を始めましょう。

Xbox One の UWP は、アプリとゲーム両方の開発をサポートします。 Xbox でゲームやアプリを実験、作成、テストするために、開発者プログラムに参加する必要はありません。 必要となるのは、[パートナー センター](https://partner.microsoft.com/dashboard)の[開発者アカウント](https://developer.microsoft.com/store/register)だけです。 ただし、Xbox One でゲームを公開して販売する場合や、Windows 10 で Xbox Live を利用する場合は、[Xbox Live クリエーターズ プログラム](https://developer.microsoft.com/games/xbox/xboxlive/creator)に参加するか、[ID@Xbox](https://www.xbox.com/Developers/id) の開発者になる必要があります。 ID@Xbox の開発者になる場合は、開発者アカウントを登録する前に、プログラムへの参加申し込みを行うことをお勧めします。 詳細については、「[開発者プログラムの概要](/gaming/xbox-live/developer-program-overview)」を参照してください。

このセクションでは、設定方法、承認手順のガイド、必要なバージョンの Visual Studio と Windows 10 ツールのインストールに関する情報と、簡単なアプリケーションを初めて構築、実行、デバッグする手順を説明します。 

| トピック      | 説明 |
|------------|-------------|
|[作業の開始](getting-started.md)| Xbox One での UWP の開発の概要を説明します。 |
|[新機能](whats-new.md)| Xbox One の UWP の新機能について説明します。 |
|[Xbox One 開発者モードのアクティブ化](devkit-activation.md)| Xbox One で開発者モードを有効にする方法について説明します。 |
|[Xbox One で開発者モードを無効にする](devkit-deactivation.md)| Xbox One で開発者モードを無効にする方法について説明します。 |
|[Xbox の開発環境に UWP を設定する](development-environment-setup.md)| Xbox One の開発環境を設定してテストする手順について説明します。 |
|[サンプル](samples.md)| GitHub の場所 (TVHelpers) へのポインターです。TVHelpers には Xbox の開発を始めるのに役立つ、XAML と JavaScript のサンプルが掲載されています。 サンプルには、XAML メディア アプリの完全なテンプレート、自動コントローラー ナビゲーション、リッチ メディアの再生、Web ベース テクノロジの検索などが含まれています。 |
|[既知の問題](known-issues.md)| Xbox One の UWP の既知の問題について説明します。 |
|[FAQ](frequently-asked-questions.md)| Xbox One の UWP に関してよく寄せられる質問です。 |
|[ツール](introduction-to-xbox-tools.md)| Xbox One 固有のツールである _Dev Home_ の概要、Windows Device Portal の使い方、開発用の Visual Studio の設定方法について説明します。 また、このセクションでは、新しい開発者向けに初めての Xbox UWP アプリケーションを使って指針を示すと共に、Fiddler ツールを使用してネットワーク トラフィックを表示する方法について説明します。 |
| [App Dev on Xbox イベント](https://developer.microsoft.com/windows/projects/campaigns/app-dev-on-xbox-event) | App Dev on Xbox イベントは、Xbox で初めてアプリを開発する開発者にとって適切な開始点となります。 記録されたセッションを視聴し、イベントに関するブログ記事を参照してください。 |
|[Xbox およびテレビ向け設計](../design/devices/designing-for-tv.md)| テレビに表示して、コントローラーを使って入力するアプリを設計するための、ベスト プラクティスについて説明します。 |
|[Xbox ベスト プラクティス](tailoring-for-xbox.md)| マウス モードを無効にする方法、画面の端に描画する方法、スケーリングを無効にする方法について説明します。 |
|[音声認識を使用した UI 要素の呼び出し](ves-on-xbox.md)| Xbox で UWP アプリの音声対応シェルをサポートするためのベスト プラクティスについて説明します。 |
|[Xbox One 上の UWP アプリとゲームのシステム リソース](system-resource-allocation.md)| アプリケーションが Xbox One で実行されている場合に利用できるリソースについて説明します。 |
|[マルチ ユーザー アプリケーションの概要](multi-user-applications.md)| Xbox One での複数ユーザーのアプリケーション (MUA) について説明します。 |
| [Xbox One の開発作業の自動化](https://github.com/Microsoft/WindowsDevicePortalWrapper/tree/v0.9.4) | GitHub の WindowsDevicePortalWrapper プロジェクトでは、アプリの開発や起動などの一般的な開発タスクを自動化できるライブラリが提供されます。 プロジェクトには、一般的なタスクの API を使用する方法を示すサンプルである XboxWdpDriver.exe が含まれています。 |
|[既存のゲームの Xbox への移行](development-lanes-landing.md)|ゲームを構築する際の基礎となるテクノロジに基づいて、UWP を使用した Xbox へのゲームの移行プロセスを迅速に処理するための詳しい手順について説明します。|
|[Xbox One でまだサポートされていない UWP 機能](/uwp/extension-sdks/uwp-limitations-on-xbox)|  Xbox One でまだ完全に機能していない UWP 機能について説明します。|

## <a name="videos"></a>ビデオ

Channel 9 の以下の講演は、Xbox でのすばらしいアプリの開発に関する優れたソースです。

* [Xbox 向けの優れたユニバーサル Windows プラットフォーム (UWP) アプリのビルド](https://channel9.msdn.com/Events/Build/2016/B883)
* [アプリを Xbox One とテレビに対応させる](https://channel9.msdn.com/Events/Build/2016/T651-R1)
* [UWP の開発 1: アダプティブ UI の作成](https://channel9.msdn.com/Events/Build/2016/L724-R1)
* [ブラウザーに留まらない Web アプリ: クロスプラットフォームとクロス デバイスの遭遇](https://channel9.msdn.com/Events/Build/2016/B888)

## <a name="see-also"></a>関連項目

- [Windows 10 UWP アプリの自動起動](automate-launching-uwp-apps.md)
- [ゲーム開発用の CPUSets](cpusets-games.md)
- [Xbox One 用のプログレッシブ Web アプリ](/microsoft-edge/progressive-web-apps/xbox-considerations)