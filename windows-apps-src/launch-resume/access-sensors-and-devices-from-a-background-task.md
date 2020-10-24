---
title: バックグラウンド タスクからのセンサーやデバイスへのアクセス
description: DeviceUseTrigger を使うと、フォアグラウンド アプリが中断しているときにも、バックグラウンドでユニバーサル Windows アプリからセンサーや周辺機器にアクセスできます。
ms.assetid: B540200D-9FF2-49AF-A224-50877705156B
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10、uwp、バックグラウンドタスク
ms.localizationpriority: medium
ms.openlocfilehash: 1939766c2fbb215980143c33f82bca669dc4df0e
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89167936"
---
# <a name="access-sensors-and-devices-from-a-background-task"></a>バックグラウンド タスクからのセンサーやデバイスへのアクセス




[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) を使うと、フォアグラウンド アプリが中断しているときにも、バックグラウンドでユニバーサル Windows アプリからセンサーや周辺機器にアクセスできます。 たとえば、アプリが実行されている場所によっては、バックグラウンド タスクを使ってデバイスまたはモニターのセンサーとデータを同期することができます。 バッテリ残量を維持し、適切なユーザーの同意を得るために、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) の使用にはこのトピックで説明するポリシーが適用されます。

バックグラウンドでセンサーまたは周辺機器にアクセスするには、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) を使うバックグラウンド タスクを作成します。 PC でこれを実行する方法を示す例については、[カスタム USB デバイスのサンプルに関するページ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomUsbDeviceAccess) をご覧ください。 電話の例は、[バックグラウンド センサーのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BackgroundSensors) に関するページをご覧ください。

> [!Important]
> **DeviceUseTrigger** は、インプロセスのバックグラウンド タスクで使うことはできません。 このトピックの情報は、アウトプロセスで実行されるバックグラウンド タスクにのみ当てはまります。

## <a name="device-background-task-overview"></a>デバイス バックグラウンド タスクの概要

アプリがユーザーに表示されなくなると、Windows はメモリと CPU リソースを解放するためにそのアプリを中断または終了します。 こうすることで、他のアプリがフォアグラウンドで実行できるようにし、バッテリの消費量を減らします。 このとき、バックグラウンド タスクの助けがないと、進行中のデータ イベントが失われます。 Windows には、バックグラウンド タスク トリガー [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) があり、アプリが中断状態になっても、各種のデバイスやセンサーでの時間のかかる同期操作や監視操作をバックグラウンドで安全に実行できるようにします。 アプリのライフサイクルについて詳しくは、「[起動、再開、バックグラウンド タスク](index.md)」をご覧ください。 バックグラウンド タスクについて詳しくは、「[バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)」をご覧ください。

**メモ**   ユニバーサル Windows アプリでは、バックグラウンドでデバイスを同期するには、ユーザーがアプリによるバックグラウンド同期を承認している必要があります。 さらに、デバイスを PC に接続して I/O をアクティブにし、最長 10 分のバックグラウンド処理を実行できるようにする必要があります。 ポリシーの適用については、このトピックの後半で詳しく説明します。

### <a name="limitation-critical-device-operations"></a>制限: 重要なデバイス操作

時間がかかるファームウェア更新など、一部の重要なデバイス操作は、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) では実行できません。 このような操作は PC でのみ、[**DeviceServicingTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceServicingTrigger) を使う特権アプリによってのみ実行できます。 *特権アプリ*とは、これらの操作を実行する権限をデバイス製造元から与えられているアプリです。 デバイス メタデータを使って、どのアプリがデバイスの特権アプリであるか (存在する場合) を指定します。 詳しくは、「[Microsoft Store デバイス アプリによるデバイスの同期と更新](/windows-hardware/drivers/devapps/device-sync-and-update-for-uwp-device-apps)」をご覧ください。

## <a name="protocolsapis-supported-in-a-deviceusetrigger-background-task"></a>DeviceUseTrigger バックグラウンド タスクでサポートされているプロトコル/API

[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) を使うバックグラウンド タスクは、システム トリガーのバックグラウンド タスクでサポートされない多くの API またはプロトコルを使うやり取りを、アプリでできるようにします。 ユニバーサル Windows アプリでは、次のプロトコルがサポートされます。

