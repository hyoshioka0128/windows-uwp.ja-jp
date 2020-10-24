---
title: バックグラウンド タスクの登録
description: ほとんどのバックグラウンド タスクを安全に登録できる再利用可能な関数の作成方法について説明します。
ms.assetid: 8B1CADC5-F630-48B8-B3CE-5AB62E3DFB0D
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10、uwp、バックグラウンドタスク
ms.localizationpriority: medium
ms.openlocfilehash: 06d9fdfe57ead1e5405a21658654a8992343bb95
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89172966"
---
# <a name="register-a-background-task"></a>バックグラウンド タスクの登録


**重要な API**

-   [**BackgroundTaskRegistration クラス**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration)
-   [**BackgroundTaskBuilder クラス**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder)
-   [**SystemCondition クラス**](/uwp/api/Windows.ApplicationModel.Background.SystemCondition)

ほとんどのバックグラウンド タスクを安全に登録できる再利用可能な関数の作成方法について説明します。

このトピックは、インプロセスのバックグラウンド タスクとアウトプロセスのバックグラウンド タスクの両方に適用されます。 このトピックの説明では、登録する必要があるバックグラウンド タスクが既に存在すると想定します。 (バックグラウンド タスクの作成方法について詳しくは、「[Create and register a background task that runs out-of-process (アウトプロセスで実行されるバックグラウンド タスクの作成と登録)](create-and-register-a-background-task.md)」または「[Create and register an in-process background task (インプロセスのバックグラウンド タスクの作成と登録)](create-and-register-an-inproc-background-task.md)」をご覧ください)。

このトピックは、バックグラウンド タスクを登録するユーティリティ関数の作り方を順に説明します。 このユーティリティ関数は、二重登録による問題を防ぐために、同じタスクが登録されていないかどうかをチェックしたうえでタスクを登録します。バックグラウンド タスクにシステムの条件を適用することができます。 ここで紹介しているユーティリティ関数は、それ自体で完結した実用的なコード例となっています。

**注**  

ユニバーサル Windows アプリは、どの種類のバックグラウンド トリガーを登録する場合でも、先に [**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) を呼び出す必要があります。

更新プログラムのリリース後にユニバーサル Windows アプリが引き続き適切に実行されるようにするには、更新後にアプリが起動する際に、[**RemoveAccess**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.removeaccess)、[**RequestAccessAsync**](/uwp/api/windows.applicationmodel.background.backgroundexecutionmanager.requestaccessasync) の順に呼び出す必要があります。 詳しくは、「[バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)」をご覧ください。

## <a name="define-the-method-signature-and-return-type"></a>メソッドのシグニチャと戻り値の型の定義

このメソッドは、タスクのエントリ ポイント、タスク名、構築済みのバックグラウンド タスク トリガーのほか、(必要に応じて) バックグラウンド タスクの [**SystemCondition**](/uwp/api/Windows.ApplicationModel.Background.SystemCondition) を引数として受け取ります。 このメソッドは、[**BackgroundTaskRegistration**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration) オブジェクトを返します。

> [!Important]
> `taskEntryPoint` -アウトプロセスで実行されるバックグラウンドタスクの場合は、名前空間名、'. '、およびバックグラウンドクラスを含むクラスの名前として作成する必要があります。 この文字列では、大文字と小文字を区別します。  たとえば、名前空間 "MyBackgroundTasks" と、バックグラウンド クラス コードを含むクラス "BackgroundTask1" がある場合、`taskEntryPoint` 用の文字列は "MyBackgroundTasks.BackgroundTask1" となります。
> バックグラウンド タスクをアプリと同じプロセスで実行する (インプロセスのバックグラウンド タスク) 場合、`taskEntryPoint` を設定する必要はありません。

