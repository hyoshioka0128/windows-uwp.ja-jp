---
Description: サウンドは、アプリケーションのユーザー エクスペリエンスの完成をサポートし、アプリケーションのオーディオ面の特徴を際立たせます。オーディオは、すべてのプラットフォームで Windows の使い勝手を一致させるために必要なものです。
label: Sound
title: サウンド
template: detail.hbs
ms.assetid: 9fa77494-2525-4491-8f26-dc733b6a18f6
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: kisai
design-contact: mattben
dev-contact: joyate
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: f04d364aac79ed232f35cbdd8378bc50393d2c74
ms.sourcegitcommit: aaa4b898da5869c064097739cf3dc74c29474691
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63789042"
---
# <a name="sound"></a>サウンド

![ヒーロー イメージ](images/header-sound.svg)

サウンドを使ってアプリを向上させるには、さまざまな方法があります。 ユーザーがイベントを音声で認識できるように、サウンドを使って他の UI 要素を補完できます。 視覚障碍のあるユーザーにとって、サウンドは効果的なユーザー インターフェイスの要素となる可能性があります。 サウンドを使ってユーザーを釘づけにするような雰囲気を作ることができます。たとえば、パズル ゲームのバックグラウンドで風変わりなサウンドトラックを再生したり、ホラー ゲームやサバイバル ゲームで不気味なサウンド効果を使う可能性があります。

## <a name="sound-global-api"></a>サウンドのグローバル API

UWP には使いやすいサウンド システムが用意されていて、「スイッチを切り替える」だけで、アプリ全体にイマーシブなオーディオ エクスペリエンスを実装することができます。

[  **ElementSoundPlayer**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.elementsoundplayer) は、XAML 内の統合的なサウンド システムで、オンにすると、すべての既定のコントロールで自動的にサウンドが再生されます。
```C#
ElementSoundPlayer.State = ElementSoundPlayerState.On;
```
**ElementSoundPlayer** には、次の 3 つの異なる状態があります: **On**、**Off**、**Auto**。

**Off** に設定すると、アプリの実行環境に関わらず、サウンドが再生されることはありません。 **On** に設定すると、すべてのプラットフォームで、アプリのサウンドが再生されます。

ElementSoundPlayer を有効にすると、空間オーディオ (3D サウンド) も自動的に有効になります。 サウンドをオンにしたまま 3D サウンドを無効にするには、ElementSoundPlayer の **SpatialAudioMode** を無効にします。 

```C#
ElementSoundPlayer.SpatialAudioMode = ElementSpatialAudioMode.Off
```

**SpatialAudioMode** プロパティの有効な値は以下のとおりです。 
- **自動**:サウンドがオンのときに、空間オーディオがオンになります。 
- **Off**: サウンドがオンでも、空間オーディオは常にオフです。
- **[オン]** :空間オーディオが常に再生されます。

