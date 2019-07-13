---
Description: XAML フレームワークで、コントロール テンプレートを作ることによって、コントロールの視覚的構造や視覚的動作をカスタマイズすることができます。
MS-HAID: dev\_ctrl\_layout\_txt.control\_templates
MSHAttr: PreferredLib:/library/windows/apps
Search.Product: eADQiWindows 10XVcnh
title: コントロール テンプレート
ms.assetid: 6E642626-A1D6-482F-9F7E-DBBA7A071DAD
label: Control templates
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: d8968104ec7b28a6b4a59eb6a83c422807282a7c
ms.sourcegitcommit: aaa4b898da5869c064097739cf3dc74c29474691
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "66362990"
---
# <a name="control-templates"></a>コントロール テンプレート

XAML フレームワークで、コントロール テンプレートを作ることによって、コントロールの視覚的構造や視覚的動作をカスタマイズすることができます。 コントロールには、[**Background**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.background)、[**Foreground**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.foreground)、[**FontFamily**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.fontfamily) などの多くのプロパティがあり、このプロパティを設定することで、コントロールの外観に関するさまざまな要素を指定できます。 ただし、これらのプロパティの設定によって変更できる内容は限られています。 [  **ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) クラスを使ってテンプレートを作成することにより、さらに細かいカスタマイズを指定できます。 ここでは、[**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) コントロールの外観をカスタマイズする **ControlTemplate** の作成方法について説明します。

> **重要な API**:[**ControlTemplate クラス**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate)、[**Control.Template プロパティ**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.template)

## <a name="custom-control-template-example"></a>カスタム コントロール テンプレートの例

既定では、[**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) コントロールの内容 (**CheckBox** の横に表示される文字列またはオブジェクト) は、選択ボックスの右側に配置され、チェック マークはユーザーがその **CheckBox** を選択したことを示します。 これらの特性は、**CheckBox** の視覚的構造や視覚的動作を表します。

次の図は、既定の [**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) を使った [**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) での `Unchecked`、`Checked`、`Indeterminate` の各状態を示しています。

![既定の CheckBox テンプレート](images/templates-checkbox-states-default.png)

[  **CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) に対して [**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) を作成することで、これらの特性を変更できます。 たとえば、チェック ボックスの内容を選択ボックスの下に配置し、ユーザーがチェック ボックスをオンにしたことを **X** で示す場合を考えます。 **CheckBox** の **ControlTemplate** に、これらの特性を指定します。

コントロールにカスタム テンプレートを使うには、[**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) をコントロールの [**Template**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.control.template) プロパティに割り当てます。 ここでは、[**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) に `CheckBoxTemplate1` という名前の **ControlTemplate** を使います。 **ControlTemplate** の Extensible Application Markup Language (XAML) は、次のセクションで示します。

```XAML
<CheckBox Content="CheckBox" Template="{StaticResource CheckBoxTemplate1}" IsThreeState="True" Margin="20"/>
```

このテンプレートを適用した後で [**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) の `Unchecked`、`Checked`、`Indeterminate` の各状態がどのようになるかを次に示します。

![カスタム CheckBox テンプレート](images/templates-checkbox-states.png)

## <a name="specify-the-visual-structure-of-a-control"></a>コントロールの視覚的構造の指定

[  **ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) を作るときには、いくつかの [**FrameworkElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.FrameworkElement) オブジェクトを組み合わせて 1 つのコントロールを作ります。 **ControlTemplate** には、ルート要素として **FrameworkElement** が 1 つだけ含まれている必要があります。 通常、ルート要素には、他の **FrameworkElement** オブジェクトが含まれています。 オブジェクトの組み合わせによって、コントロールの視覚的構造が作られます

次の XAML は、コントロールの内容を選択ボックスの下に配置するよう指定する、[**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) 用の [**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) を作成します。 ルート要素は [**Border**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Border) です。 この例では、ユーザーが **CheckBox** をオンにしたことを示す **X** を作成する [**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) と、不確定状態を示す [**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) を指定しています。 これらの **Path** と **Ellipse** では [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) が 0 に設定されているため、既定ではどちらも表示されません。

[TemplateBinding](../../xaml-platform/templatebinding-markup-extension.md) は、コントロール テンプレート内のプロパティの値を、template 宣言されたコントロールのその他の公開されているプロパティの値にリンクする特殊なバインディングです。 XAML では、TemplateBinding は ControlTemplate 定義内でのみ使用できます。 詳しくは、「[TemplateBinding マークアップ拡張](../../xaml-platform/templatebinding-markup-extension.md)」をご覧ください。