> [!div class="tabbedCodeSnippets"]
> ``` csharp
> public static BackgroundTaskRegistration RegisterBackgroundTask(
>                                                 string taskEntryPoint,
>                                                 string name,
>                                                 IBackgroundTrigger trigger,
>                                                 IBackgroundCondition condition)
> {
>     
>     // We'll add code to this function in subsequent steps.
>
> }
> ```
> ``` cpp
> BackgroundTaskRegistration^ MainPage::RegisterBackgroundTask(
>                                              Platform::String ^ taskEntryPoint,
>                                              Platform::String ^ taskName,
>                                              IBackgroundTrigger ^ trigger,
>                                              IBackgroundCondition ^ condition)
> {
>     
>     // We'll add code to this function in subsequent steps.
>
> }
> ```

## <a name="check-for-existing-registrations"></a>登録の重複確認

既に登録されたタスクかどうかを確認します。 同じタスクが二重に登録されると、1 回のトリガーにつきタスクが複数回実行され、CPU が無駄に消費されるばかりか、予期しない動作を招くこともあるため、この確認は重要です。

同じタスクが登録されているかどうかは、[**BackgroundTaskRegistration.AllTasks**](/uwp/api/windows.applicationmodel.background.backgroundtaskregistration.alltasks) プロパティを照会し、返された結果を反復処理することで確認できます。 各インスタンスの名前を調べ、登録しようとしているタスクの名前と一致した場合、ループを抜けて、フラグ変数を設定します。このフラグに応じたコード パスが次のステップで選択されます。

> **メモ**   アプリに固有のバックグラウンドタスク名を使用します。 各バックグラウンド タスクには一意の名前が付いている必要があります。

次のコードは、最後の手順で作成した [**SystemTrigger**](/uwp/api/Windows.ApplicationModel.Background.SystemTrigger) を使ってバックグラウンド タスクを登録します。

> [!div class="tabbedCodeSnippets"]
> ``` csharp
> public static BackgroundTaskRegistration RegisterBackgroundTask(
>                                                 string taskEntryPoint,
>                                                 string name,
>                                                 IBackgroundTrigger trigger,
>                                                 IBackgroundCondition condition)
> {
>     //
>     // Check for existing registrations of this background task.
>     //
>
>     foreach (var cur in BackgroundTaskRegistration.AllTasks)
>     {
>
>         if (cur.Value.Name == name)
>         {
>             //
>             // The task is already registered.
>             //
>
>             return (BackgroundTaskRegistration)(cur.Value);
>         }
>     }
>     
>     // We'll register the task in the next step.
> }
> ```
> ``` cpp
> BackgroundTaskRegistration^ MainPage::RegisterBackgroundTask(
>                                              Platform::String ^ taskEntryPoint,
>                                              Platform::String ^ taskName,
>                                              IBackgroundTrigger ^ trigger,
>                                              IBackgroundCondition ^ condition)
> {
>     //
>     // Check for existing registrations of this background task.
>     //
>     
>     auto iter   = BackgroundTaskRegistration::AllTasks->First();
>     auto hascur = iter->HasCurrent;
>     
>     while (hascur)
>     {
>         auto cur = iter->Current->Value;
>         
>         if(cur->Name == name)
>         {
>             //
>             // The task is registered.
>             //
>             
>             return (BackgroundTaskRegistration ^)(cur);
>         }
>         
>         hascur = iter->MoveNext();
>     }
>     
>     // We'll register the task in the next step.
> }
> ```

## <a name="register-the-background-task-or-return-the-existing-registration"></a>バックグラウンド タスクを登録する (または既に登録されているタスクを返す)


同じバックグラウンド タスクが既に登録されているかどうかを確認します。 登録されている場合は、そのタスクのインスタンスを返します。

登録されていない場合は、新しい [**BackgroundTaskBuilder**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskBuilder) オブジェクトを使ってタスクを登録します。 このコードは、condition パラメーターが null かどうかを確認し、null でない場合は、その condition を登録オブジェクトに追加します。 戻り値は、[**BackgroundTaskBuilder.Register**](/uwp/api/windows.applicationmodel.background.backgroundtaskbuilder.register) メソッドから返された [**BackgroundTaskRegistration**](/uwp/api/Windows.ApplicationModel.Background.BackgroundTaskRegistration) です。

