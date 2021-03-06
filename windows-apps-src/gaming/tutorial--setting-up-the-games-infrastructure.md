---
title: ゲーム プロジェクトのセットアップ
description: ゲームを作るための最初の手順は、必要なコード インフラストラクチャ作業の量を最小限に抑えるように Microsoft Visual Studio でプロジェクトを設定することです。
ms.assetid: 9fde90b3-bf79-bcb3-03b6-d38ab85803f2
ms.date: 10/24/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, セットアップ, DirectX
ms.localizationpriority: medium
ms.openlocfilehash: ca91926ec374015eeb88be6d89d3e1741d8b9c6d
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66367681"
---
# <a name="set-up-the-game-project"></a>ゲーム プロジェクトのセットアップ

このトピックでは、Visual Studio でテンプレートを使用してシンプルな UWP DirectX ゲームを設定する方法について説明します。 ゲームを作るための最初の手順は、必要なコード インフラストラクチャ作業の量を最小限に抑えるように Microsoft Visual Studio でプロジェクトを設定することです。 適切なテンプレートを使い、ゲーム開発用にプロジェクトを構成することで、設定にかかる時間を大幅に節約できることを説明します。

## <a name="objectives"></a>目標

* Visual Studio でテンプレートを使用して Direct3D ゲーム プロジェクトを設定する
* **App** ソース ファイル調べることによって、ゲームのメイン エントリ ポイントを理解する
* プロジェクトの **package.appxmanifest** ファイルを確認する
* プロジェクトに含まれているゲーム開発ツールやサポートを調べる

## <a name="how-to-set-up-the-game-project"></a>ゲーム プロジェクトを設定する方法

初めてユニバーサル Windows プラットフォーム (UWP) 向けの開発を行う場合は、Visual Studio でテンプレートを使用して、基本的なコード構造を設定することをお勧めします。

