---
title: ゲームのタッチ コントロール
description: ここでは、DirectX を使って基本的なタッチ コントロールをユニバーサル Windows プラットフォーム (UWP) C++ ゲームに追加する方法について説明します。
ms.assetid: 9d40e6e4-46a9-97e9-b848-522d61e8e109
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, タッチ, コントロール, DirectX, 入力
ms.localizationpriority: medium
ms.openlocfilehash: 546d36e26489563720f5aad8a0c9f81f85649e5a
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89168286"
---
# <a name="touch-controls-for-games"></a>ゲームのタッチ コントロール



ここでは、DirectX を使って基本的なタッチ コントロールをユニバーサル Windows プラットフォーム (UWP) C++ ゲームに追加する方法について説明します。 具体的には、平面に固定されたカメラを動かすタッチ ベースのコントロールを、指またはスタイラスでドラッグするとカメラの視点がシフトする Direct3D 環境に追加する方法を紹介します。

これらのコントロールは、プレイヤーが地図やプレイフィールドなどの 3D 環境でドラッグしてスクロールまたはパンを行うゲームに組み込むことができます。 たとえば、戦略ゲームやパズル ゲームでは、これらのコントロールを使って、プレイヤーが左右にパンすることで画面より大きいゲーム環境を確認できるようにすることが可能です。

> **メモ**   このコードは、マウスベースのパンコントロールでも動作します。 ポインター関連のイベントは、Windows ランタイム API で抽象化されるため、タッチまたはマウス ベースのポインター イベントを処理できます。

 

## <a name="objectives"></a>目的


-   DirectX ゲームで平面に固定されたカメラをパンする簡単なタッチ ドラッグ コントロールを作成する。

## <a name="set-up-the-basic-touch-event-infrastructure"></a>基本的なタッチ イベントのインフラストラクチャのセットアップ


まず、この例ではコントローラーの基本型として、**CameraPanController** を定義します。 ここでは、コントローラーを抽象的な概念、つまりユーザーが実行できる動作のセットとして定義します。

**CameraPanController** クラスは、カメラ コントローラーの状態に関する情報を定期的に更新したコレクションであり、アプリが自身の更新ループからこの情報を取得できるようにします。

```cpp
using namespace Windows::UI::Core;
using namespace Windows::System;
using namespace Windows::Foundation;
using namespace Windows::Devices::Input;
#include <directxmath.h>

// Methods to get input from the UI pointers
ref class CameraPanController
{
}
```

次に、カメラ コントローラーの状態を定義するヘッダーと、カメラ コントローラーの操作を実装する基本的なメソッドとイベント ハンドラーを作ります。

```cpp
ref class CameraPanController
{
private:
    // Properties of the controller object
    DirectX::XMFLOAT3 m_position;               // the position of the camera

    // Properties of the camera pan control
    bool m_panInUse;                
    uint32 m_panPointerID;          
    DirectX::XMFLOAT2 m_panFirstDown;           
    DirectX::XMFLOAT2 m_panPointerPosition;   
    DirectX::XMFLOAT3 m_panCommand;         
    
internal:
    // Accessor to set the position of the controller
    void SetPosition( _In_ DirectX::XMFLOAT3 pos );

       // Accessor to set the fixed "look point" of the controller
       DirectX::XMFLOAT3 get_FixedLookPoint();

    // Returns the position of the controller object
    DirectX::XMFLOAT3 get_Position();

public:

    // Methods to get input from the UI pointers
    void OnPointerPressed(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::PointerEventArgs^ args
        );

    void OnPointerMoved(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::PointerEventArgs^ args
        );

    void OnPointerReleased(
        _In_ Windows::UI::Core::CoreWindow^ sender,
        _In_ Windows::UI::Core::PointerEventArgs^ args
        );

    // Set up the Controls supported by this controller
    void Initialize( _In_ Windows::UI::Core::CoreWindow^ window );

    void Update( Windows::UI::Core::CoreWindow ^window );

};  // Class CameraPanController
```

プライベート フィールドには、カメラ コントローラーの現在の状態が含まれています。 ここでその内容を確認してみましょう。

