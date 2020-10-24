---
title: メンテナンス トリガーの使用
description: デバイスが接続されているときに、MaintenanceTrigger クラスを使って軽量のコードをバックグラウンドで実行する方法について説明します。
ms.assetid: 727D9D84-6C1D-4DF3-B3B0-2204EA4D76DD
ms.date: 07/06/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
dev_langs:
- csharp
- cppwinrt
- cpp
ms.openlocfilehash: c390280e084cd8557633f591b1686a0550f6a656
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89155766"
---
# <a name="use-a-maintenance-trigger"></a>メンテナンス トリガーの使用

**重要な API**

- [**メンテナンス トリガー**](/uwp/api/Windows.ApplicationModel.Background.MaintenanceTrigger)
- [**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder)
- [**SystemCondition**](/uwp/api/Windows.ApplicationModel.Background.SystemCondition)

[**MaintenanceTrigger**](/uwp/api/Windows.ApplicationModel.Background.MaintenanceTrigger)クラスを使用して、デバイスが接続されている間にバックグラウンドで軽量コードを実行する方法について説明します。

## <a name="create-a-maintenance-trigger-object"></a>メンテナンス トリガー オブジェクトを作る

この例は、デバイスが接続されているときにアプリを拡張するためにバックグラウンドで実行できる軽量のコードがあることを前提にしています。 ここでは主に、[**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTriggerType) に似た [**MaintenanceTrigger**](/uwp/api/Windows.ApplicationModel.Background.MaintenanceTrigger) について扱います。

バックグラウンド タスク クラスの作成について詳しくは、「[インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)」または「[アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)」をご覧ください。

新しい [**MaintenanceTrigger**](/uwp/api/Windows.ApplicationModel.Background.MaintenanceTrigger) オブジェクトを作成します。 2 つ目のパラメーター (*OneShot*) では、メンテナンス タスクを一度だけ実行するか、定期的に実行を続けるかを指定します。 *OneShot* を true に設定する場合は、1 つ目のパラメーター (*FreshnessTime*) に、バックグラウンド タスクをスケジュールするまで待機する時間 (分単位) を指定します。 *OneShot* を false に設定する場合は、*FreshnessTime* でバックグラウンド タスクを実行する間隔を指定します。

> [!NOTE]
> *FreshnessTime*が15分未満に設定されている場合は、バックグラウンドタスクを登録しようとすると例外がスローされます。

このコード例では、1時間に1回実行されるトリガーを作成します。

```csharp
uint waitIntervalMinutes = 60;
MaintenanceTrigger taskTrigger = new MaintenanceTrigger(waitIntervalMinutes, false);
```

```cppwinrt
uint32_t waitIntervalMinutes{ 60 };
Windows::ApplicationModel::Background::MaintenanceTrigger taskTrigger{ waitIntervalMinutes, false };
```

```cpp
unsigned int waitIntervalMinutes = 60;
MaintenanceTrigger ^ taskTrigger = ref new MaintenanceTrigger(waitIntervalMinutes, false);
```

## <a name="optional-add-a-condition"></a>(省略可能) 条件の追加

- いつタスクを実行するかを制御するバックグラウンド タスクの条件を必要に応じて作成します。 条件を指定すると、条件が満たされるまではバックグラウンド タスクが実行されないようにすることができます。詳しくは「[バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)」をご覧ください。

次の例では、インターネットが利用できる場合 (またはインターネットが利用できるようになった場合) にメンテナンスが実行されるように、条件を **InternetAvailable** に設定します。 指定できるバックグラウンド タスク条件の一覧については、「[**SystemConditionType**](/uwp/api/Windows.ApplicationModel.Background.SystemConditionType)」をご覧ください。

次のコードでは、メンテナンス タスク ビルダーに条件を追加します。

```csharp
SystemCondition exampleCondition = new SystemCondition(SystemConditionType.InternetAvailable);
```

```cppwinrt
Windows::ApplicationModel::Background::SystemCondition exampleCondition{
    Windows::ApplicationModel::Background::SystemConditionType::InternetAvailable };
```

```cpp
SystemCondition ^ exampleCondition = ref new SystemCondition(SystemConditionType::InternetAvailable);
```

