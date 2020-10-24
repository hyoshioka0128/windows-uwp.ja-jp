---
title: ゲームパッドと振動
description: ゲームパッドの検出、読み取り、およびゲームパッドへの振動とリアル コマンドの送信には、Windows.Gaming.Input ゲームパッド API を使用します。
ms.assetid: BB03BB8E-255F-4AE8-AC43-1E519CA860FE
ms.date: 09/06/2018
ms.topic: article
keywords: Windows 10, UWP, ゲーム, ゲームパッド, 振動
ms.localizationpriority: medium
ms.openlocfilehash: 66844b78893ffa8cb92b6b17bd11d87c1d4b1aa0
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89175326"
---
# <a name="gamepad-and-vibration"></a>ゲームパッドと振動

このページでは、[Windows.Gaming.Input.Gamepad][gamepad] とユニバーサル Windows プラットフォーム (UWP) 用の関連 API を使った、Xbox One ゲームパッドを対象にしたプログラミングの基礎について説明します。

ここでは、次の項目について紹介します。

* 接続されているゲームパッドとそのユーザーの一覧を収集する方法
* ゲームパッドが追加または削除されたことを検出する方法
* 1 つ以上のゲームパッドの入力を読み取る方法
* 振動とリアル コマンドを送信する方法
* ゲームパッドが UI ナビゲーションデバイスとして動作するしくみ

## <a name="gamepad-overview"></a>ゲームパッドの概要

Xbox ワイヤレス コントローラーや Xbox ワイヤレス コントローラー S などのゲームパッドは、汎用のゲーム入力デバイスです。 ゲームパッドは Xbox One の標準入力デバイスです。一般的に、キーボードやマウスを好まない Windows のゲーマーが選びます。 ゲームパッドは、Windows 10 および Xbox UWP アプリで [Windows.Gaming.Input][] 名前空間によってサポートされています。

Xbox One ゲームパッドには、方向パッド (または D パッド) が搭載されています。 **A**、 **B**、 **X**、 **Y**、 **ビュー**、および **メニュー** ボタン左および右の thumbsticks、バンパー、およびトリガー合計4つの振動モーター。 どちらのサムスティックも、X 軸と Y 軸のデュアル アナログの読み取り値を提供し、内側に押すとボタンとしても機能します。 各トリガーは、どれだけの距離を示すアナログ読み取りを提供します。

<!-- > [!NOTE]
> The Xbox Elite Wireless Controller is equipped with four additional **Paddle** buttons on its underside. These can be used to provide redundant access to game commands that are difficult to use together (such as the right thumbstick together with any of the **A**, **B**, **X**, or **Y** buttons) or to provide dedicated access to additional commands. -->

> [!NOTE]
> `Windows.Gaming.Input.Gamepad` では、Xbox 360 ゲームパッドもサポートされています。これには、標準 Xbox 1 ゲームパッドと同じコントロールレイアウトがあります。

### <a name="vibration-and-impulse-triggers"></a>振動とリアル トリガー

Xbox One ゲームパッドには、強弱のゲームパッドの振動を生むための独立した 2 つのモーターと、トリガーごとに鋭い振動を生む 2 つの専用のモーターがあります (この独自の機能のために、Xbox One ゲームパッドのトリガーは_リアル トリガー_と呼ばれています)。

> [!NOTE]
> Xbox 360 ゲームパッドには、 _インパルストリガー_が搭載されていません。

