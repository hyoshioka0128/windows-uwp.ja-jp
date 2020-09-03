---
description: 表示フォーカスは、ユーザーがゲームパッドやキーボードのフォーカスをフォーカス可能な要素に移動したときに、その要素の境界線をアニメーション化する発光効果です。
title: 表示フォーカス
template: detail.hbs
ms.date: 03/01/2018
ms.topic: article
keywords: windows 10, uwp
pm-contact: chphilip
design-contact: ''
dev-contact: stevenki
ms.localizationpriority: medium
ms.openlocfilehash: 6afed2347bb3944c8ea5bd9b43e83d429973dc15
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89169166"
---
# <a name="reveal-focus"></a>表示フォーカス

![ヒーロー イメージ](images/header-reveal-focus.svg)

表示フォーカスは、Xbox One やテレビ画面などの [10 フィート エクスペリエンス](../devices/designing-for-tv.md)を想定した発光効果です。 ユーザーがゲームパッドやキーボードのフォーカスをボタンなどのフォーカス可能な要素に移動したときに、その要素の境界線がアニメーション化されます。 表示フォーカスは既定で無効になっていますが、簡単に有効にできます。 

(対話型要素を発光効果で強調する表示ハイライト効果については、「[表示ハイライト](./reveal.md)」の記事をご覧ください。)


> **重要な API**:[Application.FocusVisualKind プロパティ](/uwp/api/windows.ui.xaml.application.FocusVisualKind)、[FocusVisualKind 列挙型](/uwp/api/windows.ui.xaml.focusvisualkind)、[Control.UseSystemFocusVisuals プロパティ](/uwp/api/Windows.UI.Xaml.Controls.Control.UseSystemFocusVisuals)

## <a name="how-it-works"></a>しくみ
表示フォーカスでは、フォーカスが置かれた要素に注意が向くように、要素の境界線の周囲にアニメーション化されたグロー (蛍光ライト効果) が追加されます。

![表示のビジュアル効果](images/traveling-focus-fullscreen-light-rf.gif)

この効果は、ユーザーがテレビ画面全体を注視していない場合のような 10 フィート シナリオで特に便利です。 

## <a name="examples"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合は、こちらをクリックして<a href="xamlcontrolsgallery:/item/RevealFocus">アプリを開き、表示フォーカスの動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

## <a name="how-to-use-it"></a>使用方法

既定では、表示フォーカスは無効になっています。 有効にするには、次の手順を実行します。
1. アプリのコンストラクターで、[AnalyticsInfo.VersionInfo.DeviceFamily](/uwp/api/windows.system.profile.analyticsversioninfo.DeviceFamily) プロパティを呼び出し、現在のデバイス ファミリが `Windows.Xbox` かどうかを調べます。
2. デバイス ファミリが `Windows.Xbox` である場合は、[Application.FocusVisualKind](/uwp/api/windows.ui.xaml.application.FocusVisualKind) プロパティを `FocusVisualKind.Reveal` に設定します。 

```csharp
    if(AnalyticsInfo.VersionInfo.DeviceFamily == "Windows.Xbox")
    {
        this.FocusVisualKind = FocusVisualKind.Reveal;
    }
```

**FocusVisualKind** プロパティを設定すると、[UseSystemFocusVisuals](/uwp/api/Windows.UI.Xaml.Controls.Control.UseSystemFocusVisuals) プロパティが **True** (ほとんどのコントロールの既定値) に設定されているすべてのコントロールに対して、表示フォーカス効果がシステムによって自動的に適用されます。 

## <a name="why-isnt-reveal-focus-on-by-default"></a>表示フォーカスが既定で有効になっていない理由 
ご覧のように、Xbox での実行中であるとアプリが検出した場合は、表示フォーカスを有効にすることは非常に簡単です。 それでは、システムによって自動的に有効にならないのはなぜでしょうか。 表示フォーカスを使用すると、フォーカスの視覚効果のサイズが増加し、UI レイアウトに問題が発生する可能性があります。 場合によっては、表示フォーカス効果をカスタマイズし、アプリに合わせて最適化する必要があります。

