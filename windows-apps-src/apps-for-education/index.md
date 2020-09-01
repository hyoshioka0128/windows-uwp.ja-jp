---
title: 教育用アプリを開発します。
description: このセクションでは、Windows 10 プラットフォームの教育アプリを記述するときに利用できるユニバーサル Windows アプリのリソースについて説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp, 教育
ms.assetid: 2431f253-efe3-4895-b131-34653b61f13c
ms.localizationpriority: medium
ms.openlocfilehash: 9a32efc4be4d14bf703dfd597d7f4abd53cccd1d
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89161316"
---
# <a name="develop-universal-windows-apps-for-education"></a>教育用のユニバーサル Windows アプリの開発
![テスト アプリのスクリーンショット](images/take-a-test-screen-small.png)

以下のリソースは、教育用のユニバーサル Windows アプリの作成に役立ちます。

### <a name="accessibility"></a>ユーザー補助
教育アプリでは、アクセシビリティ対応が必要です。 詳しくは、「[アクセシビリティのためのアプリ開発](https://developer.microsoft.com/windows/accessible-apps)」をご覧ください。


### <a name="secure-assessments"></a>安全な評価
評価/テストのアプリでは、多くの場合、学生がテスト中に他のコンピューターやインターネットのリソースを使用できないようにするための*ロックダウン*環境を作成する必要があります。 この機能は[テスト API](take-a-test-api.md) により利用できます。 安全なテストを行うためのオンライン アクセスのロックダウンを使ったテスト環境の例については、Windows IT センターの「[テスト](/education/windows/take-tests-in-windows-10)」Web アプリをご覧ください。

### <a name="user-input"></a>ユーザー入力
ユーザー入力は教育アプリにとって重要です。UI コントロールは、ユーザーの集中を妨げないように、応答性に優れ、直感的である必要があります。 ユニバーサル Windows アプリで利用可能な入力オプションの一般的な概要については、「[操作の基本情報](../design/input/input-primer.md)」およびその中のデザインと UI に関するセクションのトピックをご覧ください。 また、次のサンプル アプリでは、ユニバーサル Windows プラットフォームの基本的な UI 処理を利用しています。
- 「[基本的な入力のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicInput)」では、ユニバーサル Windows アプリで入力を処理する方法を示します。
- 「[ユーザー操作モードのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/UserInteractionMode)」では、ユーザー操作モードを検出して応答する方法を示します。
- [フォーカスの視覚効果のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlFocusVisuals)」では、システムによって描画される新しいフォーカスの視覚効果を利用する方法や、システムによって描画される視覚効果がニーズに合わない場合に、独自のカスタム フォーカスの視覚効果を作成する方法を示します。

Windows Ink プラットフォームの利用によって、学生が慣れ親しんだ入力モードを活用でき、教育用アプリを魅力的なものにすることができます。 Windows Ink をアプリに実装するための包括的なガイドは、「[ペン操作と Windows Ink](../design/input/pen-and-stylus-interactions.md)」およびその中のトピックをご覧ください。 次のサンプル アプリは、この API の動作の例を示します。
- [インクのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Ink)」では、JavaScript を使ってユニバーサル Windows アプリでインク機能 (キャプチャ、操作、インク ストロークの解釈など) を使う方法を示します。
- 「[単純なインクのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SimpleInk)」では、C# を使ってユニバーサル Windows アプリでインク機能 (ユーザー入力からのインクのキャプチャやインク ストロークでの手書き認識の実行など) を使う方法を示します。
- 「[複雑なインクのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ComplexInk)」では、高度な InkPresenter の機能を使ってインクを他のオブジェクトにインターリブしたり、インクを選択したり、コピー/貼り付けしたり、イベントを処理する方法を示します。 このサンプルは、C++ でユニバーサル Windows プラットフォームに基づいて構築され、デスクトップ SKU とモバイル Windows 10 SKU で実行できます。


### <a name="microsoft-store"></a>Microsoft Store
教育用アプリは、多くの場合、特定の状況下の特定の組織にリリースされます。 これについて詳しくは、「[LOB アプリの企業への配布](../publish/distribute-lob-apps-to-enterprises.md)」をご覧ください。

## <a name="related-topics"></a>関連トピック
- Windows IT センターの「[Windows 10 for Education](/education/windows/index)」