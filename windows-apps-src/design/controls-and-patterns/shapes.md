---
ms.assetid: 54CC0BD4-1961-44D7-AB40-6E8B58E42D65
title: 図形の描画
description: 楕円形、長方形、多角形、パスなどの図形を描画する方法について説明します。 Path クラスは、きわめて複雑なベクター ベースの画像記述言語を XAML UI で視覚化するための手段です。たとえば、ベジエ曲線を描画することができます。
ms.date: 11/16/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: a33670f69d86a913288608ff07efb72edab8fd17
ms.sourcegitcommit: 4f032d7bb11ea98783db937feed0fa2b6f9950ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91829662"
---
# <a name="draw-shapes"></a>図形の描画

楕円形、長方形、多角形、パスなどの図形を描画する方法について説明します。 [**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) クラスは、きわめて複雑なベクター ベースの画像記述言語を XAML UI で視覚化するための手段です。たとえば、ベジエ曲線を描画することができます。

> **重要な API**: [Path クラス](/uwp/api/Windows.UI.Xaml.Shapes.Path)、[Windows.UI.Xaml.Shapes 名前空間](/uwp/api/Windows.UI.Xaml.Shapes)、[Windows.UI.Xaml.Media 名前空間](/uwp/api/Windows.UI.Xaml.Media)


XAML UI に空間領域を定義するクラスのセットには、[**Shape**](/uwp/api/Windows.UI.Xaml.Shapes.Shape) と [**Geometry**](/uwp/api/Windows.UI.Xaml.Media.Geometry) の 2 つがあります。 これらのクラス間の主な違いは、**Shape** にはブラシが関連付けられ、画面にレンダリングできますが、**Geometry** は単に空間領域を定義するだけで、レンダリングはされない (ただし、別の UI プロパティに情報を提供する働きはある) という点です。 **Shape** は、**Geometry** で境界線が定義される [**UIElement**](/uwp/api/Windows.UI.Xaml.UIElement) と考えることができます。 このトピックでは、主に **Shape** クラスについて説明します。

[**Shape**](/uwp/api/Windows.UI.Xaml.Shapes.Shape) クラスには、[**Line**](/uwp/api/Windows.UI.Xaml.Shapes.Line)、[**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse)、[**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle)、[**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon)、[**Polyline**](/uwp/api/Windows.UI.Xaml.Shapes.Polyline)、[**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) があります。 中でも **Path** は、任意のジオメトリを定義できる興味深いクラスです。また、[**Geometry**](/uwp/api/Windows.UI.Xaml.Media.Geometry) クラスは **Path** の構成要素を定義する方法の 1 つであるため、ここに関与します。

## <a name="fill-and-stroke-for-shapes"></a>図形の Fill と Stroke

[**Shape**](/uwp/api/Windows.UI.Xaml.Shapes.Shape) をアプリのキャンバスにレンダリングするには、[**Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) を関連付ける必要があります。 **Shape** の [**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) プロパティを目的の **Brush** に設定します。 ブラシについて詳しくは、「[ブラシの使用](../style/brushes.md)」をご覧ください。

[**Shape**](/uwp/api/Windows.UI.Xaml.Shapes.Shape) には、[**Stroke**](/uwp/api/windows.ui.xaml.shapes.shape.stroke) という、図形の周囲に描画される境界線を設定することもできます。 **Stroke** にも、その外観を定義する [**Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) が必要です。また、[**StrokeThickness**](/uwp/api/windows.ui.xaml.shapes.shape.strokethickness) が 0 以外の値に設定されている必要があります。 **StrokeThickness** は、図形の境界線の太さを定義するプロパティです。 **Stroke** に対して **Brush** 値を指定しなかった場合、または **StrokeThickness** を 0 に設定した場合、図形の周囲に境界線が描画されません。

## <a name="ellipse"></a>Ellipse

[**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) は、曲線の境界を持つ図形です。 基本的な **Ellipse** を作成するには、[**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) と [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height)、および [**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) に対する [**Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) を指定します。

次の例では、[**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) を 200、[**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) を 200 に設定し、色が [**SteelBlue**](/uwp/api/windows.ui.colors.steelblue) の [**SolidColorBrush**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) を [**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) に指定して、[**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) を作成します。

```xaml
<Ellipse Fill="SteelBlue" Height="200" Width="200" />
```

