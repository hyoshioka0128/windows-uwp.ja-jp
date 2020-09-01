---
description: 現在アクティブなテーマに応じて異なるリソースを取得する追加のシステム ロジックと共に、リソースへの参照を評価して任意の XAML 属性の値を提供します。
title: ThemeResource マークアップ拡張
ms.assetid: 8A1C79D2-9566-44AA-B8E1-CC7ADAD1BCC5
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 89ae286fbc29628e8d81899265019ccdaaa038a3
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89161706"
---
# <a name="themeresource-markup-extension"></a>{ThemeResource} マークアップ拡張

現在アクティブなテーマに応じて異なるリソースを取得する追加のシステム ロジックと共に、リソースへの参照を評価して任意の XAML 属性の値を提供します。 [{StaticResource} マークアップ拡張](staticresource-markup-extension.md)と同様、リソースは [**ResourceDictionary**](/uwp/api/Windows.UI.Xaml.ResourceDictionary) で定義されており、**ThemeResource** の使用は **ResourceDictionary** 内のそのリソースのキーを参照します。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

``` syntax
<object property="{ThemeResource key}" .../>
```

## <a name="xaml-values"></a>XAML 値

| 期間 | 説明 |
|------|-------------|
| key | 要求されたリソースのキー。 このキーは、[**ResourceDictionary**](/uwp/api/Windows.UI.Xaml.ResourceDictionary) によって最初に割当てられます。 リソース キーとしては、XamlName の文法で定義されている任意の文字列を使うことができます。 |

## <a name="remarks"></a>注釈

**ThemeResource** は、XAML リソース ディクショナリ内の別の場所で定義されている XAML 属性の値を取得するための手法です。 このマークアップ拡張は、[{StaticResource} マークアップ拡張](staticresource-markup-extension.md)と同じ基本的な目的を果たします。 {StaticResource} マークアップ拡張との動作の違いとして、**ThemeResource** 参照では、システムによってどのテーマが現在使われているかに応じて、一次検索場所として異なるディクショナリを動的に使うことができます。

アプリが最初に起動されると、**ThemeResource** 参照によって行われたすべてのリソース参照が、起動時に使われたテーマに基づいて評価されます。 ただし、ユーザーが後で実行時にアクティブなテーマを変更した場合、システムは、すべての **ThemeResource** 参照を再評価し、(異なっている可能性のある) テーマに固有のリソースを取得した後、ビジュアル ツリーのすべての適切な場所に新しいリソース値を持つアプリを再表示します。 **StaticResource** は、XAML の読み込み時またはアプリの起動時に判定され、実行時には再評価されません  (XAML を動的に再読み込みする表示状態などの他の方法もありますが、これらの方法は、基本的なリソースの評価が [{StaticResource} マークアップ拡張](staticresource-markup-extension.md)によって有効化されるより高いレベルで動作します)。

**ThemeResource** は、要求されたリソースについてキーを指定する 1 個の引数を受け取ります。 リソース キーは常に、Windows ランタイム XAML の文字列です。 リソース キーを最初に指定する方法について詳しくは、「[x:Key 属性](x-key-attribute.md)」をご覧ください。

リソースの定義方法と [**ResourceDictionary**](/uwp/api/Windows.UI.Xaml.ResourceDictionary) の適切な使用方法 (サンプル コードを含む) について詳しくは、「[ResourceDictionary と XAML リソースの参照](../design/controls-and-patterns/resourcedictionary-and-xaml-resource-references.md)」をご覧ください。

**重要****StaticResource** と同様、**ThemeResource** は、XAML ファイルの中で辞書的に定義されているリソースへの前方参照を行うことはできません。 そのようなことを試みることはサポートしていません。 前方参照が失敗しなかったとしても、そのようなことを試みるだけでパフォーマンスの低下を招きます。 最善の結果を得るには、前方参照を避けるようにリソース ディクショナリの構成を調整します。

解決できないキーに **ThemeResource** を指定しようとすると、実行時に XAML 解析例外がスローされます。 デザイン ツールでも、警告やエラーが通知されることがあります。

Windows ランタイム XAML プロセッサの実装では、**ThemeResource** のバッキング クラス表現はありません。 コードで最も近いのは、[**Contains**](/uwp/api/windows.ui.xaml.resourcedictionary.contains) または [**TryGetValue**](/uwp/api/windows.ui.xaml.resourcedictionary.trygetvalue) を呼び出すなど、[**ResourceDictionary**](/uwp/api/Windows.UI.Xaml.ResourceDictionary) のコレクション API を使うことです。