## <a name="register-the-background-task"></a>バックグラウンド タスクの登録

- バックグラウンド タスクの登録関数を呼び出してバックグラウンド タスクを登録します。 バックグラウンド タスクの登録について詳しくは、「[バックグラウンド タスクの登録](register-a-background-task.md)」をご覧ください。

次のコードでは、メンテナンス タスクを登録します。 `entryPoint` と指定しているので、バックグラウンド タスクとアプリを異なるプロセスで実行するように想定されていることに注意してください。 バックグラウンド タスクとアプリを同じプロセスで実行する場合は、`entryPoint` を指定しません。

```csharp
string entryPoint = "Tasks.ExampleBackgroundTaskClass";
string taskName   = "Maintenance background task example";

BackgroundTaskRegistration task = RegisterBackgroundTask(entryPoint, taskName, taskTrigger, exampleCondition);
```

```cppwinrt
std::wstring entryPoint{ L"Tasks.ExampleBackgroundTaskClass" };
std::wstring taskName{ L"Maintenance background task example" };

Windows::ApplicationModel::Background::BackgroundTaskRegistration task{
    RegisterBackgroundTask(entryPoint, taskName, taskTrigger, exampleCondition) };
```

```cpp
String ^ entryPoint = "Tasks.ExampleBackgroundTaskClass";
String ^ taskName   = "Maintenance background task example";

BackgroundTaskRegistration ^ task = RegisterBackgroundTask(entryPoint, taskName, taskTrigger, exampleCondition);
```

> [!NOTE]
> デスクトップ以外のすべてのデバイス ファミリでは、デバイスのメモリが少なくなった場合、バックグラウンド タスクが終了することがあります。 メモリ不足の例外が検出されないか、検出されてもアプリによって処理されない場合、バックグラウンド タスクは、警告や OnCanceled イベントの発生なしに終了します。 こうすることで、フォアグラウンドのアプリのユーザー エクスペリエンスが保証されます。 バックグラウンド タスクは、このシナリオを処理できるように設計する必要があります。

> [!NOTE]
> バックグラウンドのトリガーの種類を登録する前に、ユニバーサル Windows プラットフォームアプリで [**Requestaccessasync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出す必要があります。

アプリに対する更新プログラムのリリース後にユニバーサル Windows アプリが引き続き適切に実行されるようにするには、更新後にアプリが起動する際に、[**RemoveAccess**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess)、[**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) の順に呼び出す必要があります。 詳しくは、「[バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)」をご覧ください。

> [!NOTE]
> バックグラウンド タスクの登録パラメーターは登録時に検証されます。 いずれかの登録パラメーターが有効でない場合は、エラーが返されます。 バックグラウンド タスクの登録が失敗するシナリオをアプリが適切に処理するようにします。タスクを登録しようとした後で、有効な登録オブジェクトを持っていることを前提として動作するアプリは、クラッシュする場合があります。

## <a name="related-topics"></a>関連トピック

* [インプロセスバックグラウンドタスクを作成して登録](create-and-register-an-inproc-background-task.md)します。
* [アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)
* [アプリケーション マニフェストでのバックグラウンド タスクの宣言](declare-background-tasks-in-the-application-manifest.md)
* [取り消されたバックグラウンド タスクの処理](handle-a-cancelled-background-task.md)
* [バックグラウンド タスクの進捗状況と完了の監視](monitor-background-task-progress-and-completion.md)
* [バックグラウンド タスクの登録](register-a-background-task.md)
* [バックグラウンド タスクによるシステム イベントへの応答](respond-to-system-events-with-background-tasks.md)
* [バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)
* [バックグラウンド タスクのライブ タイルの更新](update-a-live-tile-from-a-background-task.md)
* [タイマーでのバックグラウンド タスクの実行](run-a-background-task-on-a-timer-.md)
* [バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)
* [バックグラウンド タスクのデバッグ](debug-a-background-task.md)
* [UWP アプリで一時停止イベント、再開イベント、バックグラウンド イベントをトリガーする方法 (デバッグ時)](/previous-versions/hh974425(v=vs.110))