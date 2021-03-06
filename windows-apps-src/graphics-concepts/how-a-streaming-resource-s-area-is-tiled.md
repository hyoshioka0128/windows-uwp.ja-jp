---
title: ストリーミング リソースの領域をタイル表示する方法
description: ストリーミング リソースを作成するときは、次元、フォーマット要素のサイズ、およびミップマップや配列スライスの数 (該当する場合) によって、サーフェス領域全体をサポートするために必要なタイルの数が決まります。
ms.assetid: 3485FD8D-2A06-4B0A-8810-ECF37736F94B
keywords:
- ストリーミング リソースの領域をタイル表示する方法
- リソースの領域, タイル表示
- サイズの一覧表, リソース, タイル表示
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 28fac411ad814167dcef3b02424c866bd3453344
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370592"
---
# <a name="how-a-streaming-resources-area-is-tiled"></a>ストリーミング リソースの領域をタイル表示する方法


ストリーミング リソースを作成するときは、次元、フォーマット要素のサイズ、およびミップマップや配列スライスの数 (該当する場合) によって、サーフェス領域全体をサポートするために必要なタイルの数が決まります。 タイル内のピクセル/バイト レイアウトは、実装によって決定されます。 1 つのタイルに収まるピクセル数は、形式の要素のサイズに応じて固定され、標準スウィズルを使用するかどうかに関係なく同じです。

指定されたサーフェスのサイズと形式要素の幅によって使用されるタイルの数は、次のセクションの表に基づいて定義されており、予測可能です。 ミップマップを含むリソースや、サーフェスのサイズがタイルに満たない場合は、いくつかの制約が存在します。「[ミップマップのパッキング](mipmap-packing.md)」を参照してください。

アプリケーションが、ある形式でのメモリへの書き込みと別の形式での読み取りの結果に依存しない限り、複数のストリーミング リソースがさまざまな形式で同一のメモリを指定できます。 ただし、形式が同じ形式ファミリーである場合 (つまり、型指定なしの親の形式が同じである場合)、アプリケーションは、ある形式でのメモリへの書き込みと別の形式での読み取りの結果に依存する可能性があります。 たとえば、DXGI\_形式\_R8G8B8A8\_UNORM と DXGI\_形式\_R8G8B8A8\_UINT に互換性があるが DXGI ではなく\_形式\_R16G16\_UNORM します。

ある形式のデータが別の形式のエイリアスとして定義されている場合は例外です。タイルのすべてのビットに 0 が含まれている場合、そのタイルは、(メモリ レイアウトに関係なく) メモリの内容が 0 であることを解釈する任意の形式で使用できます。 DXGI 形式を 0x00 にタイルが消去されるように、\_形式\_R8\_UNORM DXGI などの形式を使用し、使用\_形式\_R32G32\_FLOAT 型とその内容を表示はまだ (0.0 f, 0.0 f)。

タイル内でのデータのレイアウトは、タイルがリソース全体に割り当てられているかどうかに依存しません。 そのため、たとえば、サーフェスの複数の場所で同時にタイルを再利用し、すべての場所で一貫性のある動作を実現できます。

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
<td align="left"><p><a href="texture2d-and-texture2darray-subresource-tiling.md">Texture2D と Texture2DArray サブリソースのタイル表示</a></p></td>
<td align="left"><p>次の表に、<a href="https://docs.microsoft.com/windows/desktop/direct3dhlsl/sm5-object-texture2d"><strong>Texture2D</strong></a> および <a href="https://docs.microsoft.com/windows/desktop/direct3dhlsl/sm5-object-texture2darray"><strong>Texture2DArray</strong></a> サブリソースがどのようにタイル表示されるかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="texture3d-subresource-tiling.md">Texture3D サブリソースのタイル表示</a></p></td>
<td align="left"><p>次の表に、<a href="https://docs.microsoft.com/windows/desktop/direct3dhlsl/sm5-object-texture3d"><strong>Texture3D</strong></a> サブリソースがどのようにタイル表示されるかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="buffer-tiling.md">バッファーのタイル</a></p></td>
<td align="left"><p><a href="introduction-to-buffers.md">バッファー </a> リソースは 64 KB のタイルに分割されます。サイズが 64 KB の倍数でない場合は、最後のタイルに空きが生じます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="mipmap-packing.md">Mipmap のパッキング</a></p></td>
<td align="left"><p>ストリーミング リソースの大きさ、形式、ミップマップの数、配列スライスに応じて、一定の数のミップ (配列スライスごとに) を一定の数のタイルにパッキングできます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ストリーミングのリソースを作成します。](creating-streaming-resources.md)

 

 




