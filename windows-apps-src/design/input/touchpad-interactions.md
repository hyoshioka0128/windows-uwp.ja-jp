---
Description: タッチパッド用に最適化されているが、入力デバイス間で機能的に一貫性がある、直感的で独特なユーザー操作エクスペリエンスを備えた Windows アプリを作成します。
title: タッチパッド操作
ms.assetid: CEDEA30A-FE94-4553-A7FB-6C1FA44F06AB
label: Touchpad interactions
template: detail.hbs
keywords: タッチパッド, PTP, タッチ, ポインター, 入力, ユーザーの操作
ms.date: 09/24/2020
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 86c47a3a510f6ed0d865064e8d140c47c8dd9f78
ms.sourcegitcommit: eda7bbe9caa9d61126e11f0f1a98b12183df794d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91220435"
---
# <a name="touchpad-design-guidelines"></a>タッチパッドの設計ガイドライン


ユーザーがタッチパッドで操作できるようにアプリを設計します。 タッチパッドは、間接的なマルチタッチ入力と、マウスのようなポインティング デバイスの精密入力を組み合わせたものです。 この組み合わせにより、タッチパッドはタッチに最適化された UI にも、生産性アプリのより小さいターゲットにも適しています。

 

![タッチパッド](images/input-patterns/input-touchpad.jpg)


タッチパッド操作には、次の 3 つが必要です。

-   標準のタッチパッド、または Windows 高精度タッチパッド。

    Precision タッチパッド向けは Windows アプリデバイス用に最適化されています。 高精度タッチパッドを使用すると、システムが指の追跡や手のひら検出などの一部のタッチパッド操作をネイティブに処理でき、さまざまなデバイス全体での一貫した操作を実現しやすくなります。

-   タッチパッドへの 1 本以上の指の直接的な接触。
-   タッチ接触の動き (または、時間のしきい値に基づく動きの欠落)。

タッチパッド センサーから提供される入力データは、次のように使うことができます。

-   1 つ以上の UI 要素に直接的な操作 (パン、回転、サイズ変更、移動など) を行う物理的なジェスチャとして解釈する。 プロパティ ウィンドウやその他のダイアログ ボックスを通じた要素との対話的操作は、間接的な操作と見なされます。
-   マウス、ペンなどの代替の入力方式として見なす。
-   他の入力方法の外観を補完するために使う (ペンで描画したインク ストロークをこするなど)。

タッチパッドは、間接的なマルチタッチ入力と、マウスのようなポインティング デバイスの精密入力を組み合わせたものです。 この組み合わせにより、タッチパッドはタッチに最適化された UI にも、生産性アプリとデスクトップ環境で使用される一般的に小さなターゲットにも適しています。 タッチ入力用に Windows アプリのデザインを最適化し、既定でタッチパッドのサポートを取得します。

タッチパッドでサポートされている操作エクスペリエンスは複合的なので、[**PointerEntered**](/uwp/api/windows.ui.xaml.uielement.pointerentered) イベントを使って、タッチ入力の組み込みサポートの他にマウス スタイル UI コマンドも提供することをお勧めします。 たとえば、コンテンツをパンするだけでなく、"前へ" ボタンと "次へ" ボタンを使ってコンテンツのページをフリップできるようにします。

このトピックで説明されているジェスチャとガイドラインを利用することで、アプリはタッチパッド入力を最小限のコードでシームレスにサポートできます。

## <a name="the-touchpad-language"></a>タッチパッド言語


システム内では一貫して、タッチパッド操作の簡単なセットが使われます。 アプリをタッチとマウス入力用に最適化すると、ユーザーが慣れている操作感がこの言語によって実現されるので、信頼感が高まり、アプリの習得や使用も簡単になります。

高精度タッチパッドでは、標準のタッチパッドよりはるかに多くのジェスチャや操作の動作を設定できます。 次の 2 つの画像は、それぞれ標準のタッチパッドと高精度タッチパッドのさまざまなタッチパッド設定ページ ([設定] &gt; [デバイス] &gt; [マウスとタッチパッド]) を示しています。

![標準のタッチパッドの設定](images/mouse-touchpad-settings-standard.png)

<sup>標準 \\ タッチパッドの \\ 設定</sup>

![Windows 高精度タッチパッドの設定](images/mouse-touchpad-settings-ptp.png)

<sup>Windows \\ Precision の \\ タッチパッドの \\ 設定</sup>

以下に、一般的なタスクを実行するためのタッチパッドに最適化されたジェスチャの例を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>3 本指でのタップ</p></td>
<td align="left"><p><strong>Cortana</strong> を使って検索、または<strong>アクション センター</strong>を表示するためのユーザー設定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3 本指でのスライド</p></td>
<td align="left"><p>仮想デスクトップのタスク ビュー開く、デスクトップを表示、または開いているアプリを切り替えるためのユーザー設定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1 本指でのタップによるプライマリ操作</p></td>
<td align="left"><p>1 本指を使って要素をタップすると、プライマリ操作 (アプリの起動、コマンドの実行など) が呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2 本指でのタップによる右クリック</p></td>
<td align="left"><p>要素を同時に 2 本の指でタップして、その要素を選択し、状況依存のコマンドを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2 本指でのスライドによるパン</p></td>
<td align="left"><p>スライドは主にパン操作に使われますが、移動、描画、筆記などの操作に使うこともできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ピンチとストレッチによるズーム</p></td>
<td align="left"><p>ピンチ ジェスチャとストレッチ ジェスチャは、通常、サイズ変更とセマンティック ズームに使われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1 本指でのプレスとスライドによる移動</p></td>
<td align="left"><p>要素をドラッグします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1 本指でのプレスとスライドによるテキストの選択</p></td>
<td align="left"><p>選択可能なテキスト内を押してスライドし、選択します。 単語を選択するには、ダブルタップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>左と右のクリック ゾーン</p></td>
<td align="left"><p>マウス デバイスの左ボタンと右ボタンの機能をエミュレートします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="hardware"></a>ハードウェア


