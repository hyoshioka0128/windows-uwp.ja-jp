---
title: OpenGL ES 2.0 から Direct3D 11 への移植
description: OpenGL ES 2.0 グラフィックス パイプラインを Direct3D 11 と Windows ランタイムに移植するための記事、概要、チュートリアルを紹介します。
ms.assetid: 1e1cf668-a15f-0c7b-8daf-3260d27c6d9c
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10、UWP、ゲーム、OpenGL、Direct3D 11, 移植, グラフィックス
ms.localizationpriority: medium
ms.openlocfilehash: 4ee100bbbe70595049ca7298839e7906e21c3e59
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57635217"
---
# <a name="port-from-opengl-es-20-to-direct3d-11"></a>OpenGL ES 2.0 から Direct3D 11 への移植



OpenGL ES 2.0 グラフィックス パイプラインを Direct3D 11 と Windows ランタイムに移植するための記事、概要、チュートリアルを紹介します。

> **注**   OpenGL ES 2.0 プロジェクトを移植する中間の手順は、Microsoft Store の角度を使用します。 ANGLE では、OpenGL ES API 呼び出しを DirectX 11 API 呼び出しに変換することにより、Windows で OpenGL ES コンテンツを実行することができます。 ANGLE について詳しくは、[Microsoft Store 用の ANGLE に関する Wiki ページ](https://go.microsoft.com/fwlink/p/?linkid=618387)をご覧ください。

 

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
<td align="left"><p><a href="map-concepts-and-infrastructure.md">OpenGL ES 2.0 を Direct3D にマップ 11.1</a></p></td>
<td align="left"><p>OpenGL ES 2.0 から Direct3D へのグラフィックス アーキテクチャの移植プロセスを初めて開始する場合は、API 間の主要な違いについて把握しておいてください。 このセクションのトピックは、グラフィックスの処理を Direct3D に移行する際に必ず必要な API の変更と移植戦略を計画するのに役立ちます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="port-a-simple-opengl-es-2-0-renderer-to-directx-11-1.md">方法: ポートの Direct3D 11.1 に単純な OpenGL ES 2.0 レンダラー</a></p></td>
<td align="left"><p>この移植作業では、基本から始めます。Visual Studio 2015 の DirectX 11 アプリ (ユニバーサル Windows) テンプレートに対応するように、頂点シェーディングされた回転する立方体の簡単なレンダラーを OpenGL ES 2.0 から Direct3D に移植します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="opengl-es-2-0-to-directx-11-1-reference.md">OpenGL ES 2.0 Direct3D 11.1 の参照</a></p></td>
<td align="left"><p>OpenGL ES 2.0 から Direct3D 11 への移植の際に API マッピングや簡単なコード サンプルを探す場合は、これらのリファレンス トピックをご覧ください。</p></td>
</tr>
</tbody>
</table>

 

 

 




