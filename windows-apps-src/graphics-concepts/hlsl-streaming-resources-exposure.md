---
title: HLSL ストリーミング リソースの露出
description: シェーダー モデル 5 のストリーミング リソースをサポートするには、Microsoft 上位レベル シェーダー言語 (HLSL) の特定の構文が必要です。
ms.assetid: 00A40D82-0565-43DC-82AB-0675B7E772E3
keywords:
- HLSL ストリーミング リソースの露出
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: decb0ff2d791417326a70b06c0fdd6a25ea2d119
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173086"
---
# <a name="hlsl-streaming-resources-exposure"></a>HLSL ストリーミング リソースの露出


[シェーダー モデル 5](/windows/desktop/direct3dhlsl/d3d11-graphics-reference-sm5) のストリーミング リソースをサポートするには、Microsoft 上位レベル シェーダー言語 (HLSL) の特定の構文が必要です。

シェーダー モデル 5 の HLSL 構文は、ストリーミング リソースのサポートを備えたデバイスでのみ使用できます。 次の表のストリーミング リソース用の関連する各 HLSL メソッドでは、1 つ (フィードバック) または 2 つ (クランプとフィードバックをこの順序で) の追加の省略可能なパラメーターを指定できます。 **Sample** メソッドの例を示します。

**Sample (サンプラー、location \[ 、offset \[ 、クランプ \[ 、フィードバック \] \] \] )**

**Sample** メソッドの例は、[**Texture2D.Sample(S,float,int,float,uint)**](/windows/desktop/direct3dhlsl/t2darray-sample-s-float-int-float-uint-) のようになります。

offset、clamp、feedback の各パラメーターは省略可能です。 必要なパラメーターまで、すべての省略可能なパラメーターを指定する必要があります。これは、C++ の既定の関数の引数に関する規則と一貫しています。 たとえば、フィードバックの状態が必要な場合、**Sample** に対して、論理的には必要ではない場合でも、offset および clamp の両方のパラメーターを明示的に指定する必要があります。

clamp パラメーターは、浮動小数点のスカラー値です。 リテラル値の clamp = 0.0f は、クランプ操作が実行されていないことを示します。

feedback パラメーターは **uint** 変数で、メモリ アクセス照会の組み込み関数 [**CheckAccessFullyMapped**](/windows/desktop/direct3dhlsl/checkaccessfullymapped) に対して指定できます。 feedback パラメーターの値を変更または解釈しないでください。コンパイラでは、値を変更したかどうかを検出するための高度な分析と診断の機能は提供されません。

[**CheckAccessFullyMapped**](/windows/desktop/direct3dhlsl/checkaccessfullymapped) の構文は次のとおりです。

**bool CheckAccessFullyMapped(in uint FeedbackVar);**

[**CheckAccessFullyMapped**](/windows/desktop/direct3dhlsl/checkaccessfullymapped) は、*FeedbackVar* の値を解釈し、アクセスされているすべてのデータがリソースにマップされていた場合は true を返します。それ以外の場合、**CheckAccessFullyMapped** は false を返します。

clamp と feedback のいずれかのパラメーターが存在する場合、コンパイラは、基本的な命令のバリアントを出力します。 たとえば、ストリーミング リソースのサンプルは、`sample_cl_s` 命令を生成します。

clamp も feedback も指定しない場合、現在の動作と変わらないようにするために、コンパイラは基本的な命令を出力します。

クランプ値が 0.0f である場合、クランプは実行されません。したがって、ドライバーのコンパイラは対象ハードウェアに合わせて命令をさらに調整することができます。 フィードバックが命令で NULL レジスタである場合、フィードバックは使用されていません。したがって、ドライバーのコンパイラはターゲット アーキテクチャに合わせて命令をさらに調整することができます。

HLSL コンパイラは、クランプが 0.0f であり、フィードバックが使用されていないことを推測する場合、対応する基本的な命令 (たとえば、`sample_cl_s` ではなく `sample` ) を生成します。

ストリーミング リソースへのアクセスが、複数のバイト コード命令で構成される場合 (構造化されたリソースなど)、コンパイラは OR 演算によって個別のフィードバック値を集計し、最終的なフィードバック値を生成します。 そのため、このような複雑なアクセスでも、1 つのフィードバック値が示されます。

フィードバックやクランプをサポートするために変更される HLSL メソッドをまとめた表を次に示します。 これらは、あらゆるサイズのタイル リソースや非ストリーミング リソースで動作します。 非ストリーミング リソースは、常に、完全にマップされているように表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><a href="/windows/desktop/direct3dhlsl/d3d11-graphics-reference-sm5-objects">HLSL オブジェクト</a> </th>
<th align="left">フィードバック オプションを持つ組み込みメソッド (*) - クランプ オプションも持つ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[RW]Texture2D</p>
<p>[RW]Texture2DArray</p>
<p>TextureCUBE</p>
<p>TextureCUBEArray</p></td>
<td align="left"><p>Gather</p>
<p>GatherRed</p>
<p>GatherGreen</p>
<p>GatherBlue</p>
<p>GatherAlpha</p>
<p>GatherCmp</p>
<p>GatherCmpRed</p>
<p>GatherCmpGreen</p>
<p>GatherCmpBlue</p>
<p>GatherCmpAlpha</p></td>
</tr>
<tr class="even">
<td align="left"><p>[RW]Texture1D</p>
<p>[RW]Texture1DArray</p>
<p>[RW]Texture2D</p>
<p>[RW]Texture2DArray</p>
<p>[RW]Texture3D</p>
<p>TextureCUBE</p>
<p>TextureCUBEArray</p></td>
<td align="left"><p>Sample*</p>
<p>SampleBias*</p>
<p>SampleCmp*</p>
<p>SampleCmpLevelZero</p>
<p>SampleGrad*</p>
<p>SampleLevel</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[RW]Texture1D</p>
<p>[RW]Texture1DArray</p>
<p>[RW]Texture2D</p>
<p>Texture2DMS</p>
<p>[RW]Texture2DArray</p>
<p>Texture2DArrayMS</p>
<p>[RW]Texture3D</p>
<p>[RW]Buffer</p>
<p>[RW]ByteAddressBuffer</p>
<p>[RW]StructuredBuffer</p></td>
<td align="left">[読み込み]</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ストリーミング リソースへのパイプライン アクセス](pipeline-access-to-streaming-resources.md)

 

 