> [!NOTE]
> Windows 10 Version 1809 ([SDK 17763](https://developer.microsoft.com/windows/downloads/windows-10-sdk)) 以降、[TemplateBinding](../../xaml-platform/templatebinding-markup-extension.md) を使用する場所で [**x:bind**](https://docs.microsoft.com/windows/uwp/xaml-platform/x-bind-markup-extension) マークアップ拡張を使用できます。 詳しくは、「[TemplateBinding マークアップ拡張](../../xaml-platform/templatebinding-markup-extension.md)」をご覧ください。

```XAML
<ControlTemplate x:Key="CheckBoxTemplate1" TargetType="CheckBox">
    <Border BorderBrush="{TemplateBinding BorderBrush}"
            BorderThickness="{TemplateBinding BorderThickness}"
            Background="{TemplateBinding Background}">
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="*"/>
                <RowDefinition Height="25"/>
            </Grid.RowDefinitions>
            <Rectangle x:Name="NormalRectangle" Fill="Transparent" Height="20" Width="20"
                       Stroke="{ThemeResource SystemControlForegroundBaseMediumHighBrush}"
                       StrokeThickness="{ThemeResource CheckBoxBorderThemeThickness}"
                       UseLayoutRounding="False"/>
            <!-- Create an X to indicate that the CheckBox is selected. -->
            <Path x:Name="CheckGlyph"
                  Data="M103,240 L111,240 119,248 127,240 135,240 123,252 135,264 127,264 119,257 111,264 103,264 114,252 z"
                  Fill="{ThemeResource CheckBoxForegroundThemeBrush}"
                  FlowDirection="LeftToRight"
                  Height="14" Width="16" Opacity="0" Stretch="Fill"/>
            <Ellipse x:Name="IndeterminateGlyph"
                     Fill="{ThemeResource CheckBoxForegroundThemeBrush}"
                     Height="8" Width="8" Opacity="0" UseLayoutRounding="False" />
            <ContentPresenter x:Name="ContentPresenter"
                              ContentTemplate="{TemplateBinding ContentTemplate}"
                              Content="{TemplateBinding Content}"
                              Margin="{TemplateBinding Padding}" Grid.Row="1"
                              HorizontalAlignment="Center"
                              VerticalAlignment="{TemplateBinding VerticalContentAlignment}"/>
        </Grid>
    </Border>
</ControlTemplate>
```

## <a name="specify-the-visual-behavior-of-a-control"></a>コントロールの視覚的動作の指定

視覚的動作は、コントロールが特定の状態にあるときの外観を指定します。 [  **CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) コントロールには、`Checked`、`Unchecked`、`Indeterminate` という 3 つのチェック状態があります。 [  **IsChecked**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.togglebutton.ischecked) プロパティの値によって **CheckBox** の状態が決まり、その状態によって、ボックスに何が表示されるかが決まります。

次の表に、考えられる [**IsChecked**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.primitives.togglebutton.ischecked) の値と、対応する [**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) の状態および **CheckBox** の外観を示します。

|                     |                    |                         |
|---------------------|--------------------|-------------------------|
| **IsChecked** の値 | **CheckBox** の状態 | **CheckBox** の外観 |
| **true**            | `Checked`          | "X" を表示。        |
| **false**           | `Unchecked`        | 空白。                  |
| **null**            | `Indeterminate`    | 円を表示。      |


[  **VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) オブジェクトを使って、コントロールが特定の状態にあるときの外観を指定します。 **VisualState** には、[**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) 内の要素の外観を変更する [**Setter**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) または [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.BeginStoryboard) が含まれています。 コントロールが [**VisualState.Name**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.visualstate.name) プロパティで指定された状態になると、**Setter** または [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) 内のプロパティの変更が適用されます。 コントロールがこの状態でなくなると、変更は削除されます。 **VisualState** オブジェクトは [**VisualStateGroup**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualStateGroup) オブジェクトに追加します。 **ControlTemplate** のルート [**FrameworkElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.FrameworkElement) に設定する [**VisualStateManager.VisualStateGroups**](https://docs.microsoft.com/dotnet/api/system.windows.visualstatemanager?view=netframework-4.8) 添付プロパティに、**VisualStateGroup** オブジェクトを追加します。

次の XAML は、`Checked`、`Unchecked`、`Indeterminate` の各状態に対する [**VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) オブジェクトを示しています。 この例では、[**ControlTemplate**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) のルート要素である [**Border**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Border) に対して [**VisualStateManager.VisualStateGroups**](https://docs.microsoft.com/dotnet/api/system.windows.visualstatemanager?view=netframework-4.8) 添付プロパティを設定します。 `Checked` **VisualState** は、(前の例で示した) `CheckGlyph` という名前の [**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) の [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) が 1 であることを指定します。 `Indeterminate` **VisualState** は、`IndeterminateGlyph` という名前の [**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) の **Opacity** が 1 であることを指定します。 `Unchecked` **VisualState** には [**Setter**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) または [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) がないため、[**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) は既定の外観に戻ります。

```XAML
<ControlTemplate x:Key="CheckBoxTemplate1" TargetType="CheckBox">
    <Border BorderBrush="{TemplateBinding BorderBrush}"
            BorderThickness="{TemplateBinding BorderThickness}"
            Background="{TemplateBinding Background}">

        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup x:Name="CheckStates">
                <VisualState x:Name="Checked">
                    <VisualState.Setters>
                        <Setter Target="CheckGlyph.Opacity" Value="1"/>
                    </VisualState.Setters>
                    <!-- This Storyboard is equivalent to the Setter. -->
                    <!--<Storyboard>
                        <DoubleAnimation Duration="0" To="1"
                         Storyboard.TargetName="CheckGlyph" Storyboard.TargetProperty="Opacity"/>
                    </Storyboard>-->
                </VisualState>
                <VisualState x:Name="Unchecked"/>
                <VisualState x:Name="Indeterminate">
                    <VisualState.Setters>
                        <Setter Target="IndeterminateGlyph.Opacity" Value="1"/>
                    </VisualState.Setters>
                    <!-- This Storyboard is equivalent to the Setter. -->
                    <!--<Storyboard>
                        <DoubleAnimation Duration="0" To="1"
                         Storyboard.TargetName="IndeterminateGlyph" Storyboard.TargetProperty="Opacity"/>
                    </Storyboard>-->
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>

        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="*"/>
                <RowDefinition Height="25"/>
            </Grid.RowDefinitions>
            <Rectangle x:Name="NormalRectangle" Fill="Transparent" Height="20" Width="20"
                       Stroke="{ThemeResource SystemControlForegroundBaseMediumHighBrush}"
                       StrokeThickness="{ThemeResource CheckBoxBorderThemeThickness}"
                       UseLayoutRounding="False"/>
            <!-- Create an X to indicate that the CheckBox is selected. -->
            <Path x:Name="CheckGlyph"
                  Data="M103,240 L111,240 119,248 127,240 135,240 123,252 135,264 127,264 119,257 111,264 103,264 114,252 z"
                  Fill="{ThemeResource CheckBoxForegroundThemeBrush}"
                  FlowDirection="LeftToRight"
                  Height="14" Width="16" Opacity="0" Stretch="Fill"/>
            <Ellipse x:Name="IndeterminateGlyph"
                     Fill="{ThemeResource CheckBoxForegroundThemeBrush}"
                     Height="8" Width="8" Opacity="0" UseLayoutRounding="False" />
            <ContentPresenter x:Name="ContentPresenter"
                              ContentTemplate="{TemplateBinding ContentTemplate}"
                              Content="{TemplateBinding Content}"
                              Margin="{TemplateBinding Padding}" Grid.Row="1"
                              HorizontalAlignment="Center"
                              VerticalAlignment="{TemplateBinding VerticalContentAlignment}"/>
        </Grid>
    </Border>
</ControlTemplate>
```

[  **VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) オブジェクトの機能をよりよく理解するために、[**CheckBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CheckBox) が `Unchecked` 状態から `Checked` 状態に変化した後、`Indeterminate` 状態に変化してから、`Unchecked` 状態に戻るとき、どのようになるかを考えてみます。 状態の遷移を次に示します。

|                                      |                                                                                                                                                                                                                                                                                                                                                |                                                   |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|
| 状態の遷移                     | 動作                                                                                                                                                                                                                                                                                                                                   | 遷移完了時の CheckBox の外観 |
| `Unchecked` から `Checked`。       | `Checked`[ **VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) の [**Setter**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) 値が適用され、`CheckGlyph` の [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) が 1 となる。                                                                                                                                                         | X が表示される。                                |
| `Checked` から `Indeterminate`。   | `Indeterminate`[ **VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) の [**Setter**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) 値が適用され、`IndeterminateGlyph` の [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) が 1 となる。 `Checked` **VisualState** の **Setter** 値が削除され、`CheckGlyph` の [**Opacity**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.brush.opacity) が 0 となる。 | 円が表示される。                            |
| `Indeterminate` から `Unchecked`。 | `Indeterminate` [**VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) の [**Setter**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) 値が削除され、`IndeterminateGlyph` の [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) が 0 となる。                                                                                                                                           | 何も表示されない。                             |

 
コントロールの表示状態の作成方法、特に、[**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) クラスとアニメーション タイプの使い方について詳しくは、「[表示状態用にストーリーボードに設定されたアニメーション](https://docs.microsoft.com/previous-versions/windows/apps/jj819808(v=win.10))」をご覧ください。

## <a name="use-tools-to-work-with-themes-easily"></a>ツールを使ってテーマを簡単に操作

コントロールにテーマをすばやく適用する方法の 1 つは、Microsoft Visual Studio の **[ドキュメント アウトライン]** でコントロールを右クリックし、 **[テーマの編集]** または **[スタイルの編集]** (右クリックしたコントロールによって異なる) をクリックすることです。 その後、 **[リソースの適用]** をクリックして既にあるテーマを適用するか、または **[空アイテムの作成]** をクリックして新しいテーマを定義できます。

## <a name="controls-and-accessibility"></a>コントロールとアクセシビリティ

コントロールのテンプレートを新しく作成するときは、コントロールの動作と外見を変更する以外にも、アクセシビリティ フレームワークに対する表現方法も変更することができます。 ユニバーサル Windows プラットフォーム (UWP) は、アクセシビリティのための Microsoft UI オートメーション フレームワークをサポートしています。 既定のコントロールとそのテンプレートはいずれも、UI オートメーションの共通のコントロール型と、その目的や機能に合ったパターンをサポートしています。 支援技術などの UI オートメーション クライアントが、これらのコントロール型とパターンを解釈することにより、アクセシビリティ対応アプリの UI という、より大きな枠組みを構成する要素としてコントロールを利用することができます。

基本的なコントロールのロジックを分離すると共に、UI オートメーションのアーキテクチャに求められるいくつかの要件を満たすために、コントロール クラスのアクセシビリティ機能は、別個のクラス (オートメーション ピア) に置かれています。 オートメーション ピアは、折に触れてコントロール テンプレートと対話します。テンプレート内の特定の名前付きパーツの存在を頼りにその機能 (支援技術によってボタン アクションを呼び出すなど) を実現しているためです。

まったく新しいカスタム コントロールを作成するときは、同時に、新しいオートメーション ピアの作成が必要になることもあります。 詳しくは、「[カスタム オートメーション ピア](../accessibility/custom-automation-peers.md)」をご覧ください。

## <a name="learn-more-about-a-controls-default-template"></a>コントロールの既定のテンプレートの詳細

XAML コントロールのスタイルとテンプレートについて説明するトピックでは、既に説明した **テーマの編集**や**スタイルの編集**の手法を使った場合に見られる、同じ XAML の開始部分を抜粋しています。 各トピックでは、表示状態の名前、使用しているテーマ リソースを示しているほか、テンプレートを含むスタイルの完全な XAML を示しています。 これらのトピックが便利なガイダンスになるのは、テンプレートを変更し始めてから元のテンプレートがどのように見えていたかを確認したり、必要な名前付きの表示状態がすべて新しいテンプレートにあることを確認したりする場合です。

## <a name="theme-resources-in-control-templates"></a>コントロール テンプレートのテーマ リソース

XAML の例を見ると、一部の属性について [{ThemeResource} マークアップ拡張機能](../../xaml-platform/themeresource-markup-extension.md) を使うリソース参照があることがわかるでしょう。 この手法では、現在アクティブであるテーマに応じて値が変わるリソースを 1 つのコントロール テンプレートで使用できます。 この点はブラシと色に特に重要です。システム全体に暗い、明るい、またはハイコントラストのいずれのテーマを適用するかをユーザーが選択できるようにすることが、テーマの主な目的であるためです。 XAML リソース システムを使うアプリはそのテーマに適切な一連のリソースを使用できます。そのため、アプリの UI のテーマの選択にはユーザーのシステム全体のテーマの選択が反映されます。

## <a name="get-the-sample-code"></a>サンプル コードを入手する

* [XAML コントロール ギャラリーのサンプル](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/XamlUIBasics)
* [カスタム テキスト編集コントロールのサンプル](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/CustomEditControl)
