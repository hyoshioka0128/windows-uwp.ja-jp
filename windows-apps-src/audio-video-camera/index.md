---
ms.assetid: 0fc12d26-f1cf-4da7-b5a7-735a5074b74a
description: このセクションでは、写真、ビデオ、オーディオをキャプチャ、再生、または編集するユニバーサル Windows (UWP) プラットフォーム アプリの作成について説明します。
title: オーディオ、ビデオ、カメラ
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: db6ee6e5b447bd54f69e35b5fd3736b03778d5a5
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89163956"
---
# <a name="audio-video-and-camera"></a>オーディオ、ビデオ、カメラ


このセクションでは、写真、ビデオ、オーディオをキャプチャ、再生、または編集するユニバーサル Windows (UWP) プラットフォーム アプリの作成について説明します。
 
| トピック                                                                                             | 説明                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [カメラ](camera.md) | UWP アプリで使用可能なカメラ機能と、その使用方法を示すハウツー記事へのリンクを示します。 |
| [メディア再生](media-playback.md) | オーディオとビデオの再生を使用する UWP アプリの作成について説明します。 |
| [画像やビデオでの顔の検出](detect-and-track-faces-in-an-image.md) | ビデオ フレームのシーケンスで顔を経時的に追跡するための [FaceTracker](/uwp/api/Windows.Media.FaceAnalysis.FaceTracker) の使用方法について説明します。 |
| [メディア コンポジションと編集](media-compositions-and-editing.md) | [**Windows.Media.Editing**](/uwp/api/Windows.Media.Editing) 名前空間の API を使って、オーディオとビデオのソース ファイルからメディア コンポジションを作成するアプリを開発する方法について説明します。 |
| [カスタムのビデオ特殊効果](custom-video-effects.md) | ビデオ ストリームのカスタム効果を作成できる **IBasicVideoEffect** インターフェイスを実装する Windows ランタイム コンポーネントを作成する方法について説明します。 |
| [カスタムのオーディオ特殊効果](custom-audio-effects.md) | オーディオ ストリームのカスタム効果を作成できる **IBasicAudioEffect** インターフェイスを実装する Windows ランタイム コンポーネントを作成する方法について説明します。 |
| [ビットマップ画像の作成、編集、保存](imaging.md) | [SoftwareBitmap](/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) オブジェクトを使って画像ファイルの読み込みと保存を行い、ビットマップ画像を表現する方法について説明します。  |
| [オーディオ デバイス情報プロパティ](audio-device-information-properties.md)  | オーディオ デバイスに関連するデバイス情報プロパティを示します。 |
| [オーディオ状態の変化の検出と対応](detect-and-respond-to-audio-state-changes.md)  | オーディオ ストリーム レベルがシステムによって変更された場合に、UWP アプリがそれを検出して対応する方法について説明します。 |
| [メディア ファイルのコード変換](transcode-media-files.md) | [Windows.Media.Transcoding](/uwp/api/Windows.Media.Transcoding) API を使って、ビデオ ファイルをある形式から別の形式にコード変換する方法について説明します。 |
| [バックグラウンドでのメディア ファイルの処理](process-media-files-in-the-background.md) | [MediaProcessingTrigger](/uwp/api/Windows.ApplicationModel.Background.MediaProcessingTrigger) とバックグラウンド タスクを使って、バックグラウンドでメディア ファイルを処理する方法について説明します。 |
| [オーディオ グラフ](audio-graphs.md) | [Windows.Media.Audio](/uwp/api/Windows.Media.Audio) 名前空間の API を使ってオーディオのルーティング、ミキシング、処理のシナリオでオーディオ グラフを作成する方法について説明します。 |
| [MIDI](midi.md) | MIDI (Musical Instrument Digital Interface) デバイスを列挙する方法と、UWP アプリとの間で MIDI メッセージを送受信する方法について説明します。 |
| [デバイスからのメディアのインポート](import-media-from-a-device.md) | 利用可能なメディア ソースの検索、ビデオ、写真、サイドカー ファイルなどのファイルのインポート、ソース デバイスからインポートしたファイルの削除など、デバイスからメディアをインポートする方法について説明します。 |
| [カメラに依存しない懐中電灯](camera-independent-flashlight.md) | デバイスにライトが搭載されている場合、ライトにアクセスして使う方法を説明します。 ライト機能は、デバイスのカメラやカメラのフラッシュ機能とは別に管理されます。 |
| [サポートされるコーデック](supported-codecs.md) | UWP アプリ用のオーディオ、ビデオ、画像のコーデックおよび形式のサポートを示します。 |
| [インストールされているコーデックの照会](codec-query.md) | デバイスにインストールされているオーディオとビデオのエンコーダーとデコーダーを照会する方法を示します。 |
| [画面の取り込み](screen-capture.md) | [Windows.Graphics.Capture 名前空間](/uwp/api/windows.graphics.capture) を使用して、ディスプレイまたはアプリケーション ウィンドウからフレームを取得する方法を説明します。これにより、ビデオ ストリームやスナップショットを作成して、共同作業に対応したインタラクティブなエクスペリエンスを構築できます。 |

## <a name="see-also"></a>関連項目
- [UWP アプリを開発する](../develop/index.md)

 

 

 