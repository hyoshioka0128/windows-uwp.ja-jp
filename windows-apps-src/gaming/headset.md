---
title: Headset
description: Windows.Gaming.Input ヘッドセット API を使用して、ヘッドセットの検出、プレイヤーの音声のキャプチャ、オーディオの再生を行います。
ms.assetid: 021CCA26-D339-4C8B-B084-0D499BD83ABE
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, ヘッドセット
ms.localizationpriority: medium
ms.openlocfilehash: 5e5b0894dbab03490cb74bdae8c231b57d397cb4
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89175296"
---
# <a name="headset"></a>Headset

このページでは、[Windows.Gaming.Input.Headset][headset] とユニバーサル Windows プラットフォーム (UWP) 用の関連 API を使った、ヘッドセットを対象にしたプログラミングの基礎について説明します。

ここでは、次の項目について紹介します。
* 入力デバイスまたはナビゲーション デバイスに接続されているヘッドセットにアクセスする方法
* ヘッドセットが接続されている、またはヘッドセットが切断されていることを検出する方法


## <a name="headset-overview"></a>ヘッドセットの概要

ヘッドセットはオーディオのキャプチャと再生を行うデバイスで、オンライン ゲームで他のプレイヤーと通信するために使用することが多く、ゲームプレイや他の創作活動で使用することもできます。 ヘッドセットは、Windows 10 および Xbox UWP アプリで [Windows.Gaming.Input][] 名前空間によってサポートされています。


## <a name="detect-and-track-headsets"></a>ヘッドセットの検出と追跡

ヘッドセットはシステムによって管理されるため、ヘッドセットを自分で作成したり初期化する必要はありません。 システムによって、ヘッドセットが接続されている入力デバイスを通じてヘッドセットへのアクセスが提供され、ヘッドセットが接続または切断されたときにはイベントが通知されます。

### <a name="igamecontrollerheadset"></a>IGameController.Headset

[Windows.Gaming.Input][] 名前空間のすべての入力デバイスでは、[IGameController][] インターフェイスが実装されます。このインターフェイスでは、現在デバイスに接続されているヘッドセットとなるように [Headset][igamecontroller.headset] プロパティを定義します。

### <a name="connecting-and-disconnecting-headsets"></a>ヘッドセットの接続と切断

ヘッドセットを接続または切断すると、[HeadsetConnected][igamecontroller.headsetconnected] および [HeadsetDisconnected][igamecontroller.headsetdisconnected] イベントが発生します。 入力デバイスに現在ヘッドセットが接続されているかどうかを追跡するため、これらのイベントのハンドラーを登録できます。

次の例は、`HeadsetConnected` イベントのハンドラーを登録する方法を示しています。

```cpp
auto inputDevice = myGamepads[0]; // or arcade stick, racing wheel

inputDevice.HeadsetConnected += ref new TypedEventHandler<IGameController^, Headset^>(IGameController^ device, Headset^ headset)
{
    // enable headset capture and playback on this device
}
```

次の例は、`HeadsetDisconnected` イベントのハンドラーを登録する方法を示しています。

```cpp
auto inputDevice = myGamepads[0]; // or arcade stick, racing wheel

inputDevice.HeadsetDisconnected += ref new TypedEventHandler<IGameController^, Headset^>(IGameController^ device, Headset^ headset)
{
    // disable headset capture and playback on this device
}
```

## <a name="using-the-headset"></a>ヘッドセットの使用

[Headset][] クラスは、XAudio エンドポイント ID を表す 2 つの文字列で構成されています。1 つはオーディオ キャプチャ (ヘッドセット マイクからの録音) 用の文字列で、もう 1 つはオーディオ レンダリング (ヘッドセットのイヤホンを使用した再生) 用の文字列です。

ここでは XAudio の使用の詳細については説明しませんが、詳しくは、[XAudio2 プログラミング ガイド](/windows/desktop/xaudio2/programming-guide)や [XAudio2 API リファレンス](/windows/desktop/xaudio2/programming-reference)をご覧ください。


[Windows. ゲーム. 入力]: /uwp/api/Windows.Gaming.Input
[igamecontroller]: /uwp/api/Windows.Gaming.Input.IGameController
[igamecontroller.headset]: /uwp/api/Windows.Gaming.Input.IGameController
[igamecontroller.headsetconnected]: /uwp/api/Windows.Gaming.Input.IGameController
[igamecontroller.headsetdisconnected]: /uwp/api/Windows.Gaming.Input.IGameController
[ヘッドフォン]: /uwp/api/Windows.Gaming.Input.Headset