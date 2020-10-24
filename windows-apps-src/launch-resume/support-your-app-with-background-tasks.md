---
title: バックグラウンド タスクによるアプリのサポート
description: このセクションの各トピックでは、トリガーに対応して軽量コードをバックグラウンドで実行する方法について説明します。
ms.assetid: EFF7CBFB-D309-4ACB-A2A5-28E19D447E32
ms.date: 08/21/2017
ms.topic: article
keywords: windows 10、uwp、バックグラウンドタスク
ms.localizationpriority: medium
ms.openlocfilehash: ac3a20afc75cc7a6cf3c9f874fa26e1b6387dd89
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89171846"
---
# <a name="support-your-app-with-background-tasks"></a>バックグラウンド タスクによるアプリのサポート


このセクションの各トピックでは、トリガーに対応して軽量コードをバックグラウンドで実行する方法について説明します。 バックグラウンド タスクを使えば、アプリが中断されている、または実行されていないときに機能を提供できます。 また、VOIP、メール、IM などのリアルタイム通信アプリにバックグラウンド タスクを使うこともできます。

## <a name="playing-media-in-the-background"></a>バックグラウンドでのメディア再生

Windows 10 バージョン 1607 以降では、バックグラウンドでのオーディオ再生がより簡単になりました。 詳しくは、「[バックグラウンドでのメディアの再生](../audio-video-camera/background-audio.md)」をご覧ください。

## <a name="in-process-and-out-of-process-background-tasks"></a>インプロセスとアウトプロセスのバックグラウンド タスク

バックグラウンド タスクを実装するにあたっては、2 つのアプローチがあります。

* インプロセス: アプリとそのバックグラウンド プロセスが同じプロセスで実行されます。
* アウトプロセス: アプリとバックグラウンド プロセスが個別のプロセスで実行されます。

インプロセス バックグラウンドのサポートは、バックグラウンド タスクの書き込みを簡略化するために、Windows 10 バージョン 1607 で導入されました。 ただし現在でも、アウトプロセスのバックグラウンド タスクを書き込むことはできます。 インプロセスのバックグラウンド タスクとアウトプロセスのバックグラウンド タスクの使い分けに関する推奨事項については、「[バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)」をご覧ください。

アウトプロセスのバックグラウンド タスクを使用すると、問題が発生した際にバックグラウンド プロセスによってアプリのプロセスがダウンすることがないので、より回復性が高くなります。 ただし、回復性が高くなる代わりに、アプリとバックグラウンド タスクの間のプロセス間通信の管理がより複雑になります。

アウトプロセスのバックグラウンド タスクは、OS が個別のプロセス (backgroundtaskhost.exe) 内で実行する、[**IBackgroundTask**](/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask) インターフェイスを実装した軽量クラスとして実装されます。 バックグラウンド タスクは [**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) クラスを使用して登録します。 このクラス名は、バックグラウンド タスクの登録時にエントリ ポイントとして指定するために使われます。

Windows 10 バージョン 1607 では、バックグラウンド タスクを作成しなくても、バックグラウンド アクティビティを有効にできます。 フォアグラウンド アプリケーションのプロセス内で、バックグラウンド コードを直接実行できます。

インプロセス バックグラウンド タスクの概要については、「[インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)」をご覧ください。

アウトプロセス バックグラウンド タスクの概要については、「[アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)」をご覧ください。

> [!TIP]
> Windows 10 以降では、バックグラウンド タスクを登録するための前提要件として、アプリをロック画面に配置する必要がなくなりました。

## <a name="background-tasks-for-system-events"></a>システム イベントに対するバックグラウンド タスク

アプリでは、[**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTrigger) クラスを使ってバックグラウンド タスクを登録することにより、システムで生成されたイベントに応答することができます。 アプリは、次のシステム イベント トリガー ([**SystemTriggerType**](/uwp/api/Windows.ApplicationModel.Background.SystemTriggerType) で定義されている) を使うことができます。

| トリガー名                     | 説明                                                                                                    |
|----------------------------------|----------------------------------------------------------------------------------------------------------------|
| **InternetAvailable**            | インターネットが利用可能になります。                                                                                |
| **NetworkStateChange**           | コストや接続の変更などネットワークの変更が行われます。                                              |
| **OnlineIdConnectedStateChange** | アカウントに関連付けられたオンライン ID が変更されます。                                                                 |
| **SmsReceived**                  | インストールされたモバイル ブロードバンド デバイスにより、新しい SMS メッセージが受け取られます。                                         |
| **TimeZoneChange**               | デバイスでタイム ゾーンが変更されます (たとえば、システムが夏時間に合わせて時刻を調整したとき)。 |

詳細については、「 [バックグラウンドタスクによるシステムイベントへの応答](respond-to-system-events-with-background-tasks.md)」を参照してください。