> **メモ**   バックグラウンドタスクの登録パラメーターは、登録時に検証されます。 いずれかの登録パラメーターが有効でない場合は、エラーが返されます。 バックグラウンド タスクの登録が失敗するシナリオをアプリが適切に処理するようにします。タスクを登録しようとした後で、有効な登録オブジェクトを持っていることを前提として動作するアプリは、クラッシュする場合があります。
> **注** アプリと同じプロセスで実行されるバックグラウンド タスクを登録する場合、`String.Empty` または `null` を `taskEntryPoint` パラメーターに送信します。

次の例には、既にあるタスクを返すか、バックグラウンド タスクを登録するコードが追加されています。また、システムの条件 (省略可能) が指定された場合の処理も追加されています。

> [!div class="tabbedCodeSnippets"]
> ``` csharp
> public static BackgroundTaskRegistration RegisterBackgroundTask(
>                                                 string taskEntryPoint,
>                                                 string name,
>                                                 IBackgroundTrigger trigger,
>                                                 IBackgroundCondition condition)
> {
>     //
>     // Check for existing registrations of this background task.
>     //
>
>     foreach (var cur in BackgroundTaskRegistration.AllTasks)
>     {
>
>         if (cur.Value.Name == taskName)
>         {
>             //
>             // The task is already registered.
>             //
>
>             return (BackgroundTaskRegistration)(cur.Value);
>         }
>     }
>
>     //
>     // Register the background task.
>     //
>
>     var builder = new BackgroundTaskBuilder();
>
>     builder.Name = name;
>
>     // in-process background tasks don't set TaskEntryPoint
>     if ( taskEntryPoint != null && taskEntryPoint != String.Empty)
>     {
>         builder.TaskEntryPoint = taskEntryPoint;
>     }
>     builder.SetTrigger(trigger);
>
>     if (condition != null)
>     {
>         builder.AddCondition(condition);
>     }
>
>     BackgroundTaskRegistration task = builder.Register();
>
>     return task;
> }
> ```
> ``` cpp
> BackgroundTaskRegistration^ MainPage::RegisterBackgroundTask(
>                                              Platform::String ^ taskEntryPoint,
>                                              Platform::String ^ taskName,
>                                              IBackgroundTrigger ^ trigger,
>                                              IBackgroundCondition ^ condition)
> {
>
>     //
>     // Check for existing registrations of this background task.
>     //
>
>     auto iter   = BackgroundTaskRegistration::AllTasks->First();
>     auto hascur = iter->HasCurrent;
>
>     while (hascur)
>     {
>         auto cur = iter->Current->Value;
>
>         if(cur->Name == name)
>         {
>             //
>             // The task is registered.
>             //
>
>             return (BackgroundTaskRegistration ^)(cur);
>         }
>
>         hascur = iter->MoveNext();
>     }
>
>     //
>     // Register the background task.
>     //
>
>     auto builder = ref new BackgroundTaskBuilder();
>
>     builder->Name = name;
>     builder->TaskEntryPoint = taskEntryPoint;
>     builder->SetTrigger(trigger);
>
>     if (condition != nullptr) {
>         
>         builder->AddCondition(condition);
>     }
>
>     BackgroundTaskRegistration ^ task = builder->Register();
>
>     return task;
> }
> ```

## <a name="complete-background-task-registration-utility-function"></a>バックグラウンド タスク登録ユーティリティ関数の完成

この例は、バックグラウンド タスク登録ユーティリティ関数全体を示しています。 ネットワーク関連のバックグラウンド タスクを除くほとんどのバックグラウンド タスクは、この関数を使って登録できます。

