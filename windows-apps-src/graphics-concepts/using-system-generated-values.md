---
title: システム生成値の使用
description: システム生成値は、シェーダー操作で一定の効率を実現するために、入力アセンブラー (IA) ステージで (ユーザー指定の入力セマンティクスに基づいて) 生成されます。
ms.assetid: C7CBA81D-68CA-4E9A-95E3-8185C280C843
keywords:
- システム生成値の使用
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 7217b52c6e9f9882997649c5f843eb119d741e0b
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89156156"
---
# <a name="span-iddirect3dconceptsusing_system-generated_valuesspanusing-system-generated-values"></a><span id="direct3dconcepts.using_system-generated_values"></span>システム生成値の使用


システムによって生成される値は、シェーダー操作の特定の効率を実現するために、 [入力アセンブラー (IA) ステージ](input-assembler-stage--ia-.md) (ユーザー指定の入力 [セマンティクス](/windows/desktop/direct3dhlsl/dx-graphics-hlsl-semantics)に基づく) によって生成されます。 インスタンス ID ([頂点シェーダー (VS) ステージ](vertex-shader-stage--vs-.md)で参照可能)、頂点 ID (VS で参照可能)、またはプリミティブ ID ([ジオメトリ シェーダー (GS) ステージ](geometry-shader-stage--gs-.md)/[ピクセル シェーダー (PS) ステージ](pixel-shader-stage--ps-.md)で参照可能) などのデータをアタッチするとにより、その後のシェーダー ストレージがそれらのシステム値を探して、そのステージでの処理を最適化できるようになります。

たとえば、VS ステージでは、インスタンス ID を参照してシェーダー用の頂点ごとの追加データを取得したり、その他の操作を実行したりできます。GS ステージや PS ステージでは、プリミティブ ID を使ってプリミティブごとのデータを同じように取得できます。

## <a name="span-idvertexidspanspan-idvertexidspanspan-idvertexidspanvertexid"></a><span id="VertexID"></span><span id="vertexid"></span><span id="VERTEXID"></span>VertexID


頂点 ID は、各シェーダー ステージでそれぞれの頂点を識別するために使われます。 これは 32 ビットの符号なし整数で、既定値は 0 です。 [入力アセンブラー (IA) ステージ](input-assembler-stage--ia-.md)でプリミティブが処理されるときに、頂点に割り当てられます。 IA ステージで頂点ごとの ID を生成するように指定するには、シェーダーの入力宣言に頂点 ID のセマンティックをアタッチします。

IA は、頂点 ID を各頂点に追加して、シェーダー ステージで使用できるようにします。 描画が呼び出されるたびに、頂点 ID は 1 ずつ増加します。 インデックス付きの描画呼び出しの間では、カウントが開始値にリセットされます。 頂点 ID がオーバーフローした場合 (2³²– 1 を超えた場合) は 0 に戻ります。

すべてのプリミティブ型の頂点には、(近接性にかかわらず) 頂点 ID が関連付けられます。

## <a name="span-idprimitiveidspanspan-idprimitiveidspanspan-idprimitiveidspanprimitiveid"></a><span id="PrimitiveID"></span><span id="primitiveid"></span><span id="PRIMITIVEID"></span>PrimitiveID


プリミティブ ID は、各シェーダー ステージでそれぞれのプリミティブを識別するために使われます。 これは 32 ビットの符号なし整数で、既定値は 0 です。 [入力アセンブラー (IA) ステージ](input-assembler-stage--ia-.md)でプリミティブが処理されるときに、プリミティブに割り当てられます。 IA ステージでプリミティブ ID を生成するように指定するには、シェーダーの入力宣言にプリミティブ ID のセマンティックをアタッチします。

IA ステージは、各プリミティブにプリミティブ ID を追加して、[ジオメトリ シェーダー (GS) ステージ](geometry-shader-stage--gs-.md)または[頂点シェーダー (VS) ステージ](vertex-shader-stage--vs-.md) (IA ステージ後に最初にアクティブになった方のステージ) で使用できるようにします。 インデックス付きの描画が呼び出されるたびに、プリミティブ ID は 1 ずつ増加します。ただし、新しいインスタンスの開始時には常にインスタンス ID が 0 にリセットされます。 その他の描画呼び出しでは、インスタンス ID の値は変わりません。 インスタンス ID がオーバーフローした場合 (2³²– 1 を超えた場合) は 0 に戻ります。

