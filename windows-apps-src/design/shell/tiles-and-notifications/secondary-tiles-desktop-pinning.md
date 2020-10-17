---
Description: デスクトップアプリケーションでは、デスクトップブリッジによってセカンダリタイルをピン留めすることができます。
title: デスクトップアプリからのセカンダリタイルのピン留め
label: Pin secondary tiles from desktop apps
template: detail.hbs
ms.date: 05/25/2017
ms.topic: article
keywords: Windows 10、デスクトップ ブリッジ、セカンダリ タイル、ピン留め、クイックスタート、コード サンプル、例、デスクトップ アプリケーション、Win32、WinForms、WPF
ms.localizationpriority: medium
ms.openlocfilehash: f0b1e167b0ce2e91b00b7facbdd53709efdc4887
ms.sourcegitcommit: c5df8832e9df8749d0c3eee9e85f4c2d04f8b27b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92100270"
---
# <a name="pin-secondary-tiles-from-desktop-apps"></a>デスクトップアプリからのセカンダリタイルのピン留め


デスクトップ [ブリッジ](https://developer.microsoft.com/windows/bridges/desktop)のおかげで、デスクトップアプリケーション (WINDOWS フォーム、WPF など) はセカンダリタイルをピン留めできます。

![セカンダリ タイルのスクリーン ショット](images/secondarytiles.png)

> [!IMPORTANT]
> **Fall Creators Update が必要**: デスクトップ ブリッジ アプリからセカンダリ タイルをピン留めするには、SDK 16299 をターゲットとし、ビルド 16299 以降を実行している必要があります。

WPF または WinForms アプリケーションからのセカンダリ タイルの追加は、純粋な UWP アプリとよく似ています。 唯一の違いは、メイン ウィンドウのハンドル (HWND) を指定する必要があることです。 これは、タイルをピン留めするときに、モーダル ダイアログが表示され、タイルをピン留めするかどうかをユーザーに確認するためです。 デスクトップ アプリケーションが、SecondaryTile オブジェクトのオーナー ウィンドウを構成しない場合、ダイアログ ボックスを描画する位置を認識することができず、操作は失敗します。


## <a name="package-your-app-with-desktop-bridge"></a>デスクトップ ブリッジを使ったアプリのパッケージ化

アプリをデスクトップブリッジでパッケージ化していない場合は、Windows ランタイム Api を使用する前に、まずこの設定を [行う必要があり](/windows/msix/desktop/source-code-overview) ます。


## <a name="enable-access-to-iinitializewithwindow-interface"></a>IInitializeWithWindow インターフェイスへのアクセスを有効にする

アプリケーションが C# や Visual Basic などのマネージ言語で記述されている場合、次の C# の例に示すように、アプリのコードで [ComImport](/dotnet/api/system.runtime.interopservices.comimportattribute) と GUID 属性を使用して IInitializeWithWindow インターフェイスを宣言します。 この例では、コード ファイルに System.Runtime.InteropServices 名前空間の using ステートメントが指定されていることを前提としています。

```csharp
[ComImport]
[Guid("3E68D4BD-7135-4D10-8018-9FB6D9F33FA1")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IInitializeWithWindow
{
    void Initialize(IntPtr hwnd);
}
```

または、C++ で記述されている場合、コードに **shobjidl.h** ヘッダー ファイルへの参照を追加します。 このヘッダー ファイルには、*IInitializeWithWindow* インターフェイスの宣言が含まれています。


## <a name="initialize-the-secondary-tile"></a>セカンダリ タイルを初期化する

通常の UWP アプリの場合とまったく同じように、新しいセカンダリ タイル オブジェクトを初期化します。 セカンダリ タイルの作成とピン留めについて詳しくは、「[セカンダリ タイルをピン留めする](secondary-tiles-pinning.md)」をご覧ください。

```csharp
// Initialize the tile with required arguments
SecondaryTile tile = new SecondaryTile(
    "myTileId5391",
    "Display name",
    "myActivationArgs",
    new Uri("ms-appx:///Assets/Square150x150Logo.png"),
    TileSize.Default);
```


## <a name="assign-the-window-handle"></a>ウィンドウ ハンドルを割り当てる

これは、デスクトップ アプリケーションにとって重要な手順です。 オブジェクトを [IInitializeWithWindow](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iinitializewithwindow) オブジェクトにキャストします。 次に [IInitializeWithWindow.Initialize](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-iinitializewithwindow-initialize) メソッドを呼び出し、モーダル ダイアログのオーナーにするウィンドウのハンドルを渡します。 次の C# の例は、アプリのメイン ウィンドウのハンドルをメソッドに渡す方法を示しています。

```csharp
// Assign the window handle
IInitializeWithWindow initWindow = (IInitializeWithWindow)(object)tile;
initWindow.Initialize(System.Diagnostics.Process.GetCurrentProcess().MainWindowHandle);
```


## <a name="pin-the-tile"></a>タイルをピン留めする

最後に、通常の UWP アプリと同様、タイルのピン留めを要求します。

```csharp
// Pin the tile
bool isPinned = await tile.RequestCreateAsync();

// TODO: Update UI to reflect whether user can now either unpin or pin
```


## <a name="send-tile-notifications"></a>タイル通知を送信する

> [!IMPORTANT]
> **2018 年 4 月のバージョン 17134.81 以降が必要**: ビルド 17134.81 以降を実行してデスクトップ ブリッジ アプリからセカンダリ タイルにタイル通知またはバッジ通知を送信する必要があります。 この.81 サービス更新プログラムの前に、デスクトップ ブリッジ アプリからセカンダリ タイルにタイル通知またはバッジ通知を送信するときに a 0x80070490 *要素が見つかりません*という例外が発生します。

タイル通知またはバッジ通知の送信は UWP アプリと同じです。 手順については、「[ローカル タイル通知の送信](sending-a-local-tile-notification.md)」を参照してください。


## <a name="resources"></a>リソース

* [完全なコード例](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/SecondaryTileSample)
* [セカンダリ タイルの概要](secondary-tiles.md)
* [セカンダリ タイルをピン留めする (UWP)](secondary-tiles-pinning.md)
* [Desktop Bridge](https://developer.microsoft.com/windows/bridges/desktop)
* [デスクトップ ブリッジのコード サンプル](https://github.com/Microsoft/DesktopBridgeToUWP-Samples)