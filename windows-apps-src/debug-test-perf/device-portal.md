---
ms.assetid: 60fc48dd-91a9-4dd6-a116-9292a7c1f3be
title: Windows Device Portal の概要
description: Windows Device Portal で、ネットワーク経由でリモートから、または USB 接続によって、デバイスの構成と管理を行うための方法を説明します。
ms.date: 04/09/2019
ms.topic: article
keywords: windows 10、uwp、デバイス ポータル
ms.localizationpriority: medium
ms.openlocfilehash: 1f776a9d0ffe15f4bec26fbf8a26ce52a73345e9
ms.sourcegitcommit: 139717a79af648a9231821bdfcaf69d8a1e6e894
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67713866"
---
# <a name="windows-device-portal-overview"></a>Windows Device Portal の概要

Windows Device Portal では、ネットワーク経由でリモートから、または USB 接続によって、デバイスの構成と管理を行えます。 また、トラブルシューティングを行うし、Windows デバイスのリアルタイムのパフォーマンスの表示に役立つ高度な診断ツールも提供します。

Windows Device Portal は、PC 上の web ブラウザーからに接続できるデバイスで web サーバーです。 デバイスでは、web ブラウザーには、するはそのデバイスのブラウザーでローカルに接続もできます。

Windows Device Portal は各デバイス ファミリで使用できますが、機能とセットアップは、各デバイスの要件に基づいて変化します。 ここでは、Device Portal の一般的な説明と、各デバイス ファミリに関するさらに詳細な情報が掲載されている記事へのリンクを示します。

Windows Device Portal の機能が実装されている[REST Api](device-portal-api-core.md)ことは、データにアクセスし、デバイスの管理をプログラム的に直接使用することができます。

## <a name="setup"></a>セットアップ

Device Portal への接続の具体的な手順はデバイスによって異なりますが、どのデバイスでも次の一般的な手順が必要です。

1. (構成、設定アプリで) デバイスで開発者モードとデバイスのポータルを有効にします。

2. ローカル ネットワーク経由または USB デバイスと PC を接続します。

3. ブラウザーでデバイス ポータルのページに移動します。 次の表は、ポートと各デバイス ファミリで使用されるプロトコルを示します。

デバイス ファミリ | 既定でオンになっているか | HTTP | HTTPS | USB
--------------|----------------|------|-------|----
HoloLens | 開発者モードでオン | 80 (既定) | 443 (既定) | http://127.0.0.1:10080
IoT | 開発者モードでオン | 8080 | レジストリ キーで有効化する | なし
Xbox | 開発者モードで有効化する | Disabled | 11443 | なし
Desktop| 開発者モードで有効化する | 50080\* | 50043\* | なし
Phone | 開発者モードで有効化する | 80| 443 | http://127.0.0.1:10080

