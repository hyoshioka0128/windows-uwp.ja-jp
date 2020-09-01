---
ms.assetid: 83b4be37-6613-4d00-a48a-0451a24a30fb
title: データ バインディング
description: データ バインディングは、アプリの UI でデータを表示し、必要に応じてそのデータとの同期を保つ方法です。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 9f4f83711c30aab94005e90e7de2db4e4b48bfc8
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89157196"
---
# <a name="data-binding"></a>データ バインディング

データ バインディングは、アプリの UI でデータを表示し、必要に応じてそのデータとの同期を保つ方法です。 データ バインディングによって、UI の問題からデータの問題を切り離すことができるため、概念的なモデルが簡素化されると共に、アプリの読みやすさ、テストの容易性、保守容易性が向上します。 マークアップでは、[{{x:Bind}} マークアップ拡張](../xaml-platform/x-bind-markup-extension.md)と [{{Binding}} マークアップ拡張](../xaml-platform/binding-markup-extension.md)のいずれを使うかを選ぶことができます。 また、同じアプリや同じ UI 要素で、この 2 つを組み合わせて使うこともできます。 {x:Bind} は Windows 10 の新機能で、パフォーマンスが向上しています。

| トピック | 説明 |
|-------|-------------|
| [データバインディングの概要](data-binding-quickstart.md) | このトピックでは、ユニバーサル Windows プラットフォーム (UWP) アプリで、コントロール (または他の UI 要素) を単一の項目にバインドする方法や、項目コントロールを項目のコレクションにバインドする方法を説明します。 また、項目のレンダリングを制御する方法、選択内容に基づいて詳細ビューを実装する方法、表示するデータを変換する方法も紹介します。 詳しくは、「[データ バインディングの詳細](data-binding-in-depth.md)」をご覧ください。 | 
| [データ バインディングの詳細](data-binding-in-depth.md) | このトピックでは、データ バインディングの機能について詳しく説明します。 |
| [デザイン サーフェイス上のサンプル データとプロトタイプを作るためのサンプル データ](displaying-data-in-the-designer.md) | (アプリのレイアウト、テンプレート、その他の視覚的なプロパティを操作するため) Visual Studio デザイナーでコントロールにデータを設定できるように、さまざまな方法で設計時のサンプル データを使うことができます。 サンプル データは、スケッチ (プロトタイプ) アプリを開発する場合にも便利で、時間の節約になります。 スケッチやプロトタイプで実行時にサンプル データを使うと、実際のライブ データに接続しなくてもアイデアを実証できます。 |
| [階層データをバインドしてマスター/詳細ビューを作る方法](how-to-bind-to-hierarchical-data-and-create-a-master-details-view.md) | チェーン内でバインドされた [<strong>CollectionViewSource</strong>](/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) インスタンスに項目コントロールをバインドすることによって、階層データの複数レベルのマスター/詳細 (リスト/詳細とも呼ばれる) ビューを作成することができます。 |
| [データ バインディングと MVVM](data-binding-and-mvvm.md) | このトピックでは、Model-View-ViewModel (MVVM) UI アーキテクチャの設計パターンについて説明します。 データ バインディングは MVVM の中核に位置し、これにより UI コードと UI 以外のコードの間の疎結合が実現されます。 |