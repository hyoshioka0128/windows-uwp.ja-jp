---
ms.assetid: 370f2c14-4f1e-47b3-9197-24205ab255a3
description: この記事では、UWP アプリで使用可能なカメラ機能と、その使用方法を示すハウツー記事へのリンクを示します。
title: カメラ
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: e5b78364f5d59889f249d6d23d414528461368b4
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89161016"
---
# <a name="camera"></a>カメラ

このセクションでは、カメラやマイクを使って写真、ビデオ、オーディオをキャプチャするユニバーサル Windows プラットフォーム (UWP) アプリの作成について説明します。

## <a name="use-the-windows-built-in-camera-ui"></a>Windows 組み込みのカメラ UI を使う

| トピック | 説明 |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Windows の組み込みカメラ UI を使った写真とビデオのキャプチャ](capture-photos-and-video-with-cameracaptureui.md) | [**CameraCaptureUI**](/uwp/api/Windows.Media.Capture.CameraCaptureUI) クラスを使用して、Windows に組み込まれているカメラ UI で写真またはビデオをキャプチャする方法を説明します。 ユーザーが写真やビデオをキャプチャしてアプリに結果を返すだけでよい場合は、これが最も早くて簡単な方法です。  |

## <a name="basic-mediacapture-tasks"></a>基本的な MediaCapture タスク

| トピック | 説明 |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [カメラ プレビューの表示](simple-camera-preview-access.md) | UWP アプリで XAML ページ内にカメラ プレビュー ストリームをすばやく表示する方法を示します。 |
| [MediaCapture を使った基本的な写真、ビデオ、およびオーディオのキャプチャ](basic-photo-video-and-audio-capture-with-MediaCapture.md) | [**MediaCapture**](/uwp/api/Windows.Media.Capture.MediaCapture) クラスを使用して写真やビデオをキャプチャする最も簡単な方法を示します。 **MediaCapture** クラスは、キャプチャ パイプラインに対する低レベルの制御を提供し、高度なキャプチャ シナリオを実現する、堅牢な一連の API を公開しますが、この記事では基本的なメディア キャプチャをアプリにすばやく簡単に追加できるようにすることを目的としています。 |
| [モバイル デバイスのカメラ UI の機能](camera-ui-features-for-mobile-devices.md) | モバイル デバイス上にのみある特殊カメラの UI 機能を活用する方法を示します。  |
                                                                                                               
## <a name="advanced-mediacapture-tasks"></a>高度な MediaCapture タスク   
                                                                                                               
| トピック                                                                                             | 説明                                                                                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [MediaCapture を使ってデバイスと画面の向きを処理する](handle-device-orientation-with-mediacapture.md) | 写真とビデオをキャプチャするときに、ヘルパー クラスを使ってデバイスの向きを処理する方法について説明します。 | 
| [カメラ プロファイルを使用したカメラ機能の検出と選択](camera-profiles.md) | カメラ プロファイルを使ってさまざまなビデオ キャプチャ デバイスの機能を検出および管理する方法について説明します。 これには、特定の解像度やフレーム レートをサポートするプロファイル、複数のカメラへの同時アクセスをサポートするプロファイル、HDR をサポートするプロファイルを選ぶなどのタスクが含まれます。 |
| [MediaCapture の形式、解像度、およびフレーム レートの設定](set-media-encoding-properties.md) | [**IMediaEncodingProperties**](/uwp/api/Windows.Media.MediaProperties.IMediaEncodingProperties) インターフェイスを使用して、カメラのプレビュー ストリームとキャプチャした写真/ビデオの解像度およびフレーム レートを設定する方法を説明します。 プレビュー ストリームの縦横比をキャプチャしたメディアの縦横比と一致させる方法についても説明します。 |
| [HDR とローライトの写真のキャプチャ](high-dynamic-range-hdr-photo-capture.md) | [**AdvancedPhotoCapture**](/uwp/api/Windows.Media.Capture.AdvancedPhotoCapture) クラスを使って、ハイ ダイナミック レンジ (HDR) 写真と低光量写真をキャプチャする方法について説明します。 |
| [写真とビデオのキャプチャのための手動カメラ制御](capture-device-controls-for-photo-and-video-capture.md) | 光学式手ブレ補正やスムーズ ズームなど、写真とビデオのキャプチャに関する拡張シナリオを可能にするために、手動デバイス制御を使う方法について説明します。 |
| [ビデオ キャプチャのための手動カメラ制御](capture-device-controls-for-video-capture.md) | この記事では、ビデオ キャプチャの拡張シナリオ (HDR ビデオ、露出の優先順位など) が手動デバイス制御によってどのように有効になるかを示します。  |
| [ビデオ キャプチャのためのビデオ手ブレ補正効果](effects-for-video-capture.md) | ビデオ手ブレ補正効果を使う方法について説明します。  |
| [MediaCapture のシーン分析](scene-analysis-for-media-capture.md) | [**SceneAnalysisEffect**](/uwp/api/Windows.Media.Core.SceneAnalysisEffect) と [**FaceDetectionEffect**](/uwp/api/Windows.Media.Core.FaceDetectionEffect) を使ってメディア キャプチャのプレビュー ストリームの内容を分析する方法について説明します。  |
| [VariablePhotoSequence で写真シーケンスをキャプチャする](variable-photo-sequence.md) | 可変の写真シーケンスをキャプチャする方法について説明します。これによって、画像を複数のフレームとして次々とキャプチャし、各フレームに別々のフォーカス、フラッシュ、ISO、露出、露出補正の設定を適用することができます。  |
| [MediaFrameReader を使ったメディア フレームの処理](process-media-frames-with-mediaframereader.md) | [**MediaCapture**](/uwp/api/Windows.Media.Capture.MediaCapture) と共に [**MediaFrameReader**](/uwp/api/Windows.Media.Capture.Frames.MediaFrameReader) を使って、色、深度、赤外線カメラ、オーディオ デバイスなどの 1 つ以上の利用可能なソースや、スケルタル トラッキング フレームを生成するようなカスタム フレーム ソースから、メディア フレームを取得する方法を示します。 この機能は、拡張現実アプリや奥行きを検出するカメラ アプリなど、メディア フレームのリアルタイム処理を実行するアプリで使用するために設計されました。  |
| [プレビュー フレームの取得](get-a-preview-frame.md) | メディア キャプチャのプレビュー ストリームから単一のプレビュー フレームを取得する方法について説明します。  |                                                                                                   


## <a name="uwp-app-samples-for-camera"></a>カメラ用の UWP アプリ サンプル

* [カメラの顔検出サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraFaceDetection)
* [カメラのプレビュー フレーム サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraGetPreviewFrame)
* [カメラの HDR サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraAdvancedCapture)
* [カメラの手動制御サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraManualControls)
* [カメラのプロファイル サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraProfile)
* [カメラの解像度サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraResolution)
* [カメラのスターター キット](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraStarterKit)
* [カメラのビデオ手ブレ補正効果サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraVideoStabilization)

## <a name="related-topics"></a>関連トピック

* [オーディオ、ビデオ、およびカメラ](index.md)
 

 