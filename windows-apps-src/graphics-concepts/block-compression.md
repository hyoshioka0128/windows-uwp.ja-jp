---
title: ブロック圧縮
description: ブロック圧縮は、テクスチャ サイズとメモリ フットプリントを減らしてパフォーマンスを向上させる、不可逆のテクスチャ圧縮技術です。 ブロック圧縮テクスチャは、1 色あたり 32 ビットのテクスチャより小さくすることができます。
ms.assetid: 2FAD6BE8-C6E4-4112-AF97-419CD27F7C73
keywords:
- ブロック圧縮
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 02b65357b52740e9b56e0e2dc11ff22723825f20
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89156456"
---
# <a name="block-compression"></a>ブロック圧縮

ブロック圧縮は、テクスチャ サイズとメモリ フットプリントを減らしてパフォーマンスを向上させる、不可逆のテクスチャ圧縮技術です。 ブロック圧縮テクスチャは、1 色あたり 32 ビットのテクスチャより小さくすることができます。

ブロック圧縮とは、テクスチャ サイズを減少させるテクスチャの圧縮方法です。 各色 32 ビットのテクスチャと比較すると、ブロック圧縮されたテクスチャは最大 75% 縮小できます。 ブロック圧縮を使用すると、メモリ フットプリントが小さくなり、アプリケーションでは通常、パフォーマンスが向上します。

ブロック圧縮は不可逆圧縮ですが、効果的であり、パイプラインで変換およびフィルターされたすべてのテクスチャに推奨されます。 画面に直接マッピングされるテクスチャ (アイコンやテキストのような UI 要素) は、処理結果が比較的目立つので、圧縮にはあまり適していません。

ブロック圧縮されたテクスチャは、すべての次元で 4 の倍数のサイズで作成する必要があります。またパイプラインの出力として使用することはできません。

## <a name="span-idbasicsspanspan-idbasicsspanspan-idbasicsspanhow-block-compression-works"></a><span id="Basics"></span><span id="basics"></span><span id="BASICS"></span>ブロック圧縮のしくみ

ブロック圧縮は、カラー データの保存に必要なメモリの量を減少させるための方法です。 ある色を元のサイズで保存し、他の色をエンコード スキームを使用して保存することにより、その画像の保存に必要なメモリの量を大幅に減少させることができます。 圧縮されたデータはハードウェアが自動的にデコードするので、圧縮されたテクスチャを使用しても、パフォーマンスの損失は発生しません。

圧縮がどのように行われるかについては、以下の 2 つの例を参照してください。 最初の例では、圧縮されないデータを保存する際に使用されるメモリの量について説明します。2 番目の例では、圧縮されたデータを保存する際に使用されるメモリの量について説明します。