**ThemeResource** はマークアップ拡張です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 XAML のすべてのマークアップ拡張では、それぞれの属性構文で "{" と "}" の文字を使います。これは規約であり、これに従って XAML プロセッサは、マークアップ拡張で属性を処理する必要があることを認識します。

### <a name="when-and-how-to-use-themeresource-rather-than-staticresource"></a>{StaticResource} ではなく {ThemeResource} を使う状況とその方法

**ThemeResource** がリソース ディクショナリの項目に解決される規則は、通常、**StaticResource** の場合と同じです。 **ThemeResource** 検索は [**ThemeDictionaries**](/uwp/api/windows.ui.xaml.resourcedictionary.themedictionaries) のコレクションで参照される [**ResourceDictionary**](/uwp/api/Windows.UI.Xaml.ResourceDictionary) ファイルまで拡張できます。これは、**StaticResource** の場合も同じです。 その違いは、**ThemeResource** では実行時に再評価を行うことができるのに対し、**StaticResource** では再評価を行うことができない点にあります。

各テーマ ディクショナリのキー セットでは、どのテーマがアクティブであるかに関係なく、キーを持つリソースの同じセットを提供する必要があります。 特定のキーを持つリソースが **HighContrast** テーマ ディクショナリに存在する場合、**Light** と **Default** にも同じ名前を持つ別のリソースが存在する必要があります。 そうでないと、ユーザーがテーマを切り替えたときにリソース検索が失敗し、アプリが適切に表示されなくなります。 テーマ ディクショナリには、サブ値を指定するために同じスコープ内からのみ参照されるキーを持つリソースを含めることができます。ただし、これらはすべてのテーマで等価である必要はありません。

通常は、リソースをテーマ ディクショナリに格納し、これらの値がテーマごとに変化するときや、変化する値によってサポートされているときにのみ、**ThemeResource** を使ってこれらのリソースを参照します。 これは、次の種類のリソースに適しています。

-   ブラシ。特に [**SolidColorBrush**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) の色。 この使い方は、既定の XAML コントロール テンプレート (generic.xaml) において **ThemeResource** の約 80% を占めています。
-   境界線、オフセット、余白、パディングなどのピクセル値。
-   **FontFamily**、**FontSize** などのフォント プロパティ。
-   通常システムによってスタイルが設定され、動的な表示に使われる、限られた数のコントロールの完全なテンプレート ([**GridViewItem**](/uwp/api/Windows.UI.Xaml.Controls.GridViewItem)、[**ListViewItem**](/uwp/api/Windows.UI.Xaml.Controls.ListViewItem) など)。
-   テキスト表示スタイル (通常はフォントの色、背景、サイズを変更する目的で使われます)。

Windows ランタイムには、特に **ThemeResource** から参照するためのリソースのセットが用意されています。 これらはすべて、Windows ソフトウェア開発キット (Windows SDK) の include/winrt/xaml/design フォルダーにある XAML ファイル themeresources.xaml に記載されています。 themeresources.xaml に定義されているテーマ ブラシと追加のスタイルについて詳しくは、「[XAML テーマ リソース リファレンス](../design/controls-and-patterns/xaml-theme-resources.md)」をご覧ください。 ブラシについては、アクティブになる可能性のある 3 種類のテーマごとに、各ブラシの色の値を表形式で示しています。

コントロール テンプレートの表示状態の XAML 定義では、テーマの変更によって変更される可能性がある基になるリソースがある場合は常に **ThemeResource** 参照を使う必要があります。 通常、システム テーマが変更されても、表示状態の変更は発生しません。 この場合、リソースでは、**ThemeResource** 参照を使って、依然アクティブな表示状態に対して値を再評価できるようにする必要があります。 たとえば、特定の UI 部分のブラシの色とそのプロパティの 1 つを変更する表示状態があり、そのブラシの色がテーマごとに異なる場合は、**ThemeResource** 参照を使って、既定のテンプレートのこのプロパティ値と、その既定のテンプレートに対する表示状態の変更を提供する必要があります。

