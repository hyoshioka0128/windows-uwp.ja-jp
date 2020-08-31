---
Search.SourceType: Video
title: iOS から UWP への移行
description: IOS 開発者がユーザーベースを拡張して、Windows 10 とユニバーサル Windows プラットフォーム (UWP) を含めるために使用できるツールについて説明します。
ms.assetid: 7a05751d-02df-4240-9ba5-d95f65a7a9c5
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ef0f712a87f0b2aea7fdb2204691e9b439315b44
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89155386"
---
# <a name="move-from-ios-to-uwp"></a>iOS から UWP への移行

ユーザー ベースを Windows 10 とユニバーサル Windows プラットフォーム (UWP) にまで拡大する方法に悩んでいる iOS 開発者向けに、便利なツールが提供されています。そしてその数は日々増え続けています。 どの方法を使うかは、対象のアプリの種類 (ゲーム、ライフ スタイル、エンタープライズなど) と、開発プロセスにどれだけ関与できるかに応じて異なります。 たとえば、OpenGL または Cocos2D に大きく依存している完成済みのゲームまたはほぼ完成しているゲームの場合は、[iOS 用 Windows ブリッジ](https://developer.microsoft.com/windows/bridges/ios)が有力な候補になります。また、スモール ビジネス用のクロスプラットフォーム アプリを計画している場合は、[Xamarin.Forms](/xamarin/xamarin-forms/) の使用を検討する必要があります。 Unity などのクロスプラットフォーム ツールでアプリを記述している場合は、[Windows に公開](https://blogs.unity3d.com/2015/09/09/windows-10-universal-apps-in-unity-5-2/)するのが簡単です。

## <a name="why-windows"></a>Windows を選ぶ理由

今日は、Windows は膨大な数のデバイスで実行されています。 UWP は、デスクトップ コンピューター、ゲーム コンソール、ホログラフィック ディスプレイなどのさまざまなデバイス間で美しく応答性に優れたユーザー インターフェイスを作るように設計された最新の API のセットを開発者に提供します。 1 つの Visual Studio ソリューションと、複数のプラットフォームに自動的に最適化されるスマートなユーザー インターフェイス コントロールにより、より少ないコードで記述したアプリをより多くのハードウェア上で実行できます。

> [!VIDEO https://channel9.msdn.com/Blogs/One-Dev-Minute/How-to-Convert-your-iOS-app-to-Windows/player]

| トピック | 説明 |
|-------|-------------|
| [iOS と UWP のアプリ開発方法の選択](selecting-an-approach-to-ios-and-uwp-app-development.md) | クロスプラットフォーム アプリを開発するときの選択肢 |
| [iOS 開発者のための UWP の概要](getting-started-with-uwp-for-ios-developers.md) | この記事は、Windows 10 用の開発を検討している iOS 開発者向けに用意されています。 |
| [Windows 10 を使用するための Mac のセットアップ](setting-up-your-mac-with-windows-10.md) | 現在の Mac コンピューターを使用して、Windows 用アプリを開発します。 |

## <a name="related-topics"></a>関連トピック

**設計者と開発者向け**
* [すべての Windows デバイスを対象としたユニバーサル Windows アプリの構築](../get-started/universal-application-platform-guide.md)
* [UWP アプリの設計アセットのダウンロード](../design/downloads/index.md)