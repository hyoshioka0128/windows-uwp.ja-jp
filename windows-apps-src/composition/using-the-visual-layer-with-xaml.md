---
ms.assetid: b7a4ac8a-d91e-461b-a060-cc6fcea8e778
title: XAML でのビジュアル レイヤーの使用
description: ビジュアル レイヤー API を既存の XAML コンテンツと組み合わせて使用し、高度なアニメーションや効果を作成する方法について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 5b0c8f9909f59cb3a0dd5e16a6bb1c46fc069bfb
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89160806"
---
# <a name="using-the-visual-layer-with-xaml"></a>XAML でのビジュアル レイヤーの使用

ビジュアル レイヤーの機能を利用するほとんどのアプリは、XAML を使用して、メイン UI コンテンツを定義します。 Windows 10 Anniversary Update では、XAML フレームワークやビジュアル レイヤーの新しい機能を利用し、これら 2 つのテクノロジを組み合わせて、魅力的なユーザー エクスペリエンスを簡単に作成することができます。
XAML とビジュアル レイヤーの相互運用機能を使用すると、XAML API 単独では実現できない、高度なアニメーションや効果を作成できます。 これには次のものが含まれます

- ぼかしやすりガラスなどのブラシ効果
- 動的な照明効果
- スクロール駆動型のアニメーションや視差効果
- 自動レイアウトのアニメーション
- ピクセル パーフェクトなドロップ シャドウ