```csharp
var ellipse1 = new Ellipse();
ellipse1.Fill = new SolidColorBrush(Windows.UI.Colors.SteelBlue);
ellipse1.Width = 200;
ellipse1.Height = 200;

// When you create a XAML element in code, you have to add
// it to the XAML visual tree. This example assumes you have
// a panel named 'layoutRoot' in your XAML file, like this:
// <Grid x:Name="layoutRoot>
layoutRoot.Children.Add(ellipse1);
```

この [**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) をレンダリングすると、次のようになります。

![レンダリングされた Ellipse。](images/shapes-ellipse.jpg)

この [**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) は、ほとんどの人が円と考える形状になっていますが、XAML ではまさにこのようにして円形を宣言します。つまり、**Ellipse** の [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) と [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) を等しい値に設定します。

[**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) を UI レイアウトに配置すると、そのサイズは、対応する [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) と [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) を持つ四角形と同じであると見なされます。境界の外側の領域は、レンダリングは適用されませんが、レイアウト スロットのサイズの一部として扱われます。

一連の 6 つの [**Ellipse**](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) 要素は [**ProgressRing**](/uwp/api/Windows.UI.Xaml.Controls.ProgressRing) コントロールのコントロール テンプレートの一部であり、2 つの同心の **Ellipse** 要素は [**RadioButton**](/uwp/api/Windows.UI.Xaml.Controls.RadioButton) の一部です。

## <a name="span-idrectanglespanspan-idrectanglespanspan-idrectanglespanrectangle"></a><span id="Rectangle"></span><span id="rectangle"></span><span id="RECTANGLE"></span>Rectangle

[**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) は、向かい合った辺の長さがそれぞれ等しい四辺形です。 基本的な **Rectangle** を作成するには、[**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width)、[**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height)、[**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) を指定します。

[**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) は、コーナーを角丸にすることもできます。 角丸コーナーを作成するには、[**RadiusX**](/uwp/api/windows.ui.xaml.shapes.rectangle.radiusx) および [**RadiusY**](/uwp/api/windows.ui.xaml.shapes.rectangle.radiusy) プロパティの値を指定します。 これらのプロパティは、コーナーの曲線を定義する楕円形の X 軸と Y 軸を指定します。 **RadiusX** の最大値は [**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) の 1/2 であり、**RadiusY** の最大値は [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) の 1/2 です。

次の例では、[**Width**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Width) が 200 で [**Height**](/uwp/api/Windows.UI.Xaml.FrameworkElement.Height) が 100 の [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) を作成します。 [**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) には値が [**Blue**](/uwp/api/windows.ui.colors.blue) の [**SolidColorBrush**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) を使い、[**Stroke**](/uwp/api/windows.ui.xaml.shapes.shape.stroke) には値が [**Black**](/uwp/api/windows.ui.colors.black) の **SolidColorBrush** を使っています。 [**StrokeThickness**](/uwp/api/windows.ui.xaml.shapes.shape.strokethickness) は 3 に設定します。 [**RadiusX**](/uwp/api/windows.ui.xaml.shapes.rectangle.radiusx) プロパティを 50、[**RadiusY**](/uwp/api/windows.ui.xaml.shapes.rectangle.radiusy) プロパティを 10 に設定することで、**Rectangle** を角丸コーナーにしています。

```xaml
<Rectangle Fill="Blue"
           Width="200"
           Height="100"
           Stroke="Black"
           StrokeThickness="3"
           RadiusX="50"
           RadiusY="10" />
```

```csharp
var rectangle1 = new Rectangle();
rectangle1.Fill = new SolidColorBrush(Windows.UI.Colors.Blue);
rectangle1.Width = 200;
rectangle1.Height = 100;
rectangle1.Stroke = new SolidColorBrush(Windows.UI.Colors.Black);
rectangle1.StrokeThickness = 3;
rectangle1.RadiusX = 50;
rectangle1.RadiusY = 10;

// When you create a XAML element in code, you have to add
// it to the XAML visual tree. This example assumes you have
// a panel named 'layoutRoot' in your XAML file, like this:
// <Grid x:Name="layoutRoot>
layoutRoot.Children.Add(rectangle1);
```

この [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) をレンダリングすると、次のようになります。

![レンダリングされた Rectangle。](images/shapes-rectangle.jpg)

