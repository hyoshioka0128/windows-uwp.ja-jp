---
title: アプリの中断の処理
description: システムがアプリを中断するときに重要なアプリケーション データを保存する方法を説明します。
ms.assetid: F84F1512-24B9-45EC-BF23-A09E0AC985B0
ms.date: 07/06/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
dev_langs:
- csharp
- vb
- cppwinrt
- cpp
ms.openlocfilehash: 1c75200a768efd258aa84b20493b9d296578a05c
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89171826"
---
# <a name="handle-app-suspend"></a>アプリの中断の処理

**重要な API**

- [**中断中**](/uwp/api/windows.ui.xaml.application.suspending)

システムがアプリを中断するときに重要なアプリケーション データを保存する方法を説明します。 このトピックの例では、[**Suspending**](/uwp/api/windows.ui.xaml.application.suspending) イベントのイベント ハンドラーを登録して文字列をファイルに保存します。

## <a name="register-the-suspending-event-handler"></a>中断イベント ハンドラーを登録する

[**Suspending**](/uwp/api/windows.ui.xaml.application.suspending) イベントを処理するために登録します。このイベントは、システムがアプリを中断する前にアプリでアプリケーション データを保存する必要があることを示します。

```csharp
using System;
using Windows.ApplicationModel;
using Windows.ApplicationModel.Activation;
using Windows.UI.Xaml;

partial class MainPage
{
   public MainPage()
   {
      InitializeComponent();
      Application.Current.Suspending += new SuspendingEventHandler(App_Suspending);
   }
}
```

```vb
Public NotInheritable Class MainPage

   Public Sub New()
      InitializeComponent()
      AddHandler Application.Current.Suspending, AddressOf App_Suspending
   End Sub
   
End Class
```

```cppwinrt
MainPage::MainPage()
{
    InitializeComponent();
    Windows::UI::Xaml::Application::Current().Suspending({ this, &MainPage::App_Suspending });
}
```

```cpp
using namespace Windows::ApplicationModel;
using namespace Windows::ApplicationModel::Activation;
using namespace Windows::Foundation;
using namespace Windows::UI::Xaml;
using namespace AppName;

MainPage::MainPage()
{
   InitializeComponent();
   Application::Current->Suspending +=
       ref new SuspendingEventHandler(this, &MainPage::App_Suspending);
}
```

## <a name="save-application-data-before-suspension"></a>中断の前にアプリケーション データを保存する

アプリでは、[**Suspending**](/uwp/api/windows.ui.xaml.application.suspending) イベントを処理する時点で、ハンドラー関数で重要なアプリケーション データを保存できます。 アプリで [**LocalSettings**](/uwp/api/windows.storage.applicationdata.localsettings) Storage API を使って、シンプルなアプリケーション データを同期的に保存する必要があります。

```csharp
partial class MainPage
{
    async void App_Suspending(
        Object sender,
        Windows.ApplicationModel.SuspendingEventArgs e)
    {
        // TODO: This is the time to save app data in case the process is terminated.
    }
}
```

```vb
Public NonInheritable Class MainPage

    Private Sub App_Suspending(
        sender As Object,
        e As Windows.ApplicationModel.SuspendingEventArgs) Handles OnSuspendEvent.Suspending

        ' TODO: This is the time to save app data in case the process is terminated.
    End Sub

End Class
```

```cppwinrt
void MainPage::App_Suspending(
    Windows::Foundation::IInspectable const& /* sender */,
    Windows::ApplicationModel::SuspendingEventArgs const& /* e */)
{
    // TODO: This is the time to save app data in case the process is terminated.
}
```

```cpp
void MainPage::App_Suspending(Object^ sender, SuspendingEventArgs^ e)
{
    // TODO: This is the time to save app data in case the process is terminated.
}
```

## <a name="release-resources"></a>リソースの解放