> [!div class="tabbedCodeSnippets"]
> ``` csharp
> //
> // Register a background task with the specified taskEntryPoint, name, trigger,
> // and condition (optional).
> //
> // taskEntryPoint: Task entry point for the background task.
> // taskName: A name for the background task.
> // trigger: The trigger for the background task.
> // condition: Optional parameter. A conditional event that must be true for the task to fire.
> //
> public static BackgroundTaskRegistration RegisterBackgroundTask(string taskEntryPoint,
>                                                                 string taskName,
>                                                                 IBackgroundTrigger trigger,
>                                                                 IBackgroundCondition condition)
> {
>     //
>     // Check for existing registrations of this background task.
>     //
>
>     foreach (var cur in BackgroundTaskRegistration.AllTasks)
>     {
>
>         if (cur.Value.Name == taskName)
>         {
>             //
>             // The task is already registered.
>             //
>
>             return (BackgroundTaskRegistration)(cur.Value);
>         }
>     }
>
>     //
>     // Register the background task.
>     //
>
>     var builder = new BackgroundTaskBuilder();
>
>     builder.Name = taskName;
>     builder.TaskEntryPoint = taskEntryPoint;
>     builder.SetTrigger(trigger);
>
>     if (condition != null)
>     {
>
>         builder.AddCondition(condition);
>     }
>
>     BackgroundTaskRegistration task = builder.Register();
>
>     return task;
> }
> ```
> ``` cpp
> //
> // Register a background task with the specified taskEntryPoint, name, trigger,
> // and condition (optional).
> //
> // taskEntryPoint: Task entry point for the background task.
> // taskName: A name for the background task.
> // trigger: The trigger for the background task.
> // condition: Optional parameter. A conditional event that must be true for the task to fire.
> //
> BackgroundTaskRegistration^ MainPage::RegisterBackgroundTask(Platform::String ^ taskEntryPoint,
>                                                              Platform::String ^ taskName,
>                                                              IBackgroundTrigger ^ trigger,
>                                                              IBackgroundCondition ^ condition)
> {
>
>     //
>     // Check for existing registrations of this background task.
>     //
>
>     auto iter   = BackgroundTaskRegistration::AllTasks->First();
>     auto hascur = iter->HasCurrent;
>
>     while (hascur)
>     {
>         auto cur = iter->Current->Value;
>
>         if(cur->Name == name)
>         {
>             //
>             // The task is registered.
>             //
>
>             return (BackgroundTaskRegistration ^)(cur);
>         }
>
>         hascur = iter->MoveNext();
>     }
>
>
>     //
>     // Register the background task.
>     //
>
>     auto builder = ref new BackgroundTaskBuilder();
>
>     builder->Name = name;
>     builder->TaskEntryPoint = taskEntryPoint;
>     builder->SetTrigger(trigger);
>
>     if (condition != nullptr) {
>
>         builder->AddCondition(condition);
>     }
>
>     BackgroundTaskRegistration ^ task = builder->Register();
>
>     return task;
> }
> ```

## <a name="related-topics"></a>関連トピック

* [アウトプロセス バックグラウンド タスクの作成と登録](create-and-register-a-background-task.md)
* [インプロセス バックグラウンド タスクの作成と登録](create-and-register-an-inproc-background-task.md)
* [アプリケーション マニフェストでのバックグラウンド タスクの宣言](declare-background-tasks-in-the-application-manifest.md)
* [取り消されたバックグラウンド タスクの処理](handle-a-cancelled-background-task.md)
* [バックグラウンド タスクの進捗状況と完了の監視](monitor-background-task-progress-and-completion.md)
* [バックグラウンド タスクによるシステム イベントへの応答](respond-to-system-events-with-background-tasks.md)
* [バックグラウンド タスクを実行するための条件の設定](set-conditions-for-running-a-background-task.md)
* [バックグラウンド タスクのライブ タイルの更新](update-a-live-tile-from-a-background-task.md)
* [メンテナンス トリガーの使用](use-a-maintenance-trigger.md)
* [タイマーでのバックグラウンド タスクの実行](run-a-background-task-on-a-timer-.md)
* [バックグラウンド タスクのガイドライン](guidelines-for-background-tasks.md)
* [バックグラウンド タスクのデバッグ](debug-a-background-task.md)
* [UWP アプリで一時停止イベント、再開イベント、バックグラウンド イベントをトリガーする方法 (デバッグ時)](/previous-versions/hh974425(v=vs.110))