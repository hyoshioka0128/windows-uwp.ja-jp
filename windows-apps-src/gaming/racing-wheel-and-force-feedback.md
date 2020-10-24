---
title: レーシング ハンドルとフォース フィードバック
description: レーシング ハンドルの検出、機能の特定、読み取り、およびレーシング ハンドルへのフォース フィードバック コマンドの送信には、Windows.Gaming.Input レーシング ハンドル API を使用します。
ms.assetid: 6287D87F-6F2E-4B67-9E82-3D6E51CBAFF9
ms.date: 05/09/2018
ms.topic: article
keywords: Windows 10, UWP, ゲーム, レーシング ハンドル, フォース フィードバック
ms.localizationpriority: medium
ms.openlocfilehash: 0d92fe45a008ee0c3864355faf8133ab8e1ebefb
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89163066"
---
# <a name="racing-wheel-and-force-feedback"></a>レース ホイールとフォース フィードバック

このページでは、ユニバーサル Windows プラットフォーム (UWP) のための、 [Windows のゲームの入出力ホイール][racingwheel] と関連 api を使用した、Xbox One レースホイールのプログラミングの基本について説明します。

ここでは、次の項目について紹介します。

* 接続されているレーシング ハンドルとそのユーザーの一覧を収集する方法
* レーシング ハンドルが追加または削除されたことを検出する方法
* 1 つ以上のレーシング ハンドルの入力を読み取る方法
* フォース フィードバック コマンドを送信する方法
* UI ナビゲーション デバイスとしてのレーシング ハンドルの動作

## <a name="racing-wheel-overview"></a>レーシング ハンドルの概要

レーシング ハンドルは、本物のレースカーのコックピットを模した入力デバイスです。 車やトラックが登場するレーシング ゲームで、アーケード スタイルとシミュレーション スタイルのどちらのゲームにも最適な入力デバイスです。 レーシング ハンドルは、Windows 10 および Xbox One UWP アプリで [Windows.Gaming.Input](/uwp/api/windows.gaming.input) 名前空間によってサポートされています。

Xbox One レーシング ハンドルは、さまざまな価格で提供されています。概して、価格が高いほど、入力とフォース フィードバック機能が優れています。 どのレーシング ハンドルにも、アナログのステアリング ハンドル、アナログのスロットルおよびブレーキのコントロール、ハンドル上のいくつかのボタンを備えています。 一部のレーシング ハンドルには、さらに、アナログのクラッチとハンドブレーキのコントロール、シフト レバー、およびフォース フィードバック機能もあります。 レーシング ハンドルの機能セットはどれも同じではなく、特定の機能のサポート状況も異なる可能性があります &mdash; たとえば、ステアリング ハンドルがサポートする回転の範囲や、シフト レバーがサポートするギア数は異なっている可能性があります。

### <a name="device-capabilities"></a>デバイスの機能

さまざまな Xbox One レース車輪が、オプションのデバイス機能とその機能のさまざまなレベルのサポートを提供しています。単一の種類の入力デバイス間のこのバリエーションレベルは、 [Windows のゲーム](/uwp/api/windows.gaming.input) でサポートされているデバイス間で一意です。 さらに、流通しているほとんどのデバイスでは、少なくともいくつかのオプションの機能またはその他のバリエーションをサポートします。 そのため、接続されている各レーシング ハンドルの機能を個別に特定し、ゲームに適した機能のバリエーションをすべてサポートすることが重要です。

