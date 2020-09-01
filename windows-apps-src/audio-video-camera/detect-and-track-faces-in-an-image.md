---
ms.assetid: 84729E44-10E9-4D7D-8575-6A9D97467ECD
description: このトピックでは、FaceDetector を使って画像内の顔を検出する方法について説明します。 FaceTracker は、ビデオ フレームのシーケンスで顔を経時的に追跡するように最適化されています。
title: 画像やビデオでの顔の検出
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: b6b2cf937646f41a2e51e6a109d272965817665f
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89160886"
---
# <a name="detect-faces-in-images-or-videos"></a>画像やビデオでの顔の検出



\[一部の情報はリリース前の製品に関する事項であり、正式版がリリースされるまでに大幅に変更される可能性があります。 ここに記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。\]

このトピックでは、[**FaceDetector**](/uwp/api/Windows.Media.FaceAnalysis.FaceDetector) を使って画像内の顔を検出する方法について説明します。 [**FaceTracker**](/uwp/api/Windows.Media.FaceAnalysis.FaceTracker) は、ビデオ フレームのシーケンスで顔を経時的に追跡するように最適化されています。

[**FaceDetectionEffect**](/uwp/api/Windows.Media.Core.FaceDetectionEffect) を使った顔を追跡する別の方法については、「[メディア キャプチャのシーン分析](scene-analysis-for-media-capture.md)」をご覧ください。

この記事のコードは、[基本的な顔検出](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicFaceDetection)と[基本的な顔追跡](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicFaceTracking)のサンプルを基にしています。 これらのサンプルをダウンロードし、該当するコンテキストで使われているコードを確認することも、サンプルを独自のアプリの開始点として使うこともできます。

## <a name="detect-faces-in-a-single-image"></a>1 つの画像内の顔を検出する

[**FaceDetector**](/uwp/api/Windows.Media.FaceAnalysis.FaceDetector) クラスを使うと、静止画像内の 1 つまたは複数の顔を検出できます。

この例では、次の名前空間の API を使っています。

[!code-cs[FaceDetectionUsing](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetFaceDetectionUsing)]

[**FaceDetector**](/uwp/api/Windows.Media.FaceAnalysis.FaceDetector) オブジェクト用と、画像から検出される [**DetectedFace**](/uwp/api/Windows.Media.FaceAnalysis.DetectedFace) オブジェクトの一覧用に、クラス メンバー変数を宣言しています。

[!code-cs[ClassVariables1](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetClassVariables1)]

顔検出は、さまざまな方法で作成できる [**SoftwareBitmap**](/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) オブジェクトに対して可能です。 この例では、[**FileOpenPicker**](/uwp/api/Windows.Storage.Pickers.FileOpenPicker) を使って、顔が検出される画像ファイルをユーザーが選べるようにしています。 ソフトウェア ビットマップの操作について詳しくは、「[イメージング](imaging.md)」をご覧ください。

[!code-cs[Picker](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetPicker)]

[**BitmapDecoder**](/uwp/api/Windows.Graphics.Imaging.BitmapDecoder) クラスを使って、**SoftwareBitmap** に画像ファイルをデコードします。 顔検出処理は、画像が小さいほど高速になるため、ソース画像の縮小が必要になる場合があります。 デコード中にこれを行うには、[**BitmapTransform**](/uwp/api/Windows.Graphics.Imaging.BitmapTransform) オブジェクトを作成し、[**ScaledWidth**](/uwp/api/windows.graphics.imaging.bitmaptransform.scaledwidth) および [**ScaledHeight**](/uwp/api/windows.graphics.imaging.bitmaptransform.scaledheight) プロパティを設定して、そのオブジェクトを [**GetSoftwareBitmapAsync**](/uwp/api/windows.graphics.imaging.bitmapdecoder.getsoftwarebitmapasync) の呼び出しに渡します。これにより、デコードされて縮小された **SoftwareBitmap** が返されます。

[!code-cs[Decode](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetDecode)]

