---
title: ゲームのオーディオ
description: ミュージックやサウンドを開発して DirectX ゲームに組み込む方法と、オーディオ信号を処理してダイナミック サウンドやポジショナル サウンドを作成する方法について説明します。
ms.assetid: ab29297a-9588-c79b-24c5-3b94b85e74a8
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, オーディオ, DirectX
ms.localizationpriority: medium
ms.openlocfilehash: 5601a3fc2c4aa1d0aa39295a220bd04c6156343f
ms.sourcegitcommit: eda7bbe9caa9d61126e11f0f1a98b12183df794d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91216555"
---
# <a name="audio-for-games"></a>ゲームのオーディオ

ミュージックやサウンドを開発して DirectX ゲームに組み込む方法と、オーディオ信号を処理してダイナミック サウンドやポジショナル サウンドを作成する方法について説明します。

オーディオプログラミングでは、DirectX で [XAudio2](/windows/win32/xaudio2/xaudio2-apis-portal) ライブラリを使用するか、Windows ランタイム [audio グラフ](../audio-video-camera/audio-graphs.md) api を使用することをお勧めします。 ここでは XAudio2 を使用します。 XAudio2 は、ゲーム開発における信号処理とオーディオ ミキシングの基礎を提供する下位レベルのオーディオ ライブラリです。多様なフォーマットがサポートされています。

[Microsoft メディア ファンデーション](/windows/desktop/medfound/microsoft-media-foundation-sdk)を使用してシンプルなサウンドやミュージックの再生を実装することもできます。 Microsoft メディア ファンデーションは、オーディオとビデオの両方に対応したメディア ファイルやストリームの再生用として設計されていますが、ゲームに利用することもできます。特に、ゲーム中の映画的なシーンや非対話型のコンポーネントに利用できます。

## <a name="concepts-at-a-glance"></a>概念の概要

このセクションで使用するオーディオ プログラミングの概念について以下に説明します。

-   信号は、サウンド プログラミングに使用する基本単位です。グラフィックスにおけるピクセルに相当します。 これらの信号を処理するデジタル シグナル プロセッサ (DSP) は、ゲーム オーディオのピクセル シェーダーのようなものです。 信号の変換、組み合わせ、またはフィルターを行います。 DSP にプログラミングすることにより、ゲームのサウンド効果やミュージックをはるかに簡単な方法で加工することができます。
-   ボイスは、2 つ以上の信号をサブミックスしたコンポジットです。 XAudio2 のボイス オブジェクトには、ソース、サブミックス、マスタリングという 3 種類のボイスがあります。 ソース ボイスは、クライアントから提供されたオーディオ データに適用されます。 ソース ボイスとサブミックス ボイスは、1 つ以上のサブミックス ボイスまたはマスタリング ボイスに向けて出力を送信します。 サブミックス ボイスとマスタリング ボイスは、それぞれに送られるすべてのボイスからオーディオをミキシングし、その結果に対して作用します。 マスタリング ボイスは、オーディオ デバイスにオーディオ データを書き込みます。
-   ミキシングは、シーンの背景で再生されるサウンド効果やバックグラウンド オーディオなど、個別のボイスを組み合わせて単一のストリームを形成するプロセスです。 サブミキシングは、エンジン音などのコンポーネント サウンドを組み合わせて、1 つのボイスを作成するプロセスです。
-   オーディオ形式。 ミュージックとサウンドの効果は、ゲームで使用する多様なデジタル形式で保存できます。 WAV のような非圧縮型や MP3 や OGG などの圧縮型の形式があります。 サンプルの圧縮率が高くなるほど、忠実度が低下します (通常、圧縮率はビット レートで表し、ビット レートが低いほど、圧縮の損失が大きくなります)。 忠実度は、圧縮方式やビット レートによって変動するため、実験しながら実際のゲームに応じた最適のレベルを探る必要があります。
-   サンプル レートと品質。 サウンドは、さまざまなレートでサンプリングできます。低いレートでサンプリングしたサウンドは忠実度が相当低くなります。 CD 品質のサンプル レートは 44.1 Khz (44100 Hz) です。 サウンドに Hi-Fi の音質が必要ない場合は、低いサンプル レートを選択できます。 プロフェッショナル向けのオーディオ アプリケーションであればサンプル レートを高く設定する必要がありますが、ゲーム中でプロ レベルの音質が求められない限り、おそらくその必要ありません。
-   サウンド エミッター (ソース)。 XAudio2 でいうサウンド エミッターとは、バックグラウンド ノズルのブリップ音であれ、ゲーム中のジュークボックスで再生する激しいロック トラックであれ、音を発する場所のことを指します。 エミッターは、ワールド座標で指定します。
-   サウンド リスナー。 サウンド リスナーはプレーヤーであったり、高度なゲームの場合は、リスナーから受け取ったサウンドを処理する AI エンティティであったりします。 そのサウンドを、プレーヤーに対して再生するオーディオ ストリームにサブミックスしたり、特定のゲーム中アクション (たとえばリスナーとしてマークを付けた AI ガードを起動する) に適用したりできます。