## <a name="conditions-for-background-tasks"></a>バックグラウンド タスクの条件

条件を追加すると、バックグラウンド タスクがトリガーされた後でも、バックグラウンド タスクを実行するタイミングを制御することができます。 バックグラウンド タスクは、トリガーされても、条件がすべて満たされるまで実行されません。 次の条件 ([**SystemConditionType**](/uwp/api/Windows.ApplicationModel.Background.SystemConditionType) 列挙型で表されます) を使うことができます。

| [条件名]           | 説明                       |
|--------------------------|-----------------------------------|
| **InternetAvailable**    | インターネットが利用可能である必要があります。   |
| **InternetNotAvailable** | インターネットが利用不可である必要があります。 |
| **SessionConnected**     | セッションが接続されている必要があります。    |
| **SessionDisconnected**  | セッションが切断されている必要があります。 |
| **UserNotPresent**       | ユーザーが不在である必要があります。            |
| **UserPresent**          | ユーザーが在席している必要があります。         |

バックグラウンド タスク [BackgroundTaskBuilder.AddCondition](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) に **InternetAvailable** 条件を追加して、ネットワーク スタックが実行されるまで、バックグラウンド タスクのトリガーを遅らせます。 この条件では、ネットワークが利用可能になるまでバックグラウンド タスクが実行されないため、電力が節約されます。 この条件では、リアルタイムのアクティブ化は行われません。

バックグラウンド タスクでネットワーク接続が必要である場合は、[IsNetworkRequested](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) を設定すると、バックグラウンド タスクが実行されている間、ネットワークは稼働状態のままになります。 これによって、デバイスがコネクト スタンバイ モードに入っている場合でも、タスクの実行中はネットワークを稼働状態に保つようにバックグラウンド タスク インフラストラクチャに指示されます。 バックグラウンドタスクで **Isnetworkrequested**が設定されていない場合、スタンバイモード (電話の画面がオフになっている場合など) では、バックグラウンドタスクがネットワークにアクセスできなくなります。  
バックグラウンド タスクの条件について詳しくは、「[バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)」をご覧ください。

## <a name="application-manifest-requirements"></a>アプリケーション マニフェストの要件

アウトプロセスを実行するバックグラウンド タスクをアプリに正常に登録するには、バックグラウンド タスクをアプリケーション マニフェストで宣言する必要があります。 ホスト アプリと同じプロセスで実行されるバックグラウンド タスクについては、アプリケーション マニフェストで宣言する必要はありません。 詳しくは、「[アプリケーション マニフェストでのバックグラウンド タスクの宣言](declare-background-tasks-in-the-application-manifest.md)」をご覧ください。

## <a name="background-tasks"></a>バックグラウンド タスク

次のリアルタイム トリガーを使うと、バックグラウンドで軽量なカスタム コードを実行できます。

| リアルタイム トリガー  | 説明 |
|--------------------|-------------|
| **コントロールチャネル** | バックグラウンド タスクでは、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) を使って接続が有効な状態を維持し、コントロール チャネルでメッセージを受け取ることができます。 アプリがソケットをリッスンしている場合は、**ControlChannelTrigger** の代わりにソケット ブローカーを使うことができます。 ソケット ブローカーの使用について詳しくは、「[SocketActivityTrigger](/uwp/api/Windows.ApplicationModel.Background.SocketActivityTrigger)」をご覧ください。 **ControlChannelTrigger** は、Windows Phone ではサポートされていません。 |
| **Timer** | バックグラウンド タスクは、15 分おきに実行できます。また、[**TimeTrigger**](/uwp/api/Windows.ApplicationModel.Background.TimeTrigger) を使って特定の時刻に実行するように設定することもできます。 詳しくは、「[タイマーでのバックグラウンド タスクの実行](run-a-background-task-on-a-timer-.md)」をご覧ください。 |
| **プッシュ通知** | バックグラウンド タスクは、[**PushNotificationTrigger**](/uwp/api/Windows.ApplicationModel.Background.PushNotificationTrigger) に応答して、直接プッシュ通知を受け取ります。 |

**注**  

