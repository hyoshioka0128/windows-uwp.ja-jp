---
ms.assetid: D6A785C6-DF28-47E6-BDC1-7A7129EC40A0
description: この記事では、MediaFrameReader で MediaCapture を使用して、オーディオ データが格納された AudioFrame をキャプチャ ソースから取得する方法を示します。
title: MediaFrameReader を使ったオーディオ フレームの処理
ms.date: 04/18/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 18ef0ee1efb7a69a8b305c9b95e84938fe6fde32
ms.sourcegitcommit: c3ca68e87eb06971826087af59adb33e490ce7da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89363895"
---
# <a name="process-audio-frames-with-mediaframereader"></a>MediaFrameReader を使ったオーディオ フレームの処理

この記事では、[**MediaFrameReader**](/uwp/api/Windows.Media.Capture.Frames.MediaFrameReader) で [**MediaCapture**](/uwp/api/Windows.Media.Capture.MediaCapture) を使用して、メディア フレーム ソースからオーディオ データを取得する方法を示します。 **MediaFrameReader** を使用して、カラー カメラ、赤外線カメラ、深度カメラなどから画像データを取得する方法については、「[MediaFrameReader を使ったメディア フレームの処理](process-media-frames-with-mediaframereader.md)」をご覧ください。 この記事では、フレーム リーダーの使用パターンの一般的な概要を示すと共に、**MediaFrameReader** クラスの追加機能として、**MediaFrameSourceGroup** を使用して複数のソースから同時にフレームを取得する方法などを説明します。 

> [!NOTE] 
> この記事で説明している機能は、Windows 10 バージョン 1803 以降でのみ利用できます。

> [!NOTE] 
> **MediaFrameReader** を使ってカラー カメラ、深度カメラ、赤外線カメラなど、さまざまなフレーム ソースからのフレームを表示する方法を示す、ユニバーサル Windows アプリのサンプルがあります。 詳しくは、「[カメラ フレームのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraFrames)」をご覧ください。

## <a name="setting-up-your-project"></a>プロジェクトの設定
オーディオ フレームを取得するためのプロセスは、他の種類のメディア フレームを取得する場合とほぼ同じです。 **MediaCapture** を使う他のアプリと同様に、カメラ デバイスにアクセスする前にアプリが *webcam* 機能を使うことを宣言する必要があります。 アプリがオーディオ デバイスからキャプチャする場合は、*microphone* デバイス機能も宣言する必要があります。 

**アプリ マニフェストに機能を追加する**

1.  Microsoft Visual Studio の**ソリューション エクスプローラー**で、**package.appxmanifest** 項目をダブルクリックしてアプリケーション マニフェストのデザイナーを開きます。
2.  **[機能]** タブを選択します。
3.  [ **Webcam** ] チェックボックスと [ **マイク**] ボックスをオンにします。
4.  画像ライブラリとビデオ ライブラリにアクセスするには、**[画像ライブラリ]** のボックスと **[ビデオ ライブラリ]** のボックスをオンにします。



## <a name="select-frame-sources-and-frame-source-groups"></a>フレーム ソースとフレーム ソース グループを選択する

オーディオ フレームをキャプチャするには、まず、マイクその他のオーディオ キャプチャ デバイスをはじめとする、オーディオ データのソースを表す [**MediaFrameSource**](/uwp/api/Windows.Media.Capture.Frames.MediaFrameSource) を初期化します。 これには、[**MediaCapture**](/uwp/api/Windows.Media.Capture.MediaCapture) オブジェクトの新しいインスタンスを作成する必要があります。 この例では、**MediaCapture** の唯一の初期化設定として、[**StreamingCaptureMode**](/uwp/api/windows.media.capture.mediacaptureinitializationsettings.streamingcapturemode) を設定し、キャプチャ デバイスからオーディオをストリームすることを示します。 

[**MediaCapture.InitializeAsync**](/uwp/api/windows.media.capture.mediacapture.initializeasync) の呼び出し後は、アクセス可能なメディア フレーム ソースの一覧を [**FrameSources**](/uwp/api/windows.media.capture.mediacapture.framesources) プロパティによって取得できます。 この例では、Linq クエリを使用して、フレームソースを記述する [**MediaFrameSourceInfo**](/uwp/api/windows.media.capture.frames.mediaframesourceinfo) で [**MediaStreamType**](/uwp/api/windows.media.capture.frames.mediaframesourceinfo.mediastreamtype) が **Audio** に設定されている (つまり、メディア ソースがオーディオ データを生成している) すべてのフレーム ソースを選択しています。

クエリが 1 つまたは複数のフレーム ソースを返す場合は、[**CurrentFormat**](/uwp/api/windows.media.capture.frames.mediaframesource.currentformat) プロパティで、ソースが目的のオーディオ形式 (この例では、浮動小数点型のオーディオ データ) をサポートしているかどうかを確認します。 [**AudioEncodingProperties**](/uwp/api/windows.media.capture.frames.mediaframeformat.audioencodingproperties) で、目的のオーディオ エンコードがサポートされていることを確認します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/Frames_Win10/cs/Frames_Win10/MainPage.xaml.cs" id="SnippetInitAudioFrameSource":::

## <a name="create-and-start-the-mediaframereader"></a>MediaFrameReader を作成して開始する

