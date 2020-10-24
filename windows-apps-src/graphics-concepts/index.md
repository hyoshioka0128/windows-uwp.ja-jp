---
title: Direct3D グラフィックスの用語集
description: Direct3D のゲームおよびアプリの開発で使用されている一般的な 3D コンピューター グラフィックス用語の概要を定義する用語集をご確認ください。
ms.assetid: c3850a92-4d05-4f72-bf0f-6a0c79e841eb
keywords:
- Direct3D グラフィックスの用語集
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 3359b81c6932bfc63c3939d2f857aaef9248e52f
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173076"
---
# <a name="direct3d-graphics-glossary"></a>Direct3D グラフィックスの用語集


Microsoft Direct3D グラフィックスの用語を定義します。 この用語集では、Direct3D のゲームおよびアプリの開発で使用されている一般的な 3D コンピューター グラフィックス用語の概要を定義します。

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
<td align="left"><p><a href="coordinate-systems-and-geometry.md">座標系とジオメトリ</a></p></td>
<td align="left"><p>Direct3D アプリケーションをプログラムするには、3D ジオメトリの原理を実務で熟知していることが必要です。 このセクションでは、3D シーンを作成するための最も重要な幾何学的概念について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="vertex-and-index-buffers.md">頂点バッファーとインデックス バッファー</a></p></td>
<td align="left"><p><em>"頂点バッファー"</em> は、頂点データを格納するメモリ バッファーです。頂点バッファー内の頂点は、変換、照明の適用、クリッピングを実行するために処理されます。 <em>インデックス バッファー</em>は、インデックス データを含むメモリ バッファーであり、プリミティブのレンダリングに使用される、頂点バッファーへの整数オフセットです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="devices.md">デバイス</a></p></td>
<td align="left"><p>Direct3D デバイスは、Direct3D のレンダリング コンポーネントです。 デバイスは、レンダリングの状態をカプセル化して格納します。また、変換や照明の操作、サーフェスへのイメージのラスタライズを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="lights-and-materials.md">照明</a></p></td>
<td align="left"><p>光源は、シーン内のオブジェクトを照射するのに使われます。 各オブジェクト頂点の色は、現在のテクスチャ マップ、頂点の色、光源に基づきます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="depth-and-stencil-buffers.md">深度バッファーとステンシル バッファー</a></p></td>
<td align="left"><p><em>深度バッファー</em>には、ビューから隠すのではなくレンダリングする多角形の領域を制御するための深度情報が格納されます。 <em>ステンシル バッファー</em>は、画像内のピクセルをマスクし、合成、デカール、ディゾルブ、フェード、スワイプ、輪郭とシルエット、両面ステンシルなどの特殊効果を生成するために使われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="textures.md">テクスチャ</a></p></td>
<td align="left"><p>テクスチャは、コンピューターにより生成された 3D 画像でリアルさを出すための強力なツールです。 Direct3D は広範囲のテクスチャリング機能セットをサポートし、高度なテクスチャリング手法に簡単にアクセスできる方法を開発者に提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="graphics-pipeline.md">グラフィックス パイプライン</a></p></td>
<td align="left"><p>Direct3D グラフィックス パイプラインは、リアルタイム ゲーム アプリケーション用のグラフィックスを生成できるように設計されています。 データは、構成可能またはプログラミング可能な各ステージを通じて、入力から出力へと流れます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="views.md">ビュー</a></p></td>
<td align="left"><p>&quot;ビュー&quot; という語は、&quot;必要な形式のデータ&quot;を意味します。 たとえば、定数バッファー ビュー (CBV) は、適切な形式の定数バッファー データを表します。 このセクションでは、最もよく使われる便利なビューについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="compute-pipeline.md">計算パイプライン</a></p></td>
<td align="left"><p>Direct3D 計算パイプラインは、大部分がグラフィックス パイプラインと並行して実行可能な計算を処理できるように設計されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="resources.md">リソース</a></p></td>
<td align="left"><p>リソースは、Direct3D パイプラインからアクセスできるメモリ内の領域です。 パイプラインでメモリに効率的にアクセスするには、パイプラインに渡すデータ (入力ジオメトリ、シェーダー リソース、テクスチャなど) をリソースに格納する必要があります。 すべての Direct3D リソースの派生元となるリソースは 2 種類あります。バッファーとテクスチャです。 各パイプライン ステージでは最大 128 個のリソースをアクティブにできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="streaming-resources.md">ストリーミング リソース</a></p></td>
<td align="left"><p><em>ストリーミング リソース</em>は、少量の物理メモリを使用する大規模な論理リソースです。 大きなリソース全体を渡すのではなく、小さなリソースのパーツを必要に応じてストリーミングします。 ストリーミング リソースは、以前は<em>タイル リソース</em>と呼ばれていました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="appendix.md">付録</a></p></td>
<td align="left"><p>これらのセクションでは、技術的な面について詳しく説明します。</p></td>
</tr>
</tbody>
</table>

 

 

 