## <a name="design-considerations"></a>設計上の考慮事項

オーディオは、ゲームの設計と開発の面できわめて重要な役割を果たします。 凡庸なゲームであっても、記憶に残るサウンドトラックや優れたボイスワーク、サウンド ミキシング、全体に秀逸なオーディオ制作が取り入れられているという単純な理由から、こうしたゲームに伝説的な評価を与えるゲーム プレーヤーも少なくありません。 ミュージックとサウンドはゲームの個性を決定するだけでなく、ゲーム全体の輪郭を定義したり、他の類似したゲームからの差別化を図ったりするための主因にもなります。 ゲームのオーディオ プロファイルの設計と開発に向けて投入した努力は、必ずそれなりの価値があるものです。

3D ポジショナル オーディオは、3D グラフィックスがもたらす没入感に新たな次元を加えるものです。 実世界のシミュレーションや映画のようなシーンの再現を目指した、複雑なゲームを開発している場合は、3D ポジショナル オーディオを利用して、プレーヤーをゲームの世界に引き込むことをお勧めします。

## <a name="directx-audio-development-roadmap"></a>DirectX オーディオ開発のロードマップ

### <a name="xaudio2-conceptual-resources"></a>XAudio2 の概念に関するリソース

XAudio2 は、DirectX 用のオーディオ ミキシング ライブラリで、主に、高パフォーマンスのオーディオ エンジンをゲーム用に開発することを目的としています。 効果音やバックグラウンド ミュージックを自分の最新のゲームに追加したいゲーム開発者にとって、XAudio2 はオーディオ グラフとミキシング エンジンを短い待機時間で提供し、ダイナミック バッファー、同期サンプルアキュレート再生、暗黙的なソース レート変換をサポートします。

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
<td align="left"><p><a href="/windows/desktop/xaudio2/xaudio2-introduction">XAudio2 の概要</a></p></td>
<td align="left"><p>XAudio2 でサポートされるオーディオ プログラミング機能を一覧します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/getting-started">XAudio2 を使う</a></p></td>
<td align="left"><p>XAudio2 の概念、XAudio2 のバージョン、RIFF オーディオ形式について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/common-audio-concepts">オーディオ プログラミングの共通概念</a></p></td>
<td align="left"><p>オーディオ開発者が知っておくべき一般的なオーディオ概念に関する概要を説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/xaudio2-voices">XAudio2 のボイス</a></p></td>
<td align="left"><p>XAudio2 のボイスの概要について説明します。XAudio2 のボイスは、オーディオ データをサブミックス、操作、マスタリングするときに使われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/xaudio2-callbacks">XAudio2 のコールバック</a></p></td>
<td align="left"><p>XAudio2 のコールバックについて説明します。XAudio2 のコールバックは、オーディオ再生の中断を防止するために使われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/audio-graphs">XAudio2 のオーディオ グラフ</a></p></td>
<td align="left"><p>XAudio2 のオーディオ処理グラフについて説明します。オーディオ処理グラフでは、クライアントから一連のオーディオ ストリームを入力として受け取り処理して、最終結果をオーディオ デバイスに配信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/xaudio2-audio-effects">XAudio2 のオーディオ エフェクト</a></p></td>
<td align="left"><p>XAudio2 のオーディオ エフェクトについて説明します。オーディオ エフェクトは、受信したオーディオ データを転送する前に何らかの処理 (リバーブ エフェクトなど) を実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/xaudio2-streaming-audio-data">XAudio2 を使ったオーディオ データのストリーミング</a></p></td>
<td align="left"><p>XAudio2 を使ったオーディオ ストリーミングについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/x3daudio">X3DAudio</a></p></td>
<td align="left"><p>X3DAudio について説明します。X3DAudio は XAudio2 と連携して、3D 空間内の1点からサウンドが聞こえてくるような効果を生み出す API です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/programming-reference">XAudio2 プログラミング リファレンス</a></p></td>
<td align="left"><p>XAudio2 API の詳しいリファレンスです。</p></td>
</tr>
</tbody>
</table>

