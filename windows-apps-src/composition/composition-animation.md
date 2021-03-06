---
ms.assetid: 386faf59-8f22-2e7c-abc9-d04216e78894
title: コンポジションのアニメーション
description: コンポジション オブジェクトと効果の多くのプロパティは、キー フレーム アニメーションや数式アニメーションを使って、時間の経過や計算に基づいて UI 要素のプロパティを変更することによりアニメーション化できます。
ms.date: 10/10/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 18208986d7d07e4d437e52dce844deecc03cf1f6
ms.sourcegitcommit: 681c1e3836d2a51cd3b31d824ece344281932bcd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240030"
---
# <a name="composition-animations"></a>コンポジションのアニメーション

Windows.UI.Composition API によって、統合された API レイヤーでコンポジター オブジェクトを作成、アニメーション化、変換、操作することができます。 コンポジションのアニメーションは、アプリケーションの UI でアニメーションを実行するための強力で効率的な手段を提供します。 コンポジション アニメーションは、アニメーションが UI スレッドから独立して 60 FPS で実行され、時間だけでなく、入力やその他のプロパティを使ってアニメーションを駆動する驚くようなエクスペリエンスを柔軟に構築できるように、一から設計されています。

## <a name="motion-in-windows"></a>Windows でのモーション

モーションのデザインは映画のようなものと考えてください。 シームレスな切り替えによって、ユーザーをストーリーに注目させておき、優れたエクスペリエンスを実現することができます。 モーションのデザインにそのような感覚を取り込むことで、あるタスクから別のタスクへ映画のようにスムーズにユーザーを移行させることができます。 モーションは、ユーザー インターフェイスとユーザー エクスペリエンスを差別化要因では多くの場合です。

Windows UI プラットフォームの基本的なビルディング ブロックとして CompositionAnimations は、アプリケーションの UI でモーションのエクスペリエンスを作成する強力かつ効率的な方法を提供します。 アニメーション エンジンは、モーションが UI スレッドから独立して、60 FPS でが実行されることを確認するを一から設計されています。 これらのアニメーションは、時間、入力、およびその他のプロパティに基づく革新的な動きのエクスペリエンスを構築する柔軟性を提供する設計されています。

### <a name="examples-of-motion"></a>モーションの例

アプリでのモーションの例をいくつか紹介します。

次の例では、アプリは接続型アニメーションを使用して項目の画像をアニメーション化し、その画像が "途切れることなく" 切り替わり、次のページにあるヘッダーの一部となります。 この効果を利用すると、画面の切り替えでユーザー コンテキストを維持することができます。

![接続されているアニメーションの例](images/animation/connected-animation-example.gif)

次の例では、視覚的な視差効果を利用し、UI のスクロールやパンを行うときに、さまざまなオブジェクトをさまざまな速度で動かします。これにより、奥行き、遠近感、および動きといった感覚が引き起こされます。

![リストと背景画像を使用した視差の例](images/animation/parallax-example.gif)

## <a name="using-compositionanimations-to-create-motion"></a>CompositionAnimations を使用してアニメーションを作成するには

UI でモーションを生成するには、開発者が XAML またはビジュアル層のいずれかでアニメーションをアクセスできます。 ビジュアル層でのアニメーションは、一連の特典の開発者を提供します。

- パフォーマンス: 従来の UI スレッドにバインドされたアニメーションの Windows UI プラットフォーム上のアニメーションではなくは、動きが滑らかなエクスペリエンスを有効にすると、60 FPS で、独立したスレッドで動作します。
- テンプレートのモデル – Windows UI 層でのアニメーションは、テンプレート、意味が 1 つのアニメーションを使用して、複数のオブジェクトとプロパティを調整または障害前の悩むことがなくパラメーターを使用します。
- カスタマイズ: Windows UI 層だけでなく、美しい UI は、簡単ですがアニメーションの種類の完全な範囲は、新しくてすばらしいを作成するには、可能な限りのエクスペリエンスのカスタマイズのグラデーションを使用

Windows UI 層でのエクスペリエンスを作成する開発者は、さまざまなアニメーションの概念をデザインを実現するへのアクセスがあります。 これらの概念のいずれかを使用するには、プロパティをアニメーション表示またはサブチャネル CompositionObject 任意のコンポーネント (ある場合)。

> [!NOTE]
> CompositionObject のすべてのプロパティはアニメーション化可能です。 プロパティがアニメーション化できるかどうかを判断する個々 の CompositionObject のドキュメントを参照してください。

> [!NOTE]
> 用語_サブチャネル_コンポーネント フォームのプロパティを参照します。 たとえば、X、またはお客様 xy のところ、Vector3 オフセット プロパティのサブチャネルします。

| アニメーションの概念 | 説明 |
| ----------------- | ----------- |
| [KeyFrameAnimations でのモーションの時間ベース](time-animations.md)  | KeyFrameAnimations は、時間の期間にわたってモーション エクスペリエンス全体を直接制御に使用されます。 開発者は、モーションの開始、終了、補間で、および従来のキーフレームの形で期間を記述します。 |
| [ExpressionAnimations 相対移動中](relation-animations.md)  | ExpressionAnimations を使用して、別のオブジェクトのプロパティの基準とした 1 つのオブジェクトのプロパティの動作を動作させる方法を記述します。 開発者は、参照に基づくリレーションシップを定義する数式を定義します。 |
| ImplicitAnimations | これらのアニメーションは、トリガー ベースされ、コア アプリケーション ロジックから個別に定義されます。 ImplicitAnimations を使用して、アニメーションがダイレクトのプロパティの変更への応答として発生する時期と方法を記述します。 |
| [入力のアニメーションでのモーションの入力に基づく](input-driven-animations.md)  | 入力のアニメーションでは、一連のタッチまたはその他の入力の様相を使用して操作に基づくアニメーションを記述する開発者を有効にするシナリオについて説明します。 これらのアニメーションはアクティブなユーザー入力やジェスチャに基づいて決まります。 |
| [NaturalMotionAnimations でモーションを物理ベース](natural-animations.md)  | NaturalMotionAnimations を使用して、エクスペリエンスが現実に基づく強制駆動モーション自然かつ使い慣れたモーションを記述します。 開発者が (Springs は、比率を抑制など) の動きの特性を定義する時刻を定義するのではなく |