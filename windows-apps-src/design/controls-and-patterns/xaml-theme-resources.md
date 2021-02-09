---
description: XAML のテーマ リソースは、アクティブなシステム テーマに応じて異なる値を適用するリソースのセットです。
MS-HAID: dev\_ctrl\_layout\_txt.xaml\_theme\_resources
MSHAttr: PreferredLib:/library/windows/apps
Search.Product: eADQiWindows 10XVcnh
title: XAML テーマ リソース
ms.assetid: 41B87DBF-E7A2-44E9-BEBA-AF6EEBABB81B
label: XAML theme resources
template: detail.hbs
ms.date: 09/24/2020
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 6da668c005f95d51f6fb0588f60fdcf63aea4fd7
ms.sourcegitcommit: a3bbd3dd13be5d2f8a2793717adf4276840ee17d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93034425"
---
# <a name="xaml-theme-resources"></a>XAML テーマ リソース

XAML のテーマ リソースは、アクティブなシステム テーマに応じて異なる値を適用するリソースのセットです。 XAML フレームワークでは、3 つのテーマがサポートされています。"Light"、"Dark"、および "HighContrast" です。

**前提条件** :このトピックでは、既に「 [ResourceDictionary と XAML リソースの参照](resourcedictionary-and-xaml-resource-references.md)」を読んでいることを前提としています。

## <a name="theme-resources-v-static-resources"></a>テーマ リソース v 静的なリソース