\* これは常に場合は、デスクトップ上のデバイスのポータルが短期の範囲内のポートを要求として (> 50,000) デバイスで既存のポートのクレームとの競合を回避します。 詳しくは、デスクトップに関する「[ポート番号を設定する](device-portal-desktop.md#registry-based-configuration-for-device-portal)」のセクションをご覧ください。  

デバイス固有のセットアップ手順については、以下をご覧ください。

- [HoloLens 用 Device Portal](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens)
- [IoT 用 Device Portal](https://go.microsoft.com/fwlink/?LinkID=616499)
- [モバイル用 Device Portal](device-portal-mobile.md)
- [Xbox 向けのデバイス ポータル](../xbox-apps/device-portal-xbox.md)
- [デスクトップ用 Device Portal](device-portal-desktop.md#set-up-device-portal-on-windows-desktop)

## <a name="features"></a>機能

### <a name="toolbar-and-navigation"></a>ツールバーとナビゲーション

ページの上部にあるツールバーでは、一般的に使用される機能へのアクセスを提供します。

- **Power**:電源オプション のアクセス。
  - **シャット ダウン**:デバイスをオフにします。
  - **再起動**:デバイスの電源が循環します。
- **ヘルプ**:ヘルプ ページが開きます。

ページの左側にあるナビゲーション ウィンドウのリンクを使用して、デバイスの管理と監視に利用可能なツールに移動します。

ここでは、デバイス ファミリに共通するツールについて説明します。 デバイスによってはその他のオプションを利用できる場合があります。 詳細については、デバイスの種類の特定のページを参照してください。

### <a name="apps-manager"></a>アプリ マネージャー

Apps manager には、インストール/アンインストールし、アプリの管理機能をパッケージ化し、ホスト デバイスにバンドルします。

![デバイスのポータル アプリはマネージャー ページ](images/device-portal/WDP_AppsManager2.png)

* **アプリを展開する**:ローカルからのパッケージ アプリ、ネットワーク、または web ホストを展開し、ネットワーク共有から圧縮しないファイルを登録します。
* **アプリがインストールされている**:ドロップダウン メニューを使用して、削除するか、デバイスにインストールされているアプリを起動します。
* **アプリを実行している**:現在実行中、必要に応じてそれらを閉じるアプリに関する情報を取得します。

#### <a name="install-sideload-an-app"></a>(サイドロード) アプリをインストールします。

Windows Device Portal を使用した開発中にアプリをサイドロードすることができます。

1. アプリ パッケージを作成した場合は、デバイス上にリモートでインストールできます。 Visual Studio でビルドすると、出力フォルダーが生成されます。

    ![アプリのインストール](images/device-portal/iot-installapp0.png)

2. Windows Device Portal のに移動、 **Apps manager**ページ。

3. **アプリを展開する**セクションで、**ローカル ストレージ**します。

4. **アプリケーション パッケージを選択して**を選択します**ファイルの選択**サイドロードするアプリ パッケージを参照します。

5. **アプリ パッケージの署名に使用される証明書の選択ファイル (.cer)** を選択します**Choose File**し、そのアプリのパッケージに関連付けられている証明書を参照します。

6. 省略可能なインストールやアプリのインストールと共にフレームワーク パッケージを選択すると、それぞれのボックスをチェック**次**して選択します。

7. 選択**インストール**のインストールを開始します。

8. デバイスが S のモードで Windows 10 を実行しているが初めてデバイスの特定の証明書がインストールされている場合、デバイスを再起動します。

#### <a name="install-a-certificate"></a>証明書をインストールします。

または、Windows Device Portal を使用して証明書をインストールし、他の手段でアプリをインストールします。

1. Windows Device Portal のに移動、 **Apps manager**ページ。

2. **アプリを展開する**セクションで、**証明書のインストール**します。

3. **アプリ パッケージの署名に使用される証明書の選択ファイル (.cer)** を選択します**ファイルの選択**サイドロードするアプリ パッケージに関連付けられている証明書を参照します。

4. 選択**インストール**のインストールを開始します。

5. デバイスが S のモードで Windows 10 を実行しているが初めてデバイスの特定の証明書がインストールされている場合、デバイスを再起動します。

#### <a name="uninstall-an-app"></a>アプリをアンインストールする

1. アプリが実行中でないことを確認します。
2. 場合を参照してください。**アプリを実行している**して閉じます。 場合は、アプリの実行中をアンインストールしようとすると、問題が生じるため、アプリを再インストールしようとしたときにします。
3. ドロップダウン リストとクリックからアプリを選択**削除**します。

### <a name="running-processes"></a>実行中のプロセス

このページには、ホスト デバイスで現在実行されているプロセスに関する詳細情報が表示されます。 これには、アプリとシステムの両方のプロセスが含まれます。 (デスクトップや IoT、HoloLens) 一部のプラットフォームでは、プロセスを終了できます。

![ページを処理するポータルを実行しているデバイス](images/device-portal/mob-device-portal-processes.png)

### <a name="file-explorer"></a>エクスプローラー

このページを表示およびサイドロードしたアプリによって保存されているファイルを操作できます。 参照してください、[アプリのファイル エクスプ ローラーを使用して](https://blogs.windows.com/buildingapps/2016/06/08/using-the-app-file-explorer-to-see-your-app-data/)ブログの投稿をファイル エクスプ ローラーとその使用方法の詳細を参照してください。

![デバイスのポータル ファイル エクスプ ローラー ページ](images/device-portal/mob-device-portal-AppFileExplorer.png)

### <a name="performance"></a>パフォーマンス

[パフォーマンス] ページには、電力使用状況、フレーム レートのようなシステム診断情報のリアルタイムのグラフが表示されます。 と CPU の負荷。

利用可能なメトリックを次に示します。

- **CPU**:使用可能な CPU 使用率の合計の割合
- **メモリ**:内の合計、使用して、使用可能なコミット、ページング、および非ページ
- **I/O**:読み取りと書き込みのデータ量
- **ネットワーク**:受信および送信データ
- **GPU**:使用可能な GPU エンジンの合計使用率の割合

![デバイスのポータルのパフォーマンス ページ](images/device-portal/mob-device-portal-perf.png)

### <a name="event-tracing-for-windows-etw-logging"></a>Event Tracing for Windows (ETW) ログ記録

ETW のログ記録 ページでは、デバイスのリアルタイムの Event Tracing for Windows (ETW) 情報を管理します。

![デバイスのポータルの ETW のログ記録 ページ](images/device-portal/mob-device-portal-etw.png)

**[Hide Providers]** (プロバイダを非表示にする) チェックボックスをオンにすると、イベントの一覧のみが表示されます。

- **登録済みプロバイダー**:イベント プロバイダーは、トレース レベルを選択します。 トレース レベルでは、これらの値の 1 つです。
  1. 異常終了または終了
  2. 重大なエラー
  3. 警告
  4. エラーではない警告
  5. 詳細なトレース

  トレースを開始するには、 **[Enable]** (有効にする) をクリックまたはタップします。 **[Enabled Providers]** (有効なプロバイダー) ドロップダウン リストにプロバイダーが追加されます。
- **カスタム プロバイダー**:カスタムの ETW プロバイダーと、トレース レベルを選択します。 GUID を使用してプロバイダーを識別します。 GUID に角かっこは含めないでください。
- **プロバイダーを有効になっている**:これには、有効なプロバイダーが一覧表示します。 ドロップダウンからプロバイダーを選択し、 **[Disable]** (無効にする) をクリックまたはタップしてトレースを停止します。 すべてのトレースを中断するには、 **[Stop All]** (すべて停止) をクリックまたはタップします。
- **プロバイダーの履歴**:これは、現在のセッション中に有効にしていた ETW プロバイダーを表示します。 無効になっているプロバイダーをアクティブ化するには、 **[Enable]** (有効にする) をクリックまたはタップします。 履歴をクリアするには、 **[Clear]** (クリア) をクリックまたはタップします。
- **フィルター/イベント**:**イベント**セクションには、テーブル形式で選択したプロバイダーから ETW イベントが一覧表示します。 テーブルは、リアルタイムで更新されます。 使用して、**フィルター**メニューに表示されるイベントをカスタム フィルターを設定します。 をクリックして、**クリア**テーブルからすべての ETW イベントを削除するボタンをクリックします。 これによってプロバイダーが無効になることはありません。 クリックすることができます**ファイルに保存する**現在収集された ETW イベントをローカルの CSV ファイルにエクスポートします。

ETW のログ記録の使用に関する詳細については、次を参照してください。、[デバイス ポータルでのデバッグ ログを表示する](https://blogs.windows.com/buildingapps/2016/06/10/using-device-portal-to-view-debug-logs-for-uwp/)ブログの投稿。

### <a name="performance-tracing"></a>パフォーマンス トレース

パフォーマンス トレース ページで表示できます、 [Windows Performance Recorder (WPR)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh448205(v=win.10))ホスト デバイスからのトレース。

![デバイスのポータルのパフォーマンス トレースのページ](images/device-portal/mob-device-portal-perf-tracing.png)

- **使用可能なプロファイル**:ドロップダウン リスト、およびクリックまたはタップしますから WPR プロファイルを選択**開始**トレースを開始します。
- **カスタム プロファイル**:をクリックしてまたはタップします**参照**を PC から WPR プロファイルを選択します。 **[Upload and start]** (アップロードして開始) をクリックまたはタップすると、トレースが開始します。

トレースを停止するには、 **[Stop]** (停止) をクリックします。 トレース ファイルまで、このページに留まります (です。ETL) のダウンロードが完了するとします。

キャプチャされます。分析のために ETL ファイルを開くことが、 [Windows Performance Analyzer](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh448170(v=win.10))します。

### <a name="device-manager"></a>デバイス マネージャー

デバイス マネージャー ページでは、デバイスに接続されているすべての周辺機器を列挙します。 それぞれのプロパティを表示する設定アイコンをクリックできます。

![デバイスのポータルのデバイス マネージャー ページ](images/device-portal/mob-device-portal-devices.png)

### <a name="networking"></a>ネットワーク

ネットワーク ページでは、デバイス上のネットワーク接続を管理します。 USB 経由のデバイスのポータルに接続している場合を除き、これらの設定を変更する可能性がありますから切断されますをデバイスのポータルです。

- **使用可能なネットワーク**:デバイスで使用できる、WiFi ネットワークを示しています。 ネットワークをクリックまたはタップすると、そのネットワークに接続し、必要に応じてパスキーを提供できます。 デバイスのポータルは、エンタープライズ認証をまだサポートしていません。 使用することも、**プロファイル**ドロップダウンを使用して既知のデバイスに Wi-fi プロファイルのいずれかに接続しようとしています。
- **IP 構成**:アドレスの各ホスト デバイスのネットワーク ポートに関する情報を表示します。

![デバイスのポータルのネットワーク ページ](images/device-portal/mob-device-portal-network.png)

## <a name="service-features-and-notes"></a>サービスの機能と注意事項

### <a name="dns-sd"></a>DNS-SD

Device Portal は DNS-SD を使用して、ローカル ネットワーク上でその存在をアドバタイズします Device Portal のすべてのインスタンスは、デバイスの種類に関係なく、"WDP._wdp._tcp.local" でアドバタイズします。 サービス インスタンスの TXT レコードは、次の情報を提供します。

Key | 種類 | 説明
----|------|-------------
S | int | Device Portal 用のセキュリティで保護されたポート。 0 (ゼロ) の場合、Device Portal は HTTPS 接続をリッスンしていません。
D | string | デバイスの種類。 "Windows.*" の形式 (Windows.Xbox、Windows.Desktop など) になります。
A | string | デバイスのアーキテクチャ。 これは、ARM、x86、AMD64 のいずれかです。  
T | null 文字で区切られた string のリスト | ユーザーが適用したデバイスのタグ。 使い方については、タグの REST API に関する説明をご覧ください。 リストは 2 つの null で終了します。  

DNS-SD レコードでアドバタイズされる HTTP ポートですべてのデバイスがリッスンしているわけではないため、HTTPS ポートでの接続をお勧めします。

### <a name="csrf-protection-and-scripting"></a>CSRF に対する保護とスクリプト

[CSRF 攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)に対する保護のために、すべての非 GET 要求に一意のトークンが必要です。 このトークン、X-CSRF-Token 要求ヘッダーは、セッション Cookie、CSRF-Token から派生します。 Device Portal の Web UI では、CSRF-Token Cookie が、各要求の X-CSRF-Token にコピーされます。

> [!IMPORTANT]
> この保護は、(コマンド ライン ユーティリティ) などのスタンドアロン クライアントから REST Api の使用状況をできないようにします。 これは 3 つの方法で解決できます。
> - 「自動-」ユーザー名を使用します。 クライアントはユーザー名の前に "auto-" を追加することによって、CSRF に対する保護を迂回できます。 このユーザー名は、ブラウザーから Device Portal にログインするために使用しないでください。サービスが CSRF 攻撃を受ける可能性があります。 以下に例を示します。デバイスのポータルのユーザー名が"admin"の場合```curl -u auto-admin:password <args>```CSRF 保護をバイパスするために使用する必要があります。
> - クライアントで cookie-to-header スキームを実装します。 そのためには、GET 要求でセッション Cookie を確立し、それ以降のすべての要求にヘッダーと Cookie の両方を含めます。
> - 認証を無効にして、HTTP を使用します。 CSRF に対する保護は HTTPS エンドポイントにのみ適用されるため、HTTP エンドポイントに接続する場合、上記のいずれの操作も必要ありません。

#### <a name="cross-site-websocket-hijacking-cswsh-protection"></a>クロスサイト WebSocket ハイジャック (CSWSH) に対する保護

[CSWSH 攻撃](https://www.christian-schneider.net/CrossSiteWebSocketHijacking.html)を防御するために、Device Portal に対して WebSocket 接続を開くすべてのクライアントは、Host ヘッダーと一致する Origin ヘッダーも提供する必要があります。 これにより、Device Portal に対して、要求が Device Portal の UI または有効なクライアント アプリケーションからの要求であることを証明します。 Origin ヘッダーがない場合、要求は拒否されます。