### <a name="xaudio2-how-to-resources"></a>XAudio2 の操作方法に関するリソース

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
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--initialize-xaudio2">方法: XAudio2 の初期化</a></p></td>
<td align="left"><p>XAudio2 エンジンのインスタンスを作成してからマスタリング ボイスを作成して、XAudio2 をオーディオ再生用に初期化する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--load-audio-data-files-in-xaudio2">方法: XAudio2 でのオーディオ データ ファイルの読み込み</a></p></td>
<td align="left"><p>XAudio2 でオーディオ データを再生するために必要な構造体を設定する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--play-a-sound-with-xaudio2">方法: XAudio2 でのサウンド再生</a></p></td>
<td align="left"><p>XAudio2 で以前読み込まれたオーディオ データを再生する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--use-submix-voices">方法: サブミックス ボイスの使用</a></p></td>
<td align="left"><p>ボイス グループを設定して、その出力を同じサブミックス ボイスに送信する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--use-source-voice-callbacks">方法: ソース ボイスのコールバックの使用</a></p></td>
<td align="left"><p>XAudio2 のソース ボイスのコールバックを使う方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--use-engine-callbacks">方法: エンジン コールバックの使用</a></p></td>
<td align="left"><p>XAudio2 のエンジン コールバックを使う方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--build-a-basic-audio-processing-graph">方法: 基本的なオーディオ処理グラフの作成</a></p></td>
<td align="left"><p>単一のマスタリング ボイスと単一のソース ボイスから構築されたオーディオ処理グラフを作る方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--dynamically-add-or-remove-voices-from-an-audio-graph">方法: オーディオ グラフでのボイスの動的な追加または削除</a></p></td>
<td align="left"><p>「<a href="/windows/desktop/xaudio2/how-to--build-a-basic-audio-processing-graph">方法: 基本的なオーディオ処理グラフの作成</a>」の手順に従って作られたグラフに対して、サブミックス ボイスを追加または削除する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--create-an-effect-chain">方法: エフェクト チェーンの作成</a></p></td>
<td align="left"><p>エフェクト チェーンをボイスに適用して、そのボイスのオーディオ データに対してカスタム処理を加える方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--create-an-xapo">方法: XAPO の作成</a></p></td>
<td align="left"><p>XAudio2 オーディオ処理オブジェクト (XAPO) を作るために <a href="/windows/desktop/api/xapo/nn-xapo-ixapo"><strong>IXAPO</strong></a> を実装する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--add-run-time-parameter-support-to-an-xapo">方法: XAPO へのランタイム パラメーター サポートの追加</a></p></td>
<td align="left"><p><a href="/windows/desktop/api/xapo/nn-xapo-ixapoparameters"><strong>IXAPOParameters</strong></a> インターフェイスを実装して XAPO にランタイム パラメーター サポートを追加する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--use-an-xapo-in-xaudio2">方法: XAudio2 での XAPO の使用</a></p></td>
<td align="left"><p>XAudio2 のエフェクト チェーンで XAPO を使って実装されるエフェクトを使う方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--use-xapofx-in-xaudio2">方法: XAudio2 での XAPOFX の使用</a></p></td>
<td align="left"><p>XAudio2 のエフェクト チェーンで XAPOFX に含まれるエフェクトの 1 つを使う方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--stream-a-sound-from-disk">方法: ディスクからのサウンドのストリーム</a></p></td>
<td align="left"><p>オーディオ バッファーの読み取り用に別のスレッドを作って XAudio2 でオーディオ データをストリームし、コールバックを使ってそのスレッドを制御する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--integrate-x3daudio-with-xaudio2">方法: XAudio2 と X3DAudio の統合</a></p></td>
<td align="left"><p>X3DAudio を使ってXAudio2 のボイスの音量やピッチの値、XAudio2 内蔵のリバーブ エフェクトのパラメーターを指定する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/xaudio2/how-to--group-audio-methods-as-an-operation-set">方法: 操作セットとしてのグループ オーディオ メソッド</a></p></td>
<td align="left"><p>XAudio2 の操作セットを使ってメソッドをグループ化し、これらのメソッドを同時に有効にする方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/xaudio2/debugging-audio-glitches-in-xaudio2">XAudio2 でのオーディオ エラーのデバッグ</a></p></td>
<td align="left"><p>XAudio2 のデバッグ ログ レベルを設定する方法について説明します。</p></td>
</tr>
</tbody>
</table>

### <a name="media-foundation-resources"></a>メディア ファンデーションに関するリソース