| プロトコル         | ユニバーサル Windows アプリの DeviceUseTrigger                                                                                                                                                    |
|------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| USB              | ![このプロトコルはサポートされています。](images/ap-tools.png)                                                                                                                                            |
| HID              | ![このプロトコルはサポートされています。](images/ap-tools.png)                                                                                                                                            |
| Bluetooth RFCOMM | ![このプロトコルはサポートされています。](images/ap-tools.png)                                                                                                                                            |
| Bluetooth GATT   | ![このプロトコルはサポートされています。](images/ap-tools.png)                                                                                                                                            |
| MTP              | ![このプロトコルはサポートされています。](images/ap-tools.png)                                                                                                                                            |
| ネットワーク (有線)    | ![このプロトコルはサポートされています。](images/ap-tools.png)                                                                                                                                            |
| ネットワーク (Wi-Fi)    | ![このプロトコルはサポートされています。](images/ap-tools.png)                                                                                                                                            |
| IDeviceIOControl | ![DeviceServicingTrigger でサポートされています。](images/ap-tools.png)                                                                                                                       |
| センサー API      | ![deviceservicingtrigger はユニバーサルセンサー api ](images/ap-tools.png) をサポートしています ( [ユニバーサルデバイスファミリ](../get-started/universal-application-platform-guide.md)のセンサーに限定) |

## <a name="registering-background-tasks-in-the-app-package-manifest"></a>バックグラウンド タスクをアプリ パッケージ マニフェストに登録する

アプリは、バックグランド タスクの一部として動作するコードで同期操作と更新操作を実行します。 このコードは、[**IBackgroundTask**](/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask) を実装する Windows ランタイム クラス (または JavaScript アプリ専用の JavaScript ページ) に埋め込まれます。 [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクを使用するには、システム トリガーのバックグラウンド タスクと同じように、フォアグラウンド アプリのマニフェスト ファイルでそれを宣言する必要があります。

この例のアプリ パッケージ マニフェスト ファイルでは、**DeviceLibrary.SyncContent** が、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) を使うバックグラウンド タスクのエントリ ポイントとなります。

```xml
<Extensions>
  <Extension Category="windows.backgroundTasks" EntryPoint="DeviceLibrary.SyncContent">
    <BackgroundTasks>
      <m2:Task Type="deviceUse" />
    </BackgroundTasks>
  </Extension>
</Extensions>
```

## <a name="introduction-to-using-deviceusetrigger"></a>DeviceUseTrigger の使用について

[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) を使うには、次の基本的な手順を実行します。 バックグラウンド タスクについて詳しくは、「[バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)」をご覧ください。

1.  アプリ マニフェストにバックグラウンド タスクを登録し、IBackgroundTask を実装する Windows ランタイム クラスまたは JavaScript アプリ専用の JavaScript ページにバックグラウンド タスク コードを埋め込みます。
2.  アプリが起動されると、タイプ [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) のトリガー オブジェクトを作成および構成し、後で使用できるようにトリガー インスタンスを格納します。
3.  バックグラウンド タスクが前に登録されているかどうかをチェックし、登録されていない場合は、トリガーに対してバックグラウンド タスクを登録します。 このトリガーに関連付けられているタスクには条件を設定できないことに注意してください。
4.  アプリからバックグラウンド タスクをトリガーする必要がある場合は、最初に [**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出して、アプリがバックグラウンド タスクを要求できるかどうかを確認する必要があります。
5.  バックグラウンド タスクを要求できる場合は、デバイス トリガー オブジェクトの [**RequestAsync**](/uwp/api/windows.applicationmodel.background.deviceusetrigger.requestasync) アクティブ化メソッドを呼び出します。
6.  バックグラウンド タスクは、(CPU 時間が割り当てられない) 他のシステム バックグラウンド タスクのように抑制されません。ただし、フォアグラウンド アプリの応答性を維持するため、低い優先順位で実行されます。
7.  次に Windows は、トリガー タイプに応じて、必要なポリシー (バックラウンド タスクを開始する前にユーザーの許可を得るなど) に準拠しているかどうかを検証します。
8.  Windows はシステム条件とタスクの実行時間を監視し、必要な条件を満たさなくなった場合はタスクを中止します。
9.  バックグラウンド タスクが進捗状況や完了を報告する際、登録タスクの進捗状況イベントまたは完了イベントとしてアプリに渡されます。

**重要**   [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger)を使用する場合は、次の重要な点を考慮してください。

-   [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) を使うバックグラウンド タスクをプログラムから実行する機能は、Windows 8.1 と Windows Phone 8.1 に初めて導入されたものです。

-   PC で周辺機器を更新するとき、ユーザーの許可を得るためのポリシーが Windows によって適用されます。

-   周辺機器を同期および更新する際、バッテリ残量を維持するためのポリシーも適用されます。

-   最大バックグラウンド時間 (実時間) など、所定のポリシー要件を満たさなくなった場合、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) を使用するバクグラウンド タスクが Windows によって中止される可能性があります。 バックグラウンド タスクを使って周辺機器を操作するときは、これらのポリシー要件を考慮する必要があります。

