---
title: DirectX ゲーム プロジェクト テンプレート
description: ユニバーサル Windows プラットフォーム (UWP) および DirectX ゲームを作成するためのテンプレートについて説明します。
ms.assetid: 41b6cd76-5c9a-e2b7-ef6f-bfbf6ef7331d
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, DirectX, テンプレート
ms.localizationpriority: medium
ms.openlocfilehash: 99d68be96858249fdd314857e1fe6d3020ee56e6
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89159036"
---
# <a name="directx-game-project-templates"></a>DirectX ゲーム プロジェクト テンプレート



DirectX とユニバーサル Windows プラットフォーム (UWP) のテンプレートは、ゲームの出発点として使ってプロジェクトをすばやく作成することができます。

## <a name="prerequisites"></a>前提条件


プロジェクトを作成するには、次の作業が必要です。

-   [Microsoft Visual Studio 2015 をダウンロードします](https://visualstudio.microsoft.com/vs/)。 Visual Studio 2015 には、デバッグ ツールなど、グラフィックス プログラミングのためのツールが含まれています。 DirectX グラフィックス、ゲーム機能、ツールの概要については、「[DirectX ゲーム開発用の Visual Studio ツール](set-up-visual-studio-for-game-development.md)」をご覧ください。

## <a name="choosing-a-template"></a>テンプレートの選択


Visual Studio 2015 には、DirectX と UWP のテンプレートが 3 つ用意されています。

-   DirectX 11 アプリ (ユニバーサル Windows) - DirectX 11 アプリ (ユニバーサル Windows) テンプレートは、DirectX 11 を使ってアプリ ウィンドウに直接レンダリングする UWP プロジェクトを作成します。
-   DirectX 12 アプリ (ユニバーサル Windows) - DirectX 12 アプリ (ユニバーサル Windows) テンプレートは、DirectX 12 を使ってアプリ ウィンドウに直接レンダリングする UWP プロジェクトを作成します。
-   DirectX 11 および XAML アプリ (ユニバーサル Windows) - DirectX 11 および XAML アプリ (ユニバーサル Windows) テンプレートは、DirectX 11 を使って XAML コントロール内にレンダリングする UWP プロジェクトを作成します。 このテンプレートは [**SwapChainPanel**](/uwp/api/Windows.UI.Xaml.Controls.SwapChainPanel) を使うため、XAML UI コントロールを使うことができます。 そのため、ユーザー インターフェイス要素をより簡単に追加できますが、XAML テンプレートを使うとパフォーマンスが低下する場合があります。

どちらのテンプレートを使うかは、必要なパフォーマンスと利用するテクノロジによって異なります。

## <a name="template-structure"></a>テンプレートの構造


DirectX ユニバーサル Windows テンプレートには、次のファイルが含まれています。

-   pch.h and pch.cpp - プリコンパイル済みヘッダーのサポートです。
-   Package.appxmanifest - アプリの展開パッケージのプロパティです。
-   \*.pfx-アプリケーションの証明書。
-   外部の依存関係 - プロジェクトが使う外部ファイルへのリンクです。
-   \*主要な .h と、 \* アプリケーションのアセットを管理し、アプリケーションの状態を更新し、フレームをレンダリングするための手順です。
-   App.h と App.cpp - アプリのメイン エントリ ポイントです。 アプリと Windows シェルを接続し、アプリケーション ライフサイクル イベントを処理します。 これらのファイルは、DirectX 11 アプリ (ユニバーサル Windows) と DirectX 12 アプリ (ユニバーサル Windows) のテンプレートにのみ表示されます。
-   App.xaml、App.xaml.cpp、App.xaml.h - アプリのメイン エントリ ポイントです。 アプリと Windows シェルを接続し、アプリケーション ライフサイクル イベントを処理します。 これらのファイルは、DirectX 11 および XAML アプリ (ユニバーサル Windows) のテンプレートにのみ表示されます。
-   DirectXPage.xaml、DirectXPage.xaml.cpp、DirectXPage.xaml.h - DirectX SwapChainPanel をホストするページ。 これらのファイルは、DirectX 11 および XAML アプリ (ユニバーサル Windows) のテンプレートにのみ表示されます。
-   Content
    -   Sample3DSceneRenderer.h and Sample3DSceneRenderer.cpp - 基本的なレンダリング パイプラインをインスタンス化するサンプル レンダラーです。
    -   SampleFpsTextRenderer.h and SampleFpsTextRenderer.cpp - Direct2D と DirectWrite を使って画面の右下隅に現在の FPS 値をレンダリングします。 これらのファイルは、DirectX 11 アプリ (ユニバーサル Windows) と DirectX 11 および XAML アプリ (ユニバーサル Windows) のテンプレートにのみ表示されます。
    -   SamplePixelShader.hlsl - シンプルなサンプル ピクセル シェーダーです。
    -   SampleVertexShader.hlsl - シンプルなサンプル頂点シェーダーです。
    -   ShaderStructures.h - サンプル頂点シェーダーに日付を送信するために使われる構造体。
-   共通
    -   StepTimer.h - アニメーションとシミュレーションのタイミングを行うためのヘルパー クラスです。
    -   DirectXHelper.h - その他のヘルパー関数。
    -   DeviceResources.h and Device Resources.cpp - 消失または作成されるデバイスについて通知する DeviceResources を所有するアプリケーションにインターフェイスを提供します。
    -   d3dx12.h - D3DX12 ユーティリティ ライブラリが含まれています。 このファイルは、DirectX 12 アプリ (ユニバーサル Windows) にのみ表示されます。
-   アセット - アプリケーションが使うロゴとスプラッシュ画面の画像です。

## <a name="next-steps"></a>次の手順


これで、出発点に立つことができました。次は、ゲーム開発の知識と Microsoft Store ゲームの開発スキルを学びます。

既にあるゲームを移植する場合は、次のトピックをご覧ください。

-   [OpenGL ES 2.0 から Direct3D 11.1 への移植](port-from-opengl-es-2-0-to-directx-11-1.md)
-   [DirectX 9 からユニバーサル Windows プラットフォームへの移植](porting-your-directx-9-game-to-windows-store.md)

新しい DirectX ゲームを作成する場合は、次のトピックをご覧ください。

-   [DirectX によるシンプルな UWP ゲームの作成](tutorial--create-your-first-uwp-directx-game.md)
-   [Marble Maze、C++ と DirectX でのユニバーサル Windows プラットフォーム ゲームの開発](developing-marble-maze-a-windows-store-game-in-cpp-and-directx.md)