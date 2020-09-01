---
title: アプリ内からのバックグラウンド タスクのトリガー
description: アプリケーショントリガーを使用して、アプリ内からアクティブ化するバックグラウンドタスクを実行する方法について説明します。
ms.date: 07/06/2018
ms.topic: article
keywords: バックグラウンドタスクトリガー、バックグラウンドタスク
ms.localizationpriority: medium
ms.openlocfilehash: 446adc9921d2d124fb6e1304a06b70fa72da3d96
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89155836"
---
# <a name="trigger-a-background-task-from-within-your-app"></a>アプリ内からのバックグラウンド タスクのトリガー

[ApplicationTrigger](/uwp/api/Windows.ApplicationModel.Background.ApplicationTrigger) を使ってアプリ内からバックグラウンド タスクをアクティブ化する方法について説明します。

アプリケーショントリガーを作成する方法の例については、次の [例](https://github.com/Microsoft/Windows-universal-samples/blob/v2.0.0/Samples/BackgroundTask/cs/BackgroundTask/Scenario5_ApplicationTriggerTask.xaml.cs)を参照してください。

このトピックでは、アプリケーションからアクティブ化する必要のあるバックグラウンド タスクがあることを前提としています。 まだバックグラウンド タスクがない場合は、[BackgroundActivity.cs](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/BackgroundActivation/cs/BackgroundActivity.cs) にサンプルのバックグラウンド タスクがあります。 または、「[アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)」の手順に従って、バックグラウンド タスクを作成してください。

## <a name="why-use-an-application-trigger"></a>アプリケーション トリガーを使う理由

**ApplicationTrigger** は、フォアグラウンド アプリから別のプロセスのコードを実行するために使用します。 **ApplicationTrigger** は、ユーザーがフォアグラウンド アプリを閉じた場合でも、バックグラウンドで実行が必要な作業がある場合に適しています。 アプリが閉じられたらバックグラウンド作業を停止する場合や、バックグラウンド作業がフォアグラウンド プロセスの状態に関連付けられている場合には、代わりに[延長実行](run-minimized-with-extended-execution.md)を使います。

## <a name="create-an-application-trigger"></a>アプリケーション トリガーの作成

新しい [ApplicationTrigger](/uwp/api/Windows.ApplicationModel.Background.ApplicationTrigger) を作成します。 これは、以下のスニペットで行われるように、フィールドに格納されます。 これは、トリガーに通知する場合に、後で新しいインスタンスを作成する必要がないようにするための利便性を考慮したものです。 ただし、トリガーへの通知には、任意の **ApplicationTrigger** インスタンスを使用できます。

```csharp
// _AppTrigger is an ApplicationTrigger field defined at a scope that will keep it alive
// as long as you need to trigger the background task.
// Or, you could create a new ApplicationTrigger instance and use that when you want to
// trigger the background task.
_AppTrigger = new ApplicationTrigger();
```

```cppwinrt
// _AppTrigger is an ApplicationTrigger field defined at a scope that will keep it alive
// as long as you need to trigger the background task.
// Or, you could create a new ApplicationTrigger instance and use that when you want to
// trigger the background task.
Windows::ApplicationModel::Background::ApplicationTrigger _AppTrigger;
```

```cpp
// _AppTrigger is an ApplicationTrigger field defined at a scope that will keep it alive
// as long as you need to trigger the background task.
// Or, you could create a new ApplicationTrigger instance and use that when you want to
// trigger the background task.
ApplicationTrigger ^ _AppTrigger = ref new ApplicationTrigger();
```

## <a name="optional-add-a-condition"></a>(省略可能) 条件の追加

いつタスクを実行するかを制御するバックグラウンド タスクの条件を作成できます。 条件を指定すると、条件が満たされるまではバックグラウンド タスクが実行されないようにすることができます。 詳しくは、「[バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)」をご覧ください。

この例では、条件は **Internetavailable** に設定されています。これにより、トリガーされると、インターネットアクセスが利用可能になるとタスクのみが実行されるようになります。 指定できる条件の一覧については、「[**SystemConditionType**](/uwp/api/Windows.ApplicationModel.Background.SystemConditionType)」をご覧ください。

```csharp
SystemCondition internetCondition = new SystemCondition(SystemConditionType.InternetAvailable);
```

```cppwinrt
Windows::ApplicationModel::Background::SystemCondition internetCondition{
    Windows::ApplicationModel::Background::SystemConditionType::InternetAvailable };
```

```cpp
SystemCondition ^ internetCondition = ref new SystemCondition(SystemConditionType::InternetAvailable)
```

バックグラウンド トリガーの条件と種類について詳しくは、「[バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)」をご覧ください。

##  <a name="call-requestaccessasync"></a>RequestAccessAsync() の呼び出し

**ApplicationTrigger** バックグラウンド タスクを登録する前に、[**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出して、ユーザーが許可しているバックグラウンド アクティビティのレベルを判断します。これは、ユーザーがアプリのバックグラウンド アクティビティを無効にしている可能性があるためです。 ユーザーがバックグラウンド アクティビティの設定を制御する方法について詳しくは、「[バックグラウンド アクティビティの最適化](../debug-test-perf/optimize-background-activity.md)」を参照してください。

```csharp
var requestStatus = await Windows.ApplicationModel.Background.BackgroundExecutionManager.RequestAccessAsync();
if (requestStatus != BackgroundAccessStatus.AlwaysAllowed)
{
   // Depending on the value of requestStatus, provide an appropriate response
   // such as notifying the user which functionality won't work as expected
}
```

## <a name="register-the-background-task"></a>バックグラウンド タスクの登録

バックグラウンド タスクの登録関数を呼び出してバックグラウンド タスクを登録します。 バックグラウンド タスクの登録と、以下のコード サンプルの **RegisterBackgroundTask()** メソッドの定義について詳しくは、「[バックグラウンド タスクの登録](register-a-background-task.md)」を参照してください。

アプリケーション トリガーを使用してフォアグラウンド プロセスの有効期間を延長することを検討している場合は、代わりに[延長実行](run-minimized-with-extended-execution.md)の使用を検討してください。 アプリケーション トリガーは、作業を行うための個別にホストされたプロセスを作成することを目的としています。 次のコード スニペットは、アウトプロセス バックグラウンド トリガーを登録します。

```csharp
string entryPoint = "Tasks.ExampleBackgroundTaskClass";
string taskName   = "Example application trigger";

BackgroundTaskRegistration task = RegisterBackgroundTask(entryPoint, taskName, appTrigger, internetCondition);
```

```cppwinrt
std::wstring entryPoint{ L"Tasks.ExampleBackgroundTaskClass" };
std::wstring taskName{ L"Example application trigger" };

Windows::ApplicationModel::Background::BackgroundTaskRegistration task{
    RegisterBackgroundTask(entryPoint, taskName, appTrigger, internetCondition) };
```

```cpp
String ^ entryPoint = "Tasks.ExampleBackgroundTaskClass";
String ^ taskName   = "Example application trigger";

BackgroundTaskRegistration ^ task = RegisterBackgroundTask(entryPoint, taskName, appTrigger, internetCondition);
```

バックグラウンド タスクの登録パラメーターは登録時に検証されます。 いずれかの登録パラメーターが有効でない場合は、エラーが返されます。 バックグラウンド タスクの登録が失敗するシナリオをアプリが適切に処理するようにします。タスクを登録しようとした後で、有効な登録オブジェクトを持っていることを前提として動作するアプリは、クラッシュする場合があります。

## <a name="trigger-the-background-task"></a>バックグラウンド タスクのトリガー

バックグラウンド タスクをトリガーする前に、[BackgroundTaskRegistration](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration) を使って、そのバックグラウンド タスクが登録されていることを確認します。 すべてのバックグラウンド タスクが登録されていることを確認するのに適したタイミングは、アプリの起動中です。

[ApplicationTrigger.RequestAsync](/uwp/api/windows.applicationmodel.background.applicationtrigger) を呼び出してバックグラウンド タスクをトリガーします。 どの **ApplicationTrigger** インスタンスでも機能します。

**ApplicationTrigger.RequestAsync** は、バックグラウンド タスク自体からは呼び出すことができません。また、アプリがバックグラウンド実行状態にある場合も呼び出すことはできません (アプリケーションの状態について詳しくは「[アプリのライフサイクル](app-lifecycle.md)」を参照してください)。
アプリでバックグラウンド アクティビティが実行されないように電源ポリシーやプライバシー ポリシーが設定されている場合は、[DisabledByPolicy](/uwp/api/windows.applicationmodel.background.applicationtriggerresult) が返される可能性があります。
また、一度に実行できる AppTrigger は 1 つだけです。 AppTrigger の実行中に別の AppTrigger を実行しようとした場合、関数によって [CurrentlyRunning](/uwp/api/windows.applicationmodel.background.applicationtriggerresult) が返されます。

```csharp
var result = await _AppTrigger.RequestAsync();
```

## <a name="manage-resources-for-your-background-task"></a>バックグラウンド タスクのリソースの管理

[BackgroundExecutionManager.RequestAccessAsync](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager) を使用して、アプリのバックグラウンド アクティビティを制限するようにユーザーが設定しているかどうかを確認します。 バッテリー使用量を注意し、ユーザーが望む操作を完了するために必要な場合にのみ、バックグラウンドで実行するようにしてください。 ユーザーがバックグラウンド アクティビティの設定を制御する方法について詳しくは、「[バックグラウンド アクティビティの最適化](../debug-test-perf/optimize-background-activity.md)」を参照してください。  

- メモリ: オペレーティング システムからバックグラウンド タスクの実行を許可されるうえで重要なのが、アプリのメモリと電力使用の調整です。 [メモリ管理 API](/uwp/api/windows.system.memorymanager) を使用して、バックグラウンド タスクが使用しているメモリ量を確認します。 バックグラウンド タスクが使用するメモリ量が多くなるほど、別のアプリがフォアグラウンドのときに、バックグラウンド タスクの実行を OS が維持することは難しくなります。 アプリが実行できるすべてのバックグラウンド アクティビティについて、最終的に管理できるのはユーザーです。また、ユーザーは、アプリがどの程度バッテリー消費に影響しているかを確認できます。  
- CPU 時間: バックグラウンド タスクは、トリガーの種類に基づいて取得するウォールクロック時間の長さによって使用が制限されます。 アプリケーション トリガーによってトリガーされるバックグラウンド タスクは、約 10 分間に制限されます。

バックグラウンド タスクに適用されるリソースの制約については、「[バックグラウンド タスクによるアプリのサポート](support-your-app-with-background-tasks.md)」をご覧ください。

## <a name="remarks"></a>注釈

Windows 10 以降、ユーザーはバック グラウンド タスクを利用するために、アプリをロック画面に追加する必要はなくなりました。

バックグラウンド タスクが **ApplicationTrigger** を使って実行されるのは、先に [**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出した場合のみです。

## <a name="related-topics"></a>関連トピック

* [バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)
* [バックグラウンド タスクのコード サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BackgroundTask)
* [インプロセスバックグラウンドタスクを作成して登録](create-and-register-an-inproc-background-task.md)します。
* [アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)
* [バックグラウンド タスクのデバッグ](debug-a-background-task.md)
* [アプリケーション マニフェストでのバックグラウンド タスクの宣言](declare-background-tasks-in-the-application-manifest.md)
* [アプリがバックグラウンドに移動したときのメモリの解放](reduce-memory-usage.md)
* [取り消されたバックグラウンド タスクの処理](handle-a-cancelled-background-task.md)
* [UWP アプリで一時停止イベント、再開イベント、バックグラウンド イベントをトリガーする方法 (デバッグ時)](/previous-versions/hh974425(v=vs.110))
* [バックグラウンド タスクの進捗状況と完了の監視](monitor-background-task-progress-and-completion.md)
* [延長実行を使ってアプリの中断を延期する](run-minimized-with-extended-execution.md)
* [バックグラウンド タスクの登録](register-a-background-task.md)
* [バックグラウンド タスクによるシステム イベントへの応答](respond-to-system-events-with-background-tasks.md)
* [バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)
* [バックグラウンド タスクのライブ タイルの更新](update-a-live-tile-from-a-background-task.md)
* [メンテナンス トリガーの使用](use-a-maintenance-trigger.md)