**ヒント**  UI の定義のシナリオで、[**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) よりも [**Border**](/uwp/api/Windows.UI.Xaml.Controls.Border) を使った方が適している場合があります。 一般に、コンテンツの周囲に四角形の図形を作成することが目的であるときは、**Border** の方が適しています。子のコンテンツを設定できるほか、高さと幅によってサイズが固定されている **Rectangle** とは異なり、コンテンツに合わせてサイズが自動的に調整されるためです。 **Border** は、[**CornerRadius**](/uwp/api/windows.ui.xaml.controls.border.cornerradius) プロパティを設定することによって、角に丸みを持たせることもできます。

また、[**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) は、コントロールの合成に適したオプションであると考えられます。 **Rectangle** の図形は多くのコントロール テンプレートで使われます。これは、フォーカス対応コントロールの "FocusVisual" 部分としてこの図形が使われるためです。 コントロールが "Focused" の表示状態にある場合は常に、この四角形が表示されます。その他の状態にある場合は非表示です。

## <a name="polygon"></a>多角形

[**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) は、任意の数の点によって境界線を定義した図形です。 1 つの点から次の点まで直線でつなぎ、最後の点を最初の点につなぐことで、境界線を作成します。 [**Points**](/uwp/api/windows.ui.xaml.shapes.polygon.points) プロパティによって、境界線を構成する点のコレクションが定義されます。 XAML では、これらの点をコンマ区切り一覧で定義します。 分離コードでは、[**PointCollection**](/uwp/api/Windows.UI.Xaml.Media.PointCollection) を使って点のコレクションを定義し、それぞれの点を [**Point**](/uwp/api/Windows.Foundation.Point) 値としてコレクションに追加します。

始点と終点が同じ [**Point**](/uwp/api/Windows.Foundation.Point) 値となるような点を明示的に宣言する必要はありません。 [**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) のレンダリング ロジックが、閉じた図形を想定して暗黙的に終点を始点に接続します。

次の例では、4 つの点を `(10,200)`、`(60,140)`、`(130,140)`、`(180,200)` に設定した [**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) を作成します。 [**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) には、[**SolidColorBrush**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) の [**LightBlue**](/uwp/api/windows.ui.colors.lightblue) 値を使います。[**Stroke**](/uwp/api/windows.ui.xaml.shapes.shape.stroke) には値を割り当てていないので、境界の輪郭は描画されません。

```xaml
<Polygon Fill="LightBlue"
         Points="10,200,60,140,130,140,180,200" />
```

```csharp
var polygon1 = new Polygon();
polygon1.Fill = new SolidColorBrush(Windows.UI.Colors.LightBlue);

var points = new PointCollection();
points.Add(new Windows.Foundation.Point(10, 200));
points.Add(new Windows.Foundation.Point(60, 140));
points.Add(new Windows.Foundation.Point(130, 140));
points.Add(new Windows.Foundation.Point(180, 200));
polygon1.Points = points;

// When you create a XAML element in code, you have to add
// it to the XAML visual tree. This example assumes you have
// a panel named 'layoutRoot' in your XAML file, like this:
// <Grid x:Name="layoutRoot>
layoutRoot.Children.Add(polygon1);
```

この [**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) をレンダリングすると、次のようになります。

![レンダリングされた Polygon。](images/shapes-polygon.jpg)

**ヒント**  [**Point**](/uwp/api/Windows.Foundation.Point) の値は、図形の頂点を宣言する場合以外のシナリオで XAML の型としてよく使われます。 たとえば、**Point** はタッチ イベントのイベント データの一部であるため、座標空間におけるタッチ操作が発生した位置を正確に認識することができます。 **Point** の詳しい情報と、それを XAML やコードで使う方法については、API リファレンスの [**Point**](/uwp/api/Windows.Foundation.Point) のトピックをご覧ください。

## <a name="line"></a>行

[**Line**](/uwp/api/Windows.UI.Xaml.Shapes.Line) は、座標空間において 2 点間に描画される単純な直線です。 **Line** は内部領域を持たないため、[**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) に何か値を指定してもすべて無視されます。 **Line** には、[**Stroke**](/uwp/api/windows.ui.xaml.shapes.shape.stroke) プロパティと [**StrokeThickness**](/uwp/api/windows.ui.xaml.shapes.shape.strokethickness) プロパティの値を必ず指定してください。指定しないと、**Line** はレンダリングされません。

