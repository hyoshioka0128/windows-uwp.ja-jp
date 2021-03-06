---
Description: このガイドラインは、アプリの効果的なヘルプ コンテンツの設計方法を説明しています。
title: アプリのヘルプのガイドライン
label: Guidelines for app help
template: detail.hbs
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: c3e73f9b-4839-4804-b379-c95b0ca4fbe8
ms.localizationpriority: medium
ms.openlocfilehash: bd2174c6bbfb84a3ea6c6956e1d0b02ed5c9be33
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57621367"
---
# <a name="guidelines-for-app-help"></a>アプリのヘルプのガイドライン



アプリケーションが複雑な場合には、ユーザーに効果的なヘルプを提供することにより、ユーザー エクスペリエンスを大幅に改善できます。 すべてのアプリケーションがユーザーにヘルプを提供する必要があるとは限らず、また提供する必要のあるヘルプの種類もアプリケーションによって大きく異なります。

ヘルプを提供する場合には、その作成時に次のガイドラインに従います。 有用でないヘルプを提供するくらいなら、ヘルプを提供しないほうがましであるという場合もあります。

## <a name="intuitive-design"></a>直感的なデザイン

ヘルプのコンテンツをどれだけ充実させたとしても、アプリがユーザーに優れたエクスペリエンスを提供するには、ヘルプに依存することはできません。 ユーザーは、アプリの重要な機能がすぐに見つからずに使えない場合には、アプリの使用をやめてしまいます。 ヘルプの質と量がどれだけ優れていても、第一印象を変えることはできません。

直感的でわかりやすいデザインは、有用なヘルプを作成するための最初の手順です。 ユーザーが関心を持ち続けて、やがてより高度な機能を使うようになるだけではありません。アプリの主要機能の知識を提供することにより、アプリを使用してその習得を継続するにつれて、知識が蓄積されていきます。

## <a name="general-instructions"></a>一般的な手順

ユーザーは問題が発生していない場合には、ヘルプ コンテンツを探すことはありません。ヘルプは問題に対する回答をすばやく効果的に提供する必要があります。 ヘルプが即座に有用でない場合や、ヘルプが複雑すぎる場合は、ユーザーはそれを無視する可能性が高くなります。

あらゆるヘルプは、次の原則に従う必要があります。

-   **簡単に理解できます。** ユーザーの混乱を招くヘルプはすべてのヘルプはありませんよりも悪いされます。

-   **簡単です。** 探しているユーザーは、回答がそれらに直接提示を消去するのに役立ちます。

-   **関連。** ユーザーは、その特定の問題を検索する必要がありますしません。 ユーザーはその場面に最も関連があって適切なヘルプ (コンテキスト ヘルプと呼ばれます) がすぐに表示されることを求めています。または容易なナビゲーションのためのインターフェイスが必要です。

-   **直接。** ユーザーは、ヘルプを検索するときに表示するヘルプ。 アプリのヘルプの中に、バグの報告、フィードバックの送信、サービス規定の表示などの機能へのリンクが含まれていてもかまいませんが、 それらはメインのヘルプ ページの補足として含むものであり、メインのヘルプのコンテンツとなるものではありません。

-   **一貫性のあります。** 種類に関係なくヘルプは、アプリの一部ではまだと UI の他の部分として扱う必要があります。 アプリの他の部分と同じ設計原則による、操作性、アクセシビリティ、スタイルが、ヘルプでも採用されている必要があります。

## <a name="types-of-help"></a>ヘルプの種類

ヘルプ コンテンツには 3 つの主要なカテゴリがあり、それぞれにメリットと適性があります。 アプリの必要に応じて、これらを組み合わせて使用します。

#### <a name="instructional-ui"></a>説明 UI

通常の場合、ユーザーはアプリの主要な機能のすべてを、操作手順を読まなくても使える必要があります。 場合によっては、アプリが特定のジェスチャの使用に依存していたり、すぐには自明ではない別の機能がある場合もあります。 そのような場合には、説明 UI によってユーザーに特定のタスクの使い方を教えることができます。

[説明用の UI のガイドラインを参照してください。](instructional-ui.md)

#### <a name="in-app-help"></a>アプリ内ヘルプ

ヘルプを表示する標準的な方法では、ユーザーの要求に応じて、アプリケーション内で表示します。 これを実装するにはいくつかの方法があります。たとえば、ヘルプ ページや、情報の説明などの方法があります。 この方法は、複雑でないユーザーの質問に直接回答する、一般的なヘルプに適しています。

[アプリ内のヘルプに関するガイドラインを参照してください。](in-app-help.md)

#### <a name="external-help"></a>外部のヘルプ

詳細なチュートリアル、高度な機能、ヘルプ トピックのライブラリなど、アプリケーション内に収めるには大きすぎるコンテンツは、外部の Web ページへのリンクとすることが適切です。 これらのリンクは、ユーザーをアプリケーションから切り離すため、できる限り慎重に使用します。

[外部ヘルプに関するガイドラインを参照してください。](external-help.md)