- [圧縮解除データの格納](#storing-uncompressed-data)
- [圧縮データの格納](#storing-compressed-data)

### <a name="span-idstoring_uncompressed_dataspanspan-idstoring_uncompressed_dataspanspan-idstoring_uncompressed_dataspanspan-idstoring-uncompressed-dataspanstoring-uncompressed-data"></a><span id="Storing_Uncompressed_Data"></span><span id="storing_uncompressed_data"></span><span id="STORING_UNCOMPRESSED_DATA"></span><span id="storing-uncompressed-data"></span>圧縮されないデータの保存

以下のイメージは、圧縮されていない 4x4 のテクスチャを表しています。 各色には、単一のカラー成分 (たとえば赤) が含まれ、1 バイトのメモリに保存されているとします。

![圧縮されていない 4 x 4 のテクスチャ](images/d3d10-block-compress-1.png)

圧縮されていないデータはメモリに順次レイアウトされ、以下のイメージに示すように、16 バイト必要となります。

![シーケンシャル メモリ内の圧縮されていないデータ](images/d3d10-block-compress-2.png)

### <a name="span-idstoring_compressed_dataspanspan-idstoring_compressed_dataspanspan-idstoring_compressed_dataspanspan-idstoring-compressed-dataspanstoring-compressed-data"></a><span id="Storing_Compressed_Data"></span><span id="storing_compressed_data"></span><span id="STORING_COMPRESSED_DATA"></span><span id="storing-compressed-data"></span>圧縮データの格納

圧縮されていないイメージがどれぐらいの量のメモリを使用するかを理解したところで、圧縮されたイメージがどれだけ多くのメモリを使わずに済むかを説明します。 [BC1](#bc1)圧縮形式では、2 つの色 (各 1 バイト) と、テクスチャ内の元の色の補間に使用される 16 個の 3 ビット インデックス (48 ビット、または 6 バイト) を保存します。

![BC1 圧縮形式](images/d3d10-block-compress-3.png)

圧縮されたデータを保存するのに必要な領域の合計は 8 バイトで、圧縮されていない例に比べて 50% のメモリを使用せずに済んでいます。 1 つ以上のカラー成分を使用する場合、使用せずに済む量はさらに多くなります。

ブロック圧縮によってかなりの量のメモリを使用せずに済むことで、パフォーマンスの向上につなげることができます。 このパフォーマンスは、イメージの画質の代償として得られるものですが (色の補間による)、多くの場合、画質の低下は顕著ではありません。

次のセクションでは、Direct3D を使用して、アプリケーションでブロック圧縮を簡単に使用する方法を示します。

## <a name="span-idusing_block_compressionspanspan-idusing_block_compressionspanspan-idusing_block_compressionspanusing-block-compression"></a><span id="Using_Block_Compression"></span><span id="using_block_compression"></span><span id="USING_BLOCK_COMPRESSION"></span>ブロック圧縮の使用

ブロック圧縮形式を指定すること以外は、圧縮されないテクスチャと同様に、ブロック圧縮テクスチャを作成します。

次に、ビューを作成して、テクスチャをパイプラインにバインドします。ブロック圧縮されたテクスチャはシェーダー ステージへの入力としてのみ使用できるので、シェーダー リソース ビューを作成します。

ブロック圧縮されたテクスチャを、圧縮されていないテクスチャを使用する場合と同様に使用します。 アプリケーションがブロック圧縮データへのメモリ ポインターを取得する場合は、ミップマップのメモリ パディングを考慮する必要があります。このメモリ パディングは、宣言されたサイズが実際のサイズと異なる原因となります。

- [仮想サイズと物理サイズの比較](#virtual-size-versus-physical-size)

### <a name="span-idvirtual_sizespanspan-idvirtual_sizespanspan-idvirtual_sizespanspan-idvirtual-size-versus-physical-sizespanvirtual-size-versus-physical-size"></a><span id="Virtual_Size"></span><span id="virtual_size"></span><span id="VIRTUAL_SIZE"></span><span id="virtual-size-versus-physical-size"></span>仮想サイズと物理サイズの比較

メモリ ポインターを使用して、ブロック圧縮されたテクスチャのメモリを扱うアプリケーション コードがある場合、アプリケーション コードの変更が必要となる可能性がある重要な考慮事項が 1 つあります。 ブロック圧縮アルゴリズムは 4 x 4 のテクセル ブロックで処理するため、ブロック圧縮されたテクスチャはすべての次元で 4 の倍数である必要があります。 これは、最初の次元が 4 で割り切れるが、さらに分割すると 4 で割り切れなくなるミップマップでは問題となります。 以下の図は、各ミップマップ レベルの仮想サイズ (宣言されたサイズ) と物理サイズ (実際のサイズ) の間の領域の違いを示しています。

![圧縮されていないミップマップ レベル対圧縮されたミップマップ レベル](images/d3d10-block-compress-pad.png)

図の左側は、圧縮されていない 60 x 40 のテクスチャに対して生成されるミップマップ レベル サイズを示しています。 最上位レベルのサイズは、テクスチャを生成する API 呼び出しから取得されます。後続の各レベルは、前のレベルのサイズの半分になります。 圧縮されていないテクスチャでは、仮想サイズ (宣言されたサイズ) と物理サイズ (実際のサイズ) との間で差はありません。

図の右側は、圧縮された 60 x 40 のテクスチャに対して生成されるミップマップ レベル サイズを示しています。 2 番目と 3 番目のレベルにはどちらも、各レベルのサイズが 4 で割り切れるように、メモリ パディングが追加されていることに注意してください。 これは、アルゴリズムが 4 x 4 のテクセル ブロックで処理できるようにするために必要です。 これは、mipmap レベルが4×4より小さい場合に特に明らかです。これらの非常に小さな mipmap レベルのサイズは、テクスチャメモリが割り当てられるときに最も近い4の係数に切り上げられます。

サンプリング ハードウェアは仮想サイズを使用します。テクスチャがサンプリングされる際、メモリ パディングは無視されます。 4 x 4 よりも小さいミップマップ レベルでは、最初の 4 つのテクセルのみが 2 x 2 のマップに使用され、最初のテクセルのみが 1 x 1 のブロックで使用されます。 ただし、物理サイズ (メモリ パディングを含む) を明らかにする API 構造はありません。

つまり、ブロック圧縮したデータを含む領域をコピーする際は、アライメントされたメモリ ブロックは注意して使用してください。 メモリ ポインターを取得するアプリケーションでこれを実行するには、必ずそのポインターがサーフェス ピッチを使用して物理メモリ サイズを明らかにするようにします。

## <a name="span-idcompression_algorithmsspanspan-idcompression_algorithmsspanspan-idcompression_algorithmsspancompression-algorithms"></a><span id="Compression_Algorithms"></span><span id="compression_algorithms"></span><span id="COMPRESSION_ALGORITHMS"></span>圧縮アルゴリズム

Direct3D のブロック圧縮方法では、圧縮されていないテクスチャ データを 4 x 4 のブロックに分割し、各ブロックを圧縮してから、そのデータを保存します。 このため、圧縮されるテクスチャは、テクスチャの次元が 4 の倍数である必要があります。

![ブロック圧縮](images/d3d10-compression-1.png)

上の図は、テクセル ブロックに分割されたテクスチャを示しています。 最初のブロックは、a ～ p のラベルがついた 16 のテクセルのレイアウトを示していますが、各ブロックには同じ構造のデータがあります。

Direct3D は圧縮スキームをいくつか実装しています。それぞれ、保存される成分数、成分ごとのビット数、および消費されるメモリ量の間で異なるトレードオフが存在します。 この表を使用すると、アプリケーションに最適なデータの種類とデータ解像度で、最も効果的に機能する形式を選択するのに役立ちます。

| ソース データ                     | データ圧縮解像度 (ビット) | 選択する圧縮形式 |
|---------------------------------|---------------------------------------|--------------------------------|
| 成分が 3 つの色およびアルファ | カラー (5:6:5)、アルファ (1) またはアルファなし  | [BC1](#bc1)                    |
| 成分が 3 つの色およびアルファ | カラー (5:6:5)、アルファ (4)              | [BC2](#bc2)                    |
| 成分が 3 つの色およびアルファ | カラー (5:6:5)、アルファ (8)              | [BC3](#bc3)                    |
| 成分が 1 つの色             | 1 つの成分 (8)                     | [BC4](#bc4)                    |
| 成分が 2 つの色             | 2 つの成分 (8:8)                  | [BC5](#bc5)                    |

- [BC1](#bc1)
- [BC2](#bc2)
- [BC3](#bc3)
- [BC4](#bc4)
- [BC5](#bc5)

### <a name="span-idbc1spanspan-idbc1spanbc1"></a><span id="BC1"></span><span id="bc1"></span>BC1

\_ \_ \_ \_ \_ \_ \_ \_ \_ 5:6:5 色 (5 ビット赤、6ビット緑、5ビット青) を使用して3コンポーネントのカラーデータを格納するには、最初のブロック圧縮形式 (BC1) (dxgi 形式 BC1、dxgi 形式 BC1 unorm、または dxgi BC1 unorm SRGB) を使用します。 データに 1 ビットのアルファが含まれている場合も、これが当てはまります。 4 x 4 のテクスチャが、可能な限り最も大きなデータ形式を使用することを想定すると、BC1 形式では必要なメモリが 48 バイト (16 色× 3 成分/色× 1 バイト/成分) から 8 バイトに減少します。

このアルゴリズムは、4 x 4 ブロックのテクセルで機能します。 このアルゴリズムでは、16色を格納するのではなく、次の図に示すように、2つの参照色 (カラー \_ 0 とカラー \_ 1) と 16 2 ビットのカラーインデックス (ブロック a – p) を保存します。

![BC1 の圧縮レイアウト](images/d3d10-compression-bc1.png)

カラー インデックス (a ～ p) は、カラー テーブルから元の色を検索するために使用します。 カラー テーブルには 4 つの色が含まれます。 最初の2色 (色 \_ 0 と色 \_ 1) は、最小と最大の色です。 他の2色 (色 \_ 2 および色 \_ 3) は、線形補間で計算された中間色です。

```cpp
color_2 = 2/3*color_0 + 1/3*color_1
color_3 = 1/3*color_0 + 2/3*color_1
```

4 つの色は、a ～ p のブロックに保存される 2 ビットのインデックス値を割り当てられます。

```cpp
color_0 = 00
color_1 = 01
color_2 = 10
color_3 = 11
```

最後に、a ～ p のブロックの各色がカラー テーブルの 4 つの色と比較され、最も近い色のインデックスが 2 ビット ブロックに保存されます。

このアルゴリズムは、1 ビットのアルファが含まれているデータにも適しています。 唯一の違いは、color \_ 3 が 0 (透明色を表します) に設定され、色 \_ 2 が色 \_ 0 と色1の線形ブレンドであることです \_ 。

```cpp
color_2 = 1/2*color_0 + 1/2*color_1;
color_3 = 0;
```

### <a name="span-idbc2spanspan-idbc2spanbc2"></a><span id="BC2"></span><span id="bc2"></span>BC2

BC2 形式 (DXGI \_ 形式 \_ BC2 \_ 、dxgi \_ 形式 \_ BC2 \_ unorm、または dxgi \_ BC2 \_ unorm \_ SRGB) を使用して、色とアルファデータを低整合性で格納するデータを格納します (高度な一貫性のあるアルファデータには [BC3](#bc3) を使用します)。 BC2 形式は、RGB データを 5:6:5 の色 (赤が 5 ビット、緑が 6 ビット、青が 5 ビット) で、アルファを独立した 4 ビットの値で保存します。 4 x 4 のテクスチャが、可能な限り最も大きなデータ形式を使用すると想定すると、この圧縮方法では必要なメモリが 64 バイト (16 色 x 4 成分/色 x 1 バイト/成分) から 16 バイトに減少します。

BC2 形式では、[BC1](#bc1) 形式と同じビット数およびデータ レイアウトで色を保存しますが、BC2 ではアルファ データを保存するためにさらに 64 ビットのメモリが必要です。

![BC2 の圧縮レイアウト](images/d3d10-compression-bc2.png)

### <a name="span-idbc3spanspan-idbc3spanbc3"></a><span id="BC3"></span><span id="bc3"></span>BC3

BC3 形式 (DXGI \_ 形式 \_ BC3 \_ 、dxgi \_ 形式 \_ BC3 \_ unorm、または dxgi \_ BC3 \_ unorm SRGB) を使用して、一貫性のある \_ カラーデータを格納します (より一貫したアルファデータを持つ [BC2](#bc2) を使用します)。 BC3 形式では、5:6:5 の色 (赤が 5 ビット、緑が 6 ビット、青が 5 ビット) を使用してカラー データを、1 バイトを使用してアルファ データを保存します。 4 x 4 のテクスチャが、可能な限り最も大きなデータ形式を使用すると想定すると、この圧縮方法では必要なメモリが 64 バイト (16 色 x 4 成分/色 x 1 バイト/成分) から 16 バイトに減少します。

BC3 形式では、[BC1](#bc1) 形式と同じビット数およびデータ レイアウトで色を保存しますが、BC3 ではアルファ データを保存するためにさらに 64 ビットのメモリが必要です。 BC3 形式では、2 つの参照値を保存し、その 2 つの間を補間することによってアルファを処理します (BC1 で RGB カラーを保存する方法と類似しています)。

このアルゴリズムは、4 x 4 ブロックのテクセルで機能します。 このアルゴリズムでは、16のアルファ値を格納する代わりに、次の図に示すように、2つの参照アルファ (アルファ \_ 0 とアルファ \_ 1) と 16 3 ビットカラーインデックス (アルファ a から p) が格納されます。

![BC3 の圧縮レイアウト](images/d3d10-compression-bc3.png)

BC3 形式では、アルファ インデックス (a ～ p) を使用して、8 つの値が含まれるルックアップ テーブルから元の色を検索します。 最初の2つの値 (アルファ \_ 0 とアルファ \_ 1) は最小値と最大値です。他の6番目の中間値は、線形補間を使用して計算されます。

このアルゴリズムでは、2 つの参照アルファ値を調べることで、補間アルファ値の数を決定します。 アルファ \_ 0 がアルファ1より大きい場合 \_ 、BC3 は6つのアルファ値を補間します。それ以外の場合は、4を補間します。 BC3 でアルファ値を 4 つのみ補間するときは、追加のアルファ値 (0 は完全に透明、255 は完全に不透明) を 2 つ設定します。 BC3 では、指定されたテクセルの元のアルファに最も近い補間アルファ値に対応するビット コードを保存することにより、4 x 4 のテクセル領域にアルファ値を圧縮します。

```cpp
if( alpha_0 > alpha_1 )
{
  // 6 interpolated alpha values.
  alpha_2 = 6/7*alpha_0 + 1/7*alpha_1; // bit code 010
  alpha_3 = 5/7*alpha_0 + 2/7*alpha_1; // bit code 011
  alpha_4 = 4/7*alpha_0 + 3/7*alpha_1; // bit code 100
  alpha_5 = 3/7*alpha_0 + 4/7*alpha_1; // bit code 101
  alpha_6 = 2/7*alpha_0 + 5/7*alpha_1; // bit code 110
  alpha_7 = 1/7*alpha_0 + 6/7*alpha_1; // bit code 111
}
else
{
  // 4 interpolated alpha values.
  alpha_2 = 4/5*alpha_0 + 1/5*alpha_1; // bit code 010
  alpha_3 = 3/5*alpha_0 + 2/5*alpha_1; // bit code 011
  alpha_4 = 2/5*alpha_0 + 3/5*alpha_1; // bit code 100
  alpha_5 = 1/5*alpha_0 + 4/5*alpha_1; // bit code 101
  alpha_6 = 0;                         // bit code 110
  alpha_7 = 255;                       // bit code 111
}
```

### <a name="span-idbc4spanspan-idbc4spanbc4"></a><span id="BC4"></span><span id="bc4"></span>BC4

成分が 1 つのカラー データを、各色に 8 ビット使用して保存するには、BC4 形式を使用します。 精度が向上した結果として ( [BC1](#bc1)を比較した場合)、BC4 は、 \[ dxgi 形式の BC4 unorm 形式を使用して、0 ~ 1 の範囲の浮動小数点データを格納するのに最適です \] \_ \_ \_ 。また、 \[ -1 ~ + 1 を指定し \] \_ \_ \_ ます。 4 x 4 のテクスチャが、可能な限り最も大きなデータ形式を使用すると想定すると、この圧縮方法では必要なメモリが 16 バイト (16 色 x 1 成分/色 x 1 バイト/成分) から 8 バイトに減少します。

このアルゴリズムは、4 x 4 ブロックのテクセルで機能します。 このアルゴリズムでは、16色を格納するのではなく、次の図に示すように、2つの参照色 (赤 \_ 0 と赤 \_ 1) と 16 3 ビットのカラーインデックス (赤 a ~ 赤 p) が格納されます。

![BC4 の圧縮レイアウト](images/d3d10-compression-bc4.png)

このアルゴリズムでは、3 ビットのインデックスを使用して、8 色が含まれるカラー テーブルから色を検索します。 最初の2色 (赤 \_ 0 と赤 \_ 1) は、最小と最大の色です。 このアルゴリズムでは、線形補間を使用して残りの色を計算します。

このアルゴリズムでは、2 つの参照値を調べることで、補間されるカラー値の数を決定します。 Red \_ 0 が赤1より大きい場合 \_ 、BC4 は6色の値を補間します。それ以外の場合は、4を補間します。 BC4 でカラー値を 4 つのみ補間するときは、追加のカラー値 (0.0f は完全に透明、1.0f は完全に不透明) を 2 つ設定します。 BC4 では、指定されたテクセルの元のアルファに最も近い補間アルファ値に対応するビット コードを保存することにより、4 x 4 のテクセル領域にアルファ値を圧縮します。

- [BC4 \_ unorm](#bc4-unorm)
- [BC4 \_ snorm](#bc4-snorm)

### <a name="span-idbc4_unormspanspan-idbc4_unormspanspan-idbc4-unormspanbc4_unorm"></a><span id="BC4_UNORM"></span><span id="bc4_unorm"></span><span id="bc4-unorm"></span>BC4 \_ unorm

単一成分データの補間は、以下のコード サンプルのように行われます。

```cpp
unsigned word red_0, red_1;

if( red_0 > red_1 )
{
  // 6 interpolated color values
  red_2 = (6*red_0 + 1*red_1)/7.0f; // bit code 010
  red_3 = (5*red_0 + 2*red_1)/7.0f; // bit code 011
  red_4 = (4*red_0 + 3*red_1)/7.0f; // bit code 100
  red_5 = (3*red_0 + 4*red_1)/7.0f; // bit code 101
  red_6 = (2*red_0 + 5*red_1)/7.0f; // bit code 110
  red_7 = (1*red_0 + 6*red_1)/7.0f; // bit code 111
}
else
{
  // 4 interpolated color values
  red_2 = (4*red_0 + 1*red_1)/5.0f; // bit code 010
  red_3 = (3*red_0 + 2*red_1)/5.0f; // bit code 011
  red_4 = (2*red_0 + 3*red_1)/5.0f; // bit code 100
  red_5 = (1*red_0 + 4*red_1)/5.0f; // bit code 101
  red_6 = 0.0f;                     // bit code 110
  red_7 = 1.0f;                     // bit code 111
}
```

参照カラーは 3 ビットのインデックス (8 つの値があるので 000 ～ 111) を割り当てられます。このインデックスは、圧縮時に red a ～ red p のブロックに保存されます。

### <a name="span-idbc4_snormspanspan-idbc4_snormspanspan-idbc4-snormspanbc4_snorm"></a><span id="BC4_SNORM"></span><span id="bc4_snorm"></span><span id="bc4-snorm"></span>BC4 \_ snorm

DXGI \_ 形式の \_ BC4 \_ snorm はまったく同じですが、データが snorm 範囲でエンコードされ、4色の値が補間される点が異なります。 単一成分データの補間は、以下のコード サンプルのように行われます。

```cpp
signed word red_0, red_1;

if( red_0 > red_1 )
{
  // 6 interpolated color values
  red_2 = (6*red_0 + 1*red_1)/7.0f; // bit code 010
  red_3 = (5*red_0 + 2*red_1)/7.0f; // bit code 011
  red_4 = (4*red_0 + 3*red_1)/7.0f; // bit code 100
  red_5 = (3*red_0 + 4*red_1)/7.0f; // bit code 101
  red_6 = (2*red_0 + 5*red_1)/7.0f; // bit code 110
  red_7 = (1*red_0 + 6*red_1)/7.0f; // bit code 111
}
else
{
  // 4 interpolated color values
  red_2 = (4*red_0 + 1*red_1)/5.0f; // bit code 010
  red_3 = (3*red_0 + 2*red_1)/5.0f; // bit code 011
  red_4 = (2*red_0 + 3*red_1)/5.0f; // bit code 100
  red_5 = (1*red_0 + 4*red_1)/5.0f; // bit code 101
  red_6 = -1.0f;                    // bit code 110
  red_7 =  1.0f;                    // bit code 111
}
```

参照カラーは 3 ビットのインデックス (8 つの値があるので 000 ～ 111) を割り当てられます。このインデックスは、圧縮時に red a ～ red p のブロックに保存されます。

### <a name="span-idbc5spanspan-idbc5spanbc5"></a><span id="BC5"></span><span id="bc5"></span>BC5

成分が 2 つのカラー データを、各色に 8 ビット使用して保存するには、BC5 形式を使用します。 精度が向上した結果として ( [BC1](#bc1)を比較した場合)、BC5 は、 \[ dxgi 形式の BC5 unorm 形式を使用して、0 ~ 1 の範囲の浮動小数点データを格納するのに最適です \] \_ \_ \_ 。また、 \[ -1 ~ + 1 を指定し \] \_ \_ \_ ます。 4 x 4 のテクスチャが、可能な限り最も大きなデータ形式を使用すると想定すると、この圧縮方法では必要なメモリが 32 バイト (16 色 x 2 成分/色 x 1 バイト/成分) から 16 バイトに減少します。

- [BC5 \_ unorm](#bc5-unorm)
- [BC5 \_ snorm](#bc5-snorm)

このアルゴリズムは、4 x 4 ブロックのテクセルで機能します。 次の図に示すように、アルゴリズムでは、両方のコンポーネントに16色を格納するのではなく、各コンポーネントの2つの参照色 (赤 \_ 0、赤 \_ 1、緑 \_ 0、および緑 \_ 1) と、各コンポーネントの 16 3 ビットカラーインデックスを格納します。

![BC5 の圧縮レイアウト](images/d3d10-compression-bc5.png)

このアルゴリズムでは、3 ビットのインデックスを使用して、8 色が含まれるカラー テーブルから色を検索します。 最初の2色 (赤 \_ 0 と赤 \_ 1 (または緑 \_ 0 と緑 \_ 1)) は、最小値と最大色です。 このアルゴリズムでは、線形補間を使用して残りの色を計算します。

このアルゴリズムでは、2 つの参照値を調べることで、補間されるカラー値の数を決定します。 Red \_ 0 が赤1より大きい場合 \_ 、BC5 は6色の値を補間します。それ以外の場合は、4を補間します。 BC5 でカラー値を 4 つのみ補間するときは、残りの 2 つのカラー値を 0.0f と 1.0f に設定します。

### <a name="span-idbc5_unormspanspan-idbc5_unormspanspan-idbc5-unormspanbc5_unorm"></a><span id="BC5_UNORM"></span><span id="bc5_unorm"></span><span id="bc5-unorm"></span>BC5 \_ unorm

単一成分データの補間は、以下のコード サンプルのように行われます。 green の成分の計算も同様です。

```cpp
unsigned word red_0, red_1;

if( red_0 > red_1 )
{
  // 6 interpolated color values
  red_2 = (6*red_0 + 1*red_1)/7.0f; // bit code 010
  red_3 = (5*red_0 + 2*red_1)/7.0f; // bit code 011
  red_4 = (4*red_0 + 3*red_1)/7.0f; // bit code 100
  red_5 = (3*red_0 + 4*red_1)/7.0f; // bit code 101
  red_6 = (2*red_0 + 5*red_1)/7.0f; // bit code 110
  red_7 = (1*red_0 + 6*red_1)/7.0f; // bit code 111
}
else
{
  // 4 interpolated color values
  red_2 = (4*red_0 + 1*red_1)/5.0f; // bit code 010
  red_3 = (3*red_0 + 2*red_1)/5.0f; // bit code 011
  red_4 = (2*red_0 + 3*red_1)/5.0f; // bit code 100
  red_5 = (1*red_0 + 4*red_1)/5.0f; // bit code 101
  red_6 = 0.0f;                     // bit code 110
  red_7 = 1.0f;                     // bit code 111
}
```

参照カラーは 3 ビットのインデックス (8 つの値があるので 000 ～ 111) を割り当てられます。このインデックスは、圧縮時に red a ～ red p のブロックに保存されます。

### <a name="span-idbc5_snormspanspan-idbc5_snormspanspan-idbc5-snormspanbc5_snorm"></a><span id="BC5_SNORM"></span><span id="bc5_snorm"></span><span id="bc5-snorm"></span>BC5 \_ snorm

DXGI \_ 形式の \_ BC5 \_ snorm はまったく同じですが、データが snorm 範囲でエンコードされていて、4つのデータ値が補間されている場合は、-1.0 f と 1.0 f の2つの値が追加されます。 単一成分データの補間は、以下のコード サンプルのように行われます。 green の成分の計算も同様です。

```cpp
signed word red_0, red_1;

if( red_0 > red_1 )
{
  // 6 interpolated color values
  red_2 = (6*red_0 + 1*red_1)/7.0f; // bit code 010
  red_3 = (5*red_0 + 2*red_1)/7.0f; // bit code 011
  red_4 = (4*red_0 + 3*red_1)/7.0f; // bit code 100
  red_5 = (3*red_0 + 4*red_1)/7.0f; // bit code 101
  red_6 = (2*red_0 + 5*red_1)/7.0f; // bit code 110
  red_7 = (1*red_0 + 6*red_1)/7.0f; // bit code 111
}
else
{
  // 4 interpolated color values
  red_2 = (4*red_0 + 1*red_1)/5.0f; // bit code 010
  red_3 = (3*red_0 + 2*red_1)/5.0f; // bit code 011
  red_4 = (2*red_0 + 3*red_1)/5.0f; // bit code 100
  red_5 = (1*red_0 + 4*red_1)/5.0f; // bit code 101
  red_6 = -1.0f;                    // bit code 110
  red_7 =  1.0f;                    // bit code 111
}
```

参照カラーは 3 ビットのインデックス (8 つの値があるので 000 ～ 111) を割り当てられます。このインデックスは、圧縮時に red a ～ red p のブロックに保存されます。

## <a name="span-iddifferencesspanspan-iddifferencesspanspan-iddifferencesspanformat-conversion"></a><span id="Differences"></span><span id="differences"></span><span id="DIFFERENCES"></span>形式の変換

Direct3D を使用すると、ビット幅が同じであれば、事前に構造化されたタイプのテクスチャとブロック圧縮されたテクスチャとの間のコピーが可能になります。

いくつかの種類の形式間でリソースをコピーできます。 このようなコピー操作では、そのリソース データを異なる形式として再解釈する、一種の形式変換を実行します。 より一般的な変換の動作と、データの再解釈との違いを示す、この例をご覧ください。

```cpp
FLOAT32 f = 1.0f;
UINT32 u;
```

'f' を 'u' のタイプとして再解釈するため、[memcpy](/cpp/c-runtime-library/reference/memcpy-wmemcpy) を使います。

```cpp
memcpy( &u, &f, sizeof( f ) ); // 'u' becomes equal to 0x3F800000.
```

上の再解釈では、基になるデータの値は変更されません。[memcpy](/cpp/c-runtime-library/reference/memcpy-wmemcpy) は浮動小数点数を符号なし整数として再解釈します。

より一般的な変換を実行するには、割り当てを使用します。

```cpp
u = f; // 'u' becomes 1.
```

上の変換では、基になるデータの値が変更されます。

次の表は、このような再解釈による形式変換に使用できる、変換元と変換先の形式を示しています。 再解釈が期待どおりに動作するためには、値を適切にエンコードする必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット幅</th>
<th align="left">圧縮されていないリソース</th>
<th align="left">ブロック圧縮されたリソース</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">32</td>
<td align="left"><p>DXGI_FORMAT_R32_UINT</p>
<p>DXGI_FORMAT_R32_SINT</p></td>
<td align="left">DXGI_FORMAT_R9G9B9E5_SHAREDEXP</td>
</tr>
<tr class="even">
<td align="left">64</td>
<td align="left"><p>DXGI_FORMAT_R16G16B16A16_UINT</p>
<p>DXGI_FORMAT_R16G16B16A16_SINT</p>
<p>DXGI_FORMAT_R32G32_UINT</p>
<p>DXGI_FORMAT_R32G32_SINT</p></td>
<td align="left"><p>DXGI_FORMAT_BC1_UNORM[_SRGB]</p>
<p>DXGI_FORMAT_BC4_UNORM</p>
<p>DXGI_FORMAT_BC4_SNORM</p></td>
</tr>
<tr class="odd">
<td align="left">128</td>
<td align="left"><p>DXGI_FORMAT_R32G32B32A32_UINT</p>
<p>DXGI_FORMAT_R32G32B32A32_SINT</p></td>
<td align="left"><p>DXGI_FORMAT_BC2_UNORM[_SRGB]</p>
<p>DXGI_FORMAT_BC3_UNORM[_SRGB]</p>
<p>DXGI_FORMAT_BC5_UNORM</p>
<p>DXGI_FORMAT_BC5_SNORM</p></td>
</tr>
</tbody>
</table>

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック

[圧縮テクスチャ リソース](compressed-texture-resources.md)