既存の XAML リソース ディクショナリから XAML リソースを参照できる XAML マークアップ拡張には、[{StaticResource} マークアップ拡張](../../xaml-platform/staticresource-markup-extension.md)と [{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)の 2 つがあります。

[{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)はアプリの読み込み時に評価され、その後、実行時にテーマが変更されたときにもそのつど評価されます。 これは通常、ユーザーがデバイスの設定を変更した場合、またはアプリ内でプログラムによってアプリの現在のテーマが変更された場合に発生します。

これに対して [{StaticResource} マークアップ拡張](../../xaml-platform/staticresource-markup-extension.md)は、XAML が最初にアプリに読み込まれるときにのみ評価されます。 これが更新されることはありません。 これは、アプリの起動時に XAML を検索し、実際のランタイム値に置き換えるようなものです。

## <a name="theme-resources-in-the-resource-dictionary-structure"></a>リソース ディクショナリ構造でのテーマ リソース

各テーマ リソースは、XAML ファイル themeresources.xaml の一部です。 設計の目的には、Windows ソフトウェア開発キット (SDK) のインストール先の \\(プログラム ファイル)\\Windows Kits\\10\\DesignTime\\CommonConfiguration\\Neutral\\UAP\\&lt;SDK version&gt;\\Generic フォルダーにある themeresources.xaml を使うことができます。 themeresources.xaml 内のリソース ディクショナリは、同じディレクトリの generic.xaml にも複製されています。

これらの物理ファイルは Windows ランタイムでランタイム検索に使われません。 そのため、明示的に DesignTime フォルダー内にあり、既定ではアプリにコピーされません。 代わりに、これらのリソース ディクショナリは Windows ランタイム自体の一部としてメモリ内に存在し、テーマ リソース (またはシステム リソース) へのアプリの XAML リソース参照は実行時にメモリ内で解決されます。

## <a name="guidelines-for-custom-theme-resources"></a>カスタム テーマ リソースのガイドライン

独自のカスタム テーマ リソースを定義して使うときは、次のガイドラインに従ってください。

- "HighContrast" ディクショナリに加えて、"Light" と "Dark" の両方のテーマ ディクショナリを指定します。 "Default" をキーとする [ResourceDictionary](/uwp/api/Windows.UI.Xaml.ResourceDictionary) を作成することもできますが、明示的に "Light"、"Dark"、"HighContrast" を使うことをお勧めします。

- [{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)を次で使用します:スタイル、セッター、コントロール テンプレート、プロパティ セッター、アニメーション。

- [ThemeDictionaries](/uwp/api/windows.ui.xaml.resourcedictionary.themedictionaries) 内のリソース定義では、[{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md) を使わないでください。 代わりに、[{StaticResource} マークアップ拡張](../../xaml-platform/staticresource-markup-extension.md)を使います。

    例外:[ThemeDictionaries](/uwp/api/windows.ui.xaml.resourcedictionary.themedictionaries) 内のアプリ テーマに依存しないリソースを参照するために [{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)を使うことができます。 このようなリソースの例として、`SystemAccentColor` などのアクセント カラー リソースや、通常は "SystemColor" というプレフィックスの付いた `SystemColorButtonFaceColor` などのシステム カラー リソースがあります。

> [!CAUTION]
> これらのガイドラインに従わないと、テーマに関連する予期しない動作がアプリで発生することがあります。 詳しくは、「[テーマ リソースのトラブルシューティング](#troubleshooting-theme-resources)」セクションをご覧ください。

## <a name="the-xaml-color-ramp-and-theme-dependent-brushes"></a>XAML 色見本とテーマ依存のブラシ

XAML における *Windows 色見本* は、"Light"、"Dark"、"HighContrast" の各テーマの色のセットを組み合わせることで構成されます。 システム テーマを変更する場合でも、システム テーマを独自の XAML 要素に適用する場合でも、カラー リソースがどのように構成されるかを理解することが重要です。

Windows アプリで色を適用する方法について詳しくは、[Windows アプリでの色使い](../style/color.md)に関する記事をご覧ください。

### <a name="light-and-dark-theme-colors"></a>Light テーマと Dark テーマの色

XAML フレームワークには、"Light" と "Dark" のテーマに合わせてカスタマイズされた名前付きの [Color](/uwp/api/Windows.UI.Color) リソースのセットが用意されています。 これらを参照するために使うキーは、`System[Simple Light/Dark Name]Color` という名前付け形式に従います。

次の表は、XAML フレームワークで提供されている "Light" と "Dark" のリソースについて、(\#aarrggbb の形式を使用して) 色のキー、簡易名、文字列表現を一覧にしたものです。 キーは、アプリでリソースを参照するときに使われます。 "Light/Dark 簡易名" は、後で説明するブラシの名前付け規則の一部として使われます。

| キー                             | Light/Dark 簡易名 | 淡色      | 濃色       |
|---------------------------------|------------------------|------------|------------|
| SystemAltHighColor              | AltHigh                | \#FFFFFFFF | \#FF000000 |
| SystemAltLowColor               | AltLow                 | \#33FFFFFF | \#33000000 |
| SystemAltMediumColor            | AltMedium              | \#99FFFFFF | \#99000000 |
| SystemAltMediumHighColor        | AltMediumHigh          | \#CCFFFFFF | \#CC000000 |
| SystemAltMediumLowColor         | AltMediumLow           | \#66FFFFFF | \#66000000 |
| SystemBaseHighColor             | BaseHigh               | \#FF000000 | \#FFFFFFFF |
| SystemBaseLowColor              | BaseLow                | \#33000000 | \#33FFFFFF |
| SystemBaseMediumColor           | BaseMedium             | \#99000000 | \#99FFFFFF |
| SystemBaseMediumHighColor       | BaseMediumHigh         | \#CC000000 | \#CCFFFFFF |
| SystemBaseMediumLowColor        | BaseMediumLow          | \#66000000 | \#66FFFFFF |
| SystemChromeAltLowColor         | ChromeAltLow           | \#FF171717 | \#FFF2F2F2 |
| SystemChromeBlackHighColor      | ChromeBlackHigh        | \#FF000000 | \#FF000000 |
| SystemChromeBlackLowColor       | ChromeBlackLow         | \#33000000 | \#33000000 |
| SystemChromeBlackMediumLowColor | ChromeBlackMediumLow   | \#66000000 | \#66000000 |
| SystemChromeBlackMediumColor    | ChromeBlackMedium      | \#CC000000 | \#CC000000 |
| SystemChromeDisabledHighColor   | ChromeDisabledHigh     | \#FFCCCCCC | \#FF333333 |
| SystemChromeDisabledLowColor    | ChromeDisabledLow      | \#FF7A7A7A | \#FF858585 |
| SystemChromeHighColor           | ChromeHigh             | \#FFCCCCCC | \#FF767676 |
| SystemChromeLowColor            | ChromeLow              | \#FFF2F2F2 | \#FF171717 |
| SystemChromeMediumColor         | ChromeMedium           | \#FFE6E6E6 | \#FF1F1F1F |
| SystemChromeMediumLowColor      | ChromeMediumLow        | \#FFF2F2F2 | \#FF2B2B2B |
| SystemChromeWhiteColor          | ChromeWhite            | \#FFFFFFFF | \#FFFFFFFF |
| SystemListLowColor              | ListLow                | \#19000000 | \#19FFFFFF |
| SystemListMediumColor           | ListMedium             | \#33000000 | \#33FFFFFF |

:::row:::
    :::column:::
        #### <a name="light-theme"></a>淡色テーマ
    :::column-end:::
    :::column:::
        #### <a name="dark-theme"></a>濃色テーマ
    :::column-end:::
:::row-end:::

#### <a name="base"></a>ベース

:::row:::
    :::column:::
        ![淡色テーマ (基本)](images/themes/light-base.png)
    :::column-end:::
    :::column:::
        ![濃色テーマ (基本)](images/themes/dark-base.png)
    :::column-end:::
:::row-end:::

#### <a name="alt"></a>Alt

:::row:::
    :::column:::
        ![淡色テーマ (代替)](images/themes/light-alt.png)
    :::column-end:::
    :::column:::
        ![濃色テーマ (代替)](images/themes/dark-alt.png)
    :::column-end:::
:::row-end:::

#### <a name="list"></a>List

:::row:::
    :::column:::
        ![淡色テーマ (リスト)](images/themes/light-list.png)
    :::column-end:::
    :::column:::
        ![濃色テーマ (リスト)](images/themes/dark-list.png)
    :::column-end:::
:::row-end:::

#### <a name="chrome"></a>クロム

:::row:::
    :::column:::
        ![淡色テーマ (クロム)](images/themes/light-chrome.png)
    :::column-end:::
    :::column:::
        ![濃色テーマ (クロム)](images/themes/dark-chrome.png)
    :::column-end:::
:::row-end:::

### <a name="windows-system-high-contrast-colors"></a>Windows システムのハイ コントラストの色

XAML フレームワークによって提供されるリソースのセットのほかに、Windows のシステム パレットから派生するカラー値のセットがあります。 これらの色は、Windows ランタイムや Windows アプリに固有のものではありません。 しかし、"HighContrast" テーマでシステムが動作しているとき (およびアプリが実行されているとき) には、XAML [Brush](/uwp/api/Windows.UI.Xaml.Media.Brush) リソースの多くでこれらの色が使われます。 XAML フレームワークには、このようなシステム全体の色がキーを持つリソースとして用意されています。 これらのキーは、`SystemColor[name]Color` という名前付け形式に従います。

次の表は、Windows システム パレットから派生したリソース オブジェクトとして XAML に用意されているシステム全体の色を示します。 "簡単操作での名前" 列は、その色が Windows の設定の UI でどのように表現されるかを示しています。 "HighContrast 簡易名" 列は、その色が XAML コモン コントロールにどのように適用されるかをひとことで表す単語になっています。 これは、後で説明するブラシの名前付け規則の一部として使われます。 "初期既定値" 列は、システムがハイ コントラストで動作していない場合に使われる値を示します。

| キー                           | 簡単操作での名前            | HighContrast 簡易名 | 初期既定値 |
|-------------------------------|--------------------------------|--------------------------|-----------------|
| SystemColorButtonFaceColor    | **ボタン テキスト** (背景)   | 背景               | \#FFF0F0F0      |
| SystemColorButtonTextColor    | **ボタン テキスト** (前景)   | フォアグラウンド               | \#FF000000      |
| SystemColorGrayTextColor      | **選択不可のテキスト**              | 無効                 | \#FF6D6D6D      |
| SystemColorHighlightColor     | **選択されたテキスト** (背景) | 強調表示                | \#FF3399FF      |
| SystemColorHighlightTextColor | **選択されたテキスト** (前景) | HighlightAlt             | \#FFFFFFFF      |
| SystemColorHotlightColor      | **ハイパーリンク**                 | ハイパーリンク                | \#FF0066CC      |
| SystemColorWindowColor        | **背景**                 | PageBackground           | \#FFFFFFFF      |
| SystemColorWindowTextColor    | **テキスト**                       | PageText                 | \#FF000000      |

Windows には複数のハイ コントラスト テーマが用意されているほか、次のように、コンピューターの簡単操作を通じて、独自のハイ コントラスト設定で使う特定の色をユーザーが設定することもできます。 このため、ハイ コントラストのカラー値の確定的な一覧を提供することはできません。

![Windows のハイ コントラストの設定 UI](images/high-contrast-settings.png)

ハイ コントラスト テーマのサポートについて詳しくは、「[ハイ コントラスト テーマ](../accessibility/high-contrast-themes.md)」をご覧ください。

### <a name="system-accent-color"></a>システムのアクセント カラー

システムのハイ コントラスト テーマの色に加えて、システムのアクセント カラーも、`SystemAccentColor` というキーを使う特別なカラー リソースとして用意されています。 このリソースは、ユーザーが Windows の個人設定でアクセント カラーとして指定した色を実行時に取得します。

> [!NOTE]
> システム カラー リソースをオーバーライドすることもできますが、特にハイ コントラスト設定については、ユーザーによる色の選択を尊重することをお勧めします。

### <a name="theme-dependent-brushes"></a>テーマ依存のブラシ

システム テーマ リソース ディクショナリの [SolidColorBrush](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) リソースの [Color](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush.Color) プロパティは、前のセクションに示したカラー リソースを使って設定されます。 XAML 要素に色を適用するには、ブラシ リソースが使われます。 ブラシ リソースのキーは、`SystemControl[Simple HighContrast name][Simple light/dark name]Brush` という名前付け形式に従います。 たとえば、`SystemControlBackgroundAltHighBrush` のように指定します。

このブラシの色の値が実行時にどのように決定されるかを見てみましょう。 "Light" と "Dark" の各リソース ディクショナリでは、このブラシは次のように定義されています。

`<SolidColorBrush x:Key="SystemControlBackgroundAltHighBrush" Color="{StaticResource SystemAltHighColor}"/>`

"HighContrast" リソース ディクショナリでは、このブラシは次のように定義されています。

`<SolidColorBrush x:Key="SystemControlBackgroundAltHighBrush" Color="{ThemeResource SystemColorButtonFaceColor}"/>`

このブラシが XAML 要素に適用されるとき、その色は、次の表に示すように現在のテーマによって実行時に決定されます。

| Theme        | 色の簡易名 | カラー リソース             | ランタイム値                                              |
|--------------|-------------------|----------------------------|------------------------------------------------------------|
| 淡色        | AltHigh           | SystemAltHighColor         | \#FFFFFFFF                                                 |
| 濃色         | AltHigh           | SystemAltHighColor         | \#FF000000                                                 |
| HighContrast | 背景        | SystemColorButtonFaceColor | 設定でボタンの背景として指定された色。 |

独自の XAML 要素に適用するブラシを決めるには、`SystemControl[Simple HighContrast name][Simple light/dark name]Brush` という名前付けスキームを使います。

<!--
For many examples of how the brushes are used in the XAML control templates, see the [Default control styles and templates](default-control-styles-and-templates.md).
-->

> [!NOTE]
> \[*HighContrast 簡易名*\]\[*Light/Dark 簡易名*\]のすべての組み合わせがブラシ リソースとして提供されているわけではありません。

## <a name="the-xaml-type-ramp"></a>XAML の書体見本

themeresources.xaml ファイルには、UI 上のテキスト コンテナー (具体的には [TextBlock](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) または [RichTextBlock](/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock)) に適用できる [Style](/uwp/api/Windows.UI.Xaml.Style) を定義するリソースがいくつか定義されています。 これらは、既定の暗黙的なスタイルとは異なります。 これらのスタイルを使うと、「 [フォントのガイドライン](../style/typography.md)」で説明されている *Windows の書体見本* に一致する XAML UI 定義を簡単に作成できるようになります。

これらのスタイルは、テキスト コンテナー全体に適用されるテキスト属性を設定するものです。 テキストの一部にのみスタイルを適用する場合は、コンテナー内のテキスト要素に属性を設定します。たとえば、[TextBlock.Inlines](/uwp/api/windows.ui.xaml.controls.textblock.inlines) の [Run](/uwp/api/Windows.UI.Xaml.Documents.Run) や [RichTextBlock.Blocks](/uwp/api/windows.ui.xaml.controls.richtextblock.blocks) の [Paragraph](/uwp/api/Windows.UI.Xaml.Documents.Paragraph) を使うことができます。

スタイルを [TextBlock](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) に適用すると、次のようになります。

![テキスト ブロック スタイル](../style/images/type/text-block-type-ramp.svg)

```XAML
<TextBlock Text="Header" Style="{StaticResource HeaderTextBlockStyle}"/>
<TextBlock Text="SubHeader" Style="{StaticResource SubheaderTextBlockStyle}"/>
<TextBlock Text="Title" Style="{StaticResource TitleTextBlockStyle}"/>
<TextBlock Text="SubTitle" Style="{StaticResource SubtitleTextBlockStyle}"/>
<TextBlock Text="Base" Style="{StaticResource BaseTextBlockStyle}"/>
<TextBlock Text="Body" Style="{StaticResource BodyTextBlockStyle}"/>
<TextBlock Text="Caption" Style="{StaticResource CaptionTextBlockStyle}"/>
```

アプリで Windows 書体見本を使用する方法のガイダンスについては、「[Windows アプリの文字体裁](../style/typography.md)」をご覧ください。

### <a name="basetextblockstyle"></a>BaseTextBlockStyle

**TargetType** : [TextBlock](/uwp/api/Windows.UI.Xaml.Controls.TextBlock)

他のすべての [TextBlock](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) コンテナー スタイルに対する一般的なプロパティを提供します。

```XAML
<!-- Usage -->
<TextBlock Text="Base" Style="{StaticResource BaseTextBlockStyle}"/>

<!-- Style definition -->
<Style x:Key="BaseTextBlockStyle" TargetType="TextBlock">
    <Setter Property="FontFamily" Value="Segoe UI"/>
    <Setter Property="FontWeight" Value="SemiBold"/>
    <Setter Property="FontSize" Value="14"/>
    <Setter Property="TextTrimming" Value="None"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="LineStackingStrategy" Value="MaxHeight"/>
    <Setter Property="TextLineBounds" Value="Full"/>
</Style>
```

### <a name="headertextblockstyle"></a>HeaderTextBlockStyle

```XAML
<!-- Usage -->
<TextBlock Text="Header" Style="{StaticResource HeaderTextBlockStyle}"/>

<!-- Style definition -->
<Style x:Key="HeaderTextBlockStyle" TargetType="TextBlock"
       BasedOn="{StaticResource BaseTextBlockStyle}">
    <Setter Property="FontSize" Value="46"/>
    <Setter Property="FontWeight" Value="Light"/>
    <Setter Property="OpticalMarginAlignment" Value="TrimSideBearings"/>
</Style>
```

### <a name="subheadertextblockstyle"></a>SubheaderTextBlockStyle

```XAML
<!-- Usage -->
<TextBlock Text="SubHeader" Style="{StaticResource SubheaderTextBlockStyle}"/>

<!-- Style definition -->
<Style x:Key="SubheaderTextBlockStyle" TargetType="TextBlock" 
       BasedOn="{StaticResource BaseTextBlockStyle}">
    <Setter Property="FontSize" Value="34"/>
    <Setter Property="FontWeight" Value="Light"/>
    <Setter Property="OpticalMarginAlignment" Value="TrimSideBearings"/>
</Style>
```

### <a name="titletextblockstyle"></a>TitleTextBlockStyle

```XAML
<!-- Usage -->
<TextBlock Text="Title" Style="{StaticResource TitleTextBlockStyle}"/>

<!-- Style definition -->
<Style x:Key="TitleTextBlockStyle" TargetType="TextBlock" 
       BasedOn="{StaticResource BaseTextBlockStyle}">
    <Setter Property="FontWeight" Value="SemiLight"/>
    <Setter Property="FontSize" Value="24"/>
    <Setter Property="OpticalMarginAlignment" Value="TrimSideBearings"/>
</Style>
```

### <a name="subtitletextblockstyle"></a>SubtitleTextBlockStyle

```XAML
<!-- Usage -->
<TextBlock Text="SubTitle" Style="{StaticResource SubtitleTextBlockStyle}"/>

<!-- Style definition -->
<Style x:Key="SubtitleTextBlockStyle" TargetType="TextBlock" 
       BasedOn="{StaticResource BaseTextBlockStyle}">
    <Setter Property="FontWeight" Value="Normal"/>
    <Setter Property="FontSize" Value="20"/>
    <Setter Property="OpticalMarginAlignment" Value="TrimSideBearings"/>
</Style>
```

### <a name="bodytextblockstyle"></a>BodyTextBlockStyle

```XAML
<!-- Usage -->
<TextBlock Text="Body" Style="{StaticResource BodyTextBlockStyle}"/>

<!-- Style definition -->
<Style x:Key="BodyTextBlockStyle" TargetType="TextBlock" 
       BasedOn="{StaticResource BaseTextBlockStyle}">
    <Setter Property="FontWeight" Value="Normal"/>
    <Setter Property="FontSize" Value="14"/>
</Style>
```

### <a name="captiontextblockstyle"></a>CaptionTextBlockStyle

```XAML
<!-- Usage -->
<TextBlock Text="Caption" Style="{StaticResource CaptionTextBlockStyle}"/>

<!-- Style definition -->
<Style x:Key="CaptionTextBlockStyle" TargetType="TextBlock" 
       BasedOn="{StaticResource BaseTextBlockStyle}">
    <Setter Property="FontSize" Value="12"/>
    <Setter Property="FontWeight" Value="Normal"/>
</Style>
```

### <a name="baserichtextblockstyle"></a>BaseRichTextBlockStyle

**TargetType** : [RichTextBlock](/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock)

他のすべての [RichTextBlock](/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock) コンテナー スタイルに対する一般的なプロパティを提供します。

```XAML
<!-- Usage -->
<RichTextBlock Style="{StaticResource BaseRichTextBlockStyle}">
    <Paragraph>Rich text.</Paragraph>
</RichTextBlock>

<!-- Style definition -->
<Style x:Key="BaseRichTextBlockStyle" TargetType="RichTextBlock">
    <Setter Property="FontFamily" Value="Segoe UI"/>
    <Setter Property="FontWeight" Value="SemiBold"/>
    <Setter Property="FontSize" Value="14"/>
    <Setter Property="TextTrimming" Value="None"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="LineStackingStrategy" Value="MaxHeight"/>
    <Setter Property="TextLineBounds" Value="Full"/>
    <Setter Property="OpticalMarginAlignment" Value="TrimSideBearings"/>
</Style>
```

### <a name="bodyrichtextblockstyle"></a>BodyRichTextBlockStyle

```XAML
<!-- Usage -->
<RichTextBlock Style="{StaticResource BodyRichTextBlockStyle}">
    <Paragraph>Rich text.</Paragraph>
</RichTextBlock>

<!-- Style definition -->
<Style x:Key="BodyRichTextBlockStyle" TargetType="RichTextBlock" BasedOn="{StaticResource BaseRichTextBlockStyle}">
    <Setter Property="FontWeight" Value="Normal"/>
</Style>
```

**注** :   [RichTextBlock](/uwp/api/Windows.UI.Xaml.Controls.RichTextBlock) スタイルには、 [TextBlock](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) に含まれているテキスト見本スタイルのすべては含まれていません。これは主に、 **RichTextBlock** のブロック ベースのドキュメント オブジェクト モデルでは、個々のテキスト要素への属性の設定がより簡単になっているためです。 また、XAML コンテンツ プロパティを使って [TextBlock.Text](/uwp/api/windows.ui.xaml.controls.textblock.text) を設定する方式では、スタイルを設定できるテキスト要素が存在しない状況になるため、コンテナーにスタイルを設定する必要があります。 これに対して **RichTextBlock** では、テキスト コンテンツは常に [Paragraph](/uwp/api/Windows.UI.Xaml.Documents.Paragraph) などの固有のテキスト要素になり、そこにページ ヘッダーやページ サブヘッダー、類似のテキスト見本定義の XAML スタイルを適用できるため、この問題はありません。

## <a name="miscellaneous-named-styles"></a>その他の名前付きスタイル

[Button](/uwp/api/Windows.UI.Xaml.Controls.Button) には、キーを持つ [Style](/uwp/api/Windows.UI.Xaml.Style) 定義の追加のセットを適用することもできます。これにより、既定の暗黙的なスタイルとは異なるスタイルを設定できます。

### <a name="textblockbuttonstyle"></a>TextBlockButtonStyle

**TargetType** : [ButtonBase](/uwp/api/Windows.UI.Xaml.Controls.Primitives.ButtonBase)

ユーザーがクリックしてアクションを実行できるテキストを表示する必要がある場合は、このスタイルを [Button](/uwp/api/Windows.UI.Xaml.Controls.Button) に適用します。 このテキストには、対話型であることがわかるように現在のアクセント カラーを使ったスタイルが設定され、テキストに適したフォーカス四角形が表示されます。 [HyperlinkButton](/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton) の暗黙的なスタイルとは異なり、 **TextBlockButtonStyle** のテキストには下線は付きません。

このテンプレートは、表示テキストにもスタイルを設定して、 **SystemControlHyperlinkBaseMediumBrush** ("PointerOver" 状態の場合)、 **SystemControlHighlightBaseMediumLowBrush** ("Pressed" 状態の場合)、 **SystemControlDisabledBaseLowBrush** ("Disabled" 状態の場合) が使われるようにします。

**TextBlockButtonStyle** リソースを適用した [Button](/uwp/api/Windows.UI.Xaml.Controls.Button) の例を以下に示します。

```XAML
<Button Content="Clickable text" Style="{StaticResource TextBlockButtonStyle}"
        Click="Button_Click"/>
```

これは、次のように表示されます。

![テキストのような外観にスタイル設定されたボタン](images/styles-textblock-button-style.png)

### <a name="navigationbackbuttonnormalstyle"></a>NavigationBackButtonNormalStyle

**TargetType** : [ボタン](/uwp/api/Windows.UI.Xaml.Controls.Button)

この [Style](/uwp/api/Windows.UI.Xaml.Style) は、ナビゲーション アプリの戻るボタンとして使うことができる [Button](/uwp/api/Windows.UI.Xaml.Controls.Button) 用の完全なテンプレートを提供します。 既定の寸法は 40 x 40 ピクセルです。 スタイルを調整するには、 **Button** の [Height](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height)、 [Width](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width)、 [FontSize](/uwp/api/windows.ui.xaml.controls.control.fontsize)、その他のプロパティを明示的に設定するか、 [BasedOn](/uwp/api/windows.ui.xaml.style.basedon) を使って派生スタイルを作成します。

**NavigationBackButtonNormalStyle** リソースを適用した [Button](/uwp/api/Windows.UI.Xaml.Controls.Button) の例を以下に示します。

```XAML
<Button Style="{StaticResource NavigationBackButtonNormalStyle}" />
```

これは、次のように表示されます。

!["戻る" ボタンとしてスタイル設定されたボタン](images/styles-back-button-normal.png)

### <a name="navigationbackbuttonsmallstyle"></a>NavigationBackButtonSmallStyle

**TargetType** : [ボタン](/uwp/api/Windows.UI.Xaml.Controls.Button)

この [Style](/uwp/api/Windows.UI.Xaml.Style) は、ナビゲーション アプリの戻るボタンとして使うことができる [Button](/uwp/api/Windows.UI.Xaml.Controls.Button) 用の完全なテンプレートを提供します。 **NavigationBackButtonNormalStyle** と同様ですが、寸法は 30 x 30 ピクセルになります。

**NavigationBackButtonSmallStyle** リソースを適用した [Button](/uwp/api/Windows.UI.Xaml.Controls.Button) の例を以下に示します。

```XAML
<Button Style="{StaticResource NavigationBackButtonSmallStyle}" />
```

## <a name="troubleshooting-theme-resources"></a>テーマ リソースのトラブルシューティング

[テーマ リソースの使用に関するガイドライン](#guidelines-for-custom-theme-resources)に従わないと、テーマに関連する予期しない動作がアプリで発生することがあります。

たとえば、淡色テーマのポップアップを開いたときに、濃色テーマのアプリの部分まで淡色テーマのように変更される場合があります。 または、淡色テーマのページに移動してから戻ってくると、元の濃色テーマのページ (またはその部分) が淡色テーマのように表示される場合もあります。

このような問題は、通常、"Default" テーマと "HighContrast" テーマを用意してハイ コントラスト シナリオをサポートした状態で、"Light" と "Dark" の両方のテーマをアプリ内の別々の部分で使っている場合に発生します。

たとえば、次のテーマ ディクショナリの定義について考えてみます。

```XAML
<!-- DO NOT USE. THIS XAML DEMONSTRATES AN ERROR. -->
<ResourceDictionary>
  <ResourceDictionary.ThemeDictionaries>
    <ResourceDictionary x:Key="Default">
      <SolidColorBrush x:Key="myBrush" Color="{ThemeResource SystemBaseHighColor}"/>
    </ResourceDictionary>
    <ResourceDictionary x:Key="HighContrast">
      <SolidColorBrush x:Key="myBrush" Color="{ThemeResource SystemColorButtonFaceColor}"/>
    </ResourceDictionary>
  </ResourceDictionary.ThemeDictionaries>
</ResourceDictionary>
```

直感的には、これは正しく見えます。 ハイ コントラストのときは `myBrush` が指す色を変更しますが、ハイ コントラストでない場合は、[{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)を利用することで `myBrush` がテーマに適した色を指すようにしています。 これは通常、アプリのビジュアル ツリー内に [FrameworkElement.RequestedTheme](/uwp/api/windows.ui.xaml.frameworkelement.requestedtheme) が設定された要素がなければ期待どおりに動作します。 しかし、ビジュアル ツリーの各部分にテーマを再設定し始めたとたんに、アプリで問題が発生することになります。

問題が発生する原因は、他のほとんどの XAML 型とは異なり、ブラシが共有リソースであるためです。 XAML サブツリーに 2 つの要素があり、同じブラシ リソースを参照する別々のテーマが設定されている場合、フレームワークが各サブツリーを走査してそれぞれの [{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)表現を更新していくと、それにつれて共有ブラシ リソースに対する変更が他のサブツリーに反映されます。これは意図した結果とは異なります。

これを修正するには、"Default" ディクショナリを置き換えて、"HighContrast" に加えて "Light" テーマと "Dark" テーマのディクショナリも個別に指定します。

```XAML
<!-- DO NOT USE. THIS XAML DEMONSTRATES AN ERROR. -->
<ResourceDictionary>
  <ResourceDictionary.ThemeDictionaries>
    <ResourceDictionary x:Key="Light">
      <SolidColorBrush x:Key="myBrush" Color="{ThemeResource SystemBaseHighColor}"/>
    </ResourceDictionary>
    <ResourceDictionary x:Key="Dark">
      <SolidColorBrush x:Key="myBrush" Color="{ThemeResource SystemBaseHighColor}"/>
    </ResourceDictionary>
    <ResourceDictionary x:Key="HighContrast">
      <SolidColorBrush x:Key="myBrush" Color="{ThemeResource SystemColorButtonFaceColor}"/>
    </ResourceDictionary>
  </ResourceDictionary.ThemeDictionaries>
</ResourceDictionary>
```

ただし、これらのリソースのいずれかが [Foreground](/uwp/api/windows.ui.xaml.controls.control.foreground) などの継承されたプロパティで参照されていると、引き続き問題が発生します。 カスタム コントロール テンプレートでは、[{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)を使って要素の前景色を指定している場合がありますが、継承された値がフレームワークによって子要素に伝達されるときは、{ThemeResource} マークアップ拡張表現で解決されたリソースへの直接参照が提供されます。 フレームワークがコントロールのビジュアル ツリーを走査する過程でテーマの変更が処理されると、問題が発生します。 フレームワークは {ThemeResource} マークアップ拡張表現を再評価して新しいブラシ リソースを取得しますが、この参照はまだコントロールの子に伝達されません。子への伝達は、次回の測定パスの間など、後で行われます。

結果として、テーマの変更に応答してコントロールのビジュアル ツリーを走査した後、フレームワークは子を走査し、それぞれに設定されている [{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)表現、または子のプロパティに設定されているオブジェクト上の表現をすべて更新します。 ここで問題が発生します。フレームワークがブラシ リソースを走査すると、その色は {ThemeResource} マークアップ拡張を使って指定されているため、ブラシ リソースが再評価されます。

この時点で、あるディクショナリのリソースに別のディクショナリから設定された色が適用され、フレームワークがテーマ ディクショナリを汚染した形になります。

この問題を解決するには、[{ThemeResource} マークアップ拡張](../../xaml-platform/staticresource-markup-extension.md)の代わりに [{StaticResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)を使います。 ガイドラインを適用したテーマ ディクショナリは次のようになります。

```XAML
<ResourceDictionary>
  <ResourceDictionary.ThemeDictionaries>
    <ResourceDictionary x:Key="Light">
      <SolidColorBrush x:Key="myBrush" Color="{StaticResource SystemBaseHighColor}"/>
    </ResourceDictionary>
    <ResourceDictionary x:Key="Dark">
      <SolidColorBrush x:Key="myBrush" Color="{StaticResource SystemBaseHighColor}"/>
    </ResourceDictionary>
    <ResourceDictionary x:Key="HighContrast">
      <SolidColorBrush x:Key="myBrush" Color="{ThemeResource SystemColorButtonFaceColor}"/>
    </ResourceDictionary>
  </ResourceDictionary.ThemeDictionaries>
</ResourceDictionary>
```

"HighContrast" ディクショナリでは、[{StaticResource} マークアップ拡張](../../xaml-platform/staticresource-markup-extension.md)ではなく [{ThemeResource} マークアップ拡張](../../xaml-platform/themeresource-markup-extension.md)が引き続き使われていることに注意してください。 この状況は、ガイドラインで既に説明した例外に当てはまります。 "HighContrast" テーマに使われるブラシの値のほとんどは、システムによって全体的に制御される色から選択されますが、これらは特別な名前付きのリソース (名前に 'SystemColor' というプレフィックスが付いているもの) として XAML に公開されています。 ハイ コントラスト設定で使う特定の色は、コンピューターの簡単操作を通じてユーザーが設定できるようになっています。 これらの色の選択は、特別な名前付きのリソースに適用されます。 XAML フレームワークでは、システム レベルでの変更の検出時にこれらのブラシを更新する場合にも、同じテーマ変更イベントを使用します。 ここで {ThemeResource} マークアップ拡張が使われているのはこのためです。