-   **m \_ 位置** は、シーン空間におけるカメラの位置です。 この例では、z 座標値は 0 に固定されています。 DirectX::XMFLOAT2 を使ってこの値を表すこともできますが、このサンプルの目的と今後の拡張性を考慮して、ここでは DirectX::XMFLOAT3 を使います。 この値を **get \_ Position** プロパティを使用してアプリ自体に渡し、それに応じてビューポートを更新できるようにします。
-   **m \_ paninuse** は、パン操作がアクティブかどうかを示すブール値です。具体的には、プレーヤーが画面にタッチしてカメラを移動しているかどうかを示します。
-   **m \_ panpointer id** は、ポインターの一意の id です。 これはこのサンプルでは使いませんが、コントローラーの状態クラスと特定のポインターを関連付けることをお勧めします。
-   **m \_ panfirstdown** は、プレーヤーが最初に画面を操作したとき、またはカメラのパン操作中にマウスをクリックした画面上のポイントです。 この値は、画面がタッチされているときや、マウスが少し揺れている場合に、ビューが不安定にならないようデッド ゾーンを設定するために後で使います。
-   **m \_ panpointer position** は、プレーヤーがポインターを現在移動している画面上のポイントです。 このメソッドを使用して、プレーヤーが移動する方向を、 **m \_ panfirstdown**と比較して確認します。
-   **m \_ pancommand** は、カメラコントローラーの最終的な計算されたコマンドです: up、down、left、または right。 x-y 平面に固定されたカメラを操作しているため、これは、DirectX::XMFLOAT2 にすることも可能です。

次の 3 つのイベント ハンドラーを使って、カメラ コントローラーの状態情報を更新します。

-   **OnPointerPressed** は、プレイヤーが指でタッチ画面を押し、その押された座標にポインターが動いたときに、アプリが呼び出すイベント ハンドラーです。
-   **OnPointerMoved** は、プレイヤーが指でタッチ画面をスワイプしたときに、アプリが呼び出すイベント ハンドラーです。 これは、ドラッグ パスの新しい座標で更新されます。
-   **OnPointerReleased** は、プレイヤーが指をタッチ画面から離したときに、アプリが呼び出すイベント ハンドラーです。

最後に、次のメソッドとプロパティを使って、カメラ コントローラーの状態情報の初期化、アクセス、更新を行います。

-   **Initialize**は、アプリがコントロールを初期化して、表示ウィンドウを定義する [**CoreWindow**](/uwp/api/Windows.UI.Core.CoreWindow) オブジェクトにそれらのコントロールを適用するときに呼び出すイベント ハンドラーです。
-   **SetPosition** は、アプリがシーン空間内のコントロールの (x、y、z) 座標を設定するときに呼び出すメソッドです。 z 座標はこのチュートリアル全体で 0 であることに注意してください。
-   **取得 \_Position** は、シーン空間でカメラの現在位置を取得するためにアプリによってアクセスされるプロパティです。 このプロパティは、カメラの現在の位置をアプリに伝える手段として使います。
-   **取得 \_Fixedlook Point** は、コントローラーカメラが接続している現在のポイントを取得するためにアプリがアクセスするプロパティです。 この例では、x-y 平面に垂直にロックされています。
-   **Update** は、コントローラーの状態を読み取り、カメラの位置を更新するメソッドです。 &lt; &gt; アプリのメインループからこのような情報を継続的に呼び出して、カメラコントローラーのデータとシーン空間内のカメラの位置を更新します。

これで、タッチ コントロールの実装に必要なコンポーネントがすべて揃いました。 タッチ ポインターまたはマウス ポインターのイベントがいつどこで発生し、その操作が何かを検出できます。 また、カメラの位置と向きをシーン空間と相対的に設定し、変化を追跡できます。 さらに、カメラの新しい位置を呼び出し元アプリに伝えることができます。

次は、これらのコンポーネントどうしを接続してみましょう。

## <a name="create-the-basic-touch-events"></a>基本的なタッチ イベントの作成


Windows ランタイムのイベント ディスパッチャーは、アプリで処理するイベントを 3 つ提供します。

-   [**PointerPressed**](/uwp/api/windows.ui.core.corewindow.pointerpressed)
-   [**PointerMoved**](/uwp/api/windows.ui.core.corewindow.pointermoved)
-   [**PointerReleased**](/uwp/api/windows.ui.core.corewindow.pointerreleased)

これらのイベントは、[**CoreWindow**](/uwp/api/Windows.UI.Core.CoreWindow) 型に実装されています。 ここでは、操作する **CoreWindow** オブジェクトが既にあると想定しています。 詳しくは、「[UWP C++ アプリで DirectX ビューを表示するための設定方法](/previous-versions/windows/apps/hh465077(v=win.10))」をご覧ください。

これらのイベントは Windows ストア アプリの実行中に起動するため、ハンドラーはプライベート フィールドに定義されているカメラ コントローラーの状態情報を更新します。

