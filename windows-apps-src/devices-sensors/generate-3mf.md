---
description: 3D Manufacturing Format (3MF) のファイルの種類の構造について説明し、その作成方法と Windows.Graphics.Printing3D API による操作について説明します。
MS-HAID: dev\_devices\_sensors.generate\_3mf
MSHAttr: PreferredLib:/library/windows/apps
Search.Product: eADQiWindows 10XVcnh
title: 3MF パッケージの生成
ms.assetid: 968d918e-ec02-42b5-b50f-7c175cc7921b
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 7beafb754ead837dd9218d4a9e0223334e12bfb1
ms.sourcegitcommit: a3bbd3dd13be5d2f8a2793717adf4276840ee17d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93034655"
---
# <a name="generate-a-3mf-package"></a>3MF パッケージの生成

**重要な API**

-   [**Printing3D**](/uwp/api/windows.graphics.printing3d)

このガイドでは、3D Manufacturing Format (3MF) ドキュメントの構造について説明し、その作成方法と [**Windows.Graphics.Printing3D**](/uwp/api/windows.graphics.printing3d) API による操作について説明します。

## <a name="what-is-3mf"></a>3MF の概要

3D Manufacturing Format (3MF) は、製造 (3D 印刷) 目的のために、XML を使って 3D モデルの外観と構造を記述するための規則のセットです。 3MF ではパーツ (必須なパーツとオプションのパーツがあります) のセットとそのリレーションシップを定義しています。そのねらいは 3D 製造デバイスのために必要なすべての情報を提供することです。 3MF に準拠したデータセットは .3mf 拡張子を持つファイルとして保存できます。

Windows 10 では、 **Windows.Graphics.Printing3D** 名前空間の [**Printing3D3MFPackage**](/uwp/api/windows.graphics.printing3d.printing3d3mfpackage) クラスが 1 つの .3mf ファイルに相当し、他のクラスはファイル内の特定の XML 要素にマップされます。 このガイドでは、3MF ドキュメントの主なパーツのそれぞれの作成方法とプログラムによる設定方法、3MF の素材の拡張の利用方法、 **Printing3D3MFPackage** オブジェクトを変換して .3mf ファイルとして保存する方法について説明します。 3MF および 3MF 素材の拡張の標準について詳しくは、「[3MF の仕様](https://3mf.io/what-is-3mf/3mf-specification/)」をご覧ください。

<!-- >**Note** This guide describes how to construct a 3MF document from scratch. If you wish to make changes to an already existing 3MF document provided in the form of a .3mf file, you simply need to convert it to a **Printing3D3MFPackage** and alter the contained classes/properties in the same way (see [link]) below). -->


## <a name="core-classes-in-the-3mf-structure"></a>3MF 構造体の主なクラス

**Printing3D3MFPackage** クラスは完全な 3MF ドキュメントを表します。3MF ドキュメントの中心となるのは、 [**Printing3DModel**](/uwp/api/windows.graphics.printing3d.printing3dmodel) クラスで表される、モデル パーツです。 3D モデルを指定する情報のほとんどは **Printing3DModel** クラスのプロパティおよびその基になるクラスのプロパティを設定して保存されます。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetInitClasses":::

<!-- >**Note** We do not yet associate the **Printing3D3MFPackage** with its corresponding **Printing3DModel** object. Only after fleshing out the **Printing3DModel** with all of the information we wish to specify will we make that association (see [link]). -->

## <a name="metadata"></a>Metadata