詳しくは、「[レーシング ハンドル機能の特定](#determining-racing-wheel-capabilities)」をご覧ください。

### <a name="force-feedback"></a>フォース フィードバック

一部の Xbox One レーシング ハンドルには、単なるバイブレーションではなく、真のフォース フィードバック &mdash; つまり、ハンドルなどのコントロール軸に実際の力を加えることができます &mdash; が備わっています ゲームはこの機能を利用して、一層の没入感を演出し (_クラッシュ ダメージのシミュレーション_、"道路の感覚")、運転をさらに難しくします。

詳しくは、「[フォース フィードバックの概要](#force-feedback-overview)」をご覧ください。

### <a name="ui-navigation"></a>UI のナビゲーション

ユーザー インターフェイスの操作に異なる入力デバイスをサポートする負担を軽くし、ゲームとデバイス間の整合性を高めるため、ほとんどの物理__ 入力デバイスは、[UI ナビゲーション コントローラー](ui-navigation-controller.md)と呼ばれる個別の論理__ 入力デバイスとして同時に機能します。 UI ナビゲーション コントローラーは、各種入力デバイスに共通の UI ナビゲーション コマンドのボキャブラリを提供します。

デバイスによってアナログ制御をどの程度重視しているかは異なり、レーシング ハンドル間のバリエーションが広いことから、通常は、[ゲームパッド](gamepad-and-vibration.md) と同様の、デジタルの方向パッド、**ビュー**、**メニュー**、**A**、**B**、**X**、および **Y** ボタンが搭載されています。これらのボタンはゲームプレイ コマンドのサポートを意図したものではなく、レーシング ハンドル ボタンとしてすぐに利用できるものではありません。

UI ナビゲーションコントローラーとして、レース車輪は、 [必要な一連](ui-navigation-controller.md#required-set) のナビゲーションコマンドを左スティック、D パッド、 **ビュー**、 **メニュー**、 **a**、 **B** の各ボタンにマップします。

| ナビゲーション コマンド | レーシング ハンドル入力 |
| ------------------:| ------------------ |
|                 上へ | 方向パッドを上           |
|               [下へ] | 方向パッドを下         |
|               Left | 方向パッドを左         |
|              Right | 方向パッドを右        |
|               表示 | 表示ボタン        |
|               メニュー | メニュー ボタン        |
|             承諾 | A ボタン           |
|             キャンセル | B ボタン           |

また、一部のレーシング ハンドルでは、ナビゲーション コマンドの[オプション セット](ui-navigation-controller.md#optional-set)を、サポートする他の入力にマップしますが、コマンドのマッピングはデバイスによって異なる可能性があります。 以下のコマンドもサポートすることを検討してください。ただし、ゲームのインターフェイスのナビゲーションの基本コマンドにはしないでください。

| ナビゲーション コマンド | レーシング ハンドル入力    |
| ------------------:| --------------------- |
|            PageUp | _状況に応じて異なる_              |
|          PageDown | _状況に応じて異なる_              |
|          Page Left | _状況に応じて異なる_              |
|         Page Right | _状況に応じて異なる_              |
|          Scroll Up | _状況に応じて異なる_              |
|        Scroll Down | _状況に応じて異なる_              |
|        Scroll Left | _状況に応じて異なる_              |
|       Scroll Right | _状況に応じて異なる_              |
|          Context 1 | X ボタン (_一般的な場合_) |
|          Context 2 | Y ボタン (_一般的_) |
|          Context 3 | _状況に応じて異なる_              |
|          Context 4 | _状況に応じて異なる_              |

## <a name="detect-and-track-racing-wheels"></a>レーシング ハンドルの検出と追跡

レーシング ハンドルの検出と追跡の方法はゲームパッドの場合とまったく同じですが、[Gamepad](/uwp/api/Windows.Gaming.Input.Gamepad) クラスの代わりに [RacingWheel](/uwp/api/windows.gaming.input.racingwheel) クラスを使用する点だけが異なります。 詳細については、「[ゲームパッドと振動](gamepad-and-vibration.md)」を参照してください。

<!-- Racing wheels are managed by the system, therefore you don't have to create or initialize them. The system provides a list of connected racing wheels and events to notify you when a racing wheel is added or removed.

### The racing wheels list

The [RacingWheel](/uwp/api/windows.gaming.input.racingwheel) class provides a static property, [RacingWheels](/uwp/api/windows.gaming.input.racingwheel.racingwheels#Windows_Gaming_Input_RacingWheel_RacingWheels), which is a read-only list of racing wheels that are currently connected. Because you might only be interested in some of the connected racing wheels, it's recommended that you maintain your own collection instead of accessing them through the `RacingWheels` property.

The following example copies all connected racing wheels into a new collection.
```cpp
auto myRacingWheels = ref new Vector<RacingWheel^>();

for (auto racingwheel : RacingWheel::RacingWheels)
{
    // This code assumes that you're interested in all racing wheels.
    myRacingWheels->Append(racingwheel);
}
```

### Adding and removing racing wheels

When a racing wheel is added or removed the [RacingWheelAdded](/uwp/api/windows.gaming.input.racingwheel.racingwheeladded) and [RacingWheelRemoved](/uwp/api/windows.gaming.input.racingwheel.racingwheelremoved) events are raised. You can register handlers for these events to keep track of the racing wheels that are currently connected.

The following example starts tracking an racing wheels that's been added.
```cpp
RacingWheel::RacingWheelAdded += ref new EventHandler<RacingWheel^>(Platform::Object^, RacingWheel^ args)
{
    // This code assumes that you're interested in all new racing wheels.
    myRacingWheels->Append(args);
}
```

The following example stops tracking a racing wheel that's been removed.
```cpp
RacingWheel::RacingWheelRemoved += ref new EventHandler<RacingWheel^>(Platform::Object^, RacingWheel^ args)
{
    unsigned int indexRemoved;

    if(myRacingWheels->IndexOf(args, &indexRemoved))
    {
        myRacingWheels->RemoveAt(indexRemoved);
    }
}
```

### Users and headsets

Each racing wheel can be associated with a user account to link their identity to their gameplay, and can have a headset attached to facilitate voice chat or in-game features. To learn more about working with users and headsets, see [Tracking users and their devices](input-practices-for-games.md#tracking-users-and-their-devices) and [Headset](headset.md). -->

## <a name="reading-the-racing-wheel"></a>レーシング ハンドルの読み取り

目的のレーシング ハンドルを特定したら、入力を収集する準備は完了です。 ただし、なじみのある一部の他の種類の入力とは違い、レーシング ハンドルはイベントを発生することによって状態の変化を伝えるわけではありません。 代わりに、イベントを_ポーリング_することで現在の状態を定期的に読み取ります。

### <a name="polling-the-racing-wheel"></a>レーシング ハンドルのポーリング

ポーリングでは、明確な時点におけるレーシング ハンドルのスナップショットをキャプチャします。 入力を収集するこのアプローチはほとんどのゲームに最適です。ゲームのロジックはイベント駆動型ではなく、確定的なループの中で実行されることが一般的なためです。また通常は、徐々に集めた多数の単一の入力によるコマンドを解釈するより、一度に集めた入力によるゲーム コマンドを解釈する方が簡単になります。

レーシング ハンドルをポーリングするには、[GetCurrentReading](/uwp/api/windows.gaming.input.racingwheel.getcurrentreading#Windows_Gaming_Input_RacingWheel_GetCurrentReading) を呼び出します。この関数はレーシング ハンドルの状態が格納された [RacingWheelReading](/uwp/api/windows.gaming.input.racingwheelreading) を返します。

次の例では、レーシング ハンドルをポーリングして現在の状態を確認します。

```cpp
auto racingwheel = myRacingWheels[0];

RacingWheelReading reading = racingwheel->GetCurrentReading();
```

読み取りデータには、レーシング ハンドルの状態だけでなく、正確にいつ状態が取得されたかを示すタイムスタンプも含まれます。　 このタイムスタンプは、以前の読み取りのタイミングや、ゲームのシミュレーションのタイミングと関連付けに便利です。

### <a name="determining-racing-wheel-capabilities"></a>レーシング ハンドル機能の特定

レーシング ハンドル コントロールの多くはオプションであるか、必須のコントロールであっても複数のバリエーションをサポートするため、レーシング ハンドルの各読み取りで収集された入力の処理を開始する前に、各レーシング ハンドルの機能を個別に特定する必要があります。

オプションのコントロールは、ハンドブレーキ、クラッチ、およびシフトレバーです。接続されているレーシング ハンドルがこれらのコントロールをサポートするかどうかは、レーシング ハンドルの [HasHandbrake](/uwp/api/windows.gaming.input.racingwheel.hashandbrake#Windows_Gaming_Input_RacingWheel_HasHandbrake)、[HasClutch](/uwp/api/windows.gaming.input.racingwheel.hasclutch#Windows_Gaming_Input_RacingWheel_HasClutch)、および [HasPatternShifter](/uwp/api/windows.gaming.input.racingwheel.haspatternshifter#Windows_Gaming_Input_RacingWheel_HasPatternShifter) プロパティをそれぞれ読み取ることで特定できます。 プロパティの値が **true** の場合、コントロールはサポートされています。そうでない場合は、サポートされません。

```cpp
if (racingwheel->HasHandbrake)
{
    // the handbrake is supported
}

if (racingwheel->HasClutch)
{
    // the clutch is supported
}

if (racingwheel->HasPatternShifter)
{
    // the pattern shifter is supported
}
```

また、ステアリング ハンドルとシフトレバーも、バリエーションがある可能性があるコントロールです。 ステアリング ハンドルでは、実際のハンドルがサポートする物理的な回転の度合いが異なり、シフトレバーでは、各レバーがサポートする前進ギアの数が異なる可能性があります。 レーシング ハンドルの `MaxWheelAngle` プロパティを読み取ることで、実際のハンドルがサポートする回転の最大角度を特定できます。この値は、サポートされる物理的な最大角度を時計回り (正) と反時計回り (負) で表します。 シフトレバーがサポートする最大の前進ギアは、レーシング ハンドルの `MaxPatternShifterGear` プロパティを読み取ることで特定できます。この値は、サポートされる最大の前進ギアを表します。&mdash; つまり、値が 4 の場合、バック ギア、ニュートラル、第 1 ギア、第 2 ギア、第 3 ギア、および第 4 ギアまでサポートされます。

```cpp
auto maxWheelDegrees = racingwheel->MaxWheelAngle;
auto maxShifterGears = racingwheel->MaxPatternShifterGear;
```

また、一部のレーシング ハンドルでは、ステアリング ハンドルを介したフォース フィードバックをサポートします。 接続されているレーシング ハンドルがフォース フィードバックをサポートするかどうかは、レーシング ハンドルの [WheelMotor](/uwp/api/windows.gaming.input.racingwheel.wheelmotor#Windows_Gaming_Input_RacingWheel_WheelMotor) プロパティを読み取ることで特定できます。 が null でない場合は、フォースフィードバックがサポートされます。 `WheelMotor` それ以外の場合はサポートされません。 **null**

```cpp
if (racingwheel->WheelMotor != nullptr)
{
    // force feedback is supported
}
```

フォース フィードバックをサポートするレーシング ハンドルのフォース フィードバック機能の使い方について詳しくは、「[フォース フィードバックの概要](#force-feedback-overview)」をご覧ください。

### <a name="reading-the-buttons"></a>ボタンの読み取り

レーシング ハンドルの各ボタン &mdash; 方向パッドの 4 方向、**前のギア** ボタンと**次のギア** ボタン、その他 16 個のボタン &mdash; は、デジタルの読み取り値によって、押されている (ダウン) か離されている (アップ) かを示します。 効率を高めるため、ボタンの読み取り値は個別のブール値としては表されません。代わりに、読み取り値はすべて、[RacingWheelButtons](/uwp/api/windows.gaming.input.racingwheelbuttons) 列挙型で表される単一のビットフィールドにパックされます。

> [!NOTE]
> レーシング ハンドルには、**ビュー** ボタンや**メニュー** ボタンなど、他にも UI 操作に使用するボタンが搭載されています。 これらのボタンは `RacingWheelButtons` 列挙型には含まれず、UI ナビゲーション デバイスとしてレーシング ハンドルを利用する場合にしか、読み取られません。 詳しくは、「[UI ナビゲーション デバイス](ui-navigation-controller.md)」をご覧ください。

ボタンの値は、[RacingWheelReading](/uwp/api/windows.gaming.input.racingwheelreading) 構造体の `Buttons` プロパティから読み取ります。 このプロパティはビットフィールドであるため、ビット演算子マスクを使用して目的のボタンの値を分離します。 対応するビットが設定されているときはボタンが押されており (ダウン)、それ以外の場合はボタンが離されています (アップ)。

次の例では、**次のギア** ボタンが押されているかどうかを判別します。

```cpp
if (RacingWheelButtons::NextGear == (reading.Buttons & RacingWheelButtons::NextGear))
{
    // Next Gear is pressed
}
```

次の例では、次のギア ボタンが離されているかどうかを判別します。

```cpp
if (RacingWheelButtons::None == (reading.Buttons & RacingWheelButtons::NextGear))
{
    // Next Gear is released (not pressed)
}
```

場合によっては、ボタンが押された状態から離した状態に切り替えるか、または離された状態に切り替わるか、複数のボタンが押されたか離されたか、またはボタンのセットが特定の方法で並べ替えられているかどうかを判断する必要があり &mdash; ます。 これらの状態を検出する方法について詳しくは、「[Detecting button transitions (ボタンの移行の検出)](input-practices-for-games.md#detecting-button-transitions)」および「[Detecting complex button arrangements (複雑なボタンのパターンの検出)](input-practices-for-games.md#detecting-complex-button-arrangements)」をご覧ください。

### <a name="reading-the-wheel"></a>ハンドルの読み取り

ステアリング ハンドルは、-1.0 ～ +1.0 のアナログの読み取り値を提供する必須のコントロールです。 -1.0 の値はハンドルを最も左に回転した位置に対応し、+1.0 の値はハンドルを最も右に回転した位置に対応します。 ステアリング ハンドルの値は、[RacingWheelReading](/uwp/api/windows.gaming.input.racingwheelreading) 構造体の `Wheel` プロパティから読み取ります。

```cpp
float wheel = reading.Wheel;  // returns a value between -1.0 and +1.0.
```

ハンドルの読み取り値は、物理的なレーシング ハンドルがサポートする回転の範囲に応じて異なる実際のハンドルの物理的な回転の角度に対応しますが、通常はハンドルの読み取り値はハンドルに合わせて調整しません。ハンドルのサポートする回転角度が広くなれば、精度も高くなります。

### <a name="reading-the-throttle-and-brake"></a>スロットルとブレーキの読み取り

スロットルとブレーキは、0.0 (完全に離された状態) ～ 1.0 (完全に押された状態) の間の浮動小数点値として表されたアナログ読み取り値をそれぞれ提供する必須のコントロールです。 スロットル コントロールの値は、[RacingWheelReading](/uwp/api/windows.gaming.input.racingwheelreading) 構造体の `Throttle` プロパティから、ブレーキ コントロールの値は `Brake` プロパティから読み取られます。

```cpp
float throttle = reading.Throttle;  // returns a value between 0.0 and 1.0
float brake    = reading.Brake;     // returns a value between 0.0 and 1.0
```

### <a name="reading-the-handbrake-and-clutch"></a>ハンドブレーキとクラッチの読み取り

ハンドブレーキとクラッチは、0.0 (完全に離された状態) ～ 1.0 (完全に押された状態) の間の浮動小数点値として表されたアナログ読み取り値をそれぞれ提供するオプションのコントロールです。 ハンドブレーキ コントロールの値は、[RacingWheelReading](/uwp/api/windows.gaming.input.racingwheelreading) 構造体の `Handbrake` プロパティから、クラッチ コントロールの値は `Clutch` プロパティから読み取られます。

```cpp
float handbrake = 0.0;
float clutch = 0.0;

if(racingwheel->HasHandbrake)
{
    handbrake = reading.Handbrake;  // returns a value between 0.0 and 1.0
}

if(racingwheel->HasClutch)
{
    clutch = reading.Clutch;        // returns a value between 0.0 and 1.0
}
```

### <a name="reading-the-pattern-shifter"></a>シフトレバーの読み取り

シフトレバーは、-1 ～ [MaxPatternShifterGear](/uwp/api/windows.gaming.input.racingwheel.maxpatternshiftergear) の符号付き整数値として表されたデジタルの読み取り値を提供するオプションのコントロールです。 -1 または 0 は_バック_ ギアと _ニュートラル_ ギアにそれぞれ対応し、正の値が大きくなるほど、高いレベルの前進ギアに対応し、最大のギアは **MaxPatternShifterGear** になります。 パターンシフターの値は、 [RacingWheelReading](/uwp/api/windows.gaming.input.racingwheelreading)構造体の[Pattern/fter歯車](/uwp/api/windows.gaming.input.racingwheelreading.patternshiftergear)プロパティから読み取られます。

```cpp
if (racingwheel->HasPatternShifter)
{
    gear = reading.PatternShifterGear;
}
```

> [!NOTE]
> シフトレバーは、サポートされる場合、必須の**前のギア** ボタンと**次のギア** ボタンと併せて存在します。これらのボタンも、プレイヤーの車の現在のギア操作に使用されます。 これらの入力を統合するための簡単な方法は、プレーヤーが車の自動転送を選択したときに、シフター (およびクラッチ) というパターンを無視し、プレーヤーが車の自動車を手動で送信したときに、そのレースが pattern シフターコントロールを備えている場合にのみ、 **前** と **次の歯車** ボタンを無視することです。 この方法がゲームに適さない場合は、別の統合方法を実装できます。

## <a name="run-the-inputinterfacing-sample"></a>InputInterfacing サンプルの実行

[InputInterfacingUWP サンプル _(github)_](https://github.com/Microsoft/Xbox-ATG-Samples/tree/master/Samples/System/InputInterfacingUWP) は、レーシング ハンドルと、種類の異なる入力デバイスとを組み合わせて使用する方法と、これらの入力デバイスが UI ナビゲーション コントローラーとしてどのように動作するかを示します。

## <a name="force-feedback-overview"></a>フォース フィードバックの概要

多くのレーシング ハンドルには、より没入型で、難易度の高いドライブ エクスペリエンスを提供するため、フォース フィードバック機能があります。 フォース フィードバックをサポートするレーシング ハンドルには、通常、単一の軸 (ハンドルの回転軸) に沿ってステアリング ハンドルに力を適用する単一のモーターが搭載されています。 Force フィードバックは、windows 10 および Xbox One の UWP アプリで、 [windows](/uwp/api/windows.gaming.input.forcefeedback) の "名前空間" によってサポートされています。

> [!NOTE]
> フォース フィードバック API は、複数軸のフォースをサポートできますが、現時点では、ハンドルの回転軸以外の軸でフィードバックをサポートしている Xbox One レーシング ハンドルはありません。

## <a name="using-force-feedback"></a>フォース フィードバックの使用

以下のセクションでは、Xbox One レーシング ハンドルのフォース フィードバック効果のプログラミングの基本を説明します。 フィードバックは効果を使用して適用されます。効果は、サウンド効果と同様に、まず、フォース フィードバック デバイスに読み込まれたうえで、開始、一時停止、再開、停止の順で実行できるようになります。ただし、レーシング ハンドルのフィードバック機能を最初に特定する必要があります。

### <a name="determining-force-feedback-capabilities"></a>フォース フィードバック機能の特定

接続されているレーシング ハンドルがフォース フィードバックをサポートするかどうかは、レーシング ハンドルの [WheelMotor](/uwp/api/windows.gaming.input.racingwheel.wheelmotor#Windows_Gaming_Input_RacingWheel_WheelMotor) プロパティを読み取ることで特定できます。 が null の場合、フォースフィードバックはサポートされていません `WheelMotor` 。それ以外の場合は、フォースフィードバックがサポートされており、それが影響を与える可能性のあるエンジンの特定のフィードバック機能を特定することができます。 **null**

```cpp
if (racingwheel->WheelMotor != nullptr)
{
    auto axes = racingwheel->WheelMotor->SupportedAxes;

    if(ForceFeedbackEffectAxes::X == (axes & ForceFeedbackEffectAxes::X))
    {
        // Force can be applied through the X axis
    }

    if(ForceFeedbackEffectAxes::Y == (axes & ForceFeedbackEffectAxes::Y))
    {
        // Force can be applied through the Y axis
    }

    if(ForceFeedbackEffectAxes::Z == (axes & ForceFeedbackEffectAxes::Z))
    {
        // Force can be applied through the Z axis
    }
}
```

### <a name="loading-force-feedback-effects"></a>フォース フィードバック効果の読み込み

フォース フィードバック効果は、ゲームのコマンドに対して自律的に "再生" されるフィードバック デバイスに読み込まれます。 いくつかの基本的な効果があります。カスタム効果は、 [IForceFeedbackEffect](/uwp/api/windows.gaming.input.forcefeedback.iforcefeedbackeffect) インターフェイスを実装するクラスを使用して作成できます。

| Effect クラス         | 効果の説明                                                                     |
| -------------------- | -------------------------------------------------------------------------------------- |
| ConditionForceEffect | デバイス内の現在のセンサーに応じて、異なる力を適用する効果です。 |
| ConstantForceEffect  | 一定の力を特定のベクトルに沿って適用する効果です。                                  |
| PeriodicForceEffect  | 波形によって定義される可変の力を特定のベクトルに沿って適用する効果です。           |
| RampForceEffect      | 線形に増加/減少する力を特定のベクトルに沿って適用する効果です。          |

```cpp
using FFLoadEffectResult = ForceFeedback::ForceFeedbackLoadEffectResult;

auto effect = ref new Windows.Gaming::Input::ForceFeedback::ConstantForceEffect();
auto time = TimeSpan(10000);

effect->SetParameters(Windows::Foundation::Numerics::float3(1.0f, 0.0f, 0.0f), time);

// Here, we assume 'racingwheel' is valid and supports force feedback

IAsyncOperation<FFLoadEffectResult>^ request
    = racingwheel->WheelMotor->LoadEffectAsync(effect);

auto loadEffectTask = Concurrency::create_task(request);

loadEffectTask.then([this](FFLoadEffectResult result)
{
    if (FFLoadEffectResult::Succeeded == result)
    {
        // effect successfully loaded
    }
    else
    {
        // effect failed to load
    }
}).wait();
```

### <a name="using-force-feedback-effects"></a>フォース フィードバック効果の使用

効果は読み込まれると、レーシング ハンドルの `WheelMotor` プロパティで関数を呼び出して同期的にまとめて開始、一時停止、再開、停止を行うことも、フィードバック効果自体で関数を呼び出して個別に行うこともできrます。 通常は、ゲームプレイを開始する前に使用するすべての効果をフィードバック デバイスに読み込んでおき、ゲームプレイの進行に合わせて、それぞれの `SetParameters` 関数を使用して効果を更新することをお勧めします。

```cpp
if (ForceFeedbackEffectState::Running == effect->State)
{
    effect->Stop();
}
else
{
    effect->Start();
}
```

また、必要な場合はいつでも、特定のレーシング ハンドルで、フォース フィードバック システム全体を非同期に有効化、無効化、またはリセットできます。

## <a name="see-also"></a>関連項目

* [Windows.Gaming.Input.UINavigationController](/uwp/api/windows.gaming.input.uinavigationcontroller)
* [Windows.Gaming.Input.IGameController](/uwp/api/windows.gaming.input.igamecontroller)
* [ゲームの入力プラクティス](input-practices-for-games.md)

[Windows.Gaming.Input]: /uwp/api/Windows.Gaming.Input
[Windows.Gaming.Input.UINavigationController]: /uwp/api/Windows.Gaming.Input.UINavigationController
[Windows.Gaming.Input.IGameController]: /uwp/api/Windows.Gaming.Input.IGameController
[racingwheel]: /uwp/api/Windows.Gaming.Input.RacingWheel
[racingwheels]: /uwp/api/Windows.Gaming.Input.RacingWheel
[racingwheeladded]: /uwp/api/Windows.Gaming.Input.RacingWheel
[racingwheelremoved]: /uwp/api/Windows.Gaming.Input.RacingWheel
[haspatternshifter]: /uwp/api/Windows.Gaming.Input.RacingWheel
[hashandbrake]: /uwp/api/Windows.Gaming.Input.RacingWheel
[hasclutch]: /uwp/api/Windows.Gaming.Input.RacingWheel
[maxpatternshiftergear]: /uwp/api/Windows.Gaming.Input.RacingWheel
[maxwheelangle]: /uwp/api/Windows.Gaming.Input.RacingWheel
[getcurrentreading]: /uwp/api/Windows.Gaming.Input.RacingWheel
[wheelmotor]: /uwp/api/Windows.Gaming.Input.RacingWheel
[racingwheelreading]: /uwp/api/Windows.Gaming.Input.RacingWheelReading
[racingwheelbuttons]: /uwp/api/Windows.Gaming.Input.RacingWheelButtons