>[!Note]
>この記事は、ゲーム サンプルに基づく一連のチュートリアルの一部です。 最新のコードは、[Direct3D ゲーム サンプルに関するページ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Simple3DGameDX)で入手できます。 このサンプルは、UWP 機能のサンプルの大規模なコレクションの一部です。 サンプルをダウンロードする手順については、「[GitHub から UWP のサンプルを取得する](https://docs.microsoft.com/windows/uwp/get-started/get-uwp-app-samples)」をご覧ください。

### <a name="use-directx-template-to-create-a-project"></a>DirectX テンプレートを使用してプロジェクトを作成する

Visual Studio テンプレートは、優先する言語および技術に基づいて、特定の種類のアプリ向けの設定とコード ファイルを集めたものです。 Microsoft Visual Studio 2017 では、多数のゲームおよびグラフィックスのアプリ開発が大幅に軽減できるテンプレートがあります。 テンプレートを使わない場合、基本的なグラフィックス レンダリングや表示フレームワークの大部分を自分で開発しなければならず、これは新人のゲーム開発者にとっては骨の折れる仕事となります。

このチュートリアルで使用するテンプレートは、**DirectX 11 アプリ (ユニバーサル Windows)** です。 

Visual Studio で DirectX 11 ゲーム プロジェクトを作成する手順を以下に示します。
1.  選択**ファイル.** &gt; **新しい**&gt; **プロジェクト.**
2.  左側のウィンドウで次のように選択します**インストール済み** &gt; **テンプレート** &gt; **Visual c** &gt; **Windows ユニバーサル。**
3.  中央のウィンドウで、 **[DirectX 11 アプリ (ユニバーサル Windows)]** テンプレートを選びます。
4.  ゲーム プロジェクトに名前を付けて、 **[OK]** をクリックします。

![新しいゲーム プロジェクトを作成するための DirectX 11 テンプレートを選択する方法を示すスクリーン ショット](images/simple-dx-game-setup-new-project.png)

このテンプレートは、DirectX と C++ を使った UWP アプリの基本的なフレームワークを提供します。 F5 キーを押して、アプリをビルドし、実行します。 パウダー ブルーの画面を確認します。 このテンプレートは、DirectX と C++ を使った UWP アプリの基本的な機能が含まれているコード ファイルを複数作成します。

## <a name="review-the-apps-main-entry-point-by-understanding-iframeworkview"></a>IFrameworkView を理解することによりアプリのメイン エントリ ポイントを確認する

**App** クラスは **IFrameworkView** クラスを継承します。

### <a name="inspect-apph"></a>**App.h** を調べる

短時間で 5 つの方法を見てみましょう**App.h** &mdash; [**初期化**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.initialize)、 [ **SetWindow** ](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.setwindow)、 [**ロード**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.load)、 [**実行**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.run)、および[**初期化**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview.uninitialize)を実装する場合、 [ **IFrameworkView** ](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication.run)ビュー プロバイダーを定義するインターフェイス。 これらのメソッドはゲームの起動時に作成されるアプリ シングルトンによって実行され、適切なイベント ハンドラーに接続されて、アプリのすべてのリソースが読み込まれます。

```cpp
    // Main entry point for our app. Connects the app with the Windows shell and handle application lifecycle events.
    ref class App sealed : public Windows::ApplicationModel::Core::IFrameworkView
    {
    public:
        App();

        // IFrameworkView Methods.
        virtual void Initialize(Windows::ApplicationModel::Core::CoreApplicationView^ applicationView);
        virtual void SetWindow(Windows::UI::Core::CoreWindow^ window);
        virtual void Load(Platform::String^ entryPoint);
        virtual void Run();
        virtual void Uninitialize();

    protected:
        ...
    };
```

### <a name="inspect-appcpp"></a>**App.cpp** を調べる

**App.cpp** ソース ファイル内の **main** メソッドを以下に示します。

```cpp
//The main function is only used to initialize our IFrameworkView class.
[Platform::MTAThread]
int main(Platform::Array<Platform::String^>^)
{
    auto direct3DApplicationSource = ref new Direct3DApplicationSource();
    CoreApplication::Run(direct3DApplicationSource);
    return 0;
}
```

このメソッドは、ビューのプロバイダー ファクトリから Direct3D ビュー プロバイダーのインスタンスを作成します (**Direct3DApplicationSource**で定義された`App.h`) を呼び出すことによってアプリ シングルトンに渡す[ **CoreApplication::Run**](/uwp/api/windows.applicationmodel.core.coreapplication.run)します。 フレームワークのビューのメソッド (これは、**アプリ**この例ではクラス) の順序で呼び出されます**初期化**-**SetWindow** -**ロード**-**OnActivated**-**実行**-**初期化**します。 呼び出す**CoreApplication::Run**がその lifycycle 開始されます。 実装の本体で、ゲームのメイン ループが存在する、 [ **IFrameworkView::Run**メソッド](/uwp/api/windows.applicationmodel.core.iframeworkview.run)、し、この例では、 **App::Run**します。

**App.cpp** 内でスクロールして **App::Run** メソッドを見つけます。 コードは次のようになります。

```cpp
//This method is called after the window becomes active.
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

このメソッドの特長。ゲームは、ウィンドウが閉じていない場合、すべてのイベントをディスパッチ、タイマーを更新、をレンダリングおよびグラフィックス パイプラインの結果を提供します。 については、これでさらに詳しく話します[UWP アプリのフレームワークを定義](tutorial--building-the-games-uwp-app-framework.md)、[レンダリング framework i:レンダリングの概要](tutorial--assembling-the-rendering-pipeline.md)、および[レンダリング framework II:ゲームのレンダリング](tutorial-game-rendering.md)します。 これで、UWP DirectX ゲームのコードの基本構造については理解できました。

## <a name="review-and-update-the-packageappxmanifest-file"></a>package.appxmanifest ファイルを確認して更新する


テンプレートに含まれるのはコード ファイルだけではありません。 **Package.appxmanifest** ファイルには、ゲームのパッケージ化と起動や Microsoft Store への提出に使うプロジェクトのメタデータが含まれます。 プレイヤーのシステムがゲームの実行に必要なリソースへのアクセスを提供するための、重要な情報も含まれます。

**ソリューション エクスプローラー**で **Package.appxmanifest** ファイルをダブルクリックして、**マニフェスト デザイナー**を起動します。

![package.appxmanifest エディターのスクリーンショット。](images/simple-dx-game-setup-app-manifest.png)

**package.appxmanifest** ファイルとパッケージ化について詳しくは、[マニフェスト デザイナー](https://docs.microsoft.com/previous-versions/br230259(v=vs.140))に関するページをご覧ください。 それでは、 **[機能]** タブとそのオプションを見てみましょう。

![Direct3D アプリの既定の機能のスクリーンショット。](images/simple-dx-game-setup-capabilities.png)

グローバルなハイ スコア ボードのための**インターネット**へのアクセスなど、ゲームで使う機能を選択しないと、該当するリソースや機能にアクセスできません。 新しいゲームを作る場合、ゲームの実行に必要な機能を忘れずに選択してください。

次に、**DirectX 11 アプリ (ユニバーサル Windows)** テンプレートの残りのファイルを見てみましょう。

## <a name="review-the-included-libraries-and-headers"></a>含まれているライブラリとヘッダーを確認する

まだ確認していないファイルがいくつかあります。 それは、Direct3D ゲーム開発シナリオに共通するその他のツールとサポートを提供するファイルです。 基本的な DirectX ゲーム プロジェクトに付属しているすべてのファイルの一覧については、「[DirectX ゲーム プロジェクト テンプレート](user-interface.md#template-structure)」を参照してください。

| テンプレート ソース ファイル         | ファイル フォルダー            | 説明 |
|------------------------------|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DeviceResources.h/.cpp       | 共通                 | すべての DirectX [デバイス リソース](tutorial--assembling-the-rendering-pipeline.md#resource)を制御するクラス オブジェクトを定義します。 デバイスが消失または作成されたときに通知される DeviceResources を所有しているアプリケーションのインターフェイスも含まれています。                                                |
| DirectXHelper.h              | 共通                 | **DX::ThrowIfFailed**、**ReadDataAsync**、**ConvertDipsToPixels などのメソッドを実装します。 **DX::ThrowIfFailed** は、DirectX Win32 API によって返されたエラー HRESULT 値を Windows ランタイム例外に変換します。 このメソッドを使って、DirectX エラーをデバッグするためのブレーク ポイントを配置します。 詳しくは、[ThrowIfFailed](https://github.com/Microsoft/DirectXTK/wiki/ThrowIfFailed) をご覧ください。 **ReadDataAsync** は、バイナリ ファイルから非同期的に読み取ります。 **ConvertDipsToPixels** は、デバイスに依存しないピクセル (DIP) 単位の長さを物理ピクセル単位の長さに変換します。 |
| StepTimer.h                  | 共通                 | ゲーム アプリまたは対話型レンダリング アプリで役に立つ、高分解能タイマーを定義します。   |
| Sample3DSceneRenderer.h/.cpp | Content                | 基本的なレンダリング パイプラインのインスタンスを作成するクラス オブジェクトを定義します。 DirectX を使った UWP に Direct3D スワップ チェーンとグラフィックス アダプターを接続する基本的なレンダラー実装を作成します。   |
| SampleFPSTextRenderer.h/.cpp | Content                | Direct2D と DirectWrite を使って画面の右下隅に現在の FPS (1 秒あたりのフレーム数) 値をレンダリングするクラス オブジェクトを定義します。  |
| SamplePixelShader.hlsl       | Content                | 非常に基本的なピクセル シェーダー用の上位レベル シェーダー言語 (HLSL) コードが含まれます。                                            |
| SampleVertexShader.hlsl      | Content                | 非常に基本的な頂点シェーダー用の上位レベル シェーダー言語 (HLSL) コードが含まれます。                                           |
| ShaderStructures.h           | Content                | MVP 行列と頂点単位のデータを頂点シェーダーに送信するために使用できるシェーダー構造体が含まれています。  |
| pch.h/.cpp                   | メイン                   | DirectX 11 API など、Direct3D アプリで使われる API 用のすべての Windows システム インクルードが含まれます。| 

### <a name="next-steps"></a>次のステップ

これで、**DirectX 11 アプリ (ユニバーサル Windows)** テンプレートを使用して UWP DirectX ゲーム プロジェクトを作成する方法と、このプロジェクトで提供されるいくつかのコンポーネントとファイルについての説明が終わりました。

次のセクションは、「[ゲームのユニバーサル Windows プラットフォーム (UWP) アプリ フレームワークの定義](tutorial--building-the-games-uwp-app-framework.md)」です。 テンプレートで提供される概念やコンポーネントの多くを、このゲームでどのように使用し、拡張しているかについて説明します。

 

 




