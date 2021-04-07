---
ms.assetid: 9347AD7C-3A90-4073-BFF4-9E8237398343
description: この記事では、UWP アプリ用のオーディオとビデオのコーデックおよび形式のサポートを示します。
title: サポートされるコーデック
ms.date: 04/01/2021
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 2d5b9fd8ed0cdde7af38de2c855d2738458eb571
ms.sourcegitcommit: ffe124f95967c49993c8dacc7c4c17f5a534a163
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2021
ms.locfileid: "106504011"
---
# <a name="supported-codecs"></a>サポートされるコーデック

この記事では、各デバイス ファミリの既定で、UWP アプリで利用可能なオーディオ、ビデオ、イメージのコーデックと形式を示します。 これらの表では、指定のデバイス ファミリの Windows 10 のインストールに含まれているコーデックを示していることに注意してください。 ユーザーやアプリが、利用可能な追加のコーデックをインストールする場合があります。 実行時に、特定のデバイスで現在利用可能なコーデックのセットを照会できます。 詳しくは、「[デバイスにインストールされているコーデックの照会](codec-query.md)」をご覧ください。

以下の表では、"D" はデコーダーのサポートを示し、"E" はエンコーダーのサポートを示します。

## <a name="audio-codec--format-support"></a>オーディオのコーデックおよび形式のサポート

次の表は、各デバイス ファミリのオーディオのコーデックと形式のサポートを示しています。

> [!NOTE] 
> AMR-NB のサポートが示されている場合、Server SKU ではこのコーデックがサポートされません。

 

### <a name="desktop"></a>デスクトップ

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-3</th>
<th align="left">MPEG-2</th>
<th align="left">ADTS</th>
<th align="left">ASF</th>
<th align="left">RIFF</th>
<th align="left">AVI</th>
<th align="left">AC-3</th>
<th align="left">AMR</th>
<th align="left">3GP</th>
<th align="left">FLAC</th>
<th align="left">WAV</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">HE-AAC v1/AAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">HE-AAC v2/eAAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AAC-LC</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">AC3</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>

<tr class="even">
<td align="left">ALAC</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AMR-NB<sup>*</sup></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">FLAC</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">G.711 (A-Law、µ-law)</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">GSM 6.10</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">IMA ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">LPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
</tr>
<tr class="odd">
<td align="left">MP3</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">MPEG-1/2</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">MS ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">WMA 1/2/3</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">WMA Pro</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">WMA Voice</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

<sup>*</sup> Windows Server Sku では使用できません。

### <a name="mobile"></a>モバイル

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-3</th>
<th align="left">MPEG-2</th>
<th align="left">ADTS</th>
<th align="left">ASF</th>
<th align="left">RIFF</th>
<th align="left">AVI</th>
<th align="left">AC-3</th>
<th align="left">AMR</th>
<th align="left">3GP</th>
<th align="left">FLAC</th>
<th align="left">WAV</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">HE-AAC v1/AAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">HE-AAC v2/eAAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AAC-LC</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">AC3</td>
<td align="left">D (Lumia Icon、830、930、1520 のみ)</td>
<td align="left"></td>
<td align="left">D (Lumia Icon、830、930、1520 のみ)</td>
<td align="left"></td>
<td align="left">D (Lumia Icon、830、930、1520 のみ)</td>
<td align="left">D (Lumia Icon、830、930、1520 のみ)</td>
<td align="left">D (Lumia Icon、830、930、1520 のみ)</td>
<td align="left">D (Lumia Icon、830、930、1520 のみ)</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>