[**Line**](/uwp/api/Windows.UI.Xaml.Shapes.Line) 図形を指定する際、[**Point**](/uwp/api/Windows.Foundation.Point) 値は使いません。[**X1**](/uwp/api/windows.ui.xaml.shapes.line.x1)、[**Y1**](/uwp/api/windows.ui.xaml.shapes.line.y1)、[**X2**](/uwp/api/windows.ui.xaml.shapes.line.x2)、[**Y2**](/uwp/api/windows.ui.xaml.shapes.line.y2) のそれぞれに対して個別に [**Double**](/dotnet/api/system.double) 値を指定します。 これで、水平方向または垂直方向の直線に対する最低限のマークアップは完成します。 たとえば、長さ 400 ピクセルの水平方向の直線を定義するには、`<Line Stroke="Red" X2="400"/>` とします。 その他の X,Y プロパティは既定で 0 に設定されるため、点で見た場合、この XAML は `(0,0)` から `(400,0)` に直線を描画していることになります。 (0,0) 以外の点から開始する必要がある場合は、[**TranslateTransform**](/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) を使って **Line** 全体を移動することができます。

```xaml
<Line Stroke="Red" X2="400"/>
```

```csharp
var line1 = new Line();
line1.Stroke = new SolidColorBrush(Windows.UI.Colors.Red);
line1.X2 = 400;

// When you create a XAML element in code, you have to add
// it to the XAML visual tree. This example assumes you have
// a panel named 'layoutRoot' in your XAML file, like this:
// <Grid x:Name="layoutRoot>
layoutRoot.Children.Add(line1);
```

## <a name="span-id_polylinespanspan-id_polylinespanspan-id_polylinespan-polyline"></a><span id="_Polyline"></span><span id="_polyline"></span><span id="_POLYLINE"></span> Polyline

[**Polyline**](/uwp/api/Windows.UI.Xaml.Shapes.Polyline) は、[**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) と同様に、図形の境界線を点のセットによって定義しますが、**Polyline** では最後の点が最初の点に接続されません。

**注**  [**Polyline**](/uwp/api/Windows.UI.Xaml.Shapes.Polyline) の始点と終点が等しくなるように明示的に [**Points**](/uwp/api/windows.ui.xaml.shapes.polyline.points) を設定することもできますが、その場合は、[**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) を使うのが一般的です。

[**Polyline**](/uwp/api/Windows.UI.Xaml.Shapes.Polyline) の [**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) を指定した場合、**Polyline** に対して設定された [**Points**](/uwp/api/windows.ui.xaml.shapes.polyline.points) の始点と終点が交わらなくても、図形の内部領域が **Fill** によって塗りつぶされます。 **Polyline** で **Fill** を指定しなかった場合のレンダリングは、複数の [**Line**](/uwp/api/Windows.UI.Xaml.Shapes.Line) 要素を個別に指定し、前の直線の終点が次の直線の始点と交わるようにした場合と同様の結果となります。

[**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) の場合と同様に、[**Points**](/uwp/api/windows.ui.xaml.shapes.polyline.points) プロパティによって境界線を構成する点のコレクションが定義されます。 XAML では、これらの点をコンマ区切り一覧で定義します。 コード ビハインドでは、[**PointCollection**](/uwp/api/Windows.UI.Xaml.Media.PointCollection) を使って点のコレクションを定義し、それぞれの点を [**Point**](/uwp/api/Windows.Foundation.Point) 構造体としてコレクションに追加します。

次の例では、4 つの点を `(10,200)`、`(60,140)`、`(130,140)`、`(180,200)` に設定した [**Polyline**](/uwp/api/Windows.UI.Xaml.Shapes.Polyline) を作成します。 [**Stroke**](/uwp/api/windows.ui.xaml.shapes.shape.stroke) は定義されていますが、[**Fill**](/uwp/api/windows.ui.xaml.shapes.shape.fill) は定義されていません。

```xaml
<Polyline Stroke="Black"
        StrokeThickness="4"
        Points="10,200,60,140,130,140,180,200" />
```

```csharp
var polyline1 = new Polyline();
polyline1.Stroke = new SolidColorBrush(Windows.UI.Colors.Black);
polyline1.StrokeThickness = 4;

var points = new PointCollection();
points.Add(new Windows.Foundation.Point(10, 200));
points.Add(new Windows.Foundation.Point(60, 140));
points.Add(new Windows.Foundation.Point(130, 140));
points.Add(new Windows.Foundation.Point(180, 200));
polyline1.Points = points;

// When you create a XAML element in code, you have to add
// it to the XAML visual tree. This example assumes you have
// a panel named 'layoutRoot' in your XAML file, like this:
// <Grid x:Name="layoutRoot>
layoutRoot.Children.Add(polyline1);
```

