---
title: よく寄せられる質問
description: 期待どおりに動作しない場合は、「Xbox での UWP に関してよく寄せられる質問」のページを参照してください。
ms.date: 03/29/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 265fe827-bd4a-48d4-b362-8793b9b25705
ms.localizationpriority: medium
ms.openlocfilehash: 7da3b6a6507f2652eb2357ab80897d9ba35d7484
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89170736"
---
# <a name="frequently-asked-questions"></a>よく寄せられる質問

期待どおりに動作しない場合には、 このページのよく寄せられる質問を確認します。 また、「[既知の問題](known-issues.md)」と「[ユニバーサル Windows アプリの開発](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/home?forum=wpdevelop)」のフォーラムも確認します。 

### <a name="why-arent-my-games-and-apps-working"></a>作成したゲームとアプリが動作しない

ゲームやアプリが動作しない場合、またストアや Live サービスにアクセスできない場合、開発者モードで実行している場合があります。 現在のモードを調べるには、コントローラーの **[ホーム]** ボタンを押します。 製品版ホーム エクスペリエンスではなく Dev Home に移動した場合は、開発者モードです。 ゲームをプレイする場合には、Dev Home を開き、**[Leave developer mode] ** ボタンを使って、リテール モードに切り替えます。

### <a name="why-cant-i-connect-to-my-xbox-one-using-visual-studio"></a>Visual Studio を使って Xbox One に接続できない

まず、リテール モードでなく、開発者モードで実行していることを確認します。 リテール モードでは、Xbox One に接続できません。 現在のモードを調べるには、コントローラーの **[ホーム]** ボタンを押します。 Dev Home ではなく Gold/Live コンテンツが表示される場合はリテール モードであるため、開発者モードのアクティブ化用アプリを実行して開発者モードに切り替える必要があります。

> [!NOTE]
> アプリを展開するには、ユーザーをサインインさせる必要があります。