これらの効果やアニメーションは既存の XAML コンテンツに適用できます。このため、新しい機能を活用するために、XAML アプリを大幅に再構成する必要はありません。
レイアウト アニメーション、シャドウ、ぼかし効果については、以下の「レシピ」セクションで説明しています。 視差効果を実装するコード サンプルについては、[ParallaxingListItems のサンプル](https://github.com/microsoft/WindowsCompositionSamples/tree/master/SampleGallery/Samples/SDK%2010586/ParallaxingListItems)をご覧ください。 [WindowsUIDevLabs リポジトリ](https://github.com/microsoft/WindowsCompositionSamples)にも、アニメーション、シャドウ、効果を実装するためのサンプルがいくつかあります。

## <a name="the-xamlcompositionbrushbase-class"></a>XamlCompositionBrushBase クラス

**XamlCompositionBrush** は、**CompositionBrush** で領域をペイントする XAML ブラシの基底クラスを提供します。 これを使用することで、XAML UI 要素に、ぼかしやすりガラスなどのコンポジション効果を簡単に適用できます。

XAML UI でのブラシの使い方について詳しくは、「[**ブラシ**](../design/style/brushes.md#xamlcompositionbrushbase)」セクションをご覧ください。

コードの例については、[**XamlCompositionBrushBase**](/uwp/api/windows.ui.xaml.media.xamlcompositionbrushbase) のリファレンス ページをご覧ください。

## <a name="the-xamllight-class"></a>XamlLight クラス

**XamlLight** は、**CompositionLight** で領域を動的に照らす XAML 照明効果の基底クラスを提供します。

XAML UI 要素の照明など、ライトの使い方について詳しくは、「[**照明**](xaml-lighting.md)」セクションをご覧ください。

コードの例については、[**XamlLight**](/uwp/api/windows.ui.xaml.media.xamllight) のリファレンス ページをご覧ください。

## <a name="the-elementcompositionpreview-class"></a>ElementCompositionPreview クラス

[**ElementCompositionPreview**](/uwp/api/windows.ui.xaml.hosting.elementcompositionpreview) は静的クラスであり、XAML とビジュアル レイヤーの相互運用機能を提供します。 ビジュアル レイヤーとその機能の概要については、「[ビジュアル レイヤー](./visual-layer.md)」をご覧ください。 **ElementCompositionPreview** クラスには、次のメソッドが用意されています。

-   [**GetElementVisual**](/uwp/api/windows.ui.xaml.hosting.elementcompositionpreview.getelementvisual) この要素のレンダリングで使用される "ハンドアウト" Visual を取得します。
-   [**SetElementChildVisual**](/uwp/api/windows.ui.xaml.hosting.elementcompositionpreview.setelementchildvisual): "ハンドイン" Visual を、この要素のビジュアル ツリーの最後の子として設定します。 この Visual は、他の要素の上に描画されます。 
-   [**GetElementChildVisual**](/uwp/api/windows.ui.xaml.hosting.elementcompositionpreview.getelementvisual): **SetElementChildVisual** を使用して設定された Visual を取得します。
-   [**GetScrollViewerManipulationPropertySet**](/uwp/api/windows.ui.xaml.hosting.elementcompositionpreview.getelementvisual): **ScrollViewer** のスクロール オフセットに基づいて 60 fps のアニメーションを作成する際に使用できるオブジェクトを取得します。

## <a name="remarks-on-elementcompositionpreviewgetelementvisual"></a>ElementCompositionPreview.GetElementVisual の解説

**ElementCompositionPreview.GetElementVisual** は、指定の **UIElement** をレンダリングするために使用される "ハンドアウト" Visual を返します。 **Visual.Opacity**、**Visual.Offset**、**Visual.Size** などのプロパティは、UIElement の状態に基づいて、XAML フレームワークによって設定されます。 これにより、暗黙的な位置変更アニメーションなどの手法が利用可能になります (「*Recipes*」をご覧ください)。

**Offset** や **Size** は XAML フレームワーク レイアウトの結果として設定されるため、開発者は、これらのプロパティの変更やアニメーション化を慎重に行う必要があります。 レイアウト内で要素の左上隅の位置がその要素の親の左上隅と同じ位置になる場合、開発者は、Offset の変更またはアニメーション化のみを行ってください。 通常、Size は変更しませんが、そのプロパティへアクセスすると便利な場合があります。 たとえば、以下に示すドロップ シャドウやすりガラスのサンプルでは、ハンドアウト Visual の Size をアニメーションへの入力として使用します。

その他の注意事項として、ハンドアウト Visual の更新されたプロパティは、対応する UIElement には反映されません。 たとえば、**UIElement.Opacity** を 0.5 に設定すると、対応するハンドアウト Visual の Opacity も 0.5 に設定されます。 ただし、ハンドアウト Visual の **Opacity** を 0.5 に設定した場合、コンテンツが 50% の不透明度で表示されますが、対応する UIElement の Opacity プロパティの値は変更されません。

### <a name="example-of-offset-animation"></a>**オフセット** アニメーションの例

#### <a name="incorrect"></a>不正解です

```xaml
<Border>
      <Image x:Name="MyImage" Margin="5" />
</Border>
```

```csharp
// Doesn’t work because Image has a margin!
ElementCompositionPreview.GetElementVisual(MyImage).StartAnimation("Offset", parallaxAnimation);
```

#### <a name="correct"></a>正解です。

```xaml
<Border>
    <Canvas Margin="5">
        <Image x:Name="MyImage" />
    </Canvas>
</Border>
```

```csharp
// This works because the Canvas parent doesn’t generate a layout offset.
ElementCompositionPreview.GetElementVisual(MyImage).StartAnimation("Offset", parallaxAnimation);
```

## <a name="the-elementcompositionpreviewsetelementchildvisual-method"></a>**ElementCompositionPreview.SetElementChildVisual** メソッド

**ElementCompositionPreview.SetElementChildVisual** を使用すると、開発者は、要素のビジュアル ツリーの一部として表示される "ハンドイン" Visual を提供できます。 これにより、開発者は、Visual ベースのコンテンツを XAML UI 内部に表示できる、"コンポジション アイランド" を作成できます。 開発者はこの手法の使用については慎重に考慮する必要があります。それは、Visual ベースのコンテンツを使用した場合、XAML コンテンツでは同等のアクセシビリティとユーザー エクスペリエンスの保証が確保されないためです。 そのため、通常この手法は、以下の「レシピ」セクションに記載されているようなカスタム効果の実装で必要となる場合にのみ使用することをお勧めします。

## <a name="getalphamask-methods"></a>**GetAlphaMask** メソッド

[**Image**](/uwp/api/Windows.UI.Xaml.Controls.Image)、[**TextBlock**](/uwp/api/Windows.UI.Xaml.Controls.TextBlock)、[**Shape**](/uwp/api/Windows.UI.Xaml.Shapes.Shape) は、それぞれ、**GetAlphaMask** と呼ばれるメソッドを実装します。このメソッドは、要素の形状を使用したグレースケール画像を表す **CompositionBrush** を返します。 この **CompositionBrush** は、コンポジション **DropShadow** の入力として使用できます。そのため、シャドウでは、四角形ではなく要素の形状を反映することができます。 これにより、テキスト、アルファを含む画像、図形に対して、ピクセル パーフェクトで輪郭ベースのシャドウを使用することができます。 この API の例については、以下の「*ドロップ シャドウ*」をご覧ください。

## <a name="recipes"></a>レシピ

### <a name="reposition-animation"></a>位置変更アニメーション

コンポジションの暗黙的なアニメーションを使用すると、開発者は、要素の親の位置を基準とした、要素のレイアウトにおける変更を自動的にアニメーション化することができます。 たとえば、以下に示すボタンの **Margin** を変更した場合に、その新しいレイアウト位置に対して自動的にアニメーション化が行われます。

#### <a name="implementation-overview"></a>実装の概要

1. ターゲット要素のハンドアウト **Visual** を取得します
1. **Offset** プロパティの変更を自動的にアニメーション化する **ImplicitAnimationCollection** を作成します
1. **ImplicitAnimationCollection** をバッキング Visual に関連付けます

```xaml
<Button x:Name="RepositionTarget" Content="Click Me" />
```

```csharp
public MainPage()
{
    InitializeComponent();
    InitializeRepositionAnimation(RepositionTarget);
}

private void InitializeRepositionAnimation(UIElement repositionTarget)
{
    var targetVisual = ElementCompositionPreview.GetElementVisual(repositionTarget);
    Compositor compositor = targetVisual.Compositor;

    // Create an animation to animate targetVisual's Offset property to its final value
    var repositionAnimation = compositor.CreateVector3KeyFrameAnimation();
    repositionAnimation.Duration = TimeSpan.FromSeconds(0.66);
    repositionAnimation.Target = "Offset";
    repositionAnimation.InsertExpressionKeyFrame(1.0f, "this.FinalValue");

    // Run this animation when the Offset Property is changed
    var repositionAnimations = compositor.CreateImplicitAnimationCollection();
    repositionAnimations["Offset"] = repositionAnimation;

    targetVisual.ImplicitAnimations = repositionAnimations;
}
```

### <a name="drop-shadow"></a>ドロップ シャドウ

ピクセル パーフェクトなドロップ シャドウを **UIElement** (たとえば、画像を含んでいる**楕円**) に適用します。 シャドウでは、アプリで作成される **SpriteVisual** が必要となるため、**ElementCompositionPreview.SetElementChildVisual** を使用して、**SpriteVisual** が含まれる “ホスト” 要素を作成する必要があります。

#### <a name="implementation-overview"></a>実装の概要

1. ホスト要素のハンドアウト **Visual** を取得します
2. Windows.UI.Composition の **DropShadow** を作成します
3. マスクを使用してターゲット要素から図形を取得するように、**DropShadow** を構成します
    - 既定では、**DropShadow** は四角形になります。つまり、ターゲットが四角形である場合は、この構成は必要ありません
4. シャドウを新しい **SpriteVisual** にアタッチし、**SpriteVisual** をホスト要素の子として設定します
5. **ExpressionAnimation** を使用して、**SpriteVisual** のサイズをホストのサイズにバインドします

```xaml
<Grid Width="200" Height="200">
    <Canvas x:Name="ShadowHost" />
    <Ellipse x:Name="CircleImage">
        <Ellipse.Fill>
            <ImageBrush ImageSource="Assets/Images/2.jpg" Stretch="UniformToFill" />
        </Ellipse.Fill>
    </Ellipse>
</Grid>
```

```csharp
public MainPage()
{
    InitializeComponent();
    InitializeDropShadow(ShadowHost, CircleImage);
}

private void InitializeDropShadow(UIElement shadowHost, Shape shadowTarget)
{
    Visual hostVisual = ElementCompositionPreview.GetElementVisual(shadowHost);
    Compositor compositor = hostVisual.Compositor;

    // Create a drop shadow
    var dropShadow = compositor.CreateDropShadow();
    dropShadow.Color = Color.FromArgb(255, 75, 75, 80);
    dropShadow.BlurRadius = 15.0f;
    dropShadow.Offset = new Vector3(2.5f, 2.5f, 0.0f);
    // Associate the shape of the shadow with the shape of the target element
    dropShadow.Mask = shadowTarget.GetAlphaMask();

    // Create a Visual to hold the shadow
    var shadowVisual = compositor.CreateSpriteVisual();
    shadowVisual.Shadow = dropShadow;

    // Add the shadow as a child of the host in the visual tree
   ElementCompositionPreview.SetElementChildVisual(shadowHost, shadowVisual);

    // Make sure size of shadow host and shadow visual always stay in sync
    var bindSizeAnimation = compositor.CreateExpressionAnimation("hostVisual.Size");
    bindSizeAnimation.SetReferenceParameter("hostVisual", hostVisual);

    shadowVisual.StartAnimation("Size", bindSizeAnimation);
}
```

次の 2 つの一覧では、同じ XAML 構造を使用する、以前の C&#35; コードと同等の [C++/WinRT](../cpp-and-winrt-apis/index.md) および [C++/CX](/cpp/cppcx/visual-c-language-reference-c-cx) を示しています。

```cppwinrt
#include <winrt/Windows.UI.Composition.h>
#include <winrt/Windows.UI.Xaml.h>
#include <winrt/Windows.UI.Xaml.Hosting.h>
#include <winrt/Windows.UI.Xaml.Shapes.h>
...
MainPage()
{
    InitializeComponent();
    InitializeDropShadow(ShadowHost(), CircleImage());
}

int32_t MyProperty();
void MyProperty(int32_t value);

void InitializeDropShadow(Windows::UI::Xaml::UIElement const& shadowHost, Windows::UI::Xaml::Shapes::Shape const& shadowTarget)
{
    auto hostVisual{ Windows::UI::Xaml::Hosting::ElementCompositionPreview::GetElementVisual(shadowHost) };
    auto compositor{ hostVisual.Compositor() };

    // Create a drop shadow
    auto dropShadow{ compositor.CreateDropShadow() };
    dropShadow.Color(Windows::UI::ColorHelper::FromArgb(255, 75, 75, 80));
    dropShadow.BlurRadius(15.0f);
    dropShadow.Offset(Windows::Foundation::Numerics::float3{ 2.5f, 2.5f, 0.0f });
    // Associate the shape of the shadow with the shape of the target element
    dropShadow.Mask(shadowTarget.GetAlphaMask());

    // Create a Visual to hold the shadow
    auto shadowVisual = compositor.CreateSpriteVisual();
    shadowVisual.Shadow(dropShadow);

    // Add the shadow as a child of the host in the visual tree
    Windows::UI::Xaml::Hosting::ElementCompositionPreview::SetElementChildVisual(shadowHost, shadowVisual);

    // Make sure size of shadow host and shadow visual always stay in sync
    auto bindSizeAnimation{ compositor.CreateExpressionAnimation(L"hostVisual.Size") };
    bindSizeAnimation.SetReferenceParameter(L"hostVisual", hostVisual);

    shadowVisual.StartAnimation(L"Size", bindSizeAnimation);
}
```

```cpp
#include "WindowsNumerics.h"

MainPage::MainPage()
{
    InitializeComponent();
    InitializeDropShadow(ShadowHost, CircleImage);
}

void MainPage::InitializeDropShadow(Windows::UI::Xaml::UIElement^ shadowHost, Windows::UI::Xaml::Shapes::Shape^ shadowTarget)
{
    auto hostVisual = Windows::UI::Xaml::Hosting::ElementCompositionPreview::GetElementVisual(shadowHost);
    auto compositor = hostVisual->Compositor;

    // Create a drop shadow
    auto dropShadow = compositor->CreateDropShadow();
    dropShadow->Color = Windows::UI::ColorHelper::FromArgb(255, 75, 75, 80);
    dropShadow->BlurRadius = 15.0f;
    dropShadow->Offset = Windows::Foundation::Numerics::float3(2.5f, 2.5f, 0.0f);
    // Associate the shape of the shadow with the shape of the target element
    dropShadow->Mask = shadowTarget->GetAlphaMask();

    // Create a Visual to hold the shadow
    auto shadowVisual = compositor->CreateSpriteVisual();
    shadowVisual->Shadow = dropShadow;

    // Add the shadow as a child of the host in the visual tree
    Windows::UI::Xaml::Hosting::ElementCompositionPreview::SetElementChildVisual(shadowHost, shadowVisual);

    // Make sure size of shadow host and shadow visual always stay in sync
    auto bindSizeAnimation = compositor->CreateExpressionAnimation("hostVisual.Size");
    bindSizeAnimation->SetReferenceParameter("hostVisual", hostVisual);

    shadowVisual->StartAnimation("Size", bindSizeAnimation);
}
```

### <a name="frosted-glass"></a>すりガラス

背景コンテンツをぼかしたり、濃淡を付けたりする効果を作成します。 開発者は、効果を使用するために Win2D NuGet パッケージをインストールする必要があります。 インストール手順については、[Win2D のホームページ](https://microsoft.github.io/Win2D/html/Introduction.htm) をご覧ください。

#### <a name="implementation-overview"></a>実装の概要

1.  ホスト要素のハンドアウト **Visual** を取得します
2.  Win2D と **CompositionEffectSourceParameter** を使用して、ぼかし効果ツリーを作成します
3.  効果ツリーに基づいて **CompositionEffectBrush** を作成します
4.  **CompositionEffectBrush** の入力を **CompositionBackdropBrush** に設定します。これにより、効果が **SpriteVisual** の背景にあるコンテンツに適用されます
5.  新しい**SpriteVisual**のコンテンツとして**CompositionEffectBrush**を設定し、 **SpriteVisual**をホスト要素の子として設定します。 代わりに XamlCompositionBrushBase を使用することもできます。
6.  **ExpressionAnimation** を使用して、**SpriteVisual** のサイズをホストのサイズにバインドします

```xaml
<Grid Width="300" Height="300" Grid.Column="1">
    <Image
        Source="Assets/Images/2.jpg"
        Width="200"
        Height="200" />
    <Canvas
        x:Name="GlassHost"
        Width="150"
        Height="300"
        HorizontalAlignment="Right" />
</Grid>
```

```csharp
public MainPage()
{
    InitializeComponent();
    InitializeFrostedGlass(GlassHost);
}

private void InitializeFrostedGlass(UIElement glassHost)
{
    Visual hostVisual = ElementCompositionPreview.GetElementVisual(glassHost);
    Compositor compositor = hostVisual.Compositor;

    // Create a glass effect, requires Win2D NuGet package
    var glassEffect = new GaussianBlurEffect
    { 
        BlurAmount = 15.0f,
        BorderMode = EffectBorderMode.Hard,
        Source = new ArithmeticCompositeEffect
        {
            MultiplyAmount = 0,
            Source1Amount = 0.5f,
            Source2Amount = 0.5f,
            Source1 = new CompositionEffectSourceParameter("backdropBrush"),
            Source2 = new ColorSourceEffect
            {
                Color = Color.FromArgb(255, 245, 245, 245)
            }
        }
    };

    //  Create an instance of the effect and set its source to a CompositionBackdropBrush
    var effectFactory = compositor.CreateEffectFactory(glassEffect);
    var backdropBrush = compositor.CreateBackdropBrush();
    var effectBrush = effectFactory.CreateBrush();

    effectBrush.SetSourceParameter("backdropBrush", backdropBrush);

    // Create a Visual to contain the frosted glass effect
    var glassVisual = compositor.CreateSpriteVisual();
    glassVisual.Brush = effectBrush;

    // Add the blur as a child of the host in the visual tree
    ElementCompositionPreview.SetElementChildVisual(glassHost, glassVisual);

    // Make sure size of glass host and glass visual always stay in sync
    var bindSizeAnimation = compositor.CreateExpressionAnimation("hostVisual.Size");
    bindSizeAnimation.SetReferenceParameter("hostVisual", hostVisual);

    glassVisual.StartAnimation("Size", bindSizeAnimation);
}
```

## <a name="additional-resources"></a>その他のリソース

- [ビジュアル レイヤーの概要](./visual-layer.md)
- [**ElementCompositionPreview** クラス](/uwp/api/Windows.UI.Xaml.Hosting.ElementCompositionPreview)
- [Windowsuidevlabs GitHub](https://github.com/microsoft/WindowsCompositionSamples)の高度な UI とコンポジションのサンプル
- [BasicXamlInterop のサンプル](https://github.com/microsoft/WindowsCompositionSamples/tree/master/SampleGallery/Samples/SDK%2010586/BasicXamlInterop)
- [ParallaxingListItems のサンプル](https://github.com/microsoft/WindowsCompositionSamples/tree/master/SampleGallery/Samples/SDK%2010586/ParallaxingListItems)