現在のバージョンでは、**FaceDetector** クラスでのみ Gray8 または Nv12 の画像がサポートされています。 **SoftwareBitmap** クラスには、ビットマップの形式を変換する [**Convert**](/uwp/api/windows.graphics.imaging.softwarebitmap.convert) メソッドが用意されています。 この例では、ソース画像を Gray8 ピクセル形式に変換しています (まだその形式になっていない場合)。 必要に応じて、[**GetSupportedBitmapPixelFormats**](/uwp/api/windows.media.faceanalysis.facedetector.getsupportedbitmappixelformats) および [**IsBitmapPixelFormatSupported**](/uwp/api/windows.media.faceanalysis.facedetector.isbitmappixelformatsupported) メソッドを使って、ピクセル形式がサポートされているかどうかを実行時に調べることができます。これにより、サポートされている一連の形式が今後のバージョンで拡張される場合に備えることができます。

[!code-cs[Format](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetFormat)]

[**CreateAsync**](/uwp/api/windows.media.faceanalysis.facedetector.createasync) を呼び出すことで **FaceDetector** オブジェクトをインスタンス化したら、[**DetectFacesAsync**](/uwp/api/windows.media.faceanalysis.facedetector.detectfacesasync) を呼び出して、適切なサイズに拡大縮小済み、サポートされているピクセル形式に変換済みのビットマップを渡します。 このメソッドは [**DetectedFace**](/uwp/api/Windows.Media.FaceAnalysis.DetectedFace) オブジェクトの一覧を返します。 **ShowDetectedFaces** はヘルパー メソッドであり、次に示しているように、画像内の顔の周りに四角形を描画します。

[!code-cs[Detect](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetDetect)]

顔検出処理の実行中に作成されたオブジェクトは必ず破棄してください。

[!code-cs[Dispose](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetDispose)]

画像を表示し、検出された顔の周りに四角形を描画するには、XAML ページに [**Canvas**](/uwp/api/Windows.UI.Xaml.Controls.Canvas) 要素を追加します。

