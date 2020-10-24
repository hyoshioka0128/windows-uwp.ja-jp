---
Description: この記事では、ビデオ ストリームのカスタム効果を作成するための IBasicVideoEffect インターフェイスを実装する Windows ランタイム コンポーネントを作成する方法について説明します。
MS-HAID: dev\_audio\_vid\_camera.custom\_video\_effects
MSHAttr: PreferredLib:/library/windows/apps
Search.Product: eADQiWindows 10XVcnh
title: カスタムのビデオ特殊効果
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 40a6bd32-a756-400f-ba34-2c5f507262c0
ms.localizationpriority: medium
ms.openlocfilehash: a80e00a44bbb1c401811f72eb7024aef25013f29
ms.sourcegitcommit: c3ca68e87eb06971826087af59adb33e490ce7da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89363955"
---
# <a name="custom-video-effects"></a>カスタムのビデオ特殊効果




この記事では、ビデオ ストリームのカスタム効果を作成するための [**IBasicVideoEffect**](/uwp/api/Windows.Media.Effects.IBasicVideoEffect) インターフェイスを実装する Windows ランタイム コンポーネントを作成する方法について説明します。 カスタム効果は、デバイスのカメラへのアクセスを提供する [MediaCapture](/uwp/api/Windows.Media.Capture.MediaCapture)、メディア クリップから複雑なコンポジションを作成するための [**MediaComposition**](/uwp/api/Windows.Media.Editing.MediaComposition) など、さまざまな Windows ランタイム API で使うことができます。

## <a name="add-a-custom-effect-to-your-app"></a>アプリへのカスタム効果の追加


カスタムのビデオ特殊効果は、[**IBasicVideoEffect**](/uwp/api/Windows.Media.Effects.IBasicVideoEffect) インターフェイスを実装するクラスで定義します。 このクラスは、アプリのプロジェクトに直接含めることはできません。 代わりに、Windows ランタイム コンポーネントを使ってビデオ特殊効果のクラスをホストする必要があります。

**ビデオ効果の Windows ランタイムコンポーネントを追加する**

1.  Microsoft Visual Studio で、ソリューションを開いた状態で、[ **ファイル** ] メニューにアクセスし、[追加]、[ ** &gt; 新しいプロジェクト**] の順番に選択します。
2.  プロジェクトの種類として **[Windows ランタイム コンポーネント (ユニバーサル Windows)]** を選びます。
3.  この例では、プロジェクトに *VideoEffectComponent* という名前を付けます。 この名前は後でコードで参照されます。
4.  **[OK]** をクリックします。
5.  プロジェクト テンプレートに基づいて、Class1.cs という名前のクラスが作成されます。 **ソリューション エクスプローラー**で、Class1.cs のアイコンを右クリックし、**[名前の変更]** をクリックします。
6.  ファイル名を *ExampleVideoEffect.cs* に変更します。 すべての参照を新しい名前に更新するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。
7.  **ExampleVideoEffect.cs** を開き、クラス定義を更新して [**IBasicVideoEffect**](/uwp/api/Windows.Media.Effects.IBasicVideoEffect) インターフェイスを実装します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetImplementIBasicVideoEffect":::


この記事の例で使うすべての型にアクセスできるように、効果のクラス ファイルに次の名前空間を含める必要があります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetEffectUsing":::


## <a name="implement-the-ibasicvideoeffect-interface-using-software-processing"></a>ソフトウェア処理を使用した IBasicVideoEffect インターフェイスの実装


ビデオ特殊効果では、[**IBasicVideoEffect**](/uwp/api/Windows.Media.Effects.IBasicVideoEffect) インターフェイスのすべてのメソッドとプロパティを実装する必要があります。 このセクションでは、このインターフェイスの実装方法の説明として、ソフトウェア処理を使用した簡単な実装を示します。

### <a name="close-method"></a>Close メソッド

[**Close**](/uwp/api/windows.media.effects.ibasicvideoeffect.close) メソッドは、クラスで効果をシャットダウンする必要があるときに呼び出されます。 このメソッドを使って、作成したすべてのリソースを破棄する必要があります。 このメソッドの [**MediaEffectClosedReason**](/uwp/api/Windows.Media.Effects.MediaEffectClosedReason) 引数により、効果が正常に終了されたかどうかがわかります。エラーが発生したり、必要なエンコード形式が効果でサポートされていないと、この引数で通知されます。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetClose":::


### <a name="discardqueuedframes-method"></a>DiscardQueuedFrames メソッド