まず、タッチ ポインターのイベント ハンドラーを設定します。 最初のイベント ハンドラーである **OnPointerPressed** では、ユーザーが画面をタッチまたはマウスをクリックしたときに表示を管理する [**CoreWindow**](/uwp/api/Windows.UI.Core.CoreWindow) からポインターの x-y 座標を取得します。

**Onポインタが押されました**

```cpp
void CameraPanController::OnPointerPressed(
                                           _In_ CoreWindow^ sender,
                                           _In_ PointerEventArgs^ args)
{
    // Get the current pointer position.
    uint32 pointerID = args->CurrentPoint->PointerId;
    DirectX::XMFLOAT2 position = DirectX::XMFLOAT2( args->CurrentPoint->Position.X, args->CurrentPoint->Position.Y );

    auto device = args->CurrentPoint->PointerDevice;
    auto deviceType = device->PointerDeviceType;
    

       if ( !m_panInUse )   // If no pointer is in this control yet.
    {
       m_panFirstDown = position;                   // Save the location of the initial contact.
       m_panPointerPosition = position;
       m_panPointerID = pointerID;              // Store the id of the pointer using this control.
       m_panInUse = TRUE;
    }
    
}
```

このハンドラーは、 **m \_ PANINUSE**を TRUE に設定することによって、カメラコントローラーがアクティブとして扱われることを現在の**CameraPanController**インスタンスに知らせるために使用します。 この方法により、アプリは **Update** を呼び出すときに、現在の位置データを使ってビューポートを更新します。

以上で、ユーザーが画面をタッチまたは表示ウィンドウをクリックしたときのカメラの動きを示す基本の値が設定されたので、次は、ユーザーが画面を押してドラッグまたはボタンを押してマウスを動かしたときに何をするかを決める必要があります。

**OnPointerMoved** イベント ハンドラーは、ポインターが動くたびに、プレイヤーがポインターを画面上でドラッグするティックごとに起動します。 アプリにポインターの現在の位置を知らせ続ける必要があるため、次のように指定します。

**OnPointerMoved**

```cpp
void CameraPanController::OnPointerMoved(
                                        _In_ CoreWindow ^sender,
                                        _In_ PointerEventArgs ^args)
{
    uint32 pointerID = args->CurrentPoint->PointerId;
    DirectX::XMFLOAT2 position = DirectX::XMFLOAT2( args->CurrentPoint->Position.X, args->CurrentPoint->Position.Y );

    m_panPointerPosition = position;
}
```

最後に、プレイヤーが画面から手を離したときに、カメラのパン動作を非アクティブにする必要があります。 **Onpointer released**を使用します。これは、ポインターが[**解放**](/uwp/api/windows.ui.core.corewindow.pointerreleased)されたときに呼び出され、 **m \_ paninuse**を FALSE に設定し、カメラのパンの移動をオフにして、ポインター ID を0に設定します。

**Onポインタが解放されました**

```cpp
void CameraPanController::OnPointerReleased(
                                             _In_ CoreWindow ^sender,
                                             _In_ PointerEventArgs ^args)
{
    uint32 pointerID = args->CurrentPoint->PointerId;
    DirectX::XMFLOAT2 position = DirectX::XMFLOAT2( args->CurrentPoint->Position.X, args->CurrentPoint->Position.Y );

    m_panInUse = FALSE;
    m_panPointerID = 0;
}
```

## <a name="initialize-the-touch-controls-and-the-controller-state"></a>タッチ コントロールとコントローラーの状態の初期化


次は、イベントをフックして、カメラ コントローラーの状態の基本的なフィールドをすべて初期化しましょう。

**化**

```cpp
void CameraPanController::Initialize( _In_ CoreWindow^ window )
{

    // Start recieving touch/mouse events.
    window->PointerPressed += 
    ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &CameraPanController::OnPointerPressed);

    window->PointerMoved += 
    ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &CameraPanController::OnPointerMoved);

    window->PointerReleased += 
    ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &CameraPanController::OnPointerReleased);


    // Initialize the state of the controller.
    m_panInUse = FALSE;             
    m_panPointerID = 0;

    //  Initialize this as it is reset on every frame.
    m_panCommand = DirectX::XMFLOAT3( 0.0f, 0.0f, 0.0f );

}
```

**Initialize** は、アプリの [**CoreWindow**](/uwp/api/Windows.UI.Core.CoreWindow) インスタンスへの参照をパラメーターとして使い、先ほど作成したイベント ハンドラーをその **CoreWindow** の適切なイベントに登録します。

