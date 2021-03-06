---
Description: このトピックでは、回転の新しい Windows UI を説明し、UWP アプリでこの新しい相互作用のメカニズムの使用時に考慮すべきユーザー エクスペリエンス ガイドラインを示します。
title: 回転
ms.assetid: f098bc05-35b3-46b2-9e9b-9ff292d067ca
label: Rotation
template: detail.hbs
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: f6593c19503fec3ee0e60920c66af7de8f2a7025
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66363638"
---
# <a name="rotation"></a>回転


この記事では、新しい Windows UI の回転について説明し、UWP アプリでこの新しい操作のメカニズムを使うときに考慮する必要があるユーザー エクスペリエンスのガイドラインを示します。

> **重要な API**:[**Windows.UI.Input**](https://docs.microsoft.com/uwp/api/Windows.UI.Input)、 [ **Windows.UI.Xaml.Input**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input)

## <a name="dos-and-donts"></a>推奨と非推奨

-   ユーザーが直接 UI 要素を回転できるように回転を使います。

## <a name="additional-usage-guidance"></a>その他の使い方のガイダンス


**回転の概要**

回転は UWP アプリで使われるタッチ操作に最適な手法であり、ユーザーがオブジェクトを回転 (時計回りまたは反時計回り) できるようにします。

入力デバイスに応じて回転操作は次のように実行されます。

-   マウスまたはアクティブなペン/スタイラスを使って、選んだオブジェクトの回転グリッパーを移動する。
-   タッチまたはパッシブなペン/スタイラスを使って、回転ジェスチャによって任意の方向にオブジェクトを回転させる。

**回転を使用する場合**

ユーザーが直接 UI 要素を回転できるように回転を使います。 次の図は、サポートされる回転操作の指の配置をいくつか示しています。

![回転がサポートされる異なる指の配置を示す図](images/ux-rotate-positions.png)

**注**  ユーザーが (たとえば、描画またはレイアウトのアプリケーション) に接続ポイントとは無関係な回転ポイントを指定しない限りは直感的とでほとんどの場合、回転ポイントは、2 つのタッチ ポイントの 1 つです。 以下の図では、回転の中心点がこのような制約を受けない場合に、どのようにユーザー エクスペリエンスが低下するかについて説明します。

1 番目の図は、最初のタッチ ポイント (親指) と 2 番目のタッチ ポイント (人差し指) を示します。人差し指は木に、親指は丸太にタッチしています。

![イメージの回転のジェスチャの 2 つの初期のタッチ ポイントを表示します。](images/ux-rotate-points1.png)
2 番目の図では、最初のタッチ ポイント (親指) の周りで回転が行われています。 回転の後で、人差し指は相変わらず木の幹にタッチし、親指は相変わらず丸太 (回転の中心点) にタッチしています。

![回転ポイントで回転した画像を表示するイメージは、2 つの初期のタッチ ポイントの 1 つに制限されます。](images/ux-rotate-points2.png)
3 番目の図では、回転の中心がアプリによって絵の中心点に定義されています (またはユーザーによって設定されています)。 回転の後で、絵が指の 1 つの周りで回転しなかったために、直接操作の画像が失われます (ユーザーがこの設定を選んだ場合を除きます)。

![回転ポイントで回転した画像を表示するイメージは、2 つの初期のタッチ ポイントのいずれかではなく、画像の中央に制限されます。](images/ux-rotate-points3.png)
最後の図では、回転の中心がアプリによって絵の左端の中央の点に定義されています (またはユーザーによって設定されています)。 この場合も、ユーザーがこの設定を選んだ場合を除いて、直接操作の画像が失われます。

![回転の中心点が最初に 2 つタッチした点のどちらでもなく、絵の左端の中央に制約された状態で回転する絵を示す図](images/ux-rotate-points4.png)

 

Windows 10 には、回転の 3 つの種類がサポートしています: 無料、制約、および結合します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">自由回転</td>
<td align="left"><p>自由回転では、ユーザーはコンテンツを 360°の任意の位置に自由に回転できます。ユーザーがオブジェクトを離すと、オブジェクトは選んだ位置にとどまります。 自由回転は、Microsoft PowerPoint、Word、Visio、ペイントと Adobe Photoshop、Illustrator、Flash などの描画アプリやレイアウト アプリで便利です。</p></td>
</tr>
<tr class="even">
<td align="left">制約付き回転</td>
<td align="left"><p>制約付き回転は、操作中は自由回転をサポートしますが、離したときに 90°単位のスナップ位置が強制されます (0、90、180、270)。 ユーザーがオブジェクトを離すと、オブジェクトは自動的に最も近いスナップ位置まで回転します。</p>
<p>制約付き回転は回転の最も一般的な方法で、コンテンツのスクロールと同じように機能します。 スナップ位置があることで、ユーザーは操作が正確でなくても目標の位置に到達できます。 制約付きの回転は Web ブラウザーやフォト アルバムのようなアプリで便利です。</p></td>
</tr>
<tr class="odd">
<td align="left">複合回転</td>
<td align="left"><p>複合回転は自由回転をサポートしますが、(<a href="guidelines-for-panning.md">パン</a>におけるレールのように) 90°単位のスナップ位置のゾーンでは制約付き回転によって強制されます。 ユーザーが各 90° のゾーンの外でオブジェクトを離した場合にはオブジェクトはその位置にとどまりますが、それ以外の場合にはオブジェクトは自動的にスナップ位置まで回転します。</p>
<div class="alert">
<strong>注</strong>  ユーザー インターフェイスのレールはターゲットの周囲がいくつかの特定の値または場所の選択に影響を与える方に移動を制限する機能です。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック


**サンプル**
* [基本的な入力サンプル](https://go.microsoft.com/fwlink/p/?LinkID=620302)
* [低待機時間の入力サンプル](https://go.microsoft.com/fwlink/p/?LinkID=620304)
* [ユーザー操作モードのサンプル](https://go.microsoft.com/fwlink/p/?LinkID=619894)
* [フォーカスの視覚効果のサンプル](https://go.microsoft.com/fwlink/p/?LinkID=619895)

**サンプルのアーカイブ**
* [入力:XAML ユーザー入力イベントのサンプル](https://go.microsoft.com/fwlink/p/?linkid=226855)
* [入力:デバイス機能のサンプル](https://go.microsoft.com/fwlink/p/?linkid=231530)
* [入力:タッチ ヒット テストのサンプル](https://go.microsoft.com/fwlink/p/?linkid=231590)
* [XAML のスクロール、パン、ズームのサンプル](https://go.microsoft.com/fwlink/p/?linkid=251717)
* [入力:簡略化されたインクのサンプル](https://go.microsoft.com/fwlink/p/?linkid=246570)
* [入力:ジェスチャと GestureRecognizer の操作](https://go.microsoft.com/fwlink/p/?LinkId=264995)
* [入力:操作とジェスチャ (C++) のサンプル](https://go.microsoft.com/fwlink/p/?linkid=231605)
* [DirectX のタッチ入力サンプル](https://go.microsoft.com/fwlink/p/?LinkID=231627)
 

 