[**DiscardQueuedFrames**](/uwp/api/windows.media.effects.ibasicvideoeffect.discardqueuedframes) メソッドは、効果をリセットする必要があるときに呼び出されます。 典型的なシナリオとしては、現在のフレームの処理で使うために前に処理したフレームを保存している場合などが挙げられます。 このメソッドが呼び出されたときは、保存した一連のフレームを破棄する必要があります。 このメソッドでは、蓄積されたビデオ フレームだけでなく、前のフレームに関連するすべての状態をリセットできます。


:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetDiscardQueuedFrames":::



### <a name="isreadonly-property"></a>IsReadOnly プロパティ

[**IsReadOnly**](/uwp/api/windows.media.effects.ibasicvideoeffect.isreadonly) プロパティは、効果の出力への書き込みを行うかどうかを示します。 アプリでビデオ フレームを変更しない場合 (ビデオ フレームの分析のみを行う場合など) は、このプロパティを true に設定します。これにより、フレーム入力がフレーム出力に効率的にコピーされるようになります。

> [!TIP]
> [**IsReadOnly**](/uwp/api/windows.media.effects.ibasicvideoeffect.isreadonly) プロパティを true に設定すると、入力フレームが出力フレームにコピーされてから [**ProcessFrame**](/uwp/api/windows.media.effects.ibasicvideoeffect.processframe) が呼び出されます。 **IsReadOnly** プロパティを true に設定しても、**ProcessFrame** での効果の出力フレームに対する書き込みは制限されません。


:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetIsReadOnly":::

### <a name="setencodingproperties-method"></a>SetEncodingProperties メソッド

[**SetEncodingProperties**](/uwp/api/windows.media.effects.ibasicvideoeffect.setencodingproperties) は、効果の対象となるビデオ ストリームのエンコード プロパティを示すために呼び出されます。 このメソッドは、ハードウェア レンダリングに使う Direct3D デバイスへの参照も提供します。 このデバイスの用途については、この後のハードウェア処理の例で説明します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetSetEncodingProperties":::


### <a name="supportedencodingproperties-property"></a>SupportedEncodingProperties プロパティ

[**SupportedEncodingProperties**](/uwp/api/windows.media.effects.ibasicvideoeffect.supportedencodingproperties) プロパティは、効果でサポートされるエンコード プロパティを確認するためにシステムでチェックされます。 効果で指定したプロパティを使ってビデオをエンコードできない場合、[**Close**](/uwp/api/windows.media.effects.ibasicvideoeffect.close) が呼び出され、効果がビデオ パイプラインから削除されます。


:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetSupportedEncodingProperties":::


> [!NOTE] 
> **SupportedEncodingProperties** から返される [**VideoEncodingProperties**](/uwp/api/Windows.Media.MediaProperties.VideoEncodingProperties) オブジェクトの一覧を空にすると、既定で ARGB32 エンコードが使われます。

 

### <a name="supportedmemorytypes-property"></a>SupportedMemoryTypes プロパティ

[**SupportedMemoryTypes**](/uwp/api/windows.media.effects.ibasicvideoeffect.supportedmemorytypes) プロパティは、ソフトウェア メモリとハードウェア (GPU) メモリのどちらのビデオ フレームにアクセスするかを確認するためにシステムでチェックされます。 [**MediaMemoryTypes.Cpu**](/uwp/api/Windows.Media.Effects.MediaMemoryTypes) を指定すると、画像データを [**SoftwareBitmap**](/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) オブジェクトに格納する入力フレームと出力フレームが渡されます。 **MediaMemoryTypes.Gpu** を指定すると、画像データを [**IDirect3DSurface**](/uwp/api/Windows.Graphics.DirectX.Direct3D11.IDirect3DSurface) オブジェクトに格納する入力フレームと出力フレームが渡されます。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetSupportedMemoryTypes":::


> [!NOTE]
> [**MediaMemoryTypes.GpuAndCpu**](/uwp/api/Windows.Media.Effects.MediaMemoryTypes) を指定すると、GPU とシステム メモリのどちらを使うかがパイプラインの効率に基づいて判断されます。 この値を使用する場合は、 [**Processframe**](/uwp/api/windows.media.effects.ibasicvideoeffect.processframe) メソッドをチェックインして、メソッドに渡された [**ソフトウェアビットマップ**](/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) または [**IDirect3DSurface**](/uwp/api/Windows.Graphics.DirectX.Direct3D11.IDirect3DSurface) にデータが含まれているかどうかを確認し、それに応じてフレームを処理する必要があります。

 

### <a name="timeindependent-property"></a>TimeIndependent プロパティ

