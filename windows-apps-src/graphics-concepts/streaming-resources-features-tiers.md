---
title: ストリーミング リソース機能の階層
description: 以前はタイル化されたリソースと呼ばれる、Direct3D ストリーミングリソースの3層の機能機能に関する記事にアクセスできます。
ms.assetid: 6AE7EA72-3929-4BB4-8780-F0CF26192D87
keywords:
- ストリーミング リソース機能の階層
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: ee27244c4d4c2797b71c9d5c8c2c5185a99596b5
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173056"
---
# <a name="streaming-resources-features-tiers"></a>ストリーミング リソース機能の階層


Direct3D は、機能の 3 階層でストリーミング リソースをサポートします。

階層 1 では、ストリーミング リソースの基本機能を提供します。

階層 2 では、サイズが 1 つ以上の標準タイル形状であるときのパックされないテクスチャ ミップマップの保証や、詳細レベル (LOD) をクランプするため、およびシェーダーの操作に関する状態を取得するためのシェーダー命令、サンプリングされた値をゼロとして処理する NULL マッピングされたタイルからの読み取りなど、階層 1 に含まれない機能が追加されます。

階層 3 では、階層 2 で提供されない Texture3D の機能を追加します。

クエリ関数は Direct3D の各バージョンで利用でき、ストリーミング リソースのハードウェアとドライバーのサポートの検証や、階層レベルの確認に利用します。

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
<td align="left"><p><a href="tier-1.md">レベル 1</a></p></td>
<td align="left"><p>このセクションでは、階層 1 のサポートについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="tier-2.md">レベル 2</a></p></td>
<td align="left"><p>ストリーミング リソースの階層 2 のサポートで、サイズが 1 つ以上の標準タイル形状であるときのパックされないテクスチャ ミップマップの保証や、詳細レベル (LOD) をクランプするため、およびシェーダーの操作に関する状態を取得するためのシェーダー命令、サンプリングされた値をゼロとして処理する NULL マッピングされたタイルからの読み取りなど、階層 1 に含まれない機能が追加されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="tier-3.md">レベル 3</a></p></td>
<td align="left"><p>階層 3 では、<a href="tier-2.md">階層 2</a> の機能に加えて、ストリーミング リソース向けの Texture3D のサポートが追加されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ストリーミング リソース](streaming-resources.md)

 

 