## <a name="getting-and-setting-the-position-of-the-camera-controller"></a>カメラ コントローラーの位置の取得と設定


シーン空間内のカメラ コントローラーの位置の取得と設定を行うメソッドをいくつか定義してみましょう。

```cpp
void CameraPanController::SetPosition( _In_ DirectX::XMFLOAT3 pos )
{
    m_position = pos;
}

// Returns the position of the controller object
DirectX::XMFLOAT3 CameraPanController::get_Position()
{
    return m_position;
}

DirectX::XMFLOAT3 CameraPanController::get_FixedLookPoint()
{
    // For this sample, we don't need to use the trig functions because our
    // look point is fixed. 
    DirectX::XMFLOAT3 result= m_position;
    result.z += 1.0f;
    return result;    

}
```

**SetPosition** は、カメラ コントローラーの位置を特定の点に設定する必要がある場合に、アプリから呼び出すことができるパブリック メソッドです。

**取得 \_Position** は、最も重要なパブリックプロパティです。これは、アプリがシーン空間でカメラコントローラーの現在位置を取得し、それに応じてビューポートを更新できるようにする方法です。

**取得 \_Fixedlook Point** はパブリックプロパティで、この例では、y 平面に通常使用されるルックポイントを取得します。 固定カメラに対して斜めの角度を作る場合は、このメソッドを変更して、x、y、z 座標値の計算時に三角関数 sin と cos を使うことができます。

## <a name="updating-the-camera-controller-state-information"></a>カメラ コントローラーの状態情報の更新


ここでは、 **m \_ panpointer position** で追跡されているポインターの座標情報を、3d シーン空間に対応する新しい座標情報に変換する計算を実行します。 Windows ストア アプリは、アプリのメイン ループが更新されるたびに、このメソッドを呼び出します。 ここで、ビューポートへのプロジェクションの前にビュー マトリックスを更新するためにアプリに渡す新しい位置情報を計算します。

```cpp

void CameraPanController::Update( CoreWindow ^window )
{
    if ( m_panInUse )
    {
        pointerDelta.x = m_panPointerPosition.x - m_panFirstDown.x;
        pointerDelta.y = m_panPointerPosition.y - m_panFirstDown.y;

        if ( pointerDelta.x > 16.0f )        // Leave 32 pixel-wide dead spot for being still.
            m_panCommand.x += 1.0f;
        else
            if ( pointerDelta.x < -16.0f )
                m_panCommand.x += -1.0f;

        if ( pointerDelta.y > 16.0f )        
            m_panCommand.y += 1.0f;
        else
            if (pointerDelta.y < -16.0f )
                m_panCommand.y += -1.0f;
    }

       DirectX::XMFLOAT3 command = m_panCommand;
   
    // Our velocity is based on the command.
    DirectX::XMFLOAT3 Velocity;
    Velocity.x =  command.x;
    Velocity.y =  command.y;
    Velocity.z =  0.0f;

    // Integrate
    m_position.x = m_position.x + Velocity.x;
    m_position.y = m_position.y + Velocity.y;
    m_position.z = m_position.z + Velocity.z;

    // Clear the movement input accumulator for use during the next frame.
    m_panCommand = DirectX::XMFLOAT3( 0.0f, 0.0f, 0.0f );

}
```

タッチまたはマウスの揺れでカメラのパンが不適切に動かないように、ポインターの周りに直径 32 ピクセルのデッド ゾーンを設定します。 また、速度値もあります。この例では、デッド ゾーンを超えるポインターのピクセル トラバーサルに対して 1:1 です。 この動作を調整し、移動速度を低下または上昇させることができます。

## <a name="updating-the-view-matrix-with-the-new-camera-position"></a>カメラの新しい位置によるビュー マトリックスの更新


これで、カメラのフォーカスが合っているシーン空間の座標の取得ができます。この座標は、アプリに指定した時間ごとに更新されます (たとえばアプリのメイン ループでは 60 秒ごと)。 次の疑似コードは、実装できる呼び出し動作を示しています。

```cpp
 myCameraPanController->Update( m_window ); 

 // Update the view matrix based on the camera position.
 myCamera->MyMethodToComputeViewMatrix(
        myController->get_Position(),        // The position in the 3D scene space.
        myController->get_FixedLookPoint(),      // The point in the space we are looking at.
        DirectX::XMFLOAT3( 0, 1, 0 )                    // The axis that is "up" in our space.
        );  
```

お疲れさまでした。 一連の簡単なカメラ パンのタッチ コントロールがゲームに実装されました。


 

 

 