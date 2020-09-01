---
Description: ドラッグ アンド ドロップ アニメーションは、リスト内で項目を移動するときや、特定の項目を別の項目上にドロップするときなど、オブジェクトを移動する際に使います。
title: ドラッグ アニメーション
ms.assetid: 6064755F-6E24-4901-A4FF-263F05F0DFD6
label: Motion--Drag and drop
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 4d346d286b6a874ff62e63ecc59a102bcb68fa73
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89156856"
---
# <a name="drag-animations"></a>ドラッグ アニメーション




ドラッグ アンド ドロップ アニメーションは、リスト内で項目を移動するときや、特定の項目を別の項目上にドロップするときなど、オブジェクトを移動する際に使います。

> **重要な API**: [**DragItemThemeAnimation クラス**](/uwp/api/windows.ui.xaml.media.animation.dragitemthemeanimation)


## <a name="dos-and-donts"></a>推奨と非推奨


**ドラッグの開始アニメーション**

-   ドラッグの開始アニメーションは、ユーザーがオブジェクトを動かし始めるときに使います。
-   ドラッグ アンド ドロップ操作の影響を受けるオブジェクトが他に存在する場合に限り、それらのオブジェクトをアニメーションに含めるようにします。
-   ドラッグの開始アニメーションによって始まったアニメーションのシーケンスの終了には、ドラッグの終了アニメーションを使います。 ドラッグの終了アニメーションにより、ドラッグの開始アニメーションで変化したドラッグされたオブジェクトのサイズが元に戻ります。

**ドラッグの終了アニメーション**

-   ドラッグの終了アニメーションは、ドラッグされたオブジェクトをドロップするときに使います。
-   ドラッグの終了アニメーションは、リストの追加および削除アニメーションと組み合わせて使います。
-   ドラッグの開始アニメーションに影響を受けるオブジェクトが存在する場合に限り、それらのオブジェクトをドラッグの終了アニメーションに含めるようにします。
-   ドラッグの終了アニメーションは、ドラッグの開始アニメーションよりも先に使わないでください。 ドラッグ シーケンスの完了後にオブジェクトを元のサイズに戻すためには、両方のアニメーションを使う必要があります。

**項目間でのドラッグの開始アニメーション**

-   項目間でのドラッグの開始アニメーションは、2 つのオブジェクトの間のドロップ可能な場所にドラッグ ソースをドラッグするときに使います。
-   適度な大きさのドロップ ターゲット領域を選んでください。 この領域が小さすぎると、ドラッグ ソースをドロップする際に重ね合わせるのが難しくなるため、好ましくありません。
-   ドロップ可能な場所を示すために影響を受けるオブジェクトが移動するときには、互いにまっすぐに引き離すことをお勧めします。 移動方向が上下になるか、左右になるかは、影響を受けるオブジェクトが並ぶ向きによって異なります。
-   ドラッグ ソースを領域内にドロップできない場合、項目間でのドラッグの開始アニメーションは使わないでください。 項目間へのドラッグの開始アニメーションは、影響を受けるオブジェクトの間にドラッグ ソースをドラッグできることをユーザーに知らせるためのものです。

**項目間でのドラッグの中止アニメーション**

-   項目間でのドラッグの中止アニメーションは、ユーザーがオブジェクトをドラッグして 2 つのオブジェクトの間のドロップ可能な領域から出すときに使います。
-   項目間でのドラッグの開始アニメーションよりも先に、項目間でのドラッグの中止アニメーションを使わないでください。


## <a name="related-articles"></a>関連記事

**開発者向け**
* [アニメーションの概要](./xaml-animation.md)
* [ドラッグ アンド ドロップ シーケンスのアニメーション化](/previous-versions/windows/apps/jj649427(v=win.10))
* [クイック スタート: ライブラリのアニメーションを使った UI のアニメーション化](/previous-versions/windows/apps/hh452703(v=win.10))
* [**DragItemThemeAnimation クラス**](/uwp/api/windows.ui.xaml.media.animation.dragitemthemeanimation)
* [**DropTargetItemThemeAnimation クラス**](/uwp/api/windows.ui.xaml.media.animation.droptargetitemthemeanimation)
* [**DragOverThemeAnimation クラス**](/uwp/api/windows.ui.xaml.media.animation.dragoverthemeanimation)


 