また、排他リソースとファイル ハンドルを、自分のアプリが中断されているときに他のアプリがアクセスできるように解放することをお勧めします。 排他リソースには、カメラ、I/O デバイス、外部デバイス、ネットワーク リソースなどがあります。 排他リソースとファイル ハンドルを明示的に解放すると、自分のアプリが中断されているときに他のアプリが排他リソースとファイル ハンドルにアクセスできるようになります。 アプリが再開されるときに、排他リソースとファイル ハンドルを再取得する必要があります。

## <a name="remarks"></a>注釈

ユーザーが別のアプリや、デスクトップまたはスタート画面に切り替えると、システムはアプリを中断します。 ユーザーが元のアプリに戻すと、システムはアプリを再開します。 システムがアプリを再開した時点で、変数とデータ構造の内容は、システムがアプリを一時停止する前の状態と同じです。 システムはアプリを厳密に中断前の状態に復元するので、ユーザーからはアプリがバックグラウンドで実行していたように見えます。

システムは、アプリの一時停止中、アプリとそのデータをメモリに保持するよう試みます。 ただし、アプリをメモリに保持するためのリソースがシステムにない場合、システムはアプリを終了します。 中断されてから終了されたアプリにユーザーが戻るときに、システムは [**Activated**](/uwp/api/windows.applicationmodel.core.coreapplicationview.activated) イベントを送って、[**OnLaunched**](/uwp/api/windows.ui.xaml.application.onlaunched) メソッドでアプリケーション データを復元する必要があります。

アプリが終了されるときは、システムはアプリに通知を送らないので、アプリは中断されたときにアプリケーション データを保存し、排他リソースとファイル ハンドルを解放して、アプリが終了後アクティブ化されるときにそれらを復元する必要があります。

ハンドラー内で非同期呼び出しを行う場合、制御はその非同期呼び出しからすぐに戻ります。 つまり、非同期呼び出しがまだ完了していない場合でも、イベント ハンドラーから制御が戻り、アプリを次の状態に移行できます。 イベント ハンドラーに渡される [**EnteredBackgroundEventArgs**](/uwp/api/Windows.ApplicationModel) オブジェクトの [**GetDeferral**](/uwp/api/Windows.ApplicationModel) メソッドを使用して、[**Windows.Foundation.Deferral**](/uwp/api/windows.foundation.deferral) オブジェクトの [**Complete**](/uwp/api/windows.foundation.deferral.complete) メソッドを呼び出した後まで中断を延期することができます。

遅延では、アプリが終了する前に、実行する必要があるコードの量を増やす必要はありません。 遅延の *Complete* メソッドが呼び出されるか、または期限になるか、*どちらか早い方*まで、終了が延期されるだけです。 Suspending 状態のときに延長するには、[**ExtendedExecutionSession**](run-minimized-with-extended-execution.md) を使用します

> [!NOTE]
> Windows 8.1 のシステムの応答性を向上させるために、アプリは中断された後にリソースに低優先度でアクセスできます。 この新しい優先度をサポートするために、中断操作のタイムアウトが延長され、アプリには通常の優先度と同程度のタイムアウト (Windows では 5 秒、Windows Phone では 1 ～ 10 秒) が与えられます。 このタイムアウトの時間枠を延長したり、変更したりすることはできません。

**Visual Studio を使用したデバッグに関する注意事項:** Visual Studio は、デバッガーにアタッチされているアプリを Windows が中断できないようにします。 これは、アプリが実行されている間、ユーザーが Visual Studio デバッグの UI を確認できるようにするためです。 アプリのデバッグ中は、Visual Studio を使ってそのアプリに中断イベントを送信できます。 **[デバッグの場所]** ツール バーが表示されていることを確認し、**[中断]** アイコンをクリックします。

## <a name="related-topics"></a>関連トピック

* [アプリのライフサイクル](app-lifecycle.md)
* [アプリのアクティブ化の処理](activate-an-app.md)
* [アプリの再開の処理](resume-an-app.md)
* [起動、中断、再開の UX ガイドライン](./index.md)
* [延長実行](run-minimized-with-extended-execution.md)

 

 