**ヒント**   これらのバックグラウンドタスクがどのように機能するかを確認するには、サンプルをダウンロードしてください。 PC でこれを実行する方法を示す例については、[カスタム USB デバイスのサンプルに関するページ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomUsbDeviceAccess) をご覧ください。 電話の例は、[バックグラウンド センサーのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BackgroundSensors) に関するページをご覧ください。
 
## <a name="frequency-and-foreground-restrictions"></a>頻度とフォアグランドの制限

アプリが操作を実行する頻度に制限はありません。ただし、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスク操作は一度に 1 つしか実行できません (他の種類のバックグラウンド タスクには影響しません)。また、バックグラウンド タスクを開始できるのは、アプリがフォアグラウンドで動作しているときだけです。 アプリがフォアグラウンドにない場合は、**DeviceUseTrigger** を使うバックグラウンド タスクを開始することはできません。 実行中のバックグラウンド タスクが完了した後でなければ、次の **DeviceUseTrigger** バックグラウンド タスクを開始できません。

## <a name="device-restrictions"></a>デバイスの制限

各アプリは [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクの登録と実行は 1 つのみに制限されていますが、(アプリが実行される) デバイスでは、複数のアプリに複数の **DeviceUseTrigger** バックグラウンド タスクの登録と実行が許可されている場合があります。 デバイスによっては、すべてのアプリの **DeviceUseTrigger** バックグラウンド タスクの合計数に制限があります。 これにより、リソースに制約のあるデバイスでバッテリを節約できます。 詳しくは、次の表をご覧ください。

1 つの [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクから、アプリは周辺機器またはセンサーに数の制限なくアクセスできます。唯一の制限は、前の表に記載されているサポートされるプロトコルと API によるものです。

## <a name="background-task-policies"></a>バックグラウンド タスクのポリシー

アプリが [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクを使うときは Windows のポリシーが適用されます。 これらのポリシーが満たされない場合は、バックグラウンド タスクが中止される場合があります。 このようなバックグラウンド タスクを使ってデバイスやセンサーを操作するときは、これらのポリシー要件を考慮する必要があります。

### <a name="task-initiation-policies"></a>タスク開始のポリシー

次の表は、ユニバーサル Windows アプリに適用されるタスク開始ポリシーを示しています。

| ポリシー | ユニバーサル Windows アプリの DeviceUseTrigger |
|--------|---------------------------------------------|
| バックグラウンド タスクを開始するとき、アプリがフォアグラウンドで動作している。 | ![ポリシーが適用される](images/ap-tools.png) |
| 対象デバイスがシステムに接続されている (ワイヤレス デバイスの場合は、接続範囲内にある)。 | ![ポリシーが適用される](images/ap-tools.png) |
| サポートされているデバイスの周辺機器用 API (USB、HID、Bluetooth、センサーなどでは Windows ランタイム API) を使って、アプリが対象デバイスにアクセスできる。 アプリがデバイスまたはセンサーにアクセスできない場合、バックグラウンド タスクへのアクセスが拒否されます。 | ![ポリシーが適用される](images/ap-tools.png) |
| アプリで指定されているバックグラウンド タスクのエントリ ポイントがアプリ パッケージ マニフェストに登録されている。 | ![ポリシーが適用される](images/ap-tools.png) |
| アプリごとに [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクが 1 つのみ実行されている。 | ![ポリシーが適用される](images/ap-tools.png) |
| (アプリが実行されている) デバイスの [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクの最大数に達していない。 | **デスクトップデバイスファミリ**: 一度に登録して実行できるタスクの数に制限はありません。 **モバイルデバイスファミリ**: 1 タスク 512 MB デバイスそれ以外の場合、2つのタスクを同時に登録して実行できます。 |
| サポートされている API とプロトコルを使う場合は、アプリが 1 つの [DeviceUseTrigger](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクからアクセスできる周辺機器またはセンサーの最大数。 | 無制限 |
| バックグラウンド タスクは、400 ミリ秒の CPU 時間を、画面がロックされている場合は 1 分ごとに消費し (1 GHz CPU の場合)、画面がロックされていない場合は 5 分ごとに消費する。 このポリシーを満たさない場合、タスクが取り消される可能性があります。 | ![ポリシーが適用される](images/ap-tools.png) |

### <a name="runtime-policy-checks"></a>実行時のポリシー チェック

タスクがバックグラウンドで実行されるとき、Windows によって次の実行時ポリシー要件が適用されます。 いずれかの実行時要件が満たされなくなった時点で、デバイス バックグラウンド タスクが中止されます。

次の表は、ユニバーサル Windows アプリに適用される実行時ポリシーを示しています。

| ポリシー チェック | ユニバーサル Windows アプリの DeviceUseTrigger |
|--------------|:-------------------------------------------:|
| 対象デバイスがシステムに接続されている (ワイヤレス デバイスの場合は、接続範囲内にある)。 | ![ポリシー チェックが適用される](images/ap-tools.png) |
| デバイスに対して標準的な I/O を実行する (5 秒ごとに 1 I/O)。 | ![ポリシー チェックが適用される](images/ap-tools.png) |
| アプリがタスクを中止していない。 | ![ポリシー チェックが適用される](images/ap-tools.png) |
| 実時間の制限 (アプリがバックグラウンドでタスクを実行できる最長時間)。 | **デスクトップデバイスファミリ**:10 分。 **モバイル デバイス ファミリ** : 時間制限なし。 リソースを節約するには、同時に実行できるタスクを 1 つか 2 つに制限。 |
| アプリが終了していない。 | ![ポリシー チェックが適用される](images/ap-tools.png) |

## <a name="best-practices"></a>ベスト プラクティス

[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクを使うアプリのベスト プラクティスを次に示します。

### <a name="programming-a-background-task"></a>バックグラウンド タスクのプログラミング

アプリで [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクを使うと、ユーザーがアプリを切り替え、フォアグラウンド アプリが Windows によって中断状態になったとき、フォアグラウンド アプリで開始された同期操作や監視操作をバックグラウンドに引き継ぐことができます。 このモデルに従って、バックグラウンド タスクを登録、実行、登録解除することをお勧めします。

1.  [**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出して、アプリがバックグラウンド タスクを要求できるかどうかを確認します。 この手順は、バックグラウンド タスクを登録する前に実行する必要があります。

2.  トリガーを要求する前にバックグランド タスクを登録します。

3.  進捗状況と完了のイベント ハンドラーをトリガーに関連付けます。 アプリが中断状態から復帰すると、待機中の進捗イベントまたは完了イベントが渡されます。アプリはこれらのイベントを使用して、バックグラウンド タスクの状態を判断します。

4.  [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクを開始するときは、オープンしているデバイスまたはセンサー オブジェクトを閉じます。それらのデバイスまたはセンサーが解放され、バックグラウンド タスクで使用できるようになります。

5.  トリガーを登録します。

6.  バックグラウンド タスクからデバイスまたはファイルにアクセスすることでバッテリに与える影響について、慎重に検討します。 たとえば、センサーのレポート間隔を頻繁に設定しすぎると、電話のバッテリをすぐに消費するほど頻繁にタスクを実行することになります。

7.  バックグラウンド タスクが完了したら、登録を解除します。

8.  バックグラウンド タスク クラスの中止イベントを登録します。 中止イベントを登録しておけば、Windows またはフォアグラウンド アプリによってバックグランド タスクが中止されたとき、バックグラウンド タスクコードからそのタスクを適切に中止できます。

9.  アプリが (中断状態ではなく) 終了した時点で登録を解除し、実行中のタスクを中止します (タスクが不要な場合)。 メモリの少ない電話などリソースに制約のあるシステムでは、この手順を実行することで、他のアプリが [**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクを使えるようになります。

    -   アプリが終了したら、登録を解除して実行中のタスクを中止します。

    -   アプリが終了すると、バックグラウンド タスクが取り消され、既存のイベント ハンドラーが既存のバックグラウンド タスクから切断されます。 これによって、バックグラウンド タスクの状態を判断できなくなります。 バックグラウンド タスクを登録解除して取り消すことで、キャンセル コードがバックグランド タスクを適切に中止できます。

### <a name="cancelling-a-background-task"></a>バックグラウンド タスクの中止

フォアグラウンド アプリからバックグラウンドで実行中のタスクを中止するには、[**DeviceUseTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceUseTrigger) バックグラウンド タスクを登録するためにアプリで使っている [**BackgroundTaskRegistration**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration) オブジェクトの Unregister メソッドを使います。 **BackgroundTaskRegistration** の [**Unregister**](/uwp/api/windows.applicationmodel.background.backgroundtaskregistration.unregister) メソッドを使ってバックグラウンド タスクを登録解除すると、バックグラウンド タスク インフラストラクチャによってバックグラウンド タスクが取り消されます。

また、[**Unregister**](/uwp/api/windows.applicationmodel.background.backgroundtaskregistration.unregister) メソッドには、現在実行中のバックグラウンド タスク インスタンスを (完了前に) 中断するかどうかを示すブール値 (true または false) が指定されます。 詳しくは、**Unregister** の API リファレンスをご覧ください。

[**Unregister**](/uwp/api/windows.applicationmodel.background.backgroundtaskregistration.unregister) に加え、[**BackgroundTaskDeferral.Complete**](/uwp/api/windows.applicationmodel.background.backgroundtaskdeferral.complete) も呼び出す必要があります。 こうすることで、バックグラウンド タスクに関連付けられた非同期操作が終了したことがシステムに通知されます。