ユニバーサル Windows アプリは、どの種類のバックグラウンド トリガーを登録する場合でも、先に [**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出す必要があります。

更新プログラムのリリース後にユニバーサル Windows アプリが引き続き適切に実行されるようにするには、更新後にアプリが起動する際に、[**RemoveAccess**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess)、[**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) の順に呼び出します。 詳しくは、「[バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)」をご覧ください。

**トリガー インスタンスの数の制限:** アプリが登録できる一部のトリガー インスタンスの数には制限があります。 アプリが [ApplicationTrigger](/uwp/api/Windows.ApplicationModel.Background.ApplicationTrigger)、[MediaProcessingTrigger](/uwp/api/windows.applicationmodel.background.mediaprocessingtrigger)、および [DeviceUseTrigger](/uwp/api/windows.applicationmodel.background.deviceusetrigger?f=255&MSPPError=-2147217396) を登録できるのは、アプリのインスタンスごとに 1 回のみです。 アプリでこの制限を超えると、登録で例外がスローされます。

## <a name="system-event-triggers"></a>システム イベント トリガー

[**SystemTriggerType**](/uwp/api/Windows.ApplicationModel.Background.SystemTriggerType) 列挙体は、次のシステム イベント トリガーを表します。

| トリガー名            | 説明                                                       |
|-------------------------|-------------------------------------------------------------------|
| **UserPresent**         | ユーザーが在席になったら、バックグラウンド タスクがトリガーされます。   |
| **UserAway**            | ユーザーが不在になったら、バックグラウンド タスクがトリガーされます。    |
| **ControlChannelReset** | コントロール チャネルがリセットされたら、バックグラウンド タスクがトリガーされます。 |
| **SessionConnected**    | セッションが接続されたら、バックグラウンド タスクがトリガーされます。   |

   
以下のシステム イベント トリガーは、ユーザーがアプリをロック画面に配置した場合や、アプリをロック画面から削除した場合に、そのことを通知します。

| トリガー名                     | 説明                                  |
|----------------------------------|----------------------------------------------|
| **LockScreenApplicationAdded**   | アプリのタイルがロック画面に追加されます。     |
| **LockScreenApplicationRemoved** | アプリのタイルがロック画面から削除されます。 |

 
## <a name="background-task-resource-constraints"></a>バックグラウンド タスク リソースの制限

バックグラウンド タスクは軽量です。 バックグラウンドの実行を最小限に抑えることにより、フォアグラウンド アプリでの最適なユーザー エクスペリエンスとバッテリ寿命が保証されます。 この設定は、リソース制約をバックグラウンド タスクに適用することにより、強制的に適用されます。

バックグラウンド タスクに使用できる時間は、ウォールクロック時間で 30 秒間に制限されています。

### <a name="memory-constraints"></a>メモリの制限

リソースには制約があるため (特にメモリの少ないデバイスの場合)、バックグラウンド タスクにはメモリの制限が存在する場合があり、これによってバックグラウンド タスクが使うことができるメモリの最大容量が決まります。 バックグラウンド タスクがこの制限を超過する操作を試行すると、操作は失敗し、タスクで処理できるメモリ不足例外が生成されることがあります。 メモリ不足例外がタスクで処理されない場合や、試行された操作がメモリ不足例外を生じさせる性質のものではなかった場合は、タスクが直ちに終了されます。  

上限 (あれば) を検出し、進行中のバックグラウンド タスクのメモリ使用量を監視するには、[**MemoryManager**](/uwp/api/Windows.System.MemoryManager) API を使って、現在のメモリ使用量と制限を問い合わせることができます。

### <a name="per-device-limit-for-apps-with-background-tasks-for-low-memory-devices"></a>メモリの少ないデバイスにおけるバックグラウンド タスクのあるアプリのデバイスごとの制限

メモリに制約のあるデバイスでは、デバイスにインストールでき、いつでもバックグラウンド タスクを使うことができるアプリの数に制限があります。 この数を超えると、すべてのバックグラウンド タスクを登録するのに必要な [**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) の呼び出しが失敗します。

### <a name="battery-saver"></a>バッテリー節約機能

バッテリー節約機能が有効であってもバックグラウンド タスクを実行しプッシュ通知を受信するようにアプリを設定していない限り、デバイスが外部電源に接続されていない状態でバッテリー残量が指定量を下回ると、バッテリー節約機能 (有効な場合) によりバックグラウンド タスクが実行されなくなります。 これによりバックグラウンド タスクを登録できなくなることはありません。

ただし、エンタープライズアプリと、Microsoft Store で公開されないアプリについては、「バックグラウンド [で無期限に実行](run-in-the-background-indefinetly.md) する」を参照して、バックグラウンドタスクまたは拡張実行セッションをバックグラウンドで無期限に実行する機能の使用方法を学習してください。

## <a name="background-task-resource-guarantees-for-real-time-communication"></a>リアルタイム通信に対するバックグラウンド タスク リソース保証

リソース クォータがリアルタイム通信機能に干渉することがないように、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) と [**PushNotificationTrigger**](/uwp/api/Windows.ApplicationModel.Background.PushNotificationTrigger) を使ったバックグラウンド タスクごとに CPU リソース保証クォータが確保されます。 リソース クォータは、先ほど説明したように、これらのバックグラウンド タスクに対して一定のままです。