詳しくは、「[振動とリアル トリガーの概要](#vibration-and-impulse-triggers-overview)」をご覧ください。

### <a name="thumbstick-deadzones"></a>サムスティックのデッドゾーン

中央の位置で待機中のサムスティックは、常に安定してニュートラルな X 軸と Y 軸の読み取り値を生成することが理想的ですが、 機械的な力とサムスティックの感度のために、中央の位置での実際の読み取り値は、理想的なニュートラルの値の近似値でしかなく、読み取りごとに異なる可能性があります。 このため、 _deadzone_ &mdash; 製造の &mdash; 違い、機械的な磨耗、またはその他のゲームパッドの問題を補正するために無視される、理想的な中心位置の近くにある小さな deadzone の値を常に使用する必要があります。

デッドゾーンを大きくすることは、意図する入力と意図しない入力とを分ける簡単な方法です。

詳しくは、「[サムスティックの読み取り](#reading-the-thumbsticks)」をご覧ください。

### <a name="ui-navigation"></a>UI のナビゲーション

ユーザー インターフェイスの操作に異なる入力デバイスをサポートする負担を軽くし、ゲームとデバイス間の整合性を高めるため、ほとんどの物理__ 入力デバイスは、[UI ナビゲーション コントローラー](ui-navigation-controller.md)と呼ばれる個別の論理__ 入力デバイスとして同時に機能します。 UI ナビゲーション コントローラーは、各種入力デバイスに共通の UI ナビゲーション コマンドのボキャブラリを提供します。

UI ナビゲーションコントローラーとして、ゲームパッドは、 [必要な一連](ui-navigation-controller.md#required-set) のナビゲーションコマンドを左スティック、D パッド、 **ビュー**、 **メニュー**、 **a**、 **B** の各ボタンにマップします。

| ナビゲーション コマンド | ゲームパッド入力                       |
| ------------------:| ----------------------------------- |
|                 上へ | 左スティックを上/方向パッドを上       |
|               [下へ] | 左スティックを下/方向パッドを下   |
|               Left | 左スティックを左/方向パッドを左   |
|              Right | 左スティックを右/方向パッドを右 |
|               表示 | 表示ボタン                         |
|               メニュー | メニュー ボタン                         |
|             承諾 | A ボタン                            |
|             キャンセル | B ボタン                            |

また、ゲームパッドはナビゲーション コマンドのすべての[オプション セット](ui-navigation-controller.md#optional-set)をその他の入力にマップします。

| ナビゲーション コマンド | ゲームパッド入力          |
| ------------------:| ---------------------- |
|            PageUp | 左トリガー           |
|          PageDown | 右トリガー          |
|          Page Left | L ボタン            |
|         Page Right | R ボタン           |
|          Scroll Up | 右スティックを上    |
|        Scroll Down | 右スティックを下  |
|        Scroll Left | 右スティックを左  |
|       Scroll Right | 右スティックを右 |
|          Context 1 | X ボタン               |
|          Context 2 | Y ボタン               |
|          Context 3 | 左スティックを押す  |
|          Context 4 | 右スティックを押す |

## <a name="detect-and-track-gamepads"></a>ゲームパッドの検出と追跡

ゲームパッドはシステムによって管理されるため、ゲームパッドを自分で作成したり初期化する必要はありません。 接続されているゲームパッドとイベントの一覧はシステムによって提供され、ゲームパッドが追加または削除されると通知されます。

### <a name="the-gamepads-list"></a>ゲームパッドの一覧

[Gamepad][] クラスには静的プロパティである [Gamepad][] が用意されています。これは、現在接続されているゲームパッドの読み取り専用リストです。 接続されているゲームパッドの一部にのみ関心があるため、プロパティを使用してアクセスするのではなく、独自のコレクションを維持することをお勧めし `Gamepads` ます。

次の例では、接続されているすべてのゲームパッドを新しいコレクションにコピーします。 バックグラウンドの他のスレッドがこのコレクションにアクセスすることに注意してください。これは、(ユーザーが [追加][] した、または作成した [padpad)][] イベントで、コレクションを読み込んだ、または更新するコードをロックする必要があることに注意してください。

```cpp
auto myGamepads = ref new Vector<Gamepad^>();
critical_section myLock{};

for (auto gamepad : Gamepad::Gamepads)
{
    // Check if the gamepad is already in myGamepads; if it isn't, add it.
    critical_section::scoped_lock lock{ myLock };
    auto it = std::find(begin(myGamepads), end(myGamepads), gamepad);

    if (it == end(myGamepads))
    {
        // This code assumes that you're interested in all gamepads.
        myGamepads->Append(gamepad);
    }
}
```

```cs
private readonly object myLock = new object();
private List<Gamepad> myGamepads = new List<Gamepad>();
private Gamepad mainGamepad;

private void GetGamepads()
{
    lock (myLock)
    {
        foreach (var gamepad in Gamepad.Gamepads)
        {
            // Check if the gamepad is already in myGamepads; if it isn't, add it.
            bool gamepadInList = myGamepads.Contains(gamepad);

            if (!gamepadInList)
            {
                // This code assumes that you're interested in all gamepads.
                myGamepads.Add(gamepad);
            }
        }
    }   
}
```

### <a name="adding-and-removing-gamepads"></a>ゲームパッドの追加と削除

ゲームパッドが追加または削除さ[れると][]、そのイベントが発生した場合は[、そのイベント][]が発生します。 これらのイベントハンドラーを登録することで、現在接続されているゲームパッドを追跡できます。

次の例では、追加されたゲームパッドの追跡を開始します。

```cpp
Gamepad::GamepadAdded += ref new EventHandler<Gamepad^>(Platform::Object^, Gamepad^ args)
{
    // Check if the just-added gamepad is already in myGamepads; if it isn't, add
    // it.
    critical_section::scoped_lock lock{ myLock };
    auto it = std::find(begin(myGamepads), end(myGamepads), args);

    if (it == end(myGamepads))
    {
        // This code assumes that you're interested in all new gamepads.
        myGamepads->Append(args);
    }
}
```

```cs
Gamepad.GamepadAdded += (object sender, Gamepad e) =>
{
    // Check if the just-added gamepad is already in myGamepads; if it isn't, add
    // it.
    lock (myLock)
    {
        bool gamepadInList = myGamepads.Contains(e);

        if (!gamepadInList)
        {
            myGamepads.Add(e);
        }
    }
};
```

次の例では、削除されたゲームパッドの追跡を停止します。 また、削除されたときに追跡しているゲームパッドの動作を処理する必要もあります。たとえば、このコードでは、1つのゲームパッドからの入力のみを追跡し、 `nullptr` 削除されたときにに設定するだけです。 ゲームパッドがアクティブになっている場合はすべてのフレームをチェックし、コントローラーが接続されていないときに入力を収集しているゲームパッドを更新する必要があります。

```cpp
Gamepad::GamepadRemoved += ref new EventHandler<Gamepad^>(Platform::Object^, Gamepad^ args)
{
    unsigned int indexRemoved;
    critical_section::scoped_lock lock{ myLock };

    if(myGamepads->IndexOf(args, &indexRemoved))
    {
        if (m_gamepad == myGamepads->GetAt(indexRemoved))
        {
            m_gamepad = nullptr;
        }

        myGamepads->RemoveAt(indexRemoved);
    }
}
```

```cs
Gamepad.GamepadRemoved += (object sender, Gamepad e) =>
{
    lock (myLock)
    {
        int indexRemoved = myGamepads.IndexOf(e);

        if (indexRemoved > -1)
        {
            if (mainGamepad == myGamepads[indexRemoved])
            {
                mainGamepad = null;
            }

            myGamepads.RemoveAt(indexRemoved);
        }
    }
};
```

詳細については、「 [ゲームの入力方法](input-practices-for-games.md) 」を参照してください。

### <a name="users-and-headsets"></a>ユーザーとヘッドセット

各ゲームパッドは、ユーザー アカウントと関連付けることでユーザーの ID をユーザーのゲームプレイにリンクできます。また、ボイス チャットやゲーム内機能を円滑化するためにヘッドセットをアタッチすることもできます。 ユーザーとの連携およびヘッドセット操作について詳しくは、[ユーザーおよびそのデバイスの追跡](input-practices-for-games.md#tracking-users-and-their-devices)と、[ヘッドセット](headset.md)に関するページをご覧ください。

## <a name="reading-the-gamepad"></a>ゲームパッドの読み取り

目的のゲームパッドを特定したら、入力を収集する準備は完了です。 ただし、なじみのある一部の他の種類の入力とは違い、ゲームパッドはイベントを発生することによって状態の変化を伝えるわけではありません。 代わりに、イベントを_ポーリング_することで現在の状態を定期的に読み取ります。

### <a name="polling-the-gamepad"></a>ゲームパッドのポーリング

ポーリングでは、明確な時点におけるナビゲーション デバイスのスナップショットをキャプチャします。 入力を収集するこのアプローチはほとんどのゲームに最適です。ゲームのロジックはイベント駆動型ではなく、確定的なループの中で実行されることが一般的なためです。また通常は、徐々に集めた多数の単一の入力によるコマンドを解釈するより、一度に集めた入力によるゲーム コマンドを解釈する方が簡単になります。

ゲームパッドをポーリングするには、[GetCurrentReading][] を呼び出します。この関数はゲームパッドの状態が格納された [GamepadReading][] を返します。

次の例では、ゲームパッドをポーリングして現在の状態を確認します。

```cpp
auto gamepad = myGamepads[0];

GamepadReading reading = gamepad->GetCurrentReading();
```

```cs
Gamepad gamepad = myGamepads[0];

GamepadReading reading = gamepad.GetCurrentReading();
```

読み取りデータには、ゲームパッドの状態だけでなく、正確にいつ状態が取得されたかを示すタイムスタンプも含まれます。　 このタイムスタンプは、以前の読み取りのタイミングや、ゲームのシミュレーションのタイミングと関連付けに便利です。

### <a name="reading-the-thumbsticks"></a>サムスティックの読み取り

各サムスティックは、X 軸と Y 軸で -1.0 ～ +1.0 のアナログの読み取り値を提供します。 X 軸では、-1.0 の値はサムスティックを最も左に移動した位置に対応し、+1.0 の値はサムスティックを最も右に移動した位置に対応します。 Y 軸では、-1.0 の値はサムスティックを最も下に移動した位置に対応し、+1.0 の値はサムスティックを最も上に移動した位置に対応します。 どちらの軸でも、スティックが中央の位置にある場合、値は約0.0 ですが、後続の読み取りの間でも正確な値は変化します。このバリエーションを緩和するための戦略については、このセクションの後半で説明します。

左のサムスティックの X 軸の値は、[GamepadReading][] 構造体の `LeftThumbstickX` プロパティから読み取られ、Y 軸の値は `LeftThumbstickY` プロパティから読み取られます。 右のサムスティックの X 軸の値は、`RightThumbstickX` プロパティから読み取られ、Y 軸の値は `RightThumbstickY` プロパティから読み取られます。

```cpp
float leftStickX = reading.LeftThumbstickX;   // returns a value between -1.0 and +1.0
float leftStickY = reading.LeftThumbstickY;   // returns a value between -1.0 and +1.0
float rightStickX = reading.RightThumbstickX; // returns a value between -1.0 and +1.0
float rightStickY = reading.RightThumbstickY; // returns a value between -1.0 and +1.0
```

```cs
double leftStickX = reading.LeftThumbstickX;   // returns a value between -1.0 and +1.0
double leftStickY = reading.LeftThumbstickY;   // returns a value between -1.0 and +1.0
double rightStickX = reading.RightThumbstickX; // returns a value between -1.0 and +1.0
double rightStickY = reading.RightThumbstickY; // returns a value between -1.0 and +1.0
```

サムスティックの値を読み取るとき、中央の位置で待機中のサムスティックの値は、一定してニュートラルの 0.0 にはなりません。サムスティックを動かし、中央の位置に戻るたびに、0.0 に近い値が生成されます。 このばらつきを少なくするために、小さな_デッドゾーン_を実装します。デッドゾーン+は、理想の中央の位置付近の、無視される範囲の値です。 デッドゾーンを実装する方法の 1 つは、サムスティックが中央から移動された距離を特定し、読み取り値が指定した距離以下の場合は無視することです。 &mdash;サムスティックの読み取りは、ピタゴラス定理を使用するだけで、平面ではなく極座標であるため、正確ではない距離を計算でき &mdash; ます。 これで、放射状のデッドゾーンが作られます。

次の例は、ピタゴラスの定理を使った基本的な放射状のデッドゾーンを示しています。

```cpp
float leftStickX = reading.LeftThumbstickX;   // returns a value between -1.0 and +1.0
float leftStickY = reading.LeftThumbstickY;   // returns a value between -1.0 and +1.0

// choose a deadzone -- readings inside this radius are ignored.
const float deadzoneRadius = 0.1;
const float deadzoneSquared = deadzoneRadius * deadzoneRadius;

// Pythagorean theorem -- for a right triangle, hypotenuse^2 = (opposite side)^2 + (adjacent side)^2
auto oppositeSquared = leftStickY * leftStickY;
auto adjacentSquared = leftStickX * leftStickX;

// accept and process input if true; otherwise, reject and ignore it.
if ((oppositeSquared + adjacentSquared) > deadzoneSquared)
{
    // input accepted, process it
}
```

```cs
double leftStickX = reading.LeftThumbstickX;   // returns a value between -1.0 and +1.0
double leftStickY = reading.LeftThumbstickY;   // returns a value between -1.0 and +1.0

// choose a deadzone -- readings inside this radius are ignored.
const double deadzoneRadius = 0.1;
const double deadzoneSquared = deadzoneRadius * deadzoneRadius;

// Pythagorean theorem -- for a right triangle, hypotenuse^2 = (opposite side)^2 + (adjacent side)^2
double oppositeSquared = leftStickY * leftStickY;
double adjacentSquared = leftStickX * leftStickX;

// accept and process input if true; otherwise, reject and ignore it.
if ((oppositeSquared + adjacentSquared) > deadzoneSquared)
{
    // input accepted, process it
}
```

各サムスティックは、内側に押すことでボタンとしても機能します。この入力の読み取りの詳細については、「[ボタンの読み取り](#reading-the-buttons)」をご覧ください。

### <a name="reading-the-triggers"></a>トリガーの読み取り

トリガーは、0.0 (完全に離された状態) ～ 1.0 (完全に押された状態) の浮動小数点値として表されます。 左のトリガーの値は、[GamepadReading][] 構造体の `LeftTrigger` プロパティから、右のトリガーの値は `RightTrigger` プロパティから読み取られます。

```cpp
float leftTrigger  = reading.LeftTrigger;  // returns a value between 0.0 and 1.0
float rightTrigger = reading.RightTrigger; // returns a value between 0.0 and 1.0
```

```cs
double leftTrigger = reading.LeftTrigger;  // returns a value between 0.0 and 1.0
double rightTrigger = reading.RightTrigger; // returns a value between 0.0 and 1.0
```

### <a name="reading-the-buttons"></a>ボタンの読み取り

各ゲームパッドボタンは &mdash; 、D パッド、左と右の2つの方向、左と右のサムスティックの押下、 **A**、 **B**、 **X**、 **Y**、**ビュー**、および**メニュー**によって、押されている (下にある &mdash; ) か、または離された (上に) かを示すデジタル読み取りが提供されます。 効率を上げるために、ボタンの読み取りは個々のブール値として表されません。これらはすべて、ビットフィールド [Padbuttons][] 列挙体によって表される1つのにパックされています。

<!-- > [!NOTE]
> The Xbox Elite Wireless Controller is equipped with four additional **paddle** buttons on its underside. These buttons are also represented in the `GamepadButtons` enumeration and their values are read in the same way as the standard gamepad buttons. -->

ボタンの値は、[GamepadReading][] 構造体の `Buttons` プロパティから読み取ります。 このプロパティはビットフィールドであるため、ビット演算子マスクを使用して目的のボタンの値を分離します。 対応するビットが設定されているときはボタンが押されており (ダウン)、それ以外の場合はボタンが離されています (アップ)。

次の例では、A ボタンが押されているかどうかを判別します。

```cpp
if (GamepadButtons::A == (reading.Buttons & GamepadButtons::A))
{
    // button A is pressed
}
```

```cs
if (GamepadButtons.A == (reading.Buttons & GamepadButtons.A))
{
    // button A is pressed
}
```

次の例では、A ボタンが離されているかどうかを判別します。

```cpp
if (GamepadButtons::None == (reading.Buttons & GamepadButtons::A))
{
    // button A is released
}
```

```cs
if (GamepadButtons.None == (reading.Buttons & GamepadButtons.A))
{
    // button A is released
}
```

場合によっては、ボタンを押された状態から離した状態に切り替えるか、または離された状態に切り替えたか、複数のボタンが押されたか離されたか、またはボタンのセットが特定の方法で並んでいるかどうかを判断する必要があり &mdash; ます。 これらの各状態を検出する方法について詳しくは、「[ボタンの状態遷移の検出](input-practices-for-games.md#detecting-button-transitions)」および「[ボタンの複雑な配置の検出](input-practices-for-games.md#detecting-complex-button-arrangements)」をご覧ください。

## <a name="run-the-gamepad-input-sample"></a>ゲームパッド入力のサンプルの実行

[GamepadUWP サンプル _(github)_](https://github.com/Microsoft/Xbox-ATG-Samples/tree/master/UWPSamples/System/GamepadUWP) は、ゲームパッドに接続して、その状態を読み取る方法を示しています。

## <a name="vibration-and-impulse-triggers-overview"></a>振動とリアル トリガーの概要

ゲームパッド内の振動モーターは、触覚的なフィードバックをユーザーに提供することを目的としています。 ゲームではこの機能を、より高い没入感を生み出す、状態情報 (ダメージを受けたなど) の伝達を助ける、重要なアイテムに近接信号を送るなど、クリエイティブな用途に利用します。

Xbox One ゲームパッドには、独立した振動モーターが合計 4 つ搭載されています。 2つはゲームパッドの本文にある大きなモータです。左側のモーターは、粗い振動を備えています。一方、右モータは、穏やか、より微妙な振動を提供します。 残り 2 つは小型のモーターで、各トリガー内に 1 つずつ組み込まれていて、トリガーを操作しているユーザーの指に直接、鋭い弾けるような振動を伝えます。Xbox One ゲームパッドのトリガーは、この独自の機能のために、_リアル トリガー_と呼ばれます。 これらのモーターが協調することで、幅広い種類の触感を生成できます。

## <a name="using-vibration-and-impulse"></a>振動とリアル トリガーの使用

ゲームパッドの振動は、[Gamepad][] クラスの [Vibration][] プロパティによって制御されます。 `Vibration` は、4つの浮動小数点値で構成される [GamepadVibration][] 構造体のインスタンスです。各値は、いずれかのモーターの強度を表します。

プロパティのメンバーは `Gamepad.Vibration` 直接変更できますが、別のインスタンスを必要な値に初期化し、 `GamepadVibration` プロパティにコピーして、 `Gamepad.Vibration` 実際のモータの輝度をすべて一度に変更することをお勧めします。

次の例は、モーターの強さを一度に変更する方法を示しています。

```cpp
// get the first gamepad
Gamepad^ gamepad = Gamepad::Gamepads->GetAt(0);

// create an instance of GamepadVibration
GamepadVibration vibration;

// ... set vibration levels on vibration struct here

// copy the GamepadVibration struct to the gamepad
gamepad.Vibration = vibration;
```

```cs
// get the first gamepad
Gamepad gamepad = Gamepad.Gamepads[0];

// create an instance of GamepadVibration
GamepadVibration vibration = new GamepadVibration();

// ... set vibration levels on vibration struct here

// copy the GamepadVibration struct to the gamepad
gamepad.Vibration = vibration;
```

### <a name="using-the-vibration-motors"></a>振動モーターの使用

左右の振動モーターの値は、0.0 (振動なし) ～ 1.0 (最も強い振動) の浮動小数点値になります。 左のモーターの強さは、[GamepadVibration][] 構造体の `LeftMotor` プロパティによって設定され、右のモーターの強さは `RightMotor` プロパティによって設定されます。

次の例では両方の振動モーターの強さを設定し、ゲームパッドの振動を有効にします。

```cpp
GamepadVibration vibration;
vibration.LeftMotor = 0.80;  // sets the intensity of the left motor to 80%
vibration.RightMotor = 0.25; // sets the intensity of the right motor to 25%
gamepad.Vibration = vibration;
```

```cs
GamepadVibration vibration = new GamepadVibration();
vibration.LeftMotor = 0.80;  // sets the intensity of the left motor to 80%
vibration.RightMotor = 0.25; // sets the intensity of the right motor to 25%
mainGamepad.Vibration = vibration;
```

この 2 つのモーターは同じではないため、これらのプロパティを同じ値に設定しても、一方のモーターともう一方のモーターの振動は同じになりません。 任意の値について、左のモーターは、 &mdash; 同じ値に対して、 &mdash; 穏やか振動をより高い周波数で生成する右モータよりも低い周波数でより強い振動を生成します。 最大値でも、左のモーターでは右のモーターと同じ高い周波数を生成することはできず、右のモーターは左のモーターほど強い力を生み出すことはできません。 ただし、これらのモーターはゲームパッドの本体によってしっかりと連結しているため、各モーターの特徴は異なり、振動の強度が異なる場合でも、プレイヤーがそれぞれの振動を完全に分けて感じることはありません。 このアレンジによって、モーターがまったく同じ場合よりも、より幅広く表現豊かに触感を生み出すことができます。

### <a name="using-the-impulse-triggers"></a>リアル トリガーの使用

各リアル トリガーのモーターの値は、0.0 (振動なし) ～ 1.0 (最も強い振動) の浮動小数点値になります。 左のトリガー モーターの強さは、[GamepadVibration][] 構造体の `LeftTrigger` プロパティによって設定され、右のトリガー の強さは `RightTrigger` プロパティによって設定されます。

次の例では両方のリアル トリガーの強さを設定し、有効にします。

```cpp
GamepadVibration vibration;
vibration.LeftTrigger = 0.75;  // sets the intensity of the left trigger to 75%
vibration.RightTrigger = 0.50; // sets the intensity of the right trigger to 50%
gamepad.Vibration = vibration;
```

```cs
GamepadVibration vibration = new GamepadVibration();
vibration.LeftTrigger = 0.75;  // sets the intensity of the left trigger to 75%
vibration.RightTrigger = 0.50; // sets the intensity of the right trigger to 50%
mainGamepad.Vibration = vibration;
```

本体のモーターと異なり、トリガー内のこの 2 つの振動モーターは同じであるため、同じ値を設定すると、どちらのモーターでも同じ振動が生成されます。 ただし、これらのモーターは何らかの形で強く連結されてはいないため、プレイヤーは振動を個別に感じます。 このアレンジでは、完全に独立した感覚を両方のトリガーに提供することができ、ゲームパッド本体のモーターよりも、個別の情報を伝えることができます。

## <a name="run-the-gamepad-vibration-sample"></a>ゲームパッドの振動のサンプルの実行

[GamepadVibrationUWP サンプル _(github)_](https://github.com/Microsoft/Xbox-ATG-Samples/tree/master/UWPSamples/System/GamepadVibrationUWP) では、ゲームパッドの振動モーターとリアル トリガーを使用して、さまざまな効果を生む方法を示しています。

## <a name="see-also"></a>関連項目

* [Windows.Gaming.Input.UINavigationController][]
* [Windows.Gaming.Input.IGameController][]
* [ゲームの入力プラクティス](input-practices-for-games.md)

[Windows. ゲーム. 入力]: /uwp/api/Windows.Gaming.Input
[Windows.Gaming.Input.UINavigationController]: /uwp/api/Windows.Gaming.Input.UINavigationController
[Windows.Gaming.Input.IGameController]: /uwp/api/Windows.Gaming.Input.IGameController
[ゲーム]: /uwp/api/Windows.Gaming.Input.Gamepad
[gamepads]: /uwp/api/Windows.Gaming.Input.Gamepad
[gamepadadded]: /uwp/api/Windows.Gaming.Input.Gamepad
[gamepadremoved]: /uwp/api/Windows.Gaming.Input.Gamepad
[getcurrentreading]: /uwp/api/Windows.Gaming.Input.Gamepad
[vibration]: /uwp/api/Windows.Gaming.Input.Gamepad
[gamepadreading]: /uwp/api/Windows.Gaming.Input.GamepadReading
[gamepadbuttons]: /uwp/api/Windows.Gaming.Input.GamepadButtons
[gamepadvibration]: /uwp/api/Windows.Gaming.Input.GamepadVibration