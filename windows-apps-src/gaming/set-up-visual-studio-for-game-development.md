---
title: ゲーム プログラミング用の Visual Studio ツール
description: イメージエディター、モデルエディター、シェーダーデザイナーなど、Visual Studio で使用できる DirectX ゲームプログラミング用のツールについて説明します。
ms.assetid: 43137bfc-7876-70e0-515c-4722f68bd064
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, UWP, ゲーム, Visual Studio, ツール, DirectX
ms.localizationpriority: medium
ms.openlocfilehash: 250450b2174ce249d1ec5afaf4c5188df9266f5e
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89159266"
---
# <a name="visual-studio-tools-for-game-programming"></a>ゲーム プログラミング用の Visual Studio ツール



**まとめ**

-   [テンプレートからの DirectX ゲーム プロジェクトの作成](user-interface.md)
-   DirectX ゲーム プログラミング用の Visual Studio ツールの使用


Visual Studio Ultimate を使って、DirectX アプリを開発する場合は、画像、モデル、シェーダー リソースを作成、編集、プレビュー、エクスポートするための追加のツールを利用できます。 また、ビルド時のリソースの変換や、DirectX グラフィックス コードのデバッグに使うことができるツールもあります。

このトピックでは、こうしたグラフィックス ツールの概要について説明します。

## <a name="image-editor"></a>イメージ エディター


イメージ エディターは、DirectX で使うリッチ テクスチャと画像形式の種類を操作するのに使います。 イメージ エディターでは、次の形式をサポートしています。

-   .png
-   .jpg、.jpeg、.jpe、.jfif
-   .dds
-   .gif
-   .bmp
-   .dib
-   .tif、.tiff
-   .tga

ビルド時にこれらを .dds ファイルに変換するには、[ビルド カスタマイズ ファイル](#build-customizations-for-3d-assets)を作成します。

詳しくは、「[テクスチャおよびイメージの使用](/visualstudio/designers/working-with-textures-and-images?view=vs-2015)」をご覧ください。

> **メモ**   イメージエディターは、完全な機能イメージ編集アプリに代わるものではありませんが、多くの単純な表示と編集のシナリオに適しています。

 

## <a name="model-editor"></a>モデル エディター


モデル エディターを使うと、基本的な 3D モデルをゼロから作成するや、フル機能を備えた 3D モデリング ツールで作成したもっと複雑な 3D モデルの表示や変更を行うことができます。 モデル エディターは DirectX アプリケーションの開発に使用する複数の 3D モデル形式をサポートしています。 ビルド時に次のファイルを .cmo ファイルに変換する[ビルド カスタマイズ ファイル](#build-customizations-for-3d-assets)を作成できます。

-   .fbx
-   .dae
-   .obj

エディターで照明を適用したモデルのスクリーンショットを次に示します。

![ティーポット](images/modeleditor.png)

詳しくは、「[3-D モデルの操作](/visualstudio/designers/working-with-3-d-models?view=vs-2015)」をご覧ください。

> **メモ**   モデルエディターは、完全な機能モデルの編集アプリに代わるものではありませんが、多くの単純な表示と編集のシナリオに適しています。

 

## <a name="shader-designer"></a>シェーダー デザイナー


HLSL でのプログラミングがわからない場合でも、シェーダー デザイナーを使うと、ゲームやアプリのカスタムの視覚効果を作成できます。

シェーダーはグラフとして視覚的に作成します。 各ノードには、その操作までの出力のプレビューが表示されます。 球体のプレビューでランバート照明を適用した例を次に示します。

![視覚シェーダー グラフ](images/shaderdesigner.png)

シェーダー エディターは、シェーダーを設計、編集、.dgsl 形式で保存するのに使います。 また、次の形式をエクスポートします。

-   .hlsl (ソース コード)
-   .cso (バイトコード)
-   .h (HLSL バイトコード配列)

ビルド時にこれらの形式を .cso ファイルに変換するには、[ビルド カスタマイズ ファイル](#build-customizations-for-3d-assets)を作成します。

シェーダー エディターでエクスポートした HLSL コードの一部を次に示します。 これは、ランバート照明ノードのコードだけです。

```hlsl
//
// Lambert lighting function
//
float3 LambertLighting(
    float3 lightNormal,
    float3 surfaceNormal,
    float3 materialAmbient,
    float3 lightAmbient,
    float3 lightColor,
    float3 pixelColor
    )
{
    // Compute the amount of contribution per light.
    float diffuseAmount = saturate(dot(lightNormal, surfaceNormal));
    float3 diffuse = diffuseAmount * lightColor * pixelColor;

    // Combine ambient with diffuse.
    return saturate((materialAmbient * lightAmbient) + diffuse);
}
```

詳しくは、「[シェーダーの操作](/visualstudio/designers/working-with-shaders?view=vs-2015)」をご覧ください。

## <a name="build-customizations-for-3d-assets"></a>3D アセットのビルドのカスタマイズ


プロジェクトにビルドのカスタマイズを追加して、リソースを Visual Studio で利用できる形式に変換できます。 その後でアプリケーションにアセットを読み込み、他の DirectX アプリケーションと同様に DirectX リソースを作成して入力することにより、アセットを使用できます。

ビルドのカスタマイズを追加するには、 **ソリューションエクスプローラー** でプロジェクトを右クリックし、[ **ビルドのカスタマイズ**] を選択します。プロジェクトには、次の種類のビルドのカスタマイズを追加できます。

-   入力として画像ファイルを受け取り、DirectDraw Surface (.dds) ファイルを出力するイメージ コンテンツ パイプライン。
-   メッシュ ファイル (.fbx など) を受け取り、.cmo メッシュ ファイルを出力するメッシュ コンテンツ パイプライン。
-   Visual Studio シェーダー エディターで作成した視覚シェーダー グラフ (.dgsl) を受け取り、コンパイル済みシェーダー出力 (.cso) ファイルを出力するシェーダー コンテンツ パイプライン。

詳しくは、「[ゲームまたはアプリケーションでの 3-D アセットの使用](/visualstudio/designers/using-3-d-assets-in-your-game-or-app?view=vs-2015)」をご覧ください。

## <a name="debugging-directx-graphics"></a>DirectX グラフィックスのデバッグ


Visual Studio には、グラフィックス固有のデバッグ ツールが用意されています。 これらのツールを使って、次のような項目をデバッグします。

-   グラフィックス パイプライン。
-   イベント呼び出し履歴。
-   オブジェクト テーブル。
-   デバイスの状態。
-   シェーダーのバグ。
-   初期化されていないか、無効な定数バッファーとパラメーター。
-   DirectX バージョンの互換性。
-   制限されている Direct2D のサポート。
-   オペレーティング システムと SDK の要件。

詳しくは、「[DirectX グラフィックスのデバッグ](/visualstudio/debugger/visual-studio-graphics-diagnostics?view=vs-2015)」をご覧ください。


 

 

 