**ThemeResource** は、一連の依存型の値で使われる場合があります。 たとえば、キーを持つリソースである [**SolidColorBrush**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) で使われる [**Color**](/uwp/api/Windows.UI.Color) で **ThemeResource** 参照を使うことがあります。 ただし、キーを持つ **SolidColorBrush** リソースを使う任意の UI プロパティで **ThemeResource** 参照を使うこともあります。この場合、テーマが変更されたときに動的な値の変更を可能にするのはそれぞれの [**Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) タイプのプロパティです。

**メモ**   `{ThemeResource}`また、テーマの切り替えでの実行時のリソースの評価は Windows 8.1 XAML でサポートされていますが、Windows 8 を対象とするアプリの XAML ではサポートされていません。

### <a name="system-resources"></a>システム リソース

一部のテーマ リソースは、システム リソース値を基になるサブ値として参照します。 システム リソースは、どの XAML リソース ディクショナリにも含まれていない特殊なリソース値です。 これらの値は、Windows ランタイム XAML サポートの動作に依存してシステム自体から値を転送し、XAML リソースが参照できる形式でその値を表します。 たとえば、"SystemColorButtonFaceColor" という名前の、RGB 色を表すシステム リソースがあります。 この色は、Windows ランタイムと Windows ランタイム アプリだけに限定されないシステム カラーとテーマの観点に基づきます。

通常、システム リソースは、ハイ コントラスト テーマの基になる値です。 ユーザーはハイ コントラスト テーマの色の選択を管理します。ユーザーは、同様に Windows ランタイム アプリに固有ではないシステム機能を使って、これらの選択を行います。 システム リソースを **ThemeResource** 参照として参照すると、Windows ランタイム アプリのハイ コントラスト テーマの既定の動作で、ユーザーによって制御されシステムによって公開される、テーマに固有のこれらの値を使うことができます。 また、これらの参照は、システムによって実行時のテーマの変更が検出された場合に再評価のマークが付けられます。

### <a name="an-example-themeresource-usage"></a>{ThemeResource} の使用例

**ThemeResource** の使い方の例として、既定の generic.xaml ファイルと themeresources.xaml ファイルから抜粋した XAML の例を示します。 ここでは、1 つのテンプレート (既定の [**Button**](/uwp/api/Windows.UI.Xaml.Controls.Button)) と、テーマの変更に対応するための 2 つのプロパティ ([**Background**](/uwp/api/windows.ui.xaml.controls.control.background) と [**Foreground**](/uwp/api/windows.ui.xaml.controls.control.foreground)) の宣言方法について注目します。

```xml
    <!-- Default style for Windows.UI.Xaml.Controls.Button -->
    <Style TargetType="Button">
        <Setter Property="Background" Value="{ThemeResource ButtonBackgroundThemeBrush}" />
        <Setter Property="Foreground" Value="{ThemeResource ButtonForegroundThemeBrush}"/>
...
```

ここで、これらのプロパティは [**Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) 値を受け取ります。[**SolidColorBrush**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) リソース (`ButtonBackgroundThemeBrush` と `ButtonForegroundThemeBrush`) の参照には、**ThemeResource** が使われています。

これらの同じプロパティは、[**Button**](/uwp/api/Windows.UI.Xaml.Controls.Button) の表示状態のいくつかによっても調整されます。 特に、背景色は、ボタンをクリックしたときに変更されます。 同様に、表示状態のストーリーボードの [**Background**](/uwp/api/windows.ui.xaml.controls.control.background) と [**Foreground**](/uwp/api/windows.ui.xaml.controls.control.foreground) のアニメーションでは、[**DiscreteObjectKeyFrame**](/uwp/api/Windows.UI.Xaml.Media.Animation.DiscreteObjectKeyFrame) オブジェクトと共に、キー フレーム値として **ThemeResource** を含むブラシへの参照を使っています。

```xml
<VisualState x:Name="Pressed">
  <Storyboard>
    <ObjectAnimationUsingKeyFrames Storyboard.TargetName="Border"
        Storyboard.TargetProperty="Background">
      <DiscreteObjectKeyFrame KeyTime="0" Value="{ThemeResource ButtonPressedBackgroundThemeBrush}" />
    </ObjectAnimationUsingKeyFrames>
    <ObjectAnimationUsingKeyFrames Storyboard.TargetName="ContentPresenter"
         Storyboard.TargetProperty="Foreground">
       <DiscreteObjectKeyFrame KeyTime="0" Value="{ThemeResource ButtonPressedForegroundThemeBrush}" />
    </ObjectAnimationUsingKeyFrames>
  </Storyboard>
</VisualState>
```