## <a name="customizing-reveal-focus"></a>表示フォーカスのカスタマイズ

表示フォーカス効果は、各コントロールのフォーカス視覚効果プロパティ ([FocusVisualPrimaryThickness](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualPrimaryThickness)、[FocusVisualSecondaryThickness](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualSecondaryThickness)、[FocusVisualPrimaryBrush](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualPrimaryBrush)、[FocusVisualSecondaryBrush](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualSecondaryBrush)) を変更することによってカスタマイズできます。 これらのプロパティでは、フォーカスの四角形の色と太さをカスタマイズできます。 (これらは、[視認性の高いフォーカスの視覚効果](../input/guidelines-for-visualfeedback.md#high-visibility-focus-visuals)を作成する場合と同じプロパティです。) 

カスタマイズを開始する前に、表示フォーカスを構成しているコンポーネントについてもう少し詳しく知っておくと便利です。

既定の表示フォーカス視覚効果は、プライマリ境界線、セカンダリ境界線、表示グローという 3 つの部分で構成されています。 プライマリ境界線は、**2 px** の幅があり、セカンダリ境界線の*外側*に描画されます。 セカンダリ境界線は、**1 px** の幅があり、プライマリ境界線の*内側*に描画されます。 表示フォーカスのグロー部分は、プライマリ境界線の幅に比例した幅があり、プライマリ境界線の*外側*に描画されます。

静的な要素に加えて、表示フォーカスの視覚効果では、アニメーション化された光が使用されます。この光は、フォーカスの停止中は振動し、フォーカスの移動時にはフォーカス方向に移動します。

![表示フォーカス レイヤー](images/reveal-breakdown.svg)

## <a name="customize-the-border-thickness"></a>境界線の幅のカスタマイズ

コントロールの境界線の種類ごとに幅を変更するには、以下のプロパティを使用します。

| 境界線の種類 | プロパティ |
| --- | --- |
| プライマリ、グロー   | [FocusVisualPrimaryThickness](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualPrimaryThickness)<br/> (プライマリ境界線を変更すると、グロー部分の幅も比例して変化します。)   |
| セカンダリ   | [FocusVisualSecondaryThickness](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualSecondaryThickness)   |


この例では、ボタンのフォーカス視覚効果で、境界線の幅を変更しています。

```xaml
<Button FocusVisualPrimaryThickness="2" FocusVisualSecondaryThickness="1"/>
```

## <a name="customize-the-margin"></a>余白のカスタマイズ

余白とは、コントロールの視覚的な境界線と、フォーカスの視覚効果で示されるセカンダリ境界線の開始点との間にあるスペースです。 既定の余白は、コントロールの境界線から 1 px の幅になります。 この余白は、[FocusVisualMargin](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualMargin) プロパティを変更することでコントロールごとに変更できます。

```xaml
<Button FocusVisualPrimaryThickness="2" FocusVisualSecondaryThickness="1" FocusVisualMargin="-3"/>
```

余白が負の値の場合は境界線がコントロールの中央から遠くなり、正の値の場合はコントロールの中央に近くなります。

## <a name="customize-the-color"></a>色のカスタマイズ

表示フォーカス視覚効果の色を変更するには、[FocusVisualPrimaryBrush](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualPrimaryBrush) プロパティと [FocusVisualSecondaryBrush](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualSecondaryBrush) プロパティを使用します。

| プロパティ | 既定のリソース | 既定のリソースの値 |
| ---- | ---- | --- | 
| [FocusVisualPrimaryBrush](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualPrimaryBrush) | SystemControlRevealFocusVisualBrush  | SystemAccentColor |
| [FocusVisualSecondaryBrush](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualSecondaryBrush)  | SystemControlFocusVisualSecondaryBrush  | SystemAltMediumColor |

(FocusPrimaryBrush プロパティに既定の **SystemControlRevealFocusVisualBrush** リソースが使用されるのは、**FocusVisualKind** が **Reveal** に設定されている場合のみです。 それ以外の場合は、**SystemControlFocusVisualPrimaryBrush** が使用されます。)


個々のコントロールのフォーカス視覚効果の色を変更するには、コントロールのプロパティを直接設定します。 次の例では、ボタンのフォーカス視覚効果の色を上書きしています。

```xaml

<!-- Specifying a color directly -->
<Button
    FocusVisualPrimaryBrush="DarkRed"
    FocusVisualSecondaryBrush="Pink"/>

<!-- Using theme resources -->
<Button
    FocusVisualPrimaryBrush="{ThemeResource SystemBaseHighColor}"
    FocusVisualSecondaryBrush="{ThemeResource SystemAccentColor}"/>    
```

アプリ全体ですべてのフォーカス視覚効果の色を変更するには、**SystemControlRevealFocusVisualBrush** リソースと **SystemControlFocusVisualSecondaryBrush** リソースを独自定義で上書きします。

```xaml
<!-- App.xaml -->
<Application.Resources>

    <!-- Override Reveal Focus default resources. -->
    <SolidColorBrush x:Key="SystemControlRevealFocusVisualBrush" Color="{ThemeResource SystemBaseHighColor}"/>
    <SolidColorBrush x:Key="SystemControlFocusVisualSecondaryBrush" Color="{ThemeResource SystemAccentColor}"/>
</Application.Resources>
```

フォーカス視覚効果の色の変更について詳しくは、「[色のブランド化とカスタマイズ](../input/guidelines-for-visualfeedback.md#color-branding--customizing)」をご覧ください。


## <a name="show-just-the-glow"></a>グロー部分のみを表示する

プライマリまたはセカンダリのフォーカス視覚効果は使用せず、グローのみを使用する場合は、コントロールの [FocusVisualPrimaryBrush](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualPrimaryBrush) プロパティを `Transparent` に設定し、[FocusVisualSecondaryThickness](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualSecondaryThickness) を `0` に設定します。 この場合は、グローにコントロールの背景色が使用され、境界線がない外観になります。 [FocusVisualPrimaryThickness](/uwp/api/windows.ui.xaml.frameworkelement.FocusVisualPrimaryThickness) を使用して、グローの幅を変更することもできます。

```xaml

<!-- Show just the glow -->
<Button
    FocusVisualPrimaryBrush="Transparent"
    FocusVisualSecondaryThickness="0" />    
```


## <a name="use-your-own-focus-visuals"></a>独自のフォーカス視覚効果を使用する

表示フォーカスをカスタマイズするもう 1 つの方法は、表示状態を使って独自のフォーカス表示効果を描画することにより、システムから提供されるフォーカス表示効果を除外することです。 詳しくは、[フォーカスの視覚効果のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlFocusVisuals)をご覧ください。


## <a name="reveal-focus-and-the-fluent-design-system"></a>表示フォーカスと Fluent Design System

表示フォーカスは、アプリに発光効果を加える Fluent Design System コンポーネントです。 Fluent Design System およびその他のコンポーネントについて詳しくは、[Fluent Design の概要](/windows/apps/fluent-design-system)をご覧ください。

## <a name="related-articles"></a>関連記事

- [表示ハイライト](./reveal.md)
- [Xbox およびテレビ向け設計](../devices/designing-for-tv.md)
- [ゲームパッドとリモコンの操作](../input/gamepad-and-remote-interactions.md)
- [フォーカスの視覚効果のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlFocusVisuals)
- [コンポジション効果](../../composition/composition-effects.md)
- [システムの科学:Fluent Design と奥行き](https://medium.com/microsoft-design/science-in-the-system-fluent-design-and-depth-fb6d0f23a53f)
- [システムの科学:Fluent Design と明るさ](https://medium.com/microsoft-design/the-science-in-the-system-fluent-design-and-light-94a17e0b3a4f)