**MediaFrameReader** の新しいインスタンスを取得するために、前の手順で選択した **MediaFrameSource** オブジェクトを渡して [**MediaCapture.CreateFrameReaderAsync**](/uwp/api/windows.media.capture.mediacapture.createframereaderasync#Windows_Media_Capture_MediaCapture_CreateFrameReaderAsync_Windows_Media_Capture_Frames_MediaFrameSource_) を呼び出します。 既定では、オーディオ フレームがバッファー モードで取得されます。これにより、フレーム損失の可能性は低くなりますが、それでもなおオーディオ フレームの処理が間に合わず、システムに割り当てられたメモリ バッファーがいっぱいになると、フレームの損失が発生します。

オーディオ データの新しいフレームが利用可能になったときにシステムによって生成される [**MediaFrameReader.FrameArrived**](/uwp/api/windows.media.capture.frames.mediaframereader.framearrived) イベントのハンドラーを登録します。 [**StartAsync**](/uwp/api/windows.media.capture.frames.mediaframereader.startasync) を呼び出して、オーディオ フレームの取得を開始します。 フレーム リーダーが開始できない場合、呼び出しから返される状態値には、[**Success**](/uwp/api/windows.media.capture.frames.mediaframereaderstartstatus) 以外の値が格納されます。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/Frames_Win10/cs/Frames_Win10/MainPage.xaml.cs" id="SnippetCreateAudioFrameReader":::

**FrameArrived** イベント ハンドラーで、センダーとしてハンドラーに渡される **MediaFrameReader** オブジェクトに対して [**TryAcquireLatestFrame**](/uwp/api/windows.media.capture.frames.mediaframereader.tryacquirelatestframe) を呼び出し、最新のメディア フレームへの参照の取得を試みます。 このオブジェクトは null の場合があるため、オブジェクトを使用する前に常に確認する必要があります。 **TryAcquireLatestFrame** から返される **MediaFrameReference** にラップされたメディア フレームの種類は、フレーム リーダーで取得対象として構成した 1 つまたは複数のフレーム ソースの種類によって異なります。 この例では、フレーム リーダーがオーディオ フレームを取得するように設定されているため、[**AudioMediaFrame**](/uwp/api/windows.media.capture.frames.mediaframereference.audiomediaframe) プロパティを使用している、基になるフレームが取得されます。 

以下の例で、この **ProcessAudioFrame** ヘルパー メソッドは、フレームのタイムスタンプや、フレームが **AudioMediaFrame** オブジェクトと非連続的かどうかなどの情報が入った [**AudioFrame**](/uwp/api/windows.media.audioframe) の取得方法を示します。 オーディオ サンプル データを読み取りまたは処理するには、[**AudioBuffer**](/uwp/api/windows.media.audiobuffer) オブジェクトを **AudioMediaFrame** オブジェクトから取得し、[**IMemoryBufferReference**](/uwp/api/windows.foundation.imemorybufferreference) を作成した後、COM メソッド **IMemoryBufferByteAccess::GetBuffer** を呼び出してデータを取得します。 ネイティブ バッファーへのアクセス方法について詳しくは、コード例の下の注をご覧ください。

データの形式は、フレーム ソースに依存します。 この例では、メディア フレーム ソースの選択時に、選択したフレーム ソースが 1 つの浮動小数点型のデータ チャネルを使用していることを明示的に確認しました。 以下の最後のコード例では、フレーム内のオーディオ データの継続期間とサンプル数を確認する方法を示します。  

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/Frames_Win10/cs/Frames_Win10/MainPage.xaml.cs" id="SnippetProcessAudioFrame":::

> [!NOTE] 
> オーディオ データを操作するためには、ネイティブ メモリ バッファーにアクセスする必要があります。 これには、以下に示すコードを追加して、COM インターフェイス **IMemoryBufferByteAccess** を使用する必要があります。 ネイティブ バッファーに対する操作は、**unsafe** キーワードを使用するメソッド内で実行する必要があります。 また **[プロジェクト] -> [プロパティ]** ダイアログの **[ビルド]** タブで、安全でないコードを許可するボックスをオンにする必要があります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/Frames_Win10/cs/Frames_Win10/FrameRenderer.cs" id="SnippetIMemoryBufferByteAccess":::

## <a name="additional-information-on-using-mediaframereader-with-audio-data"></a>オーディオ データでの MediaFrameReader の使用に関する追加情報

オーディオ フレーム ソースに関連付けられた [**AudioDeviceController**](/uwp/api/Windows.Media.Devices.AudioDeviceController) を取得するには、[**MediaFrameSource.Controller**](/uwp/api/windows.media.capture.frames.mediaframesource.controller) プロパティにアクセスします。 このオブジェクトは、キャプチャ デバイスのストリーム プロパティの取得や設定、またはキャプチャ レベルの制御に使用できます。 以下の例では、フレーム リーダーが継続的にフレームを取得するが、すべてのサンプルで値が 0 になるように、オーディオ デバイスをミュートしています。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/Frames_Win10/cs/Frames_Win10/MainPage.xaml.cs" id="SnippetAudioDeviceControllerMute":::

メディア フレーム ソースによってキャプチャされたオーディオ データは、[**AudioFrame**](/uwp/api/windows.media.audioframe) オブジェクトを使用して、[**AudioGraph**](/uwp/api/windows.media.audio.audiograph) に渡すことができます。 フレームは、[**AudioFrameInputNode**](/uwp/api/windows.media.audio.audioframeinputnode) の [**AddFrame**](/uwp/api/windows.media.audio.audioframeinputnode.addframe) メソッドに渡します。 オーディオ グラフを使用して、オーディオ信号をキャプチャ、処理、ミックスする方法について詳しくは、「[オーディオ グラフ](audio-graphs.md)」をご覧ください。

## <a name="related-topics"></a>関連トピック

* [MediaFrameReader を使ったメディア フレームの処理](process-media-frames-with-mediaframereader.md)
* [カメラ](camera.md)
* [MediaCapture を使った基本的な写真、ビデオ、およびオーディオのキャプチャ](basic-photo-video-and-audio-capture-with-MediaCapture.md)
* [カメラ フレームのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CameraFrames)
* [オーディオ グラフ](audio-graphs.md)
 
