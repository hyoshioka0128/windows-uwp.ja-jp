---
title: バックグラウンド タスクによるシステム イベントへの応答
description: SystemTrigger イベントに応答するバックグラウンド タスクを作成する方法について説明します。
ms.assetid: 43C21FEA-28B9-401D-80BE-A61B71F01A89
ms.date: 07/06/2018
ms.topic: article
keywords: windows 10、uwp、バックグラウンドタスク
ms.localizationpriority: medium
dev_langs:
- csharp
- cppwinrt
- cpp
ms.openlocfilehash: b66415b7f334eeaff7d29e2e11f111c15c718401
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89164746"
---
# <a name="respond-to-system-events-with-background-tasks"></a>バックグラウンド タスクによるシステム イベントへの応答

**重要な API**

- [**IBackgroundTask**](/uwp/api/Windows.ApplicationModel.Background.IBackgroundTask)
- [**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder)
- [**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTrigger)

[**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTriggerType) イベントに応答するバックグラウンド タスクを作成する方法について説明します。

このトピックは、既にアプリにバックグラウンド タスク クラスが作られており、システムがトリガーするイベント (インターネットの可用性が変わる、ユーザーがログインするなど) に応じてこのタスクを実行する必要があることを前提としています。 ここでは、主に [**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTriggerType) クラスについて扱います。 バックグラウンド タスク クラスの作成について詳しくは、「[インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)」または「[アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)」をご覧ください。

## <a name="create-a-systemtrigger-object"></a>SystemTrigger オブジェクトを作る

アプリ コードで新規の [**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTrigger) オブジェクトを作ります。 1 つ目のパラメーター triggerType には、このバックグラウンド タスクをアクティブ化するシステム イベント トリガーの種類を指定します。** イベントの種類の一覧については、「[**SystemTriggerType**](/uwp/api/Windows.ApplicationModel.Background.SystemTriggerType)」をご覧ください。

2 つ目のパラメーター *OneShot* では、次回システム イベントが発生したときに一度だけバックグラウンド タスクを実行するか、それともタスクの登録が解除されるまで、システム イベントが発生するたびにバックグラウンド タスクを実行するかを指定します。

次のコードでは、インターネットが利用可能になるたびにバックグラウンド タスクを実行するように指定しています。

```csharp
SystemTrigger internetTrigger = new SystemTrigger(SystemTriggerType.InternetAvailable, false);
```

```cppwinrt
Windows::ApplicationModel::Background::SystemTrigger internetTrigger{
    Windows::ApplicationModel::Background::SystemTriggerType::InternetAvailable, false};
```

```cpp
SystemTrigger ^ internetTrigger = ref new SystemTrigger(SystemTriggerType::InternetAvailable, false);
```

## <a name="register-the-background-task"></a>バックグラウンド タスクの登録

バックグラウンド タスクの登録関数を呼び出してバックグラウンド タスクを登録します。 バックグラウンド タスクの登録について詳しくは、「[バックグラウンド タスクの登録](register-a-background-task.md)」をご覧ください。

次のコードは、アウトプロセスで実行されるバックグラウンド プロセスのバックグラウンド タスクを登録するものです。 ホスト アプリと同じプロセスで実行されるバッグラウンド タスクを呼び出す場合は、`entrypoint` を設定しません。

```csharp
string entryPoint = "Tasks.ExampleBackgroundTaskClass"; // Namespace name, '.', and the name of the class containing the background task
string taskName   = "Internet-based background task";

BackgroundTaskRegistration task = RegisterBackgroundTask(entryPoint, taskName, internetTrigger, exampleCondition);
```

```cppwinrt
std::wstring entryPoint{ L"Tasks.ExampleBackgroundTaskClass" }; // don't set for in-process background tasks.
std::wstring taskName{ L"Internet-based background task" };

Windows::ApplicationModel::Background::BackgroundTaskRegistration task{
    RegisterBackgroundTask(entryPoint, taskName, internetTrigger, exampleCondition) };
```

```cpp
String ^ entryPoint = "Tasks.ExampleBackgroundTaskClass"; // don't set for in-process background tasks
String ^ taskName   = "Internet-based background task";

BackgroundTaskRegistration ^ task = RegisterBackgroundTask(entryPoint, taskName, internetTrigger, exampleCondition);
```

> [!NOTE]
> バックグラウンドのトリガーの種類を登録する前に、ユニバーサル Windows プラットフォームアプリで [**Requestaccessasync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出す必要があります。

更新プログラムのリリース後にユニバーサル Windows アプリが引き続き適切に実行されるようにするには、更新後にアプリが起動する際に、[**RemoveAccess**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess)、[**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) の順に呼び出す必要があります。 詳しくは、「[バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)」をご覧ください。

> [!NOTE]
> バックグラウンド タスクの登録パラメーターは登録時に検証されます。 いずれかの登録パラメーターが有効でない場合は、エラーが返されます。 バックグラウンド タスクの登録が失敗するシナリオをアプリが適切に処理するようにします。タスクを登録しようとした後で、有効な登録オブジェクトを持っていることを前提として動作するアプリは、クラッシュする場合があります。
 
## <a name="remarks"></a>注釈

バックグラウンド タスクの登録動作を確認するには、[バックグラウンド タスクのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BackgroundTask)をダウンロードしてください。

バックグラウンド タスクは、[**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTrigger) イベントと [**MaintenanceTrigger**](/uwp/api/Windows.ApplicationModel.Background.MaintenanceTrigger) イベントに応答して実行できます。ただし、その場合も[アプリケーション マニフェストでバックグラウンド タスクを宣言する](declare-background-tasks-in-the-application-manifest.md)必要があります。 どの種類のバックグラウンド タスクを登録する場合でも、その前に [**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) も呼び出す必要があります。

アプリでは、[**TimeTrigger**](/uwp/api/Windows.ApplicationModel.Background.TimeTrigger)、[**PushNotificationTrigger**](/uwp/api/Windows.ApplicationModel.Background.PushNotificationTrigger)、[**NetworkOperatorNotificationTrigger**](/uwp/api/Windows.ApplicationModel.Background.NetworkOperatorNotificationTrigger) の各イベントに応答するバックグラウンド タスクを登録することにより、アプリがフォアグラウンドにない場合でも、ユーザーとリアルタイムに通信できるようになります。 詳しくは、「[バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)」をご覧ください。

## <a name="related-topics"></a>関連トピック

* [アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)
* [インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)
* [アプリケーション マニフェストでのバックグラウンド タスクの宣言](declare-background-tasks-in-the-application-manifest.md)
* [取り消されたバックグラウンド タスクの処理](handle-a-cancelled-background-task.md)
* [バックグラウンド タスクの進捗状況と完了の監視](monitor-background-task-progress-and-completion.md)
* [バックグラウンド タスクの登録](register-a-background-task.md)
* [バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)
* [バックグラウンド タスクのライブ タイルの更新](update-a-live-tile-from-a-background-task.md)
* [メンテナンス トリガーの使用](use-a-maintenance-trigger.md)
* [タイマーでのバックグラウンド タスクの実行](run-a-background-task-on-a-timer-.md)
* [バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)
* [バックグラウンド タスクのデバッグ](debug-a-background-task.md)
* [UWP アプリで一時停止イベント、再開イベント、バックグラウンド イベントをトリガーする方法 (デバッグ時)](/previous-versions/hh974425(v=vs.110))