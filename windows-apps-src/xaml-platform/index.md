---
ms.assetid: b632a6cc-3503-4ab8-bfd1-dde731bd89ab
description: このセクションのトピックでは、ユニバーサル Windows プラットフォーム (UWP) アプリ用の XAML フレームワークについて説明します。
title: XAML プラットフォーム
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: e22a10e74a834daf4d256313f0e353a6829911c0
ms.sourcegitcommit: f0f933d5cf0be734373a7b03e338e65000cc3d80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65984238"
---
# <a name="xaml-platform"></a>XAML プラットフォーム


このセクションのトピックでは、プログラミング言語として C#、Microsoft Visual Basic、または Visual C++ コンポーネント拡張機能 (C++/CX) を使い、UI 定義として XAML を使う場合に、作成するアプリ全般に当てはまるプログラミングの概念について説明します。 ここでは、プロパティとイベントの使い方や、ユニバーサル Windows プラットフォーム (UWP) アプリ プログラミングへのその適用法など、基本的なプログラミングの概念について説明します。 ユニバーサル Windows プラットフォーム (UWP) は、依存関係プロパティ システムを追加することで、C#、Visual Basic、C++/CX のプロパティとその値の概念を拡張します。 このセクションのトピックでは、UWP で使われる XAML 言語についても説明し、XAML を使って UWP アプリの UI を定義する方法に関する基本的なシナリオと高度なトピックも取り上げています。

| トピック | 説明 |
|-------|-------------|
| [XAML の概要](xaml-overview.md) | ここでは、Windows ランタイム アプリの開発者を対象に、XAML 言語と XAML の概念を紹介し、Windows ランタイム アプリを作成する際に XAML でオブジェクトを宣言したり属性を設定したりするためのさまざまな方法について説明します。 |
| [依存関係プロパティの概要](dependency-properties-overview.md) | このトピックでは、C++、C#、または Visual Basic と UI の XAML 定義を使って Windows ランタイム アプリを作成するときに使うことができる依存関係プロパティ システムについて説明します。 |
| [カスタム依存関係プロパティ](custom-dependency-properties.md) | C++、C#、または Visual Basic を使った Windows ランタイム アプリでカスタム依存関係プロパティを定義および実装する方法を説明します。 |
| [添付プロパティの概要](attached-properties-overview.md) | XAML での添付プロパティの概念を説明し、例をいくつか紹介します。 |
| [カスタム添付プロパティ](custom-attached-properties.md) | XAML 添付プロパティを依存関係プロパティとして実装する方法と、添付プロパティを XAML で使うために必要なアクセサー変換を定義する方法を説明します。 |
| [イベントとルーティング イベントの概要](events-and-routed-events-overview.md) | このトピックでは、Windows ランタイム アプリで、プログラミング言語に C#、Visual Basic、または C++/CX、UI 定義に XAML を使う場合のイベントのプログラミングの概念について説明します。 イベントのハンドラーは、UI 要素の宣言の一部として XAML で割り当てることも、コードで追加することもできます。 Windows ランタイムは**ルーティング イベント**をサポートしており、特定の入力イベントとデータ イベントを、その発生元オブジェクト以外のオブジェクトで処理できます。 ルーティング イベントは、コントロール テンプレートを定義する際や、ページまたはレイアウト コンテナーを使う際に役立ちます。 |
|[デスクトップ アプリケーションの UWP コントロール (XAML アイランド)](/windows/apps/desktop/modernize/xaml-islands)| UWP XAML コントロールを使用して、Windows フォーム、WPF、または Win32 デスクトップ アプリケーションの UI を強化する方法について説明します。|