この [**Polyline**](/uwp/api/Windows.UI.Xaml.Shapes.Polyline) をレンダリングすると、次のようになります。 [**Polygon**](/uwp/api/Windows.UI.Xaml.Shapes.Polygon) とは異なり、[**Stroke**](/uwp/api/windows.ui.xaml.shapes.shape.stroke) の最初と最後の点が接続されないことに注意してください。

![レンダリングされた Polyline。](images/shapes-polyline.jpg)

## <a name="path"></a>Path

[**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) は、任意の形状を定義するために使える、最も用途が広い [**Shape**](/uwp/api/Windows.UI.Xaml.Shapes.Shape) です。 ただし、用途が広い反面、複雑さも伴います。 次に、XAML で基本的な **Path** を作成する方法を紹介します。

パスの形状は、[**Data**](/uwp/api/windows.ui.xaml.shapes.path.data) プロパティで定義します。 **Data** の設定には次の 2 つの方法があります。

- [**Data**](/uwp/api/windows.ui.xaml.shapes.path.data) には、XAML で文字列値を設定することができます。 この場合、**Path.Data** の値には、グラフィックスのシリアル化形式が使われます。 一般に、いったん構築されたこの値をテキストとして (文字列形式として) 編集することはしません。 サーフェス上のデザインや図面のメタファーを扱うことのできるデザイン ツールを使います。 その出力結果を保存 (またはエクスポート) すると、**Path.Data** 情報を含んだ XAML ファイルまたは XAML 文字列フラグメントが得られます。
- [**Data**](/uwp/api/windows.ui.xaml.shapes.path.data) プロパティは、単一の [**Geometry**](/uwp/api/Windows.UI.Xaml.Media.Geometry) オブジェクトに設定できます。 この設定は、コードまたは XAML で行うことができます。 この単一の **Geometry** は通常、[**GeometryGroup**](/uwp/api/windows.ui.xaml.media.geometrygroup) です。オブジェクト モデルの趣旨に沿って、複数のジオメトリ定義を 1 つのオブジェクトに合成できるコンテナーとして機能します。 これは主に、[**PathFigure**](/uwp/api/Windows.UI.Xaml.Media.PathFigure) の [**Segments**](/uwp/api/windows.ui.xaml.media.pathfigure.segments) 値として定義される曲線と複雑な図形を、場合によっては複数組み合わせて使う必要があるとき ([**BezierSegment**](/uwp/api/Windows.UI.Xaml.Media.BezierSegment) など) に用いる方法です。

この例に示す [**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) は、Blend for Visual Studio を使っていくつかのベクター図形を生成し、その結果を XAML として保存したものです。 **Path** 全体は、ベジエ曲線セグメントと直線セグメントから成ります。 この例の目的は、[**Path.Data**](/uwp/api/windows.ui.xaml.shapes.path.data) のシリアル化形式にどのような要素が存在し、各数値が何を表しているかをわかりやすく紹介することです。

この [**Data**](/uwp/api/windows.ui.xaml.shapes.path.data) は、"M" で示される移動コマンドによって開始され、これによってパスの絶対開始点が設定されます。

最初のセグメントは、`(100,200)` から始まり `(400,175)` で終わる三次ベジエ曲線であり、2 つの制御点 `(100,25)` および `(400,350)` を使って描かれます。 このセグメントは、[**Data**](/uwp/api/windows.ui.xaml.shapes.path.data) 属性文字列の "C" コマンドによって示されます。

2 番目のセグメントは、絶対水平直線コマンド "H" によって開始されます。これは、前のサブパスの終点 `(400,175)` から新しい終点 `(280,175)` まで描かれる直線を指定します。 これは水平直線コマンドであるため、指定される値は X 座標です。

```xaml
<Path Stroke="DarkGoldenRod" 
      StrokeThickness="3"
      Data="M 100,200 C 100,25 400,350 400,175 H 280" />
```

この [**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) をレンダリングすると、次のようになります。

![レンダリングされたシンプルなパスのスクリーンショット。](images/shapes-path.jpg)

次の例は、説明済みの手法である [**PathGeometry**](/uwp/api/Windows.UI.Xaml.Media.PathGeometry) を使った [**GeometryGroup**](/uwp/api/windows.ui.xaml.media.geometrygroup) の使用方法を示しています。 この例では、**PathGeometry** の一部として使うことができる関連ジオメトリ型の一部、つまり [**PathFigure**](/uwp/api/Windows.UI.Xaml.Media.PathFigure) と、[**PathFigure.Segments**](/uwp/api/windows.ui.xaml.media.pathfigure.segments) のセグメントとなるさまざまな要素を実行します。

