---
description: ペン、Surface dial、音声など、特定の種類の入力を操作するユニバーサル Windows プラットフォーム (UWP) アプリをカスタマイズする方法について説明します。
title: 入力と操作
keywords: アプリの入力, UWP アプリケーションのカスタマイズ
label: Input and interactions
template: detail.hbs
ms.date: 09/24/2020
ms.topic: article
ms.assetid: b771d452-c3ac-4d97-8482-eaf81bf34306
ms.localizationpriority: medium
ms.openlocfilehash: afaaa13110df78ad68c2cca1200f7c4d8931c4d6
ms.sourcegitcommit: eda7bbe9caa9d61126e11f0f1a98b12183df794d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91220615"
---
# <a name="input-and-interactions"></a>入力と操作

![入力アイコン](../images/inputs-2x.png)

<!-- <div>
  <img src="images/keyboard/keyboard-hero.jpg" alt="" />
  <img src="images/input-interactions/icons-inputdevices03.png" />
</div> -->

UWP アプリは、さまざまな入力を自動的に処理し、さまざまなデバイスで実行できます。たとえばタッチ入力を有効にする場合に、追加の作業は何も必要ありません。 ただし、特定の種類の入力やデバイス用にアプリを最適化することが必要になる場合もあります。 たとえば、ペイント アプリを作成している場合は、必要に応じてペン入力の処理方法をカスタマイズできます。

このセクションの設計とコーディングの手順は、特定の種類の入力用に UWP アプリをカスタマイズする場合に役立ちます。

:::row:::
    :::column:::
        <h3 style="margin-top: 10px; margin-bottom: 0px"><a href="input-primer.md">入力の基本情報</a></h3>
        <p style="margin-top: 0px; margin-bottom: 50px">特定のフォームファクターと組み合わせて使うときの各入力デバイスの種類とその動作、機能、制限事項を把握しておきましょう。</p>
    :::column-end:::
    :::column:::
        <h3 style="margin-top: 10px; margin-bottom: 0px"><a href="gaze-interactions.md">視線入力</a></h3>
        <p style="margin-top: 0px; margin-bottom: 50px">ユーザーの目と手の場所と動きに基づいてユーザーの視線を追跡します。</p>
    :::column-end:::
:::row-end:::

<!-- 
## Input primer

See our <b>[Input primer](index.md)</b> to familiarize yourself with each input device type and its behaviors, capabilities, and limitations when paired with certain form factors. -->

:::row:::
    :::column:::
        <h2 style="margin-top: 10px; margin-bottom: 0px">入力</h2>
        <a href="/windows/uwp/design/input/identify-input-devices">入力デバイスの識別</a><br/>
        <a href="/windows/uwp/design/input/handle-pointer-input">ポインター</a><br/>
        <a href="/windows/uwp/design/input/pen-and-stylus-interactions">ペンと Windows Ink</a><br/>
        <a href="/windows/uwp/design/input/touch-interactions">タッチ</a><br/>
        <a href="/windows/uwp/design/input/mouse-interactions">マウス</a><br/>
        <a href="/windows/uwp/design/input/keyboard-interactions">キーボード</a><br/>
        <a href="/windows/uwp/design/input/gamepad-and-remote-interactions">ゲームパッドとリモコン</a><br/>
        <a href="/windows/uwp/design/input/touchpad-interactions">タッチパッド</a><br/>
        <a href="/windows/uwp/design/input/windows-wheel-interactions">Surface Dial</a><br/>
        <a href="/windows/uwp/design/input/multiple-input-design-guidelines">複数の入力</a><br/>
        <a href="/windows/uwp/design/input/input-injection">入力の挿入</a><br/>
        <a href="/windows/uwp/design/input/custom-text-input">カスタム テキスト入力</a><br/>
    :::column-end:::
    :::column:::
        <h2 style="margin-top: 10px; margin-bottom: 0px">操作</h2>
        <a href="/windows/uwp/design/input/drag-and-drop">ドラッグ アンド ドロップ</a><br/>
        <a href="/windows/uwp/design/input/guidelines-for-panning">パン</a><br/>
        <a href="/windows/uwp/design/input/guidelines-for-rotation">回転</a><br/>
        <a href="/windows/uwp/design/input/guidelines-for-textselection">テキストと画像の選択</a><br/>
        <a href="/windows/uwp/design/input/guidelines-for-targeting">ターゲット設定</a><br/>
        <a href="/windows/uwp/design/input/guidelines-for-visualfeedback">視覚的なフィードバック</a><br/>
    :::column-end:::
    :::column:::
        <h2 style="margin-top: 10px; margin-bottom: 0px">音声と AI</h2>
        <a href="/windows/uwp/design/input/speech-interactions">音声認識</a><br/>
        <a href="/windows/uwp/design/input/cortana-interactions">Cortana</a><br/>
    :::column-end:::
:::row-end:::