[!code-xml[Canvas](./code/FaceDetection_Win10/cs/MainPage.xaml#SnippetCanvas)]

描画される四角形のスタイルの設定用に、いくつかのメンバー変数を定義します。

[!code-cs[ClassVariables2](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetClassVariables2)]

**ShowDetectedFaces** ヘルパー メソッドでは、新しい [**ImageBrush**](/uwp/api/Windows.UI.Xaml.Media.ImageBrush) が作成され、ソースが、ソース画像を表す **SoftwareBitmap**  から作成された [**SoftwareBitmapSource**](/uwp/api/Windows.UI.Xaml.Media.Imaging.SoftwareBitmapSource) に設定されます。 XAML **Canvas** コントロールの背景がイメージ ブラシに設定されます。

ヘルパー メソッドに渡された顔の一覧が空でない場合は、一覧内の各顔をループし、[**DetectedFace**](/uwp/api/Windows.Media.FaceAnalysis.DetectedFace) クラスの [**FaceBox**](/uwp/api/windows.media.faceanalysis.detectedface.facebox) プロパティを使って、画像内で顔の周りの四角形の位置とサイズを調べます。 **Canvas** コントロールはほとんどの場合、ソース画像と異なるサイズであるため、**FaceBox** の X 座標と Y 座標にも、幅と高さにも、拡大縮小値 (ソース画像のサイズと **Canvas** コントロールの実際のサイズとの比率) を掛ける必要があります。

[!code-cs[ShowDetectedFaces](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetShowDetectedFaces)]

## <a name="track-faces-in-a-sequence-of-frames"></a>フレームのシーケンスで顔を追跡する

ビデオ内の顔を検出する場合は、[**FaceDetector**](/uwp/api/Windows.Media.FaceAnalysis.FaceDetector) よりも [**FaceTracker**](/uwp/api/Windows.Media.FaceAnalysis.FaceTracker) クラスを使う方が効率的です。実装手順はほとんど同じです。 **FaceTracker** では、前に処理したフレームに関する情報を使って検出処理を最適化します。

[!code-cs[FaceTrackingUsing](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetFaceTrackingUsing)]

**FaceTracker** オブジェクトのクラス変数を宣言します。 この例では、[**ThreadPoolTimer**](/uwp/api/Windows.System.Threading.ThreadPoolTimer) を使って、定義した間隔で顔追跡を開始します。 [SemaphoreSlim](/dotnet/api/system.threading.semaphoreslim) を使って、同時に 1 つの顔追跡処理のみが実行されるようにします。

[!code-cs[ClassVariables3](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetClassVariables3)]

顔追跡処理を初期化するには、[**CreateAsync**](/uwp/api/windows.media.faceanalysis.facetracker.createasync) を呼び出して新しい **FaceTracker** オブジェクトを作成します。 目的のタイマー間隔を初期化してから、タイマーを作成します。 指定した間隔が経過するたびに **ProcessCurrentVideoFrame** ヘルパー メソッドが呼び出されます。

[!code-cs[TrackingInit](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetTrackingInit)]

**ProcessCurrentVideoFrame** ヘルパー メソッドはタイマーによって非同期的に呼び出されるため、このメソッドはまず、セマフォの **Wait** メソッドを呼び出して、追跡処理が進行中であるかどうかを調べて、そうであれば、顔を検出しようとせずに戻ります。 このメソッドの最後で、セマフォの **Release** メソッドが呼び出され、後続の **ProcessCurrentVideoFrame** が呼び出されて、処理が続行されます。

[**FaceTracker**](/uwp/api/Windows.Media.FaceAnalysis.FaceTracker) クラスは [**VideoFrame**](/uwp/api/Windows.Media.VideoFrame) オブジェクトに対して使えます。 **VideoFrame** を取得するには、複数の方法があります。たとえば、実行中の [MediaCapture](./index.md) オブジェクトからプレビュー フレームをキャプチャします。または、[**IBasicVideoEffect**](/uwp/api/Windows.Media.Effects.IBasicVideoEffect) の [**ProcessFrame**](/uwp/api/windows.media.effects.ibasicaudioeffect.processframe) メソッドを実装します。 この例では、ビデオ フレームを返す未定義のヘルパー メソッド **GetLatestFrame** をこの処理のプレースホルダーとして使っています。 実行中のメディア キャプチャ デバイスのプレビュー ストリームからビデオ フレームを取得する方法について詳しくは、「[プレビュー フレームの取得](get-a-preview-frame.md)」をご覧ください。

**FaceDetector** と同様、**FaceTracker** でも、サポートされていないピクセル形式があります。 この例では、渡されたフレームが Nv12 形式でない場合は顔検出を破棄します。

[**ProcessNextFrameAsync**](/uwp/api/windows.media.faceanalysis.facetracker.processnextframeasync) を呼び出して、フレーム内の顔を表す [**DetectedFace**](/uwp/api/Windows.Media.FaceAnalysis.DetectedFace) オブジェクトの一覧を取得します。 顔の一覧を取得したら、顔検出について先ほど説明した同じ方法でそれらの顔を表示できます。 Face tracking ヘルパーメソッドは UI スレッドで呼び出されないため、 [**CoreDispatcher**](/uwp/api/windows.ui.core.coredispatcher.runasync)の呼び出し内で ui 更新を行う必要があります。

[!code-cs[ProcessCurrentVideoFrame](./code/FaceDetection_Win10/cs/MainPage.xaml.cs#SnippetProcessCurrentVideoFrame)]

## <a name="related-topics"></a>関連トピック

* [メディア キャプチャのシーン分析](scene-analysis-for-media-capture.md)
* [基本的な顔検出のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicFaceDetection)
* [基本的な顔追跡のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicFaceTracking)
* [カメラ](camera.md)
* [MediaCapture を使った基本的な写真、ビデオ、およびオーディオのキャプチャ](basic-photo-video-and-audio-capture-with-MediaCapture.md)
* [メディア再生](media-playback.md)