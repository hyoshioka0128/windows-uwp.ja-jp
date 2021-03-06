---
title: アプリをアクティブ化する方法 (DirectX と C++)
description: ここでは、ユニバーサル Windows プラットフォーム (UWP) DirectX アプリのアクティブ化エクスペリエンスを定義する方法について説明します。
ms.assetid: b07c7da1-8a5e-5b57-6f77-6439bf653a53
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, DirectX, アクティブ化
ms.localizationpriority: medium
ms.openlocfilehash: 4aeba58af61cffa33626c64cebcbade272af109b
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368602"
---
# <a name="how-to-activate-an-app-directx-and-c"></a>アプリをアクティブ化する方法 (DirectX と C++)



ここでは、ユニバーサル Windows プラットフォーム (UWP) DirectX アプリのアクティブ化エクスペリエンスを定義する方法について説明します。

## <a name="register-the-app-activation-event-handler"></a>アプリのアクティブ化イベント ハンドラーを登録する


まず、[**CoreApplicationView::Activated**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplicationview.activated) イベントを処理するための登録を行います。このイベントは、アプリが開始され、オペレーティング システムによって初期化されるときに発生します。

次のコードをビュー プロバイダー (この例では **MyViewProvider** という名前) の [**IFrameworkView::Initialize**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.initialize) メソッドの実装に追加します。

```cpp
void App::Initialize(CoreApplicationView^ applicationView)
{
    // Register event handlers for the app lifecycle. This example includes Activated, so that we
    // can make the CoreWindow active and start rendering on the window.
    applicationView->Activated +=
        ref new TypedEventHandler<CoreApplicationView^, IActivatedEventArgs^>(this, &App::OnActivated);
  
  //...

}
```

## <a name="activate-the-corewindow-instance-for-the-app"></a>アプリの CoreWindow インスタンスをアクティブ化する


アプリの起動時に、アプリの [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) への参照を取得する必要があります。 **CoreWindow** には、アプリがウィンドウ イベントの処理に使うウィンドウ イベント メッセージ ディスパッチャーが含まれています。 アプリのアクティブ化イベントのコールバックで、[**CoreWindow::GetForCurrentThread**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.getforcurrentthread) を呼び出して、この参照を取得します。 この参照を取得したら、[**CoreWindow::Activate**](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow.activate) を呼び出して、メイン アプリ ウィンドウをアクティブ化します。

```cpp
void App::OnActivated(CoreApplicationView^ applicationView, IActivatedEventArgs^ args)
{
    // Run() won't start until the CoreWindow is activated.
    CoreWindow::GetForCurrentThread()->Activate();
}
```

## <a name="start-processing-event-message-for-the-main-app-window"></a>メイン アプリ ウィンドウのイベント メッセージの処理の開始


作成したコールバックは、アプリの [**CoreWindow**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreWindow) の [**CoreDispatcher**](https://docs.microsoft.com/uwp/api/Windows.UI.Core.CoreDispatcher) によって処理されるイベント メッセージとして発生します。 このコールバックは、アプリのメイン ループ (ビュー プロバイダーの [**IFrameworkView::Run**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run) メソッドで実装) から [**CoreDispatcher::ProcessEvents**](https://docs.microsoft.com/uwp/api/windows.ui.core.coredispatcher.processevents) を呼び出さない場合は呼び出されません。

``` syntax
// This method is called after the window becomes active.
void App::Run()
{
    while (!m_windowClosed)
    {
        if (m_windowVisible)
        {
            CoreWindow::GetForCurrentThread()->Dispatcher->ProcessEvents(CoreProcessEventsOption::ProcessAllIfPresent);

            m_main->Update();

            if (m_main->Render())
            {
                m_deviceResources->Present();
            }
        }
        else
        {
            CoreWindow::GetForCurrentThread()->Dispatcher->ProcessEvents(CoreProcessEventsOption::ProcessOneAndAllPending);
        }
    }
}
```

## <a name="related-topics"></a>関連トピック


* [(DirectX および C++) アプリを停止する方法](how-to-suspend-an-app-directx-and-cpp.md)
* [(DirectX および C++) アプリを再開する方法](how-to-resume-an-app-directx-and-cpp.md)

 

 