マウス デバイス機能 ([**MouseCapabilities**](/uwp/api/Windows.Devices.Input.MouseCapabilities)) を照会して、タッチパッド ハードウェアから直接アクセスできるアプリ UI の要素を識別します。 タッチ入力とマウス入力の両方の UI を用意することをお勧めします。

デバイス機能の照会について詳しくは、「[入力デバイスの識別](identify-input-devices.md)」をご覧ください。

## <a name="visual-feedback"></a>視覚的なフィードバック


-   移動イベントまたはホバー イベントを通じてタッチパッド カーソルが検出されたら、マウス固有の UI を表示して、要素によって公開されている機能を示します。 タッチパッド カーソルが一定の期間動かされなかった場合や、ユーザーがタッチ操作を始めた場合は、タッチパッド UI を徐々に非表示にします。 これにより、UI の簡潔さが保たれます。
-   ホバーのフィードバックにカーソルを使わないでください。要素によるフィードバックで十分です (以下の「カーソル」をご覧ください)。
-   静的テキストなど、要素で対話式操作がサポートされていない場合は、視覚的なフィードバックを返さないでください。
-   タッチパッド操作ではフォーカス用の四角形を使わないでください。 これはキーボード操作専用です。
-   同じ入力対象を表すすべての要素に対して視覚的なフィードバックを同時に表示します。

視覚的なフィードバックに関する一般的なガイダンスについては、「[視覚的なフィードバックのガイドライン](./guidelines-for-visualfeedback.md)」をご覧ください。

## <a name="cursors"></a>カーソル


タッチパッド ポインターとして利用できる標準のカーソル セットが用意されています。 これらが要素のプライマリ操作を示すために使われます。

標準のカーソルには、それぞれ対応する既定の画像が関連付けられています。 ユーザーまたはアプリは、標準のカーソルに関連付けられている既定の画像をいつでも変更できます。 UWP アプリでは、[**PointerCursor**](/uwp/api/windows.ui.core.corewindow.pointercursor) 関数を使用して、カーソル画像を指定します。

マウス カーソルをカスタマイズする必要がある場合は、以下のガイドラインに従ってください。

-   クリック可能な要素には常に矢印カーソル (![矢印カーソル](images/cursor-arrow.png)) を使います。 リンクなどのインタラクティブな要素には手の形のポインティング カーソル (![手の形のポインティング カーソル](images/cursor-pointinghand.png)) を使いません。 代わりに、前に説明したホバー効果を使います。
-   選択可能なテキストにはテキスト カーソル (![テキスト カーソル](images/cursor-text.png)) を使います。
-   ドラッグやトリミングなど、移動がメインの操作である場合は、移動カーソル (![移動カーソル](images/cursor-move.png)) を使います。 スタート画面のタイルなどでのナビゲーションがメインの操作である場合は、要素に対して移動カーソルを使いません。
-   サイズ変更ができるオブジェクトに対しては、横、縦、対角線のサイズ変更カーソル (![縦のサイズ変更カーソル](images/cursor-vertical.png), ![横のサイズ変更カーソル](images/cursor-horizontal.png), ![対角線のサイズ変更カーソル (左下、右上)](images/cursor-diagonal2.png), ![対角線のサイズ変更カーソル (左上、右下)](images/cursor-diagonal1.png)) を使います。
-   地図など、固定キャンバス内のコンテンツのパンを行うときは、手でつかむ形のカーソル (![手でつかむ形のカーソル (開いた状態)](images/cursor-pan1.png), ![手でつかむ形のカーソル (つかんだ状態)](images/cursor-pan2.png)) を使います。

## <a name="related-articles"></a>関連記事

- [ポインター入力の処理](handle-pointer-input.md)
- [入力デバイスの識別](identify-input-devices.md)

### <a name="samples"></a>サンプル

- [基本的な入力のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicInput)
- [待機時間が短い入力のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/LowLatencyInput)
- [ユーザー操作モードのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/UserInteractionMode)
- [フォーカスの視覚効果のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlFocusVisuals)

### <a name="archive-samples"></a>サンプルのアーカイブ

- [入力: デバイス機能のサンプルに関するページ](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Windows%208%20app%20samples/%5BC%23%5D-Windows%208%20app%20samples/C%23/Windows%208%20app%20samples/Input%20Device%20capabilities%20sample%20(Windows%208))
- [入力: XAML ユーザー入力イベントのサンプルに関するページ](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Input%20XAML%20user%20input%20events%20sample)
- [XAML のスクロール、パン、ズームのサンプル](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Universal%20Windows%20app%20samples/111487-Universal%20Windows%20app%20samples/XAML%20scrolling%2C%20panning%2C%20and%20zooming%20sample)
- [入力: GestureRecognizer によるジェスチャと操作](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Input%20Gestures%20and%20manipulations%20with%20GestureRecognizer)
