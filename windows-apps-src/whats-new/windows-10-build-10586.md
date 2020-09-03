---
title: Windows 10 ビルド 10586 の新着情報 - 2015 年 11 月
description: Windows 10 ビルド 10586 と新しい開発者ツールでは、新しいユニバーサル Windows プラットフォームによって強化されたツール、機能、エクスペリエンスを利用できます。
keywords: 機能, Windows 10, 1511, 10586
ms.date: 11/02/2017
ms.topic: article
ms.assetid: 0d6c65c5-2ad5-46c7-964e-a3a9833c94ce
ms.localizationpriority: medium
ms.openlocfilehash: 34db0115e25cb9d54ac44e3703d23edf56276264
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89172796"
---
# <a name="whats-new-in-windows-10-for-developers-build-10586"></a>Windows 10 ビルド 10586 の開発者向け新着情報

Windows 10 ビルド 10586 (November Update またはバージョン 1511 とも呼ばれます) では、Visual Studio 2019 や更新された SDK と組み合わせて使うことで、優れたユニバーサル Windows プラットフォーム アプリを作成するためのツール、機能、エクスペリエンスが利用可能になります。 Windows 10 の[ツールと SDK をインストール](https://developer.microsoft.com/windows/downloads#_blank)すると、[新しいユニバーサル Windows アプリを作成](../get-started/create-uwp-apps.md)したり、[Windows の既存のアプリ コード](../porting/index.md)がどのように使えるかを試したりすることができます。

## <a name="windows-10-build-10586---november-2015"></a>Windows 10 ビルド 10586 - 2015 年 11 月

機能 | 説明
 :---- | :----
 ユーザーの作業 | 新しい [Windows.UI.StartScreen.JumpList](/uwp/api/windows.ui.startscreen) クラスと [Windows.UI.StartScreen.JumpListItem](/uwp/api/windows.ui.startscreen) クラスを利用すると、アプリでは、アプリで使用するシステム管理ジャンプ リストの種類をプログラムで選択したり、ジャンプ リストへカスタム タスク エントリ ポイントやカスタム グループを追加することができます。
 入力 | [キーボード デリバリー インターセプター](/uwp/api/windows.ui.input.keyboarddeliveryinterceptor)。 アプリでショートカット キーやアクセス キー (またはホット キー)、アクセラレータ キー、アプリケーション キーなどの、キーボードからの生の入力のシステム プロセスを上書きしますが、Secure Attention Sequence (SAS) キーの組み合わせは除外します。 Ctrl + Alt + Del と Windows + L を含む Secure Attention Sequence (SAS) キーの組み合わせは引き続きシステムで処理されます。 <br /><br />[UWP アプリ](/uwp/api/windows.ui.core.corewindow)と[従来の Windows アプリ](/previous-versions/windows/desktop/inputmsg/messages)のポインター入力のチェーンはプロセスを超えて処理されます。 プロセス間の入力チェーンを実現する新しいポインター イベント。 <br /><br />[従来のデスクトップ アプリ用のインク プレゼンター](/previous-versions/windows/desktop/input_ink/ink-presenter)。 インク プレゼンター API では、アプリの [DirectComposition](/windows/desktop/directcomp/directcomposition-portal) ビジュアル ツリーに挿入された [InkPresenter](/uwp/api/Windows.UI.Input.Inking.InkPresenter) オブジェクトを通じて、入力、処理、インク入力 (標準と変更) の描画の Microsoft Win32 アプリによる管理を実現しています。
ネットワーク | Websocket ユーザー向け: [MessageWebSocket.OutputStream.FlushAsync](/uwp/api/windows.storage.streams.datawriter.flushasync) と [StreamWebSocket.OutputStream.FlushAsync](/uwp/api/windows.storage.streams.datawriter.flushasync) の実装がすべて完了したので、後は以前に発行された WriteAsync 呼び出しの完了を待ちます。 これにより、[FlushAsync](/uwp/api/windows.storage.streams.datawriter.flushasync) 呼び出し時に WebSocket が無効な状態にあると、既存のコードが例外をスローする場合があります。 <br /><br />新しいプロパティ [CookieUsageBehavior](/uwp/api/windows.web.http.filters.httpbaseprotocolfilter) が既存の [Windows.Web.Http.Filters.HttpBaseProtocolFilter クラス](/uwp/api/windows.web.http.filters.httpbaseprotocolfilter)に追加されました。 これにより、開発者は、システムによる Cookie の処理方法を制御できるようになります。
ORTC | Microsoft Edge に実装された [ORTC (Object Real-Time Communications)](/previous-versions//mt433097(v=vs.85)) を使用すると、ネイティブ Javascript API を通じ、ブラウザー、モバイル デバイス、サーバーの間で直接、Web の音声通話とビデオ通話をリアルタイムで行うことができます。 開発者は ORTC API と、グループ ビデオ通話、サイマルキャスト、スケーラブル ビデオ コーディング (SVC) などのサポートを使用して、Microsoft Edge ブラウザー上に高度なリアルタイム音声/ビデオ コミュニケーション アプリケーションを構築することができるようになりました。 ORTC API を使った Microsoft Edge ブラウザー間の 1 対 1 の音声/ビデオ通話のデモは、[テスト ドライブ サイトとデモ](https://developer.microsoft.com/microsoft-edge/testdrive/demos/ortcdemo)をご覧ください。
Microsoft Edge F12 開発者ツール | Microsoft Edge の F12 開発者ツールでは、[UserVoice](https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer) で最も要望の多かったいくつかの機能を含む、新しい改善点が導入されています。 DOM Explorer、コンソール、デバッガー、ネットワーク、パフォーマンス、メモリ、エミュレーション、そして新しい試験的機能ツールでは、完成間近の強力な新機能を試すことができます。 新しいツールは TypeScript で構築されており、常に実行されているため、再読み込みは必要ありません。 さらに、F12 開発者ツールのドキュメントが [Microsoft Edge デベロッパー サイト](https://developer.microsoft.com/microsoft-edge)の一部になり、[GitHub](https://github.com/MicrosoftEdge/MicrosoftEdge-Documentation) でも閲覧できるようになりました。 今後、ドキュメントはみなさんのフィードバックによって進化するだけでなく、ドキュメントの構築そのものに参加してもらえるようになります。 F12 開発者ツールに関する短いビデオによる説明は [Channel9 の One Dev Minute](https://channel9.msdn.com/Blogs/One-Dev-Minute/Microsoft-Edge-F12-tools) をご覧ください。
Windows Hello | Windows Hello は Windows システムやデバイスへの顔認証または指紋認証によるログインを実現します。 Providers API は、IHV と OEM によるコンピューター ビジョンの深度、赤外線、色のカラー カメラ (および関連するメタデータ) の UWP への取り込み、カメラによる Windows Hello の顔認証を実現します。 [Windows.Devices.Perception](/uwp/api/windows.devices.perception) 名前空間には、UWP アプリケーションからコンピューター ビジョン カメラの色、深度、赤外線データへのアクセスを実現するクライアント API が含まれています。
新しいゲーム API | 新しい Windows.Gaming.UI.GameBar クラスを使うと、ゲーム バーを表示または非表示にした時に通知を受け取ることができます。
Bluetooth API | 複数の API が追加、更新され、Bluetooth LE、デバイス列挙、および Bluetooth のその他の機能のサポートが拡張されました。 [Windows.Devices.Bluetooth](/uwp/api/windows.devices.bluetooth) 名前空間をご覧ください。
Smart Card API | 複数の SmartCardCryptogram API が [Windows.Devices.SmartCards](/uwp/api/windows.devices.smartcards) 名前空間に追加され、セキュアな暗号文支払いプロトコルがサポートされるようになりました。 ホスト カード エミュレーションを使って「タップして支払い」をサポートする支払いアプリでは、これらの API を使ってセキュリティとパフォーマンスを強化できます。 アプリでキーを作成して、TPM を使って使用制限のあるトランザクション キーを保護します。 また、NGC (Next Generation Credentials) フレームワークを活用してユーザーの PIN のキーを保護します。 これらの API は暗号文の生成をシステムに委任することでパフォーマンスが向上します。 これにより、他のアプリからのキーと暗号文へのあらゆるアクセスを防止することができます。
Updated Storage API | [Windows.Storage.DownloadsFolder クラス](/uwp/api/windows.storage.downloadsfolder)では、特定の[ユーザー](/uwp/api/windows.system.user)のダウンロード フォルダーに[ファイルを作成](/uwp/api/windows.storage.downloadsfolder.createfileforuserasync)したり、[フォルダーを作成](/uwp/api/windows.storage.downloadsfolder.createfolderforuserasync)したりできるようになりました。 [Windows.Storage.StorageLibrary クラス](/uwp/api/windows.storage.storagelibrary)では、特定の[ユーザー](/uwp/api/windows.system.user)の[特定のライブラリを取得](/uwp/api/windows.storage.storagelibrary.getlibraryforuserasync)できるようになりました。
Windows アプリ認定キット | Windows アプリ認定キットが更新され、テストも改善されました。 更新のリストについては、[Windows アプリ認定キット](https://developer.microsoft.com/windows/develop/app-certification-kit)のページをご覧ください。
デザインに関するダウンロード | Adobe Photoshop 用の新しい UWP アプリ デザイン テンプレートをご覧ください。 Microsoft PowerPoint と Adobe Illustrator のテンプレートも更新され、ガイドラインの PDF 版も利用可能になりました。 [デザインに関するダウンロードのページをご覧ください](../design/downloads/index.md)。