<tr class="even">
<td align="left">ALAC</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AMR-NB</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">FLAC</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">G.711 (A-Law、µ-law)</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">GSM 6.10</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">IMA ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">LPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
</tr>
<tr class="odd">
<td align="left">MP3</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">MPEG-1/2</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">MS ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">WMA 1/2/3</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">WMA Pro</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">WMA Voice</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="windows-10-iot"></a>WIndows 10 IoT

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-3</th>
<th align="left">MPEG-2</th>
<th align="left">ADTS</th>
<th align="left">ASF</th>
<th align="left">RIFF</th>
<th align="left">AVI</th>
<th align="left">AC-3</th>
<th align="left">AMR</th>
<th align="left">3GP</th>
<th align="left">FLAC</th>
<th align="left">WAV</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">HE-AAC v1/AAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">HE-AAC v2/eAAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AAC-LC</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">AC3</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>

<tr class="even">
<td align="left">ALAC</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AMR-NB</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">FLAC</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">G.711 (A-Law、µ-law)</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">GSM 6.10</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">IMA ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">LPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
</tr>
<tr class="odd">
<td align="left">MP3</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">MPEG-1/2</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">MS ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">WMA 1/2/3</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">WMA Pro</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">WMA Voice</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>



### <a name="xbox"></a>Xbox

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-3</th>
<th align="left">MPEG-2</th>
<th align="left">ADTS</th>
<th align="left">ASF</th>
<th align="left">RIFF</th>
<th align="left">AVI</th>
<th align="left">AC-3</th>
<th align="left">AMR</th>
<th align="left">3GP</th>
<th align="left">FLAC</th>
<th align="left">WAV</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">HE-AAC v1/AAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">HE-AAC v2/eAAC+</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AAC-LC</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">AC3</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>

<tr class="even">
<td align="left">ALAC</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AMR-NB</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">FLAC</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">G.711 (A-Law、µ-law)</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">GSM 6.10</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">IMA ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">LPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
</tr>
<tr class="odd">
<td align="left">MP3</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">MPEG-1/2</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">MS ADPCM</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">WMA 1/2/3</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">WMA Pro</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">WMA Voice</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="video-codec--format-support"></a>ビデオのコーデックおよび形式のサポート

次の表は、各デバイス ファミリのビデオのコーデックと形式のサポートを示しています。

> [!NOTE] 
> H.265 のサポートが示されている場合、必ずしもデバイス ファミリ内のすべてのデバイスでサポートされるわけではありません。

 

### <a name="desktop"></a>デスクトップ

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">fMP4</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-2 PS</th>
<th align="left">MPEG-2 TS</th>
<th align="left">MPEG-1</th>
<th align="left">3GPP</th>
<th align="left">3GPP2</th>
<th align="left">AVCHD</th>
<th align="left">ASF</th>
<th align="left">AVI</th>
<th align="left">MKV</th>
<th align="left">DV</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">MPEG-1<sup>*</sup></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">MPEG-2<sup>*</sup></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">MPEG-4 (Part 2)</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">(265)<sup>**</sup></td>
<td align="left">D</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">H.264</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">H.263</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">VC-1</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">WMV7/8/9</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">WMV9 Screen</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">DV</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left">D</td>
</tr>

<tr class="even">
<td align="left">VP8</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>

<tr class="even">
<td align="left">VP9</td>
<td align="left">D</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>

<tr class="even">
<td align="left">AV1<sup>**</sup></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>

<tr class="odd">
<td align="left">モーション JPEG</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

<sup>*</sup> MPEG 2/MPEG-2 コーデックは、オプションの Microsoft UWP DVD アプリケーションのインストールで使用できます。

<sup>**</sup> 対応するオプションのコーデックパックをインストールすると、-265 と AV1 が使用できるようになります。

### <a name="mobile"></a>モバイル

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">fMP4</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-2 PS</th>
<th align="left">MPEG-2 TS</th>
<th align="left">3GPP</th>
<th align="left">AVCHD</th>
<th align="left">ASF</th>
<th align="left">AVI</th>
<th align="left">MKV</th>
</tr>
</thead>
<tbody>

<tr class="odd">
<td align="left">MPEG-4 (Part 2)</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">H.265</td>
<td align="left">D</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">H.264</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">H.263</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">VC-1</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
</tr>

