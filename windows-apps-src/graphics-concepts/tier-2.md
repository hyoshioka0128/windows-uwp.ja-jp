---
title: レベル 2
description: ストリーミング リソースの階層 2 のサポートで、サイズが 1 つ以上の標準タイル形状であるときのパックされないテクスチャ ミップマップの保証や、詳細レベル (LOD) をクランプするため、およびシェーダーの操作に関する状態を取得するためのシェーダー命令、サンプリングされた値をゼロとして処理する NULL マッピングされたタイルからの読み取りなど、階層 1 に含まれない機能が追加されます。
ms.assetid: 111A28EA-661A-4D29-921A-F2E376A46DC5
keywords:
- レベル 2
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 62fbbf3f21d614739918478b58394e51dbe577f9
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89175166"
---
# <a name="tier-2"></a>レベル 2


ストリーミング リソースの階層 2 のサポートで、サイズが 1 つ以上の標準タイル形状であるときのパックされないテクスチャ ミップマップの保証や、詳細レベル (LOD) をクランプするため、およびシェーダーの操作に関する状態を取得するためのシェーダー命令、サンプリングされた値をゼロとして処理する NULL マッピングされたタイルからの読み取りなど、階層 1 に含まれない機能が追加されます。

## <a name="span-idtier_2_general_supportspanspan-idtier_2_general_supportspanspan-idtier_2_general_supportspantier-2-general-support"></a><span id="Tier_2_general_support"></span><span id="tier_2_general_support"></span><span id="TIER_2_GENERAL_SUPPORT"></span>階層2の一般サポート


階層 2 のサポートには次のものが含まれます。

-   機能レベル 11.1 以上のハードウェア。
-   前の階層のすべての機能 ([階層 1](tier-1.md) の特定の制限事項なし) に加えて、次のような項目での追加機能があります。
-   LOD のクランプとマップされた状態のフィードバックのためのシェーダー命令を利用できます。 「[HLSL ストリーミング リソースの露出](hlsl-streaming-resources-exposure.md)」をご覧ください。

これらに加えて、次のような特定のサポート問題があります。

## <a name="span-idnon-mapped_tilesspanspan-idnon-mapped_tilesspanspan-idnon-mapped_tilesspannon-mapped-tiles"></a><span id="Non-mapped_tiles"></span><span id="non-mapped_tiles"></span><span id="NON-MAPPED_TILES"></span>マップされていないタイル


マップされていないタイルからの読み取りでは、形式の欠落していないすべてのコンポーネントでは 0 を返し、欠落しているコンポーネントには既定値を返します。

マップされていないタイルへの書き込みは、メモリに移動するのは止められますが、最後にはキャッシュに移動する可能性があり、それ以降の同じアドレスへの読み取りは取得されない可能性があります。

## <a name="span-idtexture_filteringspanspan-idtexture_filteringspanspan-idtexture_filteringspantexture-filtering"></a><span id="Texture_filtering"></span><span id="texture_filtering"></span><span id="TEXTURE_FILTERING"></span>テクスチャのフィルター処理


**NULL** のタイルと **NULL** でないタイルをまたぐフットプリントを含むテクスチャ フィルタリングでは、**NULL** タイル上のテクセルの場合に全体的なフィルター処理に 0 が送られます (欠落した形式コンポーネントの既定値と共に)。 一部の初期のハードウェアはこの要件を満たしていないため、いずれかのテクセル (0 以外の重み付き) が **NULL** タイルにかかる場合、完全なフィルター処理の結果に対して 0 を返します (欠落した形式コンポーネントの既定値と共に)。 その他のハードウェアには、すべての (0 以外の重み付きの) テクセルをフィルター処理に含めるために要件の欠落は許されません。

**NULL** テクセルにアクセスすると、テクスチャの読み取りが false を返すように、状態のフィードバックに [**CheckAccessFullyMapped**](/windows/desktop/direct3dhlsl/checkaccessfullymapped) 操作が行われます。 これは、テクスチャへのアクセスの結果で書き込みがシェーダーでどのようにマスクされるかや、テクスチャ形式に含まれるコンポーネントの数には関係なく行われます (これらの組み合わせによって、テクスチャへのアクセスが必要ないことがわかる場合があります)。

## <a name="span-idalignment_constraintsspanspan-idalignment_constraintsspanspan-idalignment_constraintsspanalignment-constraints"></a><span id="Alignment_constraints"></span><span id="alignment_constraints"></span><span id="ALIGNMENT_CONSTRAINTS"></span>配置の制約


標準のタイル形状の場合の配置の制約: すべての次元で 1 つ以上の標準のタイルを塗りつぶすミップマップは、標準のタイルを使用することが保証され、残りは 1 つの**ユニット**として N 個のタイルにパックされたと見なされます (N はアプリケーションに報告される)。 アプリケーションは、N 個のタイルをタイル プール内の分離された任意の場所にマッピングすることができますが、パックされたタイルのすべてをマッピングするか、すべてをマッピングしないかのいずれかにする必要があります。 ミップ パッキングは、配列スライスごとにパックされたタイルの一意のセットです。

## <a name="span-idmin_max_reduction_filteringspanspan-idmin_max_reduction_filteringspanspan-idmin_max_reduction_filteringspanminmax-reduction-filtering"></a><span id="Min_Max_reduction_filtering"></span><span id="min_max_reduction_filtering"></span><span id="MIN_MAX_REDUCTION_FILTERING"></span>最小/最大削減フィルター処理


最小/最大除去フィルタリングはサポートされます。 「[ストリーミング リソース テクスチャ サンプリング機能](streaming-resources-texture-sampling-features.md)」をご覧ください。

## <a name="span-idlimitationsspanspan-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="Limitations"></span><span id="limitations"></span><span id="LIMITATIONS"></span>事項


いずれかの次元で標準のタイル サイズより小さいミップマップが含まれるストリーミング リソースは、1 より大きい配列サイズを持つことはできません。

重複するマッピングがあるときにタイルにアクセスする方法に関する制限は引き続き適用されます。 「[重複するマッピングを含むタイルのアクセス制限](tile-access-limitations-with-duplicate-mappings.md)」をご覧ください。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[ストリーミング リソース機能の階層](streaming-resources-features-tiers.md)

 

 