<!-- <div class="side-by-side">
<div class="side-by-side-content">
<p>
<b>[Surface Dial](windows-wheel-interactions.md)</b><br/>
Learn how to integrate this brand new category of input device into your Windows apps.</br>
This device is intended as a secondary, multi-modal input device that complements or modifies input from a primary device.
</p>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p>
<b>[Cortana](cortana-interactions.md)</b><br/>
Extend the basic functionality of Cortana with voice commands that launch and execute a single action in an external application.
</p>
</div>
<div class="side-by-side-content-right">
<p>
<b>[Speech](speech-interactions.md)</b><br/>
Integrate speech recognition and text-to-speech (also known as TTS, or speech synthesis) directly into the user experience of your app.
</p>
</div>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p>
<b>[Pen](pen-and-stylus-interactions.md)</b><br/>
Optimize your UWP app for pen input to provide both standard pointer device functionality and the best Windows Ink experience for your users.
</p>
</div>
<div class="side-by-side-content-right">
<p>
<b>[Keyboard](keyboard-interactions.md)</b><br/>
Keyboard input is an important part of the overall user interaction experience for apps. The keyboard is indispensable to people with certain disabilities or users who just consider it a more efficient way to interact with an app.
</p>
</div>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p>
<b>[Touch](touch-interactions.md)</b><br/>
UWP includes a number of different mechanisms for handling touch input, all of which enable you to create an immersive experience that your users can explore with confidence.
</p>
</div>
<div class="side-by-side-content-right">
<p>
<b>[Touchpad](touchpad-interactions.md)</b><br/>
A touchpad combines both indirect multi-touch input with the precision input of a pointing device, such as a mouse. This combination makes the touchpad suited to both a touch-optimized UI and the smaller targets of productivity apps.
</p>
</div>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p>
<b>[Mouse](mouse-interactions.md)</b><br/>
Mouse input is best suited for user interactions that require precision when pointing and clicking. This inherent precision is naturally supported by the UI of Windows, which is optimized for the imprecise nature of touch.
</p>
</div>
<div class="side-by-side-content-right">
<p>
<b>[Gamepad and remote control](gamepad-and-remote-interactions.md)</b><br/>
UWP apps now support gamepad and remote control input. Gamepads and remote controls are the primary input devices for Xbox and TV experiences.
</p>
</div>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<p>
<b>[Multiple inputs](multiple-input-design-guidelines.md)</b><br/>
To accommodate as many users and devices as possible, we recommend that you design your apps to work with as many input types as possible (gesture, speech, touch, touchpad, mouse, and keyboard). Doing so will maximize flexibility, usability, and accessibility.
</p>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p>
<b>[Identify input devices](identify-input-devices.md)</b><br/>
Identify the input devices connected to a Windows app device and identify their capabilities and attributes.
</p>
</div>
<div class="side-by-side-content-right">
<p>
<b>[Handle pointer input](handle-pointer-input.md)</b><br/>
Receive, process, and manage input data from pointing devices, such as touch, mouse, pen/stylus, and touchpad, in Windows apps.
</p>
</div>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p><b>[Custom text input](custom-text-input.md)</b><br/>
The core text APIs in the Windows.UI.Text.Core namespace enable a UWP app to receive text input from any text service supported on Windows devices. This enables the app to receive text in any language and from any input type, like keyboard, speech, or pen.
</p>
</div>
<div class="side-by-side-content-right">
<p>
<b>[Selecting text and images](guidelines-for-textselection.md)</b><br/>
This article describes selecting and manipulating text, images, and controls and provides user experience guidelines that should be considered when using these mechanisms in your apps.
</p>
</div>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<p>
<b>[Panning](guidelines-for-panning.md)</b><br/>
Panning or scrolling lets users navigate within a single view, to display the content of the view that does not fit within the viewport.
</p>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p>
<b>[Optical zoom and resizing](guidelines-for-optical-zoom.md)</b><br/>
This article describes Windows zooming and resizing elements and provides user experience guidelines for using these interaction mechanisms in your apps.
</p>
</div>
<div class="side-by-side-content-right">
<p>
<b>[Rotation](guidelines-for-rotation.md)</b><br/>
This article describes the new Windows UI for rotation and provides user experience guidelines that should be considered when using this new interaction mechanism in your UWP app.
</p>
</div>
</div>
</div>

<div class="side-by-side">
<div class="side-by-side-content">
<div class="side-by-side-content-left">
<p><b>[Targeting](guidelines-for-targeting.md)</b><br/>
Touch targeting in Windows uses the full contact area of each finger that is detected by a touch digitizer. The larger, more complex set of input data reported by the digitizer is used to increase precision when determining the user's intended (or most likely) target.
</p>
</div>
<div class="side-by-side-content-right">
<p><b>[Visual feedback](guidelines-for-visualfeedback.md)</b><br/>
Use visual feedback to show users when their interactions are detected, interpreted, and handled. Visual feedback can help users by encouraging interaction. It indicates the success of an interaction, which improves the user's sense of control. It also relays system status and reduces errors.
</p>
</div>
</div>
</div> -->