[**TimeIndependent**](/uwp/api/windows.media.effects.ibasicvideoeffect.timeindependent) プロパティは、効果のタイミングを合わせる必要がないかどうかを示します。 true に設定すると、効果のパフォーマンスを高めるために最適化を使用できるようになります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetTimeIndependent":::

### <a name="setproperties-method"></a>SetProperties メソッド

[**SetProperties**](/uwp/api/windows.media.imediaextension.setproperties) メソッドは、呼び出し元のアプリで効果のパラメーターを調整するために使われます。 プロパティは、プロパティ名と値の [**IPropertySet**](/uwp/api/Windows.Foundation.Collections.IPropertySet) マップとして渡されます。


:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetSetProperties":::


指定の値に基づいて各ビデオ フレームのピクセルを暗くする簡単な例を次に示します。 プロパティを宣言し、呼び出し元アプリで設定された値を TryGetValue で取得しています。 値が設定されていない場合は、既定値の .5 が使われます。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetFadeValue":::


### <a name="processframe-method"></a>ProcessFrame メソッド

[**ProcessFrame**](/uwp/api/windows.media.effects.ibasicvideoeffect.processframe) メソッドは、ビデオの画像データを変更するためのメソッドです。 このメソッドはフレームごとに 1 回呼び出され、[**ProcessVideoFrameContext**](/uwp/api/Windows.Media.Effects.ProcessVideoFrameContext) オブジェクトが渡されます。 このオブジェクトには、処理対象の着信フレームを格納する入力 [**VideoFrame**](/uwp/api/Windows.Media.VideoFrame) オブジェクトと、ビデオ パイプラインの残りの部分に渡す画像データを書き込む出力 **VideoFrame** オブジェクトが含まれています。 それらの **VideoFrame** オブジェクトのそれぞれに [**SoftwareBitmap**](/uwp/api/windows.media.videoframe.softwarebitmap) プロパティと [**Direct3DSurface**](/uwp/api/windows.media.videoframe.direct3dsurface) プロパティがありますが、どちらを使用できるかは [**SupportedMemoryTypes**](/uwp/api/windows.media.effects.ibasicvideoeffect.supportedmemorytypes) で指定した値で決まります。

ここでは、ソフトウェア処理を使用した **ProcessFrame** メソッドの簡単な実装例を示します。 [**SoftwareBitmap**](/uwp/api/Windows.Graphics.Imaging.SoftwareBitmap) オブジェクトの操作について詳しくは、「[イメージング](imaging.md)」をご覧ください。 ハードウェア処理を使用した **ProcessFrame** の実装例については、この記事の後半で紹介します。

**SoftwareBitmap** のデータ バッファーにアクセスするには COM 相互運用機能が必要になるため、効果のクラス ファイルに **System.Runtime.InteropServices** 名前空間を含める必要があります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetCOMUsing":::


効果の名前空間に次のコードを追加して、画像のバッファーにアクセスするためのインターフェイスをインポートします。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetCOMImport":::


> [!NOTE]
> この手法では管理対象外のネイティブの画像バッファーにアクセスするため、アンセーフ コードを許可するようにプロジェクトを構成する必要があります。
> 1.  ソリューション エクスプローラーで、VideoEffectComponent プロジェクトを右クリックし、**[プロパティ]** を選択します。
> 2.  **[ビルド]** タブを選択します。
> 3.  [ **アンセーフコードを許可する** ] チェックボックスをオンにします。

 

これで、**ProcessFrame** メソッドの実装を追加できます。 最初に、入力と出力の両方のソフトウェア ビットマップから [**BitmapBuffer**](/uwp/api/Windows.Graphics.Imaging.BitmapBuffer) オブジェクトを取得します。 出力フレームが書き込み用で、入力フレームが読み取り用です。 次に、[**CreateReference**](/uwp/api/windows.graphics.imaging.bitmapbuffer.createreference) を呼び出して、各バッファーの [**IMemoryBufferReference**](/uwp/api/Windows.Foundation.IMemoryBufferReference) を取得します。 その後、実際のデータ バッファーを取得するために、先ほど定義した COM 相互運用機能のインターフェイス (**IMemoryByteAccess**) として **IMemoryBufferReference** オブジェクトをキャストし、**GetBuffer** を呼び出します。

