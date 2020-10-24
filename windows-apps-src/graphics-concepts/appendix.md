---
title: 付録
description: 浮動小数点ルールの技術的な詳細、データ型の変換、ラスタライズルール、およびテクスチャブロックの圧縮に関するトピックへのリンクの表を表示します。
ms.assetid: 461CCE6F-BAF0-4965-90A5-FD36B511F72C
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 41762bf24202d155ed7af288ff43ea898b43e46d
ms.sourcegitcommit: 8e0e4cac79554e86dc7f035c4b32cb1f229142b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88942772"
---
# <a name="appendices"></a>付録

これらのセクションでは、技術的な面について詳しく説明します。

## <a name="span-idin-this-sectionspanin-this-section"></a><span id="in-this-section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="floating-point-rules.md">浮動小数点の規則</a></p></td>
<td align="left"><p>Direct3D は、複数の浮動小数点表現をサポートします。 すべての浮動小数点演算は、IEEE 754 32 ビット単精度浮動小数点ルールのサブセットの定義のもとで動作します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="data-type-conversion.md">データ型の変換</a></p></td>
<td align="left"><p>次のセクションでは、Direct3D がデータ型の間の変換を処理する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="rasterization-rules.md">ラスター化ルール</a></p></td>
<td align="left"><p>ラスター化ルールは、ベクトル データをラスター データにマップする方法を定義します。 ラスター データは、整数値の位置に配置されてからカリングおよびクリッピングされ (描画するピクセルの数を最小限にするため)、ピクセル単位の属性が (頂点単位の属性から) 補間された後、ピクセル シェーダーに渡されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="texture-block-compression.md">テクスチャのブロック圧縮</a></p></td>
<td align="left"><p>Direct3D 11 では、テクスチャのブロック圧縮 (BC) サポートが拡張され、BC6H および BC7 アルゴリズムが組み込まれています。 BC6H はハイ ダイナミック レンジのカラー ソース データをサポートし、BC7 は標準 RGB ソース データのアーティファクトを低減して標準よりも優れた品質の圧縮を提供します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[Direct3D グラフィックス学習ガイド](index.md)

 

 