メディア ファンデーション (MF) は、ストリーミング オーディオやビデオの再生用のメディア プラットフォームです。 メディア ファンデーション API を使って、さまざまなアルゴリズムでエンコードされ圧縮されたオーディオやビデオをストリーミングできます。 リアルタイムのゲームプレイ シナリオ向けには設計されていませんが、オーディオやビデオのコンポーネントのさらなるリニア キャプチャとプレゼンテーションのための、強力なツールと広範なコーデック サポートを提供します。

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
<td align="left"><p><a href="/windows/desktop/medfound/about-the-media-foundation-sdk">メディア ファンデーションに関するページ</a></p></td>
<td align="left"><p>このセクションでは、メディア ファンデーション API とメディア ファンデーション API をサポートするために使用可能なツールに関する一般的な情報について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/medfound/media-foundation-programming--essential-concepts">メディア ファンデーション: 基本概念</a></p></td>
<td align="left"><p>メディア ファンデーション アプリケーションを作る前に知っておく必要がある概念をいくつか紹介します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/medfound/media-foundation-architecture">メディア ファンデーションのアーキテクチャ</a></p></td>
<td align="left"><p>Microsoft メディア ファンデーションの一般的な設計と、Microsoft メディア ファンデーションで使われるメディア プリミティブと処理パイプラインについて説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/medfound/audio-video-capture">オーディオ/ビデオのキャプチャ</a></p></td>
<td align="left"><p>Microsoft メディア ファンデーションを使ってオーディオやビデオのキャプチャを実行する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/medfound/audio-video-playback">オーディオ/ビデオの再生</a></p></td>
<td align="left"><p>アプリでオーディオ/ビデオの再生を実装する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/medfound/supported-media-formats-in-media-foundation">メディア ファンデーションでサポートされるメディア形式</a></p></td>
<td align="left"><p>Microsoft メディア ファンデーションでネイティブ サポートされるメディア形式を一覧します (サード パーティによっては、カスタム プラグインを作ることによって、追加の形式をサポートできます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/medfound/encoding-and-file-authoring">エンコードとファイルのオーサリング</a></p></td>
<td align="left"><p>Microsoft メディア ファンデーションを使ってオーディオやビデオのエンコード、メディア ファイルのオーサリングを実行する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/medfound/windows-media-codecs">Windows Media コーデック</a></p></td>
<td align="left"><p>Windows Media オーディオおよびビデオのコーデックが備えている機能を使い、圧縮されたデータ ストリームを生成、消費する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/medfound/media-foundation-programming-reference">メディア ファンデーション プログラミング リファレンス</a></p></td>
<td align="left"><p>メディア ファンデーション API のリファレンス情報です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/medfound/media-foundation-sdk-samples">メディア ファンデーション SDK サンプル</a></p></td>
<td align="left"><p>メディア ファンデーションを使う方法について示すサンプル アプリの一覧です。</p></td>
</tr>
</tbody>
</table>

### <a name="windows-runtime-xaml-media-types"></a>Windows ランタイム XAML メディア タイプ

[DirectX と XAML の相互運用機能](/previous-versions/windows/apps/hh825871(v=win.10))を使っている場合は、DirectX と C++ で Windows ランタイム XAML メディア API を UWP アプリに組み込み、ゲーム シナリオを簡素化することができます。

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
<td align="left"><p><a href="/uwp/api/Windows.UI.Xaml.Controls.MediaElement"><strong>Windows.UI.Xaml.Controls.MediaElement</strong></a></p></td>
<td align="left"><p>オーディオ、ビデオ、またはその両方を格納するオブジェクトを表す XAML 要素です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/uwp/audio-video-camera/index">オーディオ、ビデオ、およびカメラ</a></p></td>
<td align="left"><p>ユニバーサル Windows プラットフォーム (UWP) アプリに基本的なオーディオやビデオを組み込む方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/uwp/design/controls-and-patterns/media-playback">MediaElement</a></p></td>
<td align="left"><p>UWP アプリでローカルに保存されているメディア ファイルを再生する方法について説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/uwp/design/controls-and-patterns/media-playback">MediaElement</a></p></td>
<td align="left"><p>UWP アプリにメディア ファイルを低遅延でストリーミングする方法について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/uwp/audio-video-camera/media-casting">メディアのキャスト</a></p></td>
<td align="left"><p>リモート再生コントラクトを使って、UWP アプリから別のデバイスへメディアをストリーミングする方法について説明します。</p></td>
</tr>
</tbody>
</table>

## <a name="reference"></a>リファレンス

-   [XAudio2 の概要](/windows/desktop/xaudio2/xaudio2-introduction)
-   [XAudio2 プログラミング ガイド](/windows/desktop/xaudio2/programming-guide)
-   [Microsoft メディア ファンデーションの概要](/windows/desktop/medfound/microsoft-media-foundation-sdk)

## <a name="related-topics"></a>関連トピック

-   [XAudio2 プログラミング ガイド](/windows/desktop/xaudio2/programming-guide)