詳しくは、このページの「[展開の失敗を修正する](#fixing-deployment-failures)」をご覧ください。

### <a name="how-do-i-switch-between-retail-mode-and-developer-mode"></a>リテール モードと開発者モードの切り替え方法

これらの状態について詳しくは、「[Xbox One の開発者モードのアクティブ化](devkit-activation.md)」の指示に従います。

### <a name="how-do-i-know-if-i-am-in-retail-mode-or-developer-mode"></a>リテール モードと開発者モードのどちらで実行されているかを確認する方法

これらの状態について詳しくは、「[Xbox One の開発者モードのアクティブ化](devkit-activation.md)」の指示に従います。 

現在のモードを調べるには、コントローラーの **[ホーム]** ボタンを押します。 
- Dev Home が表示される場合は開発者モードです。
- Gold/Live コンテンツが表示された場合はリテール モードです。

### <a name="will-my-games-and-apps-still-work-if-i-activate-developer-mode"></a>開発者モードをアクティブ化してもゲームやアプリは動作しますか

はい、開発者モードからリテール モードに切り替えて、ゲームをプレイできます。 詳しくは、「[Xbox One の開発者モードのアクティブ化](devkit-activation.md)」をご覧ください。 

### <a name="can-i-develop-and-publish-x86-apps-for-xbox"></a>Xbox 用の x86 アプリを開発および公開できますか
Xbox では、x86 アプリの開発または x86 アプリのストアへの申請をサポートしなくなりました。 

### <a name="will-i-lose-my-games-and-apps-or-saved-changes"></a>ゲームやアプリや保存した変更を失うことがありますか

開発者プログラムへの参加を停止しても、インストールしたゲームやアプリは失われません。 またオンラインでプレイした場合には、保存したゲームはすべて Live アカウントのクラウド プロファイルに保存されていますので、それを失うことはありません。

### <a name="how-do-i-leave-the-developer-program"></a>開発者プログラムへの参加を停止する方法

開発者プログラムへの参加を停止する方法について詳しくは、「[Xbox One の開発者モードのアクティブ化](devkit-deactivation.md)」をご覧ください。

### <a name="i-sold-my-xbox-one-and-left-it-in-developer-mode-how-do-i-deactivate-developer-mode"></a>Xbox One を開発者モードにしたままで売却した場合に、 開発者モードを非アクティブ化する方法

Xbox One へのアクセス権がなくなった場合は、Windows パートナーセンターで非アクティブ化できます。 詳細については、 [Xbox One Developer Mode の非](devkit-deactivation.md#deactivate-your-console-using-partner-center)アクティブ化に関するトピックの「**パートナーセンターを使用したコンソールの非アクティブ化**」セクションを参照してください。 

### <a name="i-left-the-developer-program-using-partner-center-but-im-in-still-developer-mode-what-do-i-do"></a>パートナーセンターを使用して開発者プログラムを残しましたが、まだ開発者モードです。 どうすればよいですか。

Dev Home を開始し、**[Leave developer mode]** ボタンを選択します。 コンソールがリテール モードで再起動します。 

### <a name="can-i-publish-my-app"></a>自分のアプリを公開できますか

[開発者アカウント](https://developer.microsoft.com/store/register)を持っている場合は、パートナーセンターを使用して[アプリを発行](../publish/index.md)できます。 市販の Xbox One コンソールで作成されテストされた UWP アプリは、Windows で現在行われているものと同様の取り込み、レビュー、公開のプロセスが行われ、さらに Xbox One の標準を満たすための追加のレビューが行われます。

### <a name="can-i-publish-my-game"></a>自分のゲームを公開できますか

UWP と Xbox One の開発者モードを使って、Xbox One でゲームの構築とテストを行えます。 UWP ゲームを発行するには、に登録する [ID@XBOX](https://www.xbox.com/Developers/id) か、 [Xbox Live](https://developer.microsoft.com/games/xbox/xboxlive/creator)作成者プログラムに参加する必要があります。 詳細については、「 [開発者プログラムの概要](https://developer.microsoft.com/games/xbox/docs/xboxlive/get-started/developer-program-overview.html)」を参照してください。

### <a name="will-the-standard-game-engines-work"></a>標準的なゲーム エンジンは機能しますか

このリリースの「[既知の問題](known-issues.md)」ページを確認してください。

### <a name="what-capabilities-and-system-resources-are-available-to-uwp-games-on-xbox-one"></a>Xbox One の UWP ゲームで利用可能な機能とシステム リソース 

詳しくは、「[Xbox One 上の UWP アプリとゲームのシステム リソース](system-resource-allocation.md)」をご覧ください。

### <a name="if-i-create-a-directx-12-uwp-game-will-it-run-on-my-xbox-one-in-developer-mode"></a>DirectX 12 の UWP ゲームを作成する場合、それは Xbox One の開発者モードで動作しますか

詳しくは、「[Xbox One 上の UWP アプリとゲームのシステム リソース](system-resource-allocation.md)」をご覧ください。

### <a name="will-the-entire-uwp-api-surface-be-available-on-xbox"></a>Xbox では UWP API のすべてを利用できますか

このリリースの「[既知の問題](known-issues.md)」ページを確認してください。

### <a name="fixing-deployment-failures"></a>展開の失敗を修正する

Visual Studio からアプリを展開できない場合、次の手順が問題の解決に役立つ場合があります。 それでも解決できない場合には、フォーラムに投稿してみます。

> [!NOTE]
> アプリを展開するには、ユーザーをサインインさせる必要があります。 0x87e10008 エラー メッセージが表示された場合は、ユーザーがサインインしているかどうかを確認し、もう一度サインインさせます。

Visual Studio が Xbox One に接続できない場合:

1. 開発者モードであることを確認します (このページで既に説明した方法を確認します)。
2. 開発用 PC が正しく設定されていることを確認します。 [Xbox One の UWP アプリ開発の概要](getting-started.md)の*すべての*指示に従いましたか。 

3. まだお持ちでない場合は、 [開発環境のセットアップ](development-environment-setup.md) に関するトピックと「 [Xbox One tools の概要](introduction-to-xbox-tools.md) 」トピックを参照してください。

4. 開発用 PC から本体の IP アドレスに "ping" ができることを確認します。
  > [!NOTE]
  > 展開のパフォーマンスを最大限に引き出すために、本体には、有線接続を使用することをお勧めします。

5. **[デバッグ]** タブの [認証] ドロップダウン リストで [ユニバーサル (暗号化されていないプロトコル)] を使用していることを確認します。詳しくは、「[開発環境のセットアップ](development-environment-setup.md)」をご覧ください。


### <a name="if-im-building-an-app-using-htmljavascript-how-do-i-enable-gamepad-navigation"></a>HTML/JavaScript を使用したアプリを構築する場合に、ゲームパッドのナビゲーションを有効にする方法

TVHelpers は、JavaScript と XAML/C# のサンプルとライブラリです。JavaScript と C# による、Xbox One とテレビの優れたエクスペリエンスの構築をサポートします。 TVJS は Xbox One のための優れた UWP アプリの構築をサポートします。 TVJS には、自動コントローラー ナビゲーション、リッチ メディアの再生、検索などのサポートが含まれています。 ホストされた Web アプリで TVJS を使うと、パッケージ化された Web UWP アプリを使う場合のように容易に、すべての Windows ランタイム API にアクセスできます。

詳細については、 [TVHelpers](https://github.com/Microsoft/TVHelpers) プロジェクトとプロジェクト [wiki](https://github.com/Microsoft/TVHelpers/wiki)を参照してください。

## <a name="see-also"></a>関連項目
- [Xbox One の UWP に関する既知の問題](known-issues.md)
- [Xbox One の UWP](index.md)
- [Xbox One の UWP](index.md)