<tr class="odd">
<td align="left">モーション JPEG</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="windows-10-iot"></a>Windows 10 IoT

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">fMP4</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-2 PS</th>
<th align="left">MPEG-2 TS</th>
<th align="left">MPEG-1</th>
<th align="left">3GPP</th>
<th align="left">3GPP2</th>
<th align="left">AVCHD</th>
<th align="left">ASF</th>
<th align="left">AVI</th>
<th align="left">MKV</th>
<th align="left">DV</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">MPEG-1</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">MPEG-2<sup>*</sup></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">MPEG-4 (Part 2)</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">(265)<sup>**</sup></td>
<td align="left">D</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">H.264</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">H.263</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">VC-1</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">WMV7/8/9</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">WMV9 Screen</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">VP8</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">VP9</td>
<td align="left">D</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">AV1<sup>**</sup></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">DV</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">モーション JPEG</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

<sup>*</sup> MPEG 2/MPEG-2 コーデックは、オプションの Microsoft UWP DVD アプリケーションのインストールで使用できます。

<sup>**</sup> 対応するオプションのコーデックパックをインストールすると、-265 と AV1 が使用できるようになります。
 



 

### <a name="xbox"></a>Xbox

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック/コンテナー</th>
<th align="left">fMP4</th>
<th align="left">MPEG-4</th>
<th align="left">MPEG-2 PS</th>
<th align="left">MPEG-2 TS</th>
<th align="left">MPEG-1</th>
<th align="left">3GPP</th>
<th align="left">AVCHD</th>
<th align="left">ASF</th>
<th align="left">AVI</th>
<th align="left">MKV</th>
<th align="left">DV</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">MPEG-1</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">MPEG-2</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">MPEG-4 (Part 2)</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">H.265</td>
<td align="left">D</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">H.264</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">H.263</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">VC-1</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">VP8</td>
<td align="left"></td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">VP9</td>
<td align="left">D</td>
<td align="left">D/E</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">AV1</td>
<td align="left">D</td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">DV</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
</tr>
<tr class="odd">
<td align="left">モーション JPEG</td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left">D</td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

## <a name="image-codec--format-support"></a>イメージのコーデックおよび形式のサポート 

<table>
<colgroup>
<col width="7%" />
<col width="7%" />
<col width="7%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コーデック</th>
<th align="left">デスクトップ</th>
<th align="left">他のデバイス ファミリ</th>
</tr>
</thead>
<tr class="odd">
<td align="left">BMP</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
</tr>
<tr class="even">
<td align="left">DDS</td>
<td align="left">D/E<sup>1</sup></td>
<td align="left">D/E<sup>1</sup></td>
</tr>
<tr class="odd">
<td align="left">DNG</td>
<td align="left">D<sup>2</sup></td>
<td align="left">D<sup>2</sup></td>
</tr>
<tr class="even">
<td align="left">GIF</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
</tr>
<tr class="odd">
<td align="left">ICO</td>
<td align="left">D</td>
<td align="left">D</td>
</tr>
<tr class="even">
<td align="left">JPEG</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
</tr>
<tr class="odd">
<td align="left">JPEG-XR</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
</tr>
<tr class="even">
<td align="left">PNG</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
</tr>
<tr class="odd">
<td align="left">TIFF</td>
<td align="left">D/E</td>
<td align="left">D/E</td>
</tr>
<tr class="even">
<td align="left">RAW 形式のカメラ</td>
<td align="left">D<sup>3</sup></td>
<td align="left">いいえ</td>
</tr>
</table>

<sup>1</sup> BC5 圧縮による BC1 を使用する DDS イメージはサポートされています。  
<sup>2</sup> 非未加工の埋め込みプレビューのある dng イメージがサポートされています。  
<sup>3</sup> 特定のカメラの未加工の形式のみがサポートされています。  

イメージ コーデックの詳細については、「[ネイティブ WIC コーデック](/windows/desktop/wic/native-wic-codecs)」をご覧ください。