3MF ドキュメントのモデル パーツは、 **Metadata** プロパティに保存される文字列のキー/値ペアの形式でメタデータを保持できます。 さまざまな定義済みの名前のメタデータがありますが、他のペアをパーツの拡張として追加することも可能です (詳しくは、「[3MF の仕様](https://3mf.io/what-is-3mf/3mf-specification/)」に記載されています)。 メタデータの処理方法の決定はパッケージの受信者 (3D 製造デバイス) に依存しますが、できるだけ多くの基本情報を 3MF パッケージに含めることが望ましい方法です。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetMetadata":::

## <a name="mesh-data"></a>メッシュ データ

このガイドにおいては、メッシュとは、頂点のセットから作成される 3 次元形状のボディを意味します (必ずしも 1 つの立体として見えるとは限りません)。 メッシュ パーツは [**Printing3DMesh**](/uwp/api/windows.graphics.printing3d.printing3dmesh) クラスで表されます。 有効なメッシュ オブジェクトは、すべての頂点の位置、およびいくつかの頂点のセットの間に存在する三角形の表面についての情報を含む必要があります。

次のメソッドは、メッシュに頂点を追加して、3D 空間での位置を与えます。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetVertices":::

次のメソッドは、頂点間で描画されるすべての三角形を定義します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetTriangleIndices":::

> [!NOTE]
> すべての三角形では、(三角形をメッシュ オブジェクトの外側から見て) 反時計回りでインデックスを定義する必要があります。これにより、表面の法線ベクトルが外側に向きます。

Printing3DMesh オブジェクトが頂点と三角形の有効なセットを含む場合、それはモデルの **Meshes** プロパティに追加される必要があります。 パッケージに含まれるすべての **Printing3DMesh** オブジェクトは、 **Printing3DModel** クラスの **Meshes** プロパティの下に保存される必要があります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetMeshAdd":::


## <a name="create-materials"></a>素材の作成


3D モデルは複数の素材のデータを保持できます。 この規則は、1 回の印刷ジョブで複数の素材を使用できる 3D 製造デバイスを活用するためのものです。 また複数の *種類* の素材グループがあり、それぞれがさまざまな個々の素材をサポートできます。 各素材グループは一意の参照 ID 番号を持つ必要があります。グループ内の各素材も一意の ID を持つ必要があります。

これにより、モデル内の別のメッシュ オブジェクトがこれらの素材を参照できます。 さらに、各メッシュの個々の三角形は、別の素材を指定できます。 また、1 つの三角形内で別の素材が表され、三角形の各頂点が別の素材に割り当てられて、表面の素材はそれらのグラデーションとして計算されることさえも可能です。

このガイドではまず、異なる種類の素材をそれぞれの素材グループ内に作成して、それをモデル オブジェクトのリソースとして保存する方法を示します。 次に、個々のメッシュと個々の三角形に別の素材を割り当てます。

### <a name="base-materials"></a>Base materials

既定の素材の種類は **Base Material** です。これは **Color Material** 値 (下記を参照) と名前属性を持ちます。これは使用する素材の *種類* を指定するために使用します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetBaseMaterialGroup":::

> [!NOTE]
> 3D 製造デバイスは、利用可能な物理素材と、3MF に保存されている仮想素材要素のマップを決定します。 素材のマッピングは 1:1 とは限りません。3D プリンターが 1 つの素材のみを使用できる場合、オブジェクトや表面が別の素材に割り当てられている場合でも、全モデルをその素材で印刷します。

### <a name="color-materials"></a>色素材

**Color Materials** は **Base Materials** に似ていますが、名前は含まれません。 そのため、マシンが使用する素材の種類を指定できません。 色のデータのみを保持し、マシンが素材の種類を選択します (マシンがユーザーに選択を求める場合もあります)。 次のコードでは、以前のメソッドからの `colrMat` オブジェクトが使用されています。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetColorMaterialGroup":::

### <a name="composite-materials"></a>複合素材

**Composite Materials** は製造デバイスに、さまざまな **Base Materials** を一定の組み合わせで使用するように指示します。 各 **Composite Material Group** は材料を使う 1 つの **Base Material Group** のみを参照する必要があります。 さらに、このグループ内で利用できる **Base Materials** は **Material Indices** の一覧にリストされている必要があります。これは比率を指定する際に各 **Composite Material** によって参照されます (すべての **Composite Material** は単に **Base Materials** の比率です)。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetCompositeMaterialGroup":::

### <a name="texture-coordinate-materials"></a>テクスチャ座標の素材

3MF は 2D 画像を使って 3D モデルの表面に色を付けることをサポートします。 これによりモデルは、三角形の表面ごとに、より多くの色データを伝えることができます (三角形の頂点ごとに 1 つの色の値を持つ場合と比べて)。 **Color Materials** と同様に、テクスチャ座標の素材は色データのみを伝えます。 2D テクスチャを使うには、まずテクスチャ リソースを宣言する必要があります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetTextureResource":::

> [!NOTE]
> テクスチャ データは、パッケージ内のモデル パーツでなく、3MF パッケージ自体に属しています。

次に **Texture3Coord Materials** を記入する必要があります。 これらはそれぞれテクスチャ リソースを参照し、画像の特定の点を (UV 座標で) 指定します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetTexture2CoordMaterialGroup":::

## <a name="map-materials-to-faces"></a>素材を表面にマップ

素材と各三角形の頂点のマッピングを指定するには、モデルのメッシュ オブジェクトにさらに処理を行う必要があります (モデルに複数のメッシュが含まれる場合、それぞれに素材が割り当てられる必要があります)。 既に説明したように、素材は頂点ごと、三角形ごとに割り当てられます。 次のコードを参照して、この情報の入力と解釈の方法を確認します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetMaterialIndices":::

## <a name="components-and-build"></a>Component とビルド

Component 構造体により、ユーザーは印刷可能な 3D モデルに複数のメッシュ オブジェクトを配置できます。 [**Printing3DComponent**](/uwp/api/windows.graphics.printing3d.printing3dcomponent) オブジェクトには、1 つのメッシュと他のコンポーネントへの参照のリストが含まれています。 これは実際には、 [**Printing3DComponentWithMatrix**](/uwp/api/windows.graphics.printing3d.printing3dcomponentwithmatrix) オブジェクトのリストです。 各 **Printing3DComponentWithMatrix** オブジェクトには **Printing3DComponent** が含まれ、また重要なことに、メッシュと **Printing3DComponent** に含まれるコンポーネントに適用される変換マトリックスが含まれます。

たとえば、自動車のモデルは、車のボディのメッシュを保持する、1 つの "ボディ" **Printing3DComponent** から構成されることができます。 この場合、"ボディ" コンポーネントには、4 つの異なる **Printing3DComponentWithMatrix** オブジェクトへの参照が含まれ、そのすべてが、"車輪" メッシュを持つ、同じ **Printing3DComponent** を参照し、4 つの異なる変換マトリックスを含みます (これにより、車輪を車のボディの 4 つの異なる位置にマッピングします)。 このシナリオでは、最終製品には合計 5 つのメッシュが含まれる場合でも、"ボディ" メッシュと "車輪" メッシュはそれぞれ 1 度だけ保存される必要があります。

すべての **Printing3DComponent** オブジェクトはモデルの **Components** プロパティで直接参照される必要があります。 印刷ジョブで使用される 1 つの特定のコンポーネントは **Build** プロパティに保存されています。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetComponents":::

## <a name="save-package"></a>パッケージの保存
素材とコンポーネントを定義したモデルが完成したので、それをパッケージに保存します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetSavePackage":::

この関数は、テクスチャが正しく指定されていることを確認します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetFixTexture":::

ここでは、アプリ内から印刷ジョブを開始するか (「 [アプリからの 3D 印刷](./3d-print-from-app.md)」をご覧ください)、またはこの **Printing3D3MFPackage** を .3mf ファイルとして保存します。

次のメソッドは、完成した **Printing3D3MFPackage** を取得して、そのデータを .3mf ファイルに保存します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/devices-sensors/3dprinthowto/cs/Generate3MFMethods.cs" id="SnippetSaveTo3mf":::

## <a name="related-topics"></a>関連トピック

[アプリからの3D 印刷](./3d-print-from-app.md)  
[3D 印刷の UWP サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/3DPrinting)
 

 

 