これで、データ バッファーが取得され、入力バッファーからの読み取りと出力バッファーへの書き込みが可能になります。 [**GetPlaneDescription**](/uwp/api/windows.graphics.imaging.bitmapbuffer.getplanedescription) を呼び出して、バッファーのレイアウトを取得します。バッファーの幅、ストライド、初期オフセットについての情報が提供されます。 ピクセルあたりのビット数は、[**SetEncodingProperties**](/uwp/api/windows.media.effects.ibasicvideoeffect.setencodingproperties) メソッドで既に設定したエンコード プロパティで決まります。 バッファーの形式情報を使って、各ピクセルのバッファーへのインデックスを特定します。 ソース バッファーのピクセル値をターゲット バッファーにコピーし、そのカラー値にこの効果の FadeValue プロパティで定義した値を掛けます。これで、指定した値に応じてピクセルが暗くなります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffect.cs" id="SnippetProcessFrameSoftwareBitmap":::


## <a name="implement-the-ibasicvideoeffect-interface-using-hardware-processing"></a>ハードウェア処理を使用した IBasicVideoEffect インターフェイスの実装


カスタムのビデオ特殊効果をハードウェア (GPU) 処理を使って作成する場合も、方法は上記のソフトウェア処理を使った場合とほぼ同じです。 このセクションでは、効果にハードウェア処理を使う場合のいくつかの違いについて説明します。 この例では、Win2D Windows ランタイム API を使います。 Win2D を使う方法について詳しくは、[Win2D のドキュメント](https://microsoft.github.io/Win2D/html/Introduction.htm)をご覧ください。

次の手順に従って、この記事の最初に「**アプリへのカスタム効果の追加**」で作成したプロジェクトに Win2D NuGet パッケージを追加します。

**効果のプロジェクトへの Win2D NuGet パッケージの追加するには**

1.  **ソリューション エクスプローラー**で、**VideoEffectComponent** プロジェクトを右クリックし、**[NuGet パッケージの管理]** をクリックします。
2.  ウィンドウの上部で **[参照]** タブをクリックします。
3.  検索ボックスに **「Win2D」** と入力します。
4.  **[Win2D.uwp]** を選択し、右のウィンドウで **[インストール]** を選択します。
5.  **[変更の確認]** ダイアログに、インストールするパッケージが表示されます。 **[OK]** をクリックします。
6.  パッケージのライセンスに同意します。

基本的なプロジェクトのセットアップに含まれる名前空間に加え、Win2D で提供される次の名前空間を含める必要があります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffectWin2D.cs" id="SnippetUsingWin2D":::


この効果では画像データの操作に GPU メモリを使うため、[**SupportedMemoryTypes**](/uwp/api/windows.media.effects.ibasicvideoeffect.supportedmemorytypes) プロパティで [**MediaMemoryTypes.Gpu**](/uwp/api/Windows.Media.Effects.MediaMemoryTypes) を返します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffectWin2D.cs" id="SnippetSupportedMemoryTypesWin2D":::


効果でサポートするエンコード プロパティを [**SupportedEncodingProperties**](/uwp/api/windows.media.effects.ibasicvideoeffect.supportedencodingproperties) プロパティで設定します。 Win2D を操作するときは、ARGB32 エンコードを使う必要があります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffectWin2D.cs" id="SnippetSupportedEncodingPropertiesWin2D":::


[**SetEncodingProperties**](/uwp/api/windows.graphics.imaging.softwarebitmap.convert) メソッドを使って、メソッドに渡される [**IDirect3DDevice**](/uwp/api/Windows.Graphics.DirectX.Direct3D11.IDirect3DDevice) から新しい Win2D **CanvasDevice** オブジェクトを作成します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffectWin2D.cs" id="SnippetSetEncodingPropertiesWin2D":::


[**SetProperties**](/uwp/api/windows.media.imediaextension.setproperties) の実装は前述のソフトウェア処理の例と同じです。 この例では、**BlurAmount** プロパティを使って Win2D のぼかし効果を設定します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffectWin2D.cs" id="SnippetSetPropertiesWin2D":::

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffectWin2D.cs" id="SnippetBlurAmountWin2D":::


最後に、画像データを実際に処理する [**ProcessFrame**](/uwp/api/windows.media.effects.ibasicvideoeffect.processframe) メソッドを実装します。

Win2D API を使って、入力フレームの [**Direct3DSurface**](/uwp/api/windows.media.videoframe.direct3dsurface) プロパティから **CanvasBitmap** を作成します。 出力フレームの **Direct3DSurface** から **CanvasRenderTarget** を作成し、このレンダー ターゲットから **CanvasDrawingSession** を作成します。 新しい Win2D **GaussianBlurEffect** を初期化し、[**SetProperties**](/uwp/api/windows.media.imediaextension.setproperties) で **BlurAmount** プロパティを使って効果を公開します。 最後に、**CanvasDrawingSession.DrawImage** メソッドを呼び出して、入力ビットマップをレンダー ターゲットにぼかし効果を使って描画します。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffectComponent/ExampleVideoEffectWin2D.cs" id="SnippetProcessFrameWin2D":::


## <a name="adding-your-custom-effect-to-your-app"></a>アプリへのカスタム効果の追加


アプリからビデオ特殊効果を使うには、効果のプロジェクトへの参照をアプリに追加する必要があります。

1.  ソリューション エクスプローラーで、アプリのプロジェクトの下にある **[参照設定]** を右クリックし、**[参照の追加]** を選択します。
2.  **[プロジェクト]** タブを展開し、**[ソリューション]** を選択して、効果のプロジェクトの名前に対応するチェック ボックスをオンにします。 この例では、名前は *VideoEffectComponent*です。
3.  **[OK]** をクリックします。

### <a name="add-your-custom-effect-to-a-camera-video-stream"></a>カメラのビデオ ストリームへのカスタム効果の追加

「[シンプルなカメラ プレビューへのアクセス](simple-camera-preview-access.md)」の手順に従って、カメラからのシンプルなプレビュー ストリームを設定できます。 この手順を実行すると、カメラのビデオ ストリームへのアクセスに使う初期化済みの [**MediaCapture**](/uwp/api/Windows.Media.Capture.MediaCapture) オブジェクトが得られます。

カスタムのビデオ特殊効果をカメラ ストリームに追加するには、まず、新しい [**VideoEffectDefinition**](/uwp/api/Windows.Media.Effects.VideoEffectDefinition) オブジェクトを作成し、効果の名前空間とクラスの名前を渡します。 次に、 **MediaCapture** オブジェクトの [**addvideoeffect**](/uwp/api/windows.media.capture.mediacapture.addvideoeffectasync) メソッドを呼び出して、指定したストリームに効果を追加します。 この例では、[**MediaStreamType.VideoPreview**](/uwp/api/Windows.Media.Capture.MediaStreamType) 値を使って、効果をプレビュー ストリームに追加するように指定します。 アプリがビデオ キャプチャをサポートしている場合は、**MediaStreamType.VideoRecord** を使ってキャプチャ ストリームに効果を追加することもできます。 **AddVideoEffect** から、カスタム効果を表す [**IMediaExtension**](/uwp/api/Windows.Media.IMediaExtension) オブジェクトが返されます。 効果の設定は SetProperties メソッドを使って設定できます。

効果が追加されると、[**StartPreviewAsync**](/uwp/api/windows.media.capture.mediacapture.startpreviewasync) が呼び出されてプレビュー ストリームが始まります。

:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffect_Win10/MainPage.xaml.cs" id="SnippetAddVideoEffectAsync":::



### <a name="add-your-custom-effect-to-a-clip-in-a-mediacomposition"></a>MediaComposition のクリップへのカスタム効果の追加

ビデオ クリップからメディア コンポジションを作成する一般的なガイダンスについては、「[メディア コンポジションと編集](media-compositions-and-editing.md)」をご覧ください。 次のコード スニペットは、カスタムのビデオ特殊効果を使ってシンプルなメディア コンポジションを作成する例を示しています。 [**CreateFromFileAsync**](/uwp/api/windows.media.editing.mediaclip.createfromfileasync) を呼び出して [**MediaClip**](/uwp/api/Windows.Media.Editing.MediaClip) オブジェクトを作成し、ユーザーが [**FileOpenPicker**](/uwp/api/Windows.Storage.Pickers.FileOpenPicker) で選択したビデオ ファイルを渡して新しい [**MediaComposition**](/uwp/api/Windows.Media.Editing.MediaComposition) にクリップを追加します。 次に、新しい [**VideoEffectDefinition**](/uwp/api/Windows.Media.Effects.VideoEffectDefinition) オブジェクトを作成し、効果の名前空間とクラスの名前を渡します。 最後に、**MediaClip** オブジェクトの [**VideoEffectDefinitions**](/uwp/api/windows.media.editing.mediaclip.videoeffectdefinitions) コレクションに効果の定義を追加します。


:::code language="csharp" source="~/../snippets-windows/windows-uwp/audio-video-camera/VideoEffect_Win10/cs/VideoEffect_Win10/MainPage.xaml.cs" id="SnippetAddEffectToComposition":::


## <a name="related-topics"></a>関連トピック
* [シンプルなカメラ プレビューへのアクセス](simple-camera-preview-access.md)
* [メディア コンポジションと編集](media-compositions-and-editing.md)
* [Win2D ドキュメント](https://microsoft.github.io/Win2D/html/Introduction.htm)
* [メディア再生](media-playback.md)