これらのブラシはそれぞれ generic.xaml で事前に定義されています。XAML の前方参照を避けるためには、これらのブラシは、これを使う任意のテンプレートに先だって定義されている必要があります。 "Default" テーマ ディクショナリのための定義を次に示します。

```xml
    <ResourceDictionary.ThemeDictionaries>
        <ResourceDictionary x:Key="Default">
...
            <SolidColorBrush x:Key="ButtonBackgroundThemeBrush" Color="Transparent" />
            <SolidColorBrush x:Key="ButtonForegroundThemeBrush" Color="#FFFFFFFF" />
...
            <SolidColorBrush x:Key="ButtonPressedBackgroundThemeBrush" Color="#FFFFFFFF" />
            <SolidColorBrush x:Key="ButtonPressedForegroundThemeBrush" Color="#FF000000" />
...
```

他の各テーマ ディクショナリにも、次に示すようにこれらのブラシが定義されています。

```xml
        <ResourceDictionary x:Key="HighContrast">
            <!-- High Contrast theme resources -->
...
            <SolidColorBrush x:Key="ButtonBackgroundThemeBrush" Color="{ThemeResource SystemColorButtonFaceColor}" />
            <SolidColorBrush x:Key="ButtonForegroundThemeBrush" Color="{ThemeResource SystemColorButtonTextColor}" />

...
            <SolidColorBrush x:Key="ButtonPressedBackgroundThemeBrush" Color="{ThemeResource SystemColorButtonTextColor}" />
            <SolidColorBrush x:Key="ButtonPressedForegroundThemeBrush" Color="{ThemeResource SystemColorButtonFaceColor}" />
```

この [**Color**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush.Color) 値は、システム リソースに対するもう 1 つの **ThemeResource** 参照です。 システム リソースを参照し、テーマの変更に応じてシステム リソースを変更する場合は、**ThemeResource** を使って参照を行う必要があります。

## <a name="windows8-behavior"></a>Windows 8 の動作

Windows 8 では **ThemeResource** マークアップ拡張はサポートされていませんでしたが、Windows 8.1 以降で利用できるようになりました。 また、Windows 8 は、Windows ランタイム アプリのテーマ関連リソースの動的切り替えをサポートしていません。 XAML テンプレートとスタイルのテーマ変更を認識するには、アプリを再起動する必要がありました。 これは褒められたユーザー エクスペリエンスではありません。そのため、アプリを再コンパイルして Windows 8.1 をターゲットにすることを強くお勧めします。そうすれば、**ThemeResource** を利用したスタイルを使うことができ、ユーザーがテーマを切り替えたときに動的にテーマを切り替えることができます。 Windows 8 用にコンパイルしたアプリは、Windows 8.1 上で実行しても Windows 8 のときと同じ動作になります。

## <a name="design-time-tools-support-for-the-themeresource-markup-extension"></a>設計時ツールの **{ThemeResource}** マークアップ拡張のサポート

Microsoft Visual Studio 2013 では、XAML ページで **{ThemeResource}** マークアップ拡張を使うときに Microsoft IntelliSense のドロップダウンに可能なキー値を含めることができます。 たとえば、「{ThemeResource」と入力するとすぐに、[XAML テーマ リソース](../design/controls-and-patterns/xaml-theme-resources.md)のリソース キーが表示されます。

**{ThemeResource}** の一部としてリソース キーが存在すると、**[定義へ移動]** (F12 キー) 機能でそのリソースを解決して、テーマ リソースが定義されている設計時の generic.xaml を表示できます。 テーマ リソースを何度も定義されるため (テーマごとに)、**[定義へ移動]** ではファイルで見つかった最初の定義に移動します。これは **Default** の定義です。 他の定義が必要な場合は、ファイル内のキー名を検索して、他のテーマの定義を参照できます。

## <a name="related-topics"></a>関連トピック

* [ResourceDictionary と XAML リソースの参照](../design/controls-and-patterns/resourcedictionary-and-xaml-resource-references.md)
* [XAML テーマ リソース](../design/controls-and-patterns/xaml-theme-resources.md)
* [**ResourceDictionary**](/uwp/api/Windows.UI.Xaml.ResourceDictionary)
* [x:Key 属性](x-key-attribute.md)
 