[ピクセル シェーダー (PS) ステージ](pixel-shader-stage--ps-.md)には、プリミティブ ID 用の入力はありません。ただし、プリミティブ ID を指定するピクセル シェーダー入力では、定数補間モードが使われます。

隣接プリミティブに対するプリミティブ ID の自動生成はサポートされていません。 隣接性を持つトライアングル ストリップなど、隣接性のあるプリミティブ型では、隣接性を持たないトライアングル ストリップ内のプリミティブ セットのような内部プリミティブ (非隣接プリミティブ) に対してのみ、プリミティブ ID が維持されます。

## <a name="span-idinstanceidspanspan-idinstanceidspanspan-idinstanceidspaninstanceid"></a><span id="InstanceID"></span><span id="instanceid"></span><span id="INSTANCEID"></span>InstanceID


インスタンス ID は、各シェーダー ステージで現在処理されているジオメトリのインスタンスを識別するために使われます。 これは 32 ビットの符号なし整数で、既定値は 0 です。

頂点シェーダーの入力宣言にインスタンス ID のセマンティックが含まれている場合、[入力アセンブラー (IA) ステージ](input-assembler-stage--ia-.md) は各頂点にインスタンス ID を追加します。 インデックス付きの描画が呼び出されるたびに、インスタンス ID は 1 ずつ増加します。 その他の描画呼び出しでは、インスタンス ID の値は変わりません。 インスタンス ID がオーバーフローした場合 (2³²– 1 を超えた場合) は 0 に戻ります。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>よう


次の図は、[入力アセンブラー (IA) ステージ](input-assembler-stage--ia-.md)で、インスタンス化されたトライアングル ストリップにどのようにシステム値がアタッチされるかを示しています。

![インスタンス化されたトライアングル ストリップのシステム値の図](images/d3d10-ia-example.png)

下の表は、同じサンプル トライアングル ストリップの 2 つのインスタンスに対して生成されるシステム値を示したものです。 最初のインスタンス (インスタンス U) は青で示され、2 番目のインスタンス (インスタンス V) は緑で示されています。 実線はプリミティブ内の頂点を結び、破線は隣接頂点を結んでいます。

次の表に、インスタンス U のシステム生成値を示します。

| 頂点データ    | C,U | D,U | E,U | F,U | G,U | H,U | I,U | J,U | K,U | L,U |
|----------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| **VertexID**   | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
| **InstanceID** | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   |

 

トライアングル ストリップのインスタンス U には 3 つの三角形プリミティブがあり、次のシステム生成値が与えられます。

|                 |     |     |     |
|-----------------|-----|-----|-----|
| **PrimitiveID** | 0   | 1   | 2   |
| **InstanceID**  | 0   | 0   | 0   |

 

次の表に、インスタンス V のシステム生成値を示します。

| 頂点データ    | C,V | D,V | E,V | F,V | G,V | H,V | I,V | J,V | K,V | L,V |
|----------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| **VertexID**   | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
| **InstanceID** | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   |

 

トライアングル ストリップのインスタンス V には 3 つの三角形プリミティブがあり、次のシステム生成値が与えられます。

|                 |     |     |     |
|-----------------|-----|-----|-----|
| **PrimitiveID** | 0   | 1   | 2   |
| **InstanceID**  | 1   | 1   | 1   |

 

[入力アセンブラー (IA) ステージ](input-assembler-stage--ia-.md)では、頂点、プリミティブ、インスタンスの ID が生成されます。各インスタンスには、一意のインスタンス ID が与えられることに注意してください。 データはストリップ カットで終了し、それによってトライアングル ストリップの各インスタンスが分離されます。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[入力アセンブラー (IA) ステージ](input-assembler-stage--ia-.md)

 

 