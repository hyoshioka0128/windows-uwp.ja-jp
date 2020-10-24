---
title: マウス モードを無効にする方法
description: HTML および XAML/C# ユニバーサル Windows プラットフォーム (UWP) アプリケーションで既定のマウスモードをオフにする方法について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.assetid: e57ee4e6-7807-4943-a933-c2b4dc80fc01
ms.localizationpriority: medium
ms.openlocfilehash: 16b2df2d84c0064c2549c75d867123d90e663314
ms.sourcegitcommit: 45dec3dc0f14934b8ecf1ee276070b553f48074d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094599"
---
# <a name="how-to-disable-mouse-mode"></a>マウス モードを無効にする方法
マウス モードは、すべてのアプリケーションについて既定でオンになっています。つまり、オプトアウトしていないすべてのアプリケーションがマウス ポインターを受け取ります (コンソール上の Edge ブラウザー内のアプリケーションに似ています)。 コントローラーの方向移動操作を最適化するため、マウス モードは無効にすることを強くお勧めします。   
   
## <a name="html"></a>HTML   
JavaScript ユニバーサル Windows プラットフォーム (UWP) アプリでコントローラーの方向移動操作を有効にするには、[TVHelpers 方向ナビゲーション](https://github.com/Microsoft/TVHelpers/wiki/Using-DirectionalNavigation) JavaScript ライブラリを使います。 アプリ パッケージに方向ナビゲーションの JavaScript ファイルを含め、コントローラーの方向移動操作を必要とするすべての HTML ページにこのファイルへの参照を追加します。

```code
<script src="directionalnavigation-1.0.0.0.js"></script>
```
詳しくは、[方向ナビゲーションに関する Wiki](https://github.com/Microsoft/TVHelpers/wiki/Using-DirectionalNavigation) をご覧ください。

マウス モードをオフにして、DOM または WinRT のゲームパッド API を直接使う場合は、API を必要とするすべてのページで次のコードを実行します。 
   
```code
navigator.gamepadInputEmulation = "gamepad";
```   

   このプロパティの既定値は `mouse` で、マウス モードを有効にします。 このプロパティを `keyboard` に設定すると、マウス モードが無効になり、代わりにゲームパッドによって DOM のキーボード イベントが生成されます。 このプロパティを `gamepad` に設定すると、マウス モードは無効になりますが、DOM のキーボード イベントは生成されず、DOM または WinRT のゲームパッド API のみを使用できます。

## <a name="xaml"></a>XAML    
マウス モードを無効にするには、次のコードをアプリのコンストラクターに追加します。   
   
```code
public App() {
        this.InitializeComponent();
        this.RequiresPointerMode = Windows.UI.Xaml.ApplicationRequiresPointerMode.WhenRequested;
        this.Suspending += OnSuspending;
}
```

## <a name="cdirectx"></a>C++/DirectX   
C++/DirectX アプリを作成する場合は、特に操作は必要ありません。 マウス モードは、HTML アプリケーションと XAML アプリケーションのみに適用されます。

## <a name="see-also"></a>関連項目
- [Xbox のベスト プラクティス](tailoring-for-xbox.md)
- [Xbox One の UWP](index.md)