```xaml
<Path Stroke="Black" StrokeThickness="1" Fill="#CCCCFF">
    <Path.Data>
        <GeometryGroup>
            <RectangleGeometry Rect="50,5 100,10" />
            <RectangleGeometry Rect="5,5 95,180" />
            <EllipseGeometry Center="100, 100" RadiusX="20" RadiusY="30"/>
            <RectangleGeometry Rect="50,175 100,10" />
            <PathGeometry>
                <PathGeometry.Figures>
                    <PathFigureCollection>
                        <PathFigure IsClosed="true" StartPoint="50,50">
                            <PathFigure.Segments>
                                <PathSegmentCollection>
                                    <BezierSegment Point1="75,300" Point2="125,100" Point3="150,50"/>
                                    <BezierSegment Point1="125,300" Point2="75,100"  Point3="50,50"/>
                                </PathSegmentCollection>
                            </PathFigure.Segments>
                        </PathFigure>
                    </PathFigureCollection>
                </PathGeometry.Figures>
            </PathGeometry>
        </GeometryGroup>
    </Path.Data>
</Path>
```

```csharp
var path1 = new Windows.UI.Xaml.Shapes.Path();
path1.Fill = new SolidColorBrush(Windows.UI.Color.FromArgb(255, 204, 204, 255));
path1.Stroke = new SolidColorBrush(Windows.UI.Colors.Black);
path1.StrokeThickness = 1;

var geometryGroup1 = new GeometryGroup();
var rectangleGeometry1 = new RectangleGeometry();
rectangleGeometry1.Rect = new Rect(50, 5, 100, 10);
var rectangleGeometry2 = new RectangleGeometry();
rectangleGeometry2.Rect = new Rect(5, 5, 95, 180);
geometryGroup1.Children.Add(rectangleGeometry1);
geometryGroup1.Children.Add(rectangleGeometry2);

var ellipseGeometry1 = new EllipseGeometry();
ellipseGeometry1.Center = new Point(100, 100);
ellipseGeometry1.RadiusX = 20;
ellipseGeometry1.RadiusY = 30;
geometryGroup1.Children.Add(ellipseGeometry1);

var pathGeometry1 = new PathGeometry();
var pathFigureCollection1 = new PathFigureCollection();
var pathFigure1 = new PathFigure();
pathFigure1.IsClosed = true;
pathFigure1.StartPoint = new Windows.Foundation.Point(50, 50);
pathFigureCollection1.Add(pathFigure1);
pathGeometry1.Figures = pathFigureCollection1;

var pathSegmentCollection1 = new PathSegmentCollection();
var pathSegment1 = new BezierSegment();
pathSegment1.Point1 = new Point(75, 300);
pathSegment1.Point2 = new Point(125, 100);
pathSegment1.Point3 = new Point(150, 50);
pathSegmentCollection1.Add(pathSegment1);

var pathSegment2 = new BezierSegment();
pathSegment2.Point1 = new Point(125, 300);
pathSegment2.Point2 = new Point(75, 100);
pathSegment2.Point3 = new Point(50, 50);
pathSegmentCollection1.Add(pathSegment2);
pathFigure1.Segments = pathSegmentCollection1;

geometryGroup1.Children.Add(pathGeometry1);
path1.Data = geometryGroup1;

// When you create a XAML element in code, you have to add
// it to the XAML visual tree. This example assumes you have
// a panel named 'layoutRoot' in your XAML file, like this:
// <Grid x:Name="layoutRoot>
layoutRoot.Children.Add(path1);
```

この [**Path**](/uwp/api/Windows.UI.Xaml.Shapes.Path) をレンダリングすると、次のようになります。

![レンダリングされた複雑なパスのスクリーンショット。](images/shapes-path-2.png)

[**PathGeometry**](/uwp/api/Windows.UI.Xaml.Media.PathGeometry) を使うと、[**Path.Data**](/uwp/api/windows.ui.xaml.shapes.path.data) 文字列を設定した場合よりも読みやすくなることがあります。 また、[**Path.Data**](/uwp/api/windows.ui.xaml.shapes.path.data) では、スケーラブル ベクター グラフィックス (SVG) の画像パスの定義と互換性のある構文が使われます。これにより、SVG からグラフィックスを移植したり、Blend などのツールからの出力として移植したりする際に役立ちます。