---
title: 反射光
description: 反射光では、光がオブジェクトの表面に当たり、カメラに向かって反射する明るい反射光を指定します。
ms.assetid: 71F87137-B00F-48CE-8E6A-F98A139A742A
keywords:
- 反射光
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: f60bd4019f330058d4396a5b0d75d00f90ecff09
ms.sourcegitcommit: 39fb8c0dff1b98ededca2f12e8ea7977c2eddbce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91750188"
---
# <a name="specular-lighting"></a>反射光


*反射光*では、光がオブジェクトの表面に当たり、カメラに向かって反射する明るい反射光を指定します。 反射光は拡散光よりも強い光で、オブジェクトの表面から短時間で消えます。 反射光の方が拡散光よりも計算に時間がかかりますが、反射光を使用すると、表面の表現力が格段に向上します。

反射光のモデリングでは、光が進む方向と、見る人の目の方向をシステムが認識している必要があります。 システムはフォン反射光モデルの簡易版を使用します。これは、中間ベクトルを使用して、反射光のおおよその強さを計算します。

既定の光源の状態では、反射光は計算されません。

## <a name="span-idspecular_lighting_equationspanspan-idspecular_lighting_equationspanspan-idspecular_lighting_equationspanspecular-lighting-equation"></a><span id="Specular_Lighting_Equation"></span><span id="specular_lighting_equation"></span><span id="SPECULAR_LIGHTING_EQUATION"></span>反射光の方程式


反射光は次の方程式で表されます。

> 反射光 = Cs \* sum \[ Ls \* (N)H)<sup>P</sup> \* \*\]

変数とその型および範囲は次のとおりです。

| パラメーター    | 既定値 | Type                                                             | 説明                                                                                            |
|--------------|---------------|------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| Cₛ           | (0,0,0,0)     | 赤、緑、青、およびアルファ透明度 (浮動小数点値) | 反射の色。                                                                                        |
| Sum          | 該当なし           | 該当なし                                                              | 各ライトの鏡面コンポーネントの総和。                                                          |
| N            | 該当なし           | 3D ベクトル (x、y、z 浮動小数点値)                    | 頂点法線。                                                                                         |
| H            | 該当なし           | 3D ベクトル (x、y、z 浮動小数点値)                    | 中間ベクトル。 中間ベクトルのセクションを参照してください。                                                |
| <sup>P</sup> | 0.0           | 浮動小数点数                                                   | 鏡面反射の係数。 範囲は 0 から +infinity です。                                                     |
| Lₚ           | (0,0,0,0)     | 赤、緑、青、およびアルファ透明度 (浮動小数点値) | 明るい鏡面色。                                                                                  |
| Atten        | 該当なし           | 浮動小数点数                                                   | 光の減衰値。 「[減衰とスポットライト係数](attenuation-and-spotlight-factor.md)」を参照してください。 |
| スポット         | 該当なし           | 浮動小数点数                                                   | スポットライト係数。 「[減衰とスポットライト係数](attenuation-and-spotlight-factor.md)」を参照してください。        |

 

Cₛ の値は以下のどちらかになります。

-   頂点の色 1。鏡面マテリアル ソースが拡散の頂点の色であり、最初の頂点の色が頂点の宣言において指定されている場合。
-   頂点の色 2。鏡面マテリアル ソースが反射の頂点の色であり、2 番目の頂点の色が頂点の宣言において指定されている場合。
-   マテリアルの反射色

**メモ**   スペキュラマテリアルソースオプションが使用されており、頂点の色が指定されていない場合は、素材の反射色が使用されます。

 

反射コンポーネントは、すべての光が個別に処理されて補間されると、0 ～ 255 になるようにクランプされます。

## <a name="span-idthe_halfway_vectorspanspan-idthe_halfway_vectorspanspan-idthe_halfway_vectorspanthe-halfway-vector"></a><span id="The_Halfway_Vector"></span><span id="the_halfway_vector"></span><span id="THE_HALFWAY_VECTOR"></span>中間ベクトル


中間ベクトル (H) は、オブジェクトの頂点から光源までのベクトルと、オブジェクトの頂点からカメラの市場でのベクトルの 2 つのベクトルの中間に存在しています。 Direct3D では、中間ベクトルの計算に 2 通りの方法を用意しています。 (直角の反射光ではなく) カメラと相対的な反射光が有効な場合、カメラの位置と頂点の位置の他、光の方向ベクトルを併せて使用して、中間ベクトルを計算します。 これは次の数式で表されます。

> H = norm(norm(Cₚ - Vₚ) + L<sub>dir</sub>)

 

| パラメーター       | 既定値 | Type                                          | 説明                                                  |
|-----------------|---------------|-----------------------------------------------|--------------------------------------------------------------|
| Cₚ              | 該当なし           | 3D ベクトル (x、y、z 浮動小数点値) | カメラの位置。                                             |
| Vₚ              | 該当なし           | 3D ベクトル (x、y、z 浮動小数点値) | 頂点の位置。                                             |
| L<sub>dir</sub> | 該当なし           | 3D ベクトル (x、y、z 浮動小数点値) | 頂点の位置からライトの位置への方向ベクトル。 |

 

この方法で中間ベクトルを決定すると、計算の負荷が高くなる可能性があります。 または、(カメラと相対的な反射光ではなく) 直角反射光を使用する場合は、視点までの z 軸上の距離が無限であるものとして扱われます。 この式は次のようになります。

> H = norm((0,0,1) + L<sub>dir</sub>)

この設定は計算の負荷は低くなりますが、精度も落ちるため、正投影を使用するアプリケーションでの使用が最適です。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>よう


この例では、オブジェクトの色は、シーンの反射光の色とマテリアルの反射色を使用しています。

この方程式では、生成されるオブジェクトの頂点の色は、マテリアルの色と光の色の組み合わせになります。

次の 2 つの図は、鏡面マテリアルの色 (灰色) と、反射光の色 (白) を表しています。

![灰色の球体の図](images/amb1.jpg)![白の球体の図](images/lightwhite.jpg)

生成された反射光は、次の図のようになります。

![反射光の図](images/lights.jpg)

反射光に環境光と拡散光を追加すると、次の図のようになります。 これら 3 種類の光をすべて使用すると、本物のオブジェクトにより近い表現ができます。

![反射光、環境光、拡散光を組み合わせた結果の図](images/lightads.jpg)

反射光は、拡散光よりも計算の負荷が高くなります。 これは通常、表面の材質についての視覚的な手がかりを提供するために使用されます。 反射光は表面のマテリアルのサイズと色によって変化します。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[光源の計算](mathematics-of-lighting.md)

 

 