空間オーディオと XAML による空間オーディオの処理方法について詳しくは、[「オーディオ グラフ」の「空間オーディオ」](/windows/uwp/audio-video-camera/audio-graphs#spatial-audio)をご覧ください。

### <a name="sound-for-tv-and-xbox"></a>テレビや Xbox のサウンド

サウンドは 10 フィート エクスペリエンスの重要なパーツであるため、既定では、**ElementSoundPlayer** の状態は **Auto**、つまり、アプリが Xbox で実行されているときにのみサウンドが再生されます。
Xbox やテレビ向けの設計について詳しくは、「[Xbox およびテレビ向け設計](https://go.microsoft.com/fwlink/?LinkId=760736)」の記事をご覧ください。

## <a name="sound-volume-override"></a>音量設定のオーバーライド

アプリ内のすべてのサウンドは、**Volume** コントロールで小さくすることができます。 しかし、アプリ内のサウンドを*システムの音量より大きく*することができません。

アプリの音量レベルを設定するには、次のように呼び出します。
```C#
ElementSoundPlayer.Volume = 0.5;
```
ここで、最大の音量はシステムの音量に相対的に1.0、最小は 0.0 (本質的にサイレント)です。

## <a name="control-level-state"></a>コントロール レベルの状態

コントロールの既定のサウンドが望ましくない場合は、これを無効にできます。 サウンドを無効にするには、コントロールで **ElementSoundMode** を使います。

**ElementSoundMode** には、次の 2 つの状態があります: **Off** と **Default**。 設定しないと、**Default** になります。 **Off** に設定すると、コントロールが再生するすべてのサウンドはミュートされます (*フォーカスを除く*)。

```XAML
<Button Name="ButtonName" Content="More Info" ElementSoundMode="Off"/>
```

```C#
ButtonName.ElementSoundState = ElementSoundMode.Off;
```

## <a name="is-this-the-right-sound"></a>適切なサウンドの選択

カスタム コントロールを作成したり、既にあるコントロールのサウンドを変更したりするときには、システムが提供するすべてのサウンドの使用法を理解することが重要です。

各サウンドは特定の基本的なユーザー操作に関連付けられています。すべての対話式操作で再生するサウンドをカスタマイズできますが、このセクションでは、すべての UWP アプリで一貫したエクスペリエンスを維持するためにサウンドを使う必要がある、というシナリオを説明します。

### <a name="invoking-an-element"></a>要素の呼び出し

現在のシステムで最も一般的な、コントロールにトリガーされるサウンドは、**Invoke** サウンドです。 このサウンドは、ユーザーがタップ、クリック、入力、スペース、または、ゲームパッドの [A] ボタンを押すことでコントロールを呼び出したときに、再生されます。

通常このサウンドは、ユーザーが[入力デバイス](../input/index.md)を介して明示的に単純なコントロールまたはコントロールの一部を対象としたときにのみ再生されます。

<SelectButtonClick.mp3 サウンド クリップ>

任意のコントロール イベントからこのサウンドを再生するには、シンプルに **ElementSoundPlayer** から Play メソッドを呼び出し、**ElementSound.Invoke** に渡します。
```C#
ElementSoundPlayer.Play(ElementSoundKind.Invoke);
```

### <a name="showing--hiding-content"></a>コンテンツの表示と非表示

XAML には多くのポップアップやダイアログ、閉じることができる UI があり、これらのオーバーレイのいずれかをトリガーするすべての操作で **Show** または **Hide** サウンドを呼び出す必要があります、

オーバーレイのコンテンツ ウィンドウをビューに読み込むときに、**Show** サウンドを呼び出す必要があります。

<OverlayIn.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.Show);
```
逆に、オーバーレイのコンテンツ ウィンドウを閉じる (または簡易非表示にする) ときに、**Hide** サウンドを呼び出す必要があります。

<OverlayOut.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.Hide);
```
### <a name="navigation-within-a-page"></a>ページ内でのナビゲーション

アプリのページ内でパネルまたはビューの間を移動する場合 ([タブとピボット](../controls-and-patterns/pivot.md)に関するページを参照してください)、通常は双方向の移動になります。 つまり、現在表示しているアプリのページを離れずに、次のビュー/パネルまたは前のビュー/パネルに移動できます。

このナビゲーションの概念に関するオーディオ エクスペリエンスは、**MovePrevious** サウンドと **MoveNext** サウンドに包含されています。

リストの*次の項目*と考えられるビュー/パネルに移動するときは、次のように呼び出します。

<PageTransitionRight.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.MoveNext);
```
リストの*前の項目*と考えられるビュー/パネルに移動するときは、次のように呼び出します。

<PageTransitionLeft.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.MovePrevious);
```
### <a name="back-navigation"></a>戻るナビゲーション

アプリ内で現在のページから前のページにナビゲーションするときは、**GoBack** サウンドを呼び出す必要があります。

<BackButtonClick.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.GoBack);
```
### <a name="focusing-on-an-element"></a>要素へのフォーカス

マイクロソフトのシステムの **Focus** サウンドは、唯一の暗黙的なサウンドです。 つまり、ユーザーは、何かを直接操作していなくてもサウンドが聞こえます。

フォーカスは、ユーザーがアプリをナビゲーションしたときに、ゲームパッド、キーボード、リモート、キネクトのいずれかで起こります。 通常、**Focus** サウンドは、*PointerEntered またはマウス ホバー イベント時には再生されません*。

コントロールがフォーカスされたときに **Focus** サウンドを再生するように設定するには、次のように呼び出します。

<ElementFocus1.mp3 サウンド クリップ>

```C#
ElementSoundPlayer.Play(ElementSoundKind.Focus);
```
### <a name="cycling-focus-sounds"></a>フォーカス サウンドの循環

**ElementSound.Focus** 呼び出しの追加機能として、サウンド システムは、既定で、ナビゲーション トリガーごとに 4 つの異なるサウンドを循環させます。 つまり、2 つの同じフォーカス サウンドが前後して再生されることはありません。

この循環機能の目的は、フォーカス サウンドが単調になることを防ぎ、ユーザーの注意をひかない状態を保つことです。フォーカス サウンドは、最もよく再生されるため、最も繊細なサウンドにする必要があります。

## <a name="related-articles"></a>関連記事

* [Xbox およびテレビ向け設計](https://go.microsoft.com/fwlink/?LinkId=760736)
* [ElementSoundPlayer クラスのドキュメント](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.elementsoundplayer)