アプリでは、特に何も行わなくても、[**ControlChannelTrigger**](/uwp/api/Windows.Networking.Sockets.ControlChannelTrigger) と [**PushNotificationTrigger**](/uwp/api/Windows.ApplicationModel.Background.PushNotificationTrigger) を使ったバックグラウンド タスクごとにリソース保証クォータが確保されます。 システムは、これらのタスクを常に重要なバックグラウンド タスクとして扱います。

## <a name="maintenance-trigger"></a>メンテナンス トリガー

メンテナンス タスクは、デバイスが AC 電源に接続されているときにだけ実行されます。 詳しくは、「[メンテナンス トリガーの使用](use-a-maintenance-trigger.md)」をご覧ください。

## <a name="background-tasks-for-sensors-and-devices"></a>センサーとデバイスのバックグラウンド タスク

アプリでは、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) クラスによりバックグラウンド タスクからセンサーと周辺デバイスにアクセスできます。 このトリガーは、データの同期や監視など長期間にわたる操作に使用できます。 システム イベントのタスクとは異なり、**DeviceUseTrigger** タスクは、アプリがフォアグラウンドで実行されており条件が設定されていない場合にのみトリガーできます。

> [!IMPORTANT]
> **DeviceUseTrigger** と **DeviceServicingTrigger** は、インプロセスのバックグラウンド タスクでは使用できません。

時間がかかるファームウェア更新など、一部の重要なデバイス操作は、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) では実行できません。 このような操作は PC でのみ、[**DeviceServicingTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger) を使う特権アプリによってのみ実行できます。 *特権アプリ*とは、これらの操作を実行する権限をデバイス製造元から与えられているアプリです。 デバイス メタデータを使って、どのアプリがデバイスの特権アプリであるか (存在する場合) を指定します。 詳細については、「[デバイスの同期と Microsoft Store デバイスアプリの更新プログラム](/windows-hardware/drivers/devapps/device-sync-and-update-for-uwp-device-apps)」を参照してください。

## <a name="managing-background-tasks"></a>バックグラウンド タスクの管理

バックグラウンド タスクは、イベントとローカル ストレージを使って進行状況、完了、キャンセルをアプリに報告できます。 アプリは、バックグラウンド タスクがスローした例外をキャッチしたり、アプリの更新中にバックグラウンド タスクの登録を行うこともできます。 詳細については、

[取り消されたバックグラウンド タスクの処理](handle-a-cancelled-background-task.md)  
[バックグラウンド タスクの進捗状況と完了の監視](monitor-background-task-progress-and-completion.md)

アプリの起動中に、バックグラウンド タスクの登録を確認します。 アプリのグループ化されていないバックグラウンド タスクが BackgroundTaskBuilder.AllTasks に存在することを確認します。 存在しないものを再登録します。 不要になったタスクの登録を解除します。 これにより、アプリを起動するたびに、すべてのバックグラウンド タスクの登録が最新の状態になります。

## <a name="related-topics"></a>関連トピック

**Windows 10 におけるマルチタスクの概念的ガイダンス**

* [Launching, resuming, and multitasking](index.md)

**関連するバックグラウンド タスクのガイダンス**

* [バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)
* [バックグラウンド タスクからのセンサーやデバイスへのアクセス](access-sensors-and-devices-from-a-background-task.md)
* [インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)
* [アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)
* [アウトプロセスのバックグラウンド タスクをインプロセスのバックグラウンド タスクへ変換](convert-out-of-process-background-task.md)
* [バックグラウンド タスクのデバッグ](debug-a-background-task.md)
* [アプリケーション マニフェストでのバックグラウンド タスクの宣言](declare-background-tasks-in-the-application-manifest.md)
* [バックグラウンド タスクの登録のグループ化](group-background-tasks.md)
* [取り消されたバックグラウンド タスクの処理](handle-a-cancelled-background-task.md)
* [UWP アプリで一時停止イベント、再開イベント、バックグラウンド イベントをトリガーする方法 (デバッグ時)](/visualstudio/debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio)
* [バックグラウンド タスクの進捗状況と完了の監視](monitor-background-task-progress-and-completion.md)
* [バックグラウンドでのメディアの再生](../audio-video-camera/background-audio.md)
* [バックグラウンド タスクの登録](register-a-background-task.md)
* [バックグラウンド タスクによるシステム イベントへの応答](respond-to-system-events-with-background-tasks.md)
* [タイマーでのバックグラウンド タスクの実行](run-a-background-task-on-a-timer-.md)
* [UWP アプリが更新された際のバックグラウンド タスクの実行](run-a-background-task-during-updatetask.md)
* [バックグラウンドで無期限に実行する](run-in-the-background-indefinetly.md)
* [バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)
* [アプリ内からのバックグラウンド タスクのトリガー](trigger-background-task-from-app.md)
* [バックグラウンド タスクのライブ タイルの更新](update-a-live-tile-from-a-background-task.md)
* [メンテナンス トリガーの使用](use-a-maintenance-trigger.md)