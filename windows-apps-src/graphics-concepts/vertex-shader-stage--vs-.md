---
title: 頂点シェーダー (VS) ステージ
description: 頂点シェーダー (VS) ステージでは、頂点を処理し、多くの場合は変換、スキン、照明の適用などの操作を実行します。 頂点シェーダーは 1 つの入力頂点を受け取り、1 つの出力頂点を生成します。
ms.assetid: 5133C4BB-B4E6-4697-9276-F718AD44869C
keywords:
- 頂点シェーダー (VS) ステージ
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 88a990470d0ff8aea5c6415584bd63b2b4b65981
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89156056"
---
# <a name="vertex-shader-vs-stage"></a>頂点シェーダー (VS) ステージ


頂点シェーダー (VS) ステージでは、頂点を処理し、多くの場合は変換、スキン、照明の適用などの操作を実行します。 頂点シェーダーは 1 つの入力頂点を受け取り、1 つの出力頂点を生成します。

## <a name="span-idpurpose_and_usesspanspan-idpurpose_and_usesspanspan-idpurpose_and_usesspanpurpose-and-uses"></a><span id="Purpose_and_uses"></span><span id="purpose_and_uses"></span><span id="PURPOSE_AND_USES"></span>目的と用途


頂点シェーダー (VS) ステージは、頂点ごとに次のような個別の処理を実行するために使われます。

-   変換
-   スキン適用
-   モーフィング
-   頂点ごとの照明の適用

頂点シェーダー ステージはプログラム可能なシェーダー ステージであり、[グラフィックス パイプライン](graphics-pipeline.md)の図では角丸ブロックとして示されています。 このシェーダー ステージではシェーダー モデル 4.0 の[共通シェーダー コア](/windows/desktop/direct3dhlsl/dx-graphics-hlsl-common-core)が使われます。

頂点シェーダー (VS) ステージは、入力アセンブラーから頂点を受け取って処理します。 頂点シェーダーは常に、1 つの入力頂点を処理して 1 つの出力頂点を生成します。 パイプラインを実行するには、頂点シェーダー ステージが常にアクティブになっている必要があります。 頂点の変更や変換が必要ない場合は、パススルー頂点シェーダーを作成してパイプラインに設定する必要があります。

頂点シェーダーの各入力頂点は、最大 16 個の 32 ビット ベクトル (それぞれ最大 4 要素) で構成できます。 各出力頂点は、最大 16 個の 32 ビット 4 要素ベクトルで構成できます。 すべての頂点シェーダーには、少なくとも 1 つの入力と 1 つの出力が必要です。それぞれは 1 つのスカラー値でもかまいません。

頂点シェーダー ステージでは、入力アセンブラーから、VertexID と InstanceID の 2 つのシステム生成値を使うことができます (システム値とセマンティクスに関する説明をご覧ください)。 VertexID と InstanceID はどちらも頂点レベルで有意であり、ハードウェアによって生成された ID を渡すことができるのは、それらを認識する最初のステージだけです。このため、これらの ID は頂点シェーダー ステージにしか渡すことができません。

頂点シェーダーは常にすべての頂点に対して実行され、これには隣接性を持つ入力プリミティブ トポロジ内の隣接頂点も含まれます。 頂点シェーダーが実行された回数は、CPU から VSInvocations パイプライン統計を使って照会できます。

頂点シェーダーでは、スクリーン空間の微分を必要としない読み込み操作とテクスチャのサンプリング操作を実行できます (HLSL 組み込み関数の [Sample (DirectX HLSL テクスチャ オブジェクト)](/windows/desktop/direct3dhlsl/dx-graphics-hlsl-to-sample)、[SampleCmpLevelZero (DirectX HLSL テクスチャ オブジェクト)](/windows/desktop/direct3dhlsl/dx-graphics-hlsl-to-samplecmplevelzero)、[SampleGrad (DirectX HLSL テクスチャ オブジェクト)](/windows/desktop/direct3dhlsl/dx-graphics-hlsl-to-samplegrad) が使われます)。

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


システム生成値 VertexID と InstanceID を持つ単一の頂点。 頂点シェーダーの各入力頂点は、最大 16 個の 32 ビット ベクトル (それぞれ最大 4 要素) で構成できます。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


単一の頂点。 各出力頂点は、最大 16 個の 32 ビット 4 要素ベクトルで構成できます。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[グラフィックス パイプライン](graphics-pipeline.md)

 

 