---
title: 関心のあるポイント (POI) の地図への表示
description: プッシュピン、画像、図形、XAML UI 要素を使って、関心のあるポイント (POI) を地図に追加します。
ms.assetid: CA00D8EB-6C1B-4536-8921-5EAEB9B04FCA
ms.date: 08/11/2017
ms.topic: article
keywords: Windows 10, UWP, 地図, 位置情報, プッシュピン
ms.localizationpriority: medium
ms.openlocfilehash: c27132c0728c85238b80e710c62d2e733ee1dd5d
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89155806"
---
# <a name="display-points-of-interest-on-a-map"></a>関心のあるポイントの地図への表示

プッシュピン、画像、図形、XAML UI 要素を使って、関心のあるポイント (POI) を地図に追加します。 POI は、地図上の特定のポイントであり、関心のあるものを表します。 たとえば、企業、市区町村、友人の所在地を示すことができます。

アプリで POI を表示する方法について詳しくは、GitHub の [Windows-universal-samples リポジトリ](https://github.com/Microsoft/Windows-universal-samples)から[ユニバーサル Windows プラットフォーム (UWP) の地図サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl)をダウンロードしてください。

地図にプッシュピン、画像、図形を表示するには、[**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon)、[**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard)、[**MapPolygon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapPolygon)、[**MapPolyline**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapPolyline) の各オブジェクトを、[**MapElementsLayer**](/uwp/api/windows.ui.xaml.controls.maps.mapelementslayer) オブジェクトの **MapElements** コレクションに追加します。 次に、そのレイヤー オブジェクトをマップ コントロールの **Layers** コレクションに追加します。

>[!NOTE]
> 以前のリリースでは、このガイドで、マップの要素を [**MapElements**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.MapElements) コレクションに追加する方法を示していました。 引き続き同じアプローチを使うこともできますが、その場合は新しいマップ レイヤー モデルの利点が活かされません。 詳しくは、このガイドの「[レイヤーの使用](#layers)」をご覧ください。

[**Button**](/uwp/api/Windows.UI.Xaml.Controls.Button)、[**HyperlinkButton**](/uwp/api/Windows.UI.Xaml.Controls.HyperlinkButton)、[**TextBlock**](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) などの XAML ユーザー インターフェイス要素を地図に表示することもできます。そのためには、それらの要素を [**MapItemsControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapItemsControl) に追加するか、[**MapControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の [**Children**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.children) として追加します。

地図に配置する要素の数が多い場合、[地図にタイル画像をオーバーレイする](overlay-tiled-images.md)ことを検討します。 地図に道路情報を表示するには、「[ルートとルート案内の表示](routes-and-directions.md)」をご覧ください。

## <a name="add-a-pushpin"></a>プッシュピンの追加

[**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) クラスを使って、プッシュピンなどの画像をオプションのテキストと共に地図に表示します。 既定の画像をそのまま使うか、[**Image**](/uwp/api/windows.ui.xaml.controls.maps.mapicon.image) プロパティを使ってカスタム画像を指定できます。 次の画像はそれぞれ、[**Title**](/uwp/api/windows.ui.xaml.controls.maps.mapicon.title) プロパティに値を指定しない、短いタイトル、長いタイトル、非常に長いタイトルを指定した場合の **MapIcon** の既定の画像です。

![さまざまな長さのタイトルを含むサンプルの MapIcon。](images/mapctrl-mapicons.png)

次の例では、シアトル市の地図を表示して、既定の画像とオプションのタイトルを使って [**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) を追加し、スペース ニードルの場所を示しています。 また、アイコンを地図の中央に配置し、拡大しています。 マップ コントロールを使用する方法に関する一般的な情報については、「[2D、3D、Streetside ビューでの地図の表示](display-maps.md)」をご覧ください。

```csharp
public void AddSpaceNeedleIcon()
{
    var MyLandmarks = new List<MapElement>();

    BasicGeoposition snPosition = new BasicGeoposition { Latitude = 47.620, Longitude = -122.349 };
    Geopoint snPoint = new Geopoint(snPosition);

    var spaceNeedleIcon = new MapIcon
    {
        Location = snPoint,
        NormalizedAnchorPoint = new Point(0.5, 1.0),
        ZIndex = 0,
        Title = "Space Needle"
    };

    MyLandmarks.Add(spaceNeedleIcon);

    var LandmarksLayer = new MapElementsLayer
    {
        ZIndex = 1,
        MapElements = MyLandmarks
    };

    myMap.Layers.Add(LandmarksLayer);

    myMap.Center = snPoint;
    myMap.ZoomLevel = 14;

}
```

この例では、次の POI (中央の既定の画像) が地図に表示されます。

![MapIcon を使った地図](images/displaypoidefault.png)

次のコード行では、プロジェクトの Assets フォルダーに保存されているカスタム イメージを使って [**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) が表示されます。 **MapIcon** の [**Image**](/uwp/api/windows.ui.xaml.controls.maps.mapicon.image) プロパティでは、[**RandomAccessStreamReference**](/uwp/api/Windows.Storage.Streams.RandomAccessStreamReference) 型の値が想定されています。 この型では、[**Windows.Storage.Streams**](/uwp/api/Windows.Storage.Streams) 名前空間用に **using** ステートメントが必要になります。

>[!NOTE]
>複数の地図アイコンに同じ画像を使う場合は、パフォーマンスが最大限に高まるように、ページ レベルまたはアプリ レベルで [**RandomAccessStreamReference**](/uwp/api/Windows.Storage.Streams.RandomAccessStreamReference) を宣言します。

```csharp
    MapIcon1.Image =
        RandomAccessStreamReference.CreateFromUri(new Uri("ms-appx:///Assets/customicon.png"));
```

[**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) クラスを使うときは、次の考慮事項を念頭に置いてください。

-   [**Image**](/uwp/api/windows.ui.xaml.controls.maps.mapicon.image) プロパティがサポートしている最大画像サイズは 2048 × 2048 ピクセルです。
-   既定では、地図アイコンの画像は必ず表示されるとは限りません。 このクラスが地図上の他の要素やラベルを覆い隠す場合には、このクラスは非表示になることがあります。 地図アイコンを表示したままにするには、このアイコンの [**CollisionBehaviorDesired**](/uwp/api/windows.ui.xaml.controls.maps.mapicon.collisionbehaviordesired) プロパティを [**MapElementCollisionBehavior.RemainVisible**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapElementCollisionBehavior) に設定します。
-   [**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) のオプションの [**Title**](/uwp/api/windows.ui.xaml.controls.maps.mapicon.title) は、必ず表示されるとは限りません。 テキストが表示されない場合は、[**MapControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の [**ZoomLevel**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel) プロパティの値を減らして、地図を縮小してください。
-   地図上の特定の場所を指す [**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) 画像 (たとえば、プッシュピンや矢印など) を表示する場合は、[**NormalizedAnchorPoint**](/uwp/api/windows.ui.xaml.controls.maps.mapicon.normalizedanchorpoint) プロパティの値を画像上にあるポインターのおおよその位置に設定することを検討してください。 **NormalizedAnchorPoint** の値を、画像の左上隅を示す既定値 (0, 0) のままにした場合、地図の [**ZoomLevel**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel) を変更すると、画像が別の場所を示した状態になる可能性があります。
-   [Altitude](/uwp/api/windows.devices.geolocation.basicgeoposition) と [AltitudeReferenceSystem](/uwp/api/windows.devices.geolocation.geopoint.AltitudeReferenceSystem) を明示的に設定しない場合、[**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) はサーフェスに配置されます。

## <a name="add-a-3d-pushpin"></a>3D プッシュピンの追加

3 次元オブジェクトをマップに追加できます。 [MapModel3D](/uwp/api/windows.ui.xaml.controls.maps.mapmodel3d) クラスを使って、[3D Manufacturing Format (3MF)](https://3mf.io/specification/) ファイルから 3D オブジェクトをインポートします。

次の画像では、3D のコーヒー カップを使って、付近の喫茶店の場所を示しています。

![地図上のマグ](images/mugs.png)

次のコードでは、3MF ファイルのインポートを使って、地図にコーヒー カップを追加します。 シンプルにするために、このコードでは地図の中央に画像を追加していますが、実際のコードでは通常、特定の場所に画像を追加することになります。

```csharp
public async void Add3DMapModel()
{
    var mugStreamReference = RandomAccessStreamReference.CreateFromUri
        (new Uri("ms-appx:///Assets/mug.3mf"));

    var myModel = await MapModel3D.CreateFrom3MFAsync(mugStreamReference,
        MapModel3DShadingOption.Smooth);

    myMap.Layers.Add(new MapElementsLayer
    {
       ZIndex = 1,
       MapElements = new List<MapElement>
       {
          new MapElement3D
          {
              Location = myMap.Center,
              Model = myModel,
          },
       },
    });
}
```

## <a name="add-an-image"></a>イメージの追加

レストランやランドマークの画像など、地図の場所に関連する大きい画像を表示します。 ユーザーが地図を縮小すると、画像のサイズも比例的に縮小され、より広い範囲の地図を表示できるようになります。 これは特定の場所をマークする [**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon) とは少し異なります。MapIcon は小さいのが通常で、ユーザーが地図の拡大や縮小を行ってもサイズは変わりません。

![MapBillboard 画像](images/map-billboard.png)

次のコードは、上記の画像に表示されている [**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) を示しています。

```csharp
public void AddLandmarkPhoto()
{
    // Create MapBillboard.

    RandomAccessStreamReference mapBillboardStreamReference =
        RandomAccessStreamReference.CreateFromUri(new Uri("ms-appx:///Assets/billboard.jpg"));

    var mapBillboard = new MapBillboard(myMap.ActualCamera)
    {
        Location = myMap.Center,
        NormalizedAnchorPoint = new Point(0.5, 1.0),
        Image = mapBillboardStreamReference
    };

    // Add MapBillboard to a layer on the map control.

    var MyLandmarkPhotos = new List<MapElement>();

    MyLandmarkPhotos.Add(mapBillboard);

    var LandmarksPhotoLayer = new MapElementsLayer
    {
        ZIndex = 1,
        MapElements = MyLandmarkPhotos
    };

    myMap.Layers.Add(LandmarksPhotoLayer);
}
```

このコードには、少し詳しく説明するに値する部分が 3 つあります。画像、リファレンス カメラ、および [**NormalizedAnchorPoint**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard.NormalizedAnchorPoint) のことです。

### <a name="image"></a>Image

この例は、プロジェクトの **Assets** フォルダーに保存されたカスタム画像を示しています。 [**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) の [**Image**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard.Image) プロパティでは、[**RandomAccessStreamReference**](/uwp/api/Windows.Storage.Streams.RandomAccessStreamReference) 型の値が想定されています。 この型では、[**Windows.Storage.Streams**](/uwp/api/Windows.Storage.Streams) 名前空間用に **using** ステートメントが必要になります。

>[!NOTE]
>複数の地図アイコンに同じ画像を使う場合は、パフォーマンスが最大限に高まるように、ページ レベルまたはアプリ レベルで [**RandomAccessStreamReference**](/uwp/api/Windows.Storage.Streams.RandomAccessStreamReference) を宣言します。

### <a name="reference-camera"></a>リファレンス カメラ

 [**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) 画像は地図の [**ZoomLevel**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.ZoomLevel) の変更に合わせて拡大および縮小するため、その [**ZoomLevel**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.ZoomLevel) が標準の 1x 倍率のときに画像がどこに表示されるかを定義することが重要になります。 その位置は [**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) のリファレンス カメラで定義されます。リファレンス カメラを設定するには、[**MapCamera**](/uwp/api/windows.ui.xaml.controls.maps.mapcamera) オブジェクトを [**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) のコンストラクターに渡す必要があります。

 [**Geopoint**](/uwp/api/windows.devices.geolocation.geopoint) で目的の位置を定義し、その [**Geopoint**](/uwp/api/windows.devices.geolocation.geopoint) を使用することで、[**MapCamera**](/uwp/api/windows.ui.xaml.controls.maps.mapcamera) オブジェクトを作成できます。  ただし、この例で使用している [**MapCamera**](/uwp/api/windows.ui.xaml.controls.maps.mapcamera) オブジェクトは、単純にマップ コントロールの [**ActualCamera**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.ActualCamera) プロパティから返されたものです。 これは地図の内部カメラです。 このカメラの現在の位置がリファレンス カメラの位置となり、1x 倍率ではこの位置に [**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) 画像が表示されます。

 アプリでユーザーが地図を縮小できるようにしている場合、画像のサイズも縮小されます。これは、1x 倍率の画像はリファレンス カメラの位置で固定されたままになりますが、地図の内部カメラは高度が上がるためです。

### <a name="normalizedanchorpoint"></a>NormalizedAnchorPoint

[**NormalizedAnchorPoint**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard.NormalizedAnchorPoint) は、[**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) の [**Location**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard.Location) プロパティに固定される画像のポイントです。 ポイント 0.5,1 は画像の下部中央になります。 [**MapBillboard**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard) の [**Location**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard.Location) プロパティをマップ コントロールの中央に設定しているので、画像の下部中央がマップ コントロールの中央に固定されることになります。 ポイントが中心になるように画像を表示するには、[**NormalizedAnchorPoint**](/uwp/api/windows.ui.xaml.controls.maps.mapbillboard.NormalizedAnchorPoint) を 0.5,0.5 に設定します。  

## <a name="add-a-shape"></a>図形を追加する

マルチポイント図形を地図に表示するには、[**MapPolygon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapPolygon) クラスを使います。 次の例は、[UWP の地図サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl)から抜粋したもので、地図に赤色のボックス (境界線は青色) を表示します。

```csharp
public void HighlightArea()
{
    // Create MapPolygon.

    double centerLatitude = myMap.Center.Position.Latitude;
    double centerLongitude = myMap.Center.Position.Longitude;

    var mapPolygon = new MapPolygon
    {
        Path = new Geopath(new List<BasicGeoposition> {
                    new BasicGeoposition() {Latitude=centerLatitude+0.0005, Longitude=centerLongitude-0.001 },
                    new BasicGeoposition() {Latitude=centerLatitude-0.0005, Longitude=centerLongitude-0.001 },
                    new BasicGeoposition() {Latitude=centerLatitude-0.0005, Longitude=centerLongitude+0.001 },
                    new BasicGeoposition() {Latitude=centerLatitude+0.0005, Longitude=centerLongitude+0.001 },
                }),
        ZIndex = 1,
        FillColor = Colors.Red,
        StrokeColor = Colors.Blue,
        StrokeThickness = 3,
        StrokeDashed = false,
    };

    // Add MapPolygon to a layer on the map control.
    var MyHighlights = new List<MapElement>();

    MyHighlights.Add(mapPolygon);

    var HighlightsLayer = new MapElementsLayer
    {
        ZIndex = 1,
        MapElements = MyHighlights
    };

    myMap.Layers.Add(HighlightsLayer);
}
```

## <a name="add-a-line"></a>線を追加する


[**MapPolyline**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapPolyline) クラスを使って、線を地図に表示します。 次の例は、[UWP の地図サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl)から抜粋したもので、地図に破線を表示します。

```csharp
public void DrawLineOnMap()
{
    // Create Polyline.

    double centerLatitude = myMap.Center.Position.Latitude;
    double centerLongitude = myMap.Center.Position.Longitude;
    var mapPolyline = new MapPolyline
    {
        Path = new Geopath(new List<BasicGeoposition> {
                    new BasicGeoposition() {Latitude=centerLatitude-0.0005, Longitude=centerLongitude-0.001 },
                    new BasicGeoposition() {Latitude=centerLatitude+0.0005, Longitude=centerLongitude+0.001 },
                }),
        StrokeColor = Colors.Black,
        StrokeThickness = 3,
        StrokeDashed = true,
    };

   // Add Polyline to a layer on the map control.

   var MyLines = new List<MapElement>();

   MyLines.Add(mapPolyline);

   var LinesLayer = new MapElementsLayer
   {
       ZIndex = 1,
       MapElements = MyLines
   };

   myMap.Layers.Add(LinesLayer);

}
```

## <a name="add-xaml"></a>XAML の追加

XAML を使って、カスタム UI 要素を地図に表示します。 XAML を地図に配置するには、XAML の位置と正規化されたアンカー ポイントを指定します。

-   [**SetLocation**](/windows/desktop/tablet/icontextnode-setlocation) を呼び出して、XAML を地図に配置する位置を設定します。
-   [**SetNormalizedAnchorPoint**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.setnormalizedanchorpoint)を呼び出して、指定した場所に対応する XAML 上の相対的な位置を設定します。

次の例では、シアトル市の地図を表示して、XAML の [**Border**](/uwp/api/Windows.UI.Xaml.Controls.Border) コントロールを追加し、スペース ニードルの場所を示しています。 また、そのエリアを地図の中央に配置し、拡大しています。 マップ コントロールを使用する方法に関する一般的な情報については、「[2D、3D、Streetside ビューでの地図の表示](display-maps.md)」をご覧ください。

```csharp
private void displayXAMLButton_Click(object sender, RoutedEventArgs e)
{
   // Specify a known location.
   BasicGeoposition snPosition = new BasicGeoposition { Latitude = 47.620, Longitude = -122.349 };
   Geopoint snPoint = new Geopoint(snPosition);

   // Create a XAML border.
   Border border = new Border
   {
      Height = 100,
      Width = 100,
      BorderBrush = new SolidColorBrush(Windows.UI.Colors.Blue),
      BorderThickness = new Thickness(5),
   };

   // Center the map over the POI.
   MapControl1.Center = snPoint;
   MapControl1.ZoomLevel = 14;

   // Add XAML to the map.
   MapControl1.Children.Add(border);
   MapControl.SetLocation(border, snPoint);
   MapControl.SetNormalizedAnchorPoint(border, new Point(0.5, 0.5));
}
```

この例では、地図に青色の境界線が表示されます。

![地図上の関心がある場所に表示された xaml のスクリーンショット](images/displaypoixaml.png)

次の例では、データ バインディングを使って、ページの XAML マークアップで XAML UI 要素を直接追加する方法を示しています。 コンテンツを表示する他の XAML 要素と同様に、[**Children**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.children) は [**MapControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の既定のコンテンツ プロパティであり、XAML マークアップで明示的に指定する必要はありません。

次の例では、2 つの XAML コントロールを [**MapControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) の暗黙的な子として表示する方法を示しています。 これらのコントロールは、地図上のデータがバインドされた場所に表示されます。

```xml
<maps:MapControl>
    <TextBox Text="Seattle" maps:MapControl.Location="{x:Bind SeattleLocation}"/>
    <TextBox Text="Bellevue" maps:MapControl.Location="{x:Bind BellevueLocation}"/>
</maps:MapControl>
```

これらの場所を設定するには、分離コード ファイルでプロパティを使います。

```csharp
public Geopoint SeattleLocation { get; set; }
public Geopoint BellevueLocation { get; set; }
```

次の例は、[**MapItemsControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapItemsControl) に含まれる 2 つの XAML コントロールを表示する方法を示しています。これらのコントロールは、地図上のデータがバインドされた場所に表示されます。

```xml
<maps:MapControl>
  <maps:MapItemsControl>
    <TextBox Text="Seattle" maps:MapControl.Location="{x:Bind SeattleLocation}"/>
    <TextBox Text="Bellevue" maps:MapControl.Location="{x:Bind BellevueLocation}"/>
  </maps:MapItemsControl>
</maps:MapControl>
```

次の例では、[**MapItemsControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapItemsControl) にバインドされている XAML 要素のコレクションが表示されます。

```xml
<maps:MapControl x:Name="MapControl" MapTapped="MapTapped" MapDoubleTapped="MapTapped" MapHolding="MapTapped">
  <maps:MapItemsControl ItemsSource="{x:Bind LandmarkOverlays}">
      <maps:MapItemsControl.ItemTemplate>
          <DataTemplate>
              <StackPanel Background="Black" Tapped ="Overlay_Tapped">
                  <TextBlock maps:MapControl.Location="{Binding Location}" Text="{Binding Title}"
                    maps:MapControl.NormalizedAnchorPoint="0.5,0.5" FontSize="20" Margin="5"/>
              </StackPanel>
          </DataTemplate>
      </maps:MapItemsControl.ItemTemplate>
  </maps:MapItemsControl>
</maps:MapControl>
```

上の例の ``ItemsSource`` プロパティは、分離コード ファイルで [IList](/dotnet/api/system.collections.ilist) 型のプロパティにバインドされます。

```csharp
public sealed partial class Scenario1 : Page
{
    public IList LandmarkOverlays { get; set; }

    public MyClassConstructor()
    {
         SetLandMarkLocations();
         this.InitializeComponent();   
    }

    private void SetLandMarkLocations()
    {
        LandmarkOverlays = new List<MapElement>();

        var pikePlaceIcon = new MapIcon
        {
            Location = new Geopoint(new BasicGeoposition
            { Latitude = 47.610, Longitude = -122.342 }),
            Title = "Pike Place Market"
        };

        LandmarkOverlays.Add(pikePlaceIcon);

        var SeattleSpaceNeedleIcon = new MapIcon
        {
            Location = new Geopoint(new BasicGeoposition
            { Latitude = 47.6205, Longitude = -122.3493 }),
            Title = "Seattle Space Needle"
        };

        LandmarkOverlays.Add(SeattleSpaceNeedleIcon);
    }
}
```

<a id="layers" />

## <a name="working-with-layers"></a>レイヤーの使用

このガイドの例では、要素を [MapElementLayers](/uwp/api/windows.ui.xaml.controls.maps.mapelementslayer) コレクションに追加しています。 その後、そのコレクションをマップ コントロールの **Layers** プロパティに追加する方法が示されています。 以前のリリースでは、このガイドで、次のようにマップの要素を [**MapElements**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.MapElements) コレクションに追加する方法を示していました。

```csharp
var pikePlaceIcon = new MapIcon
{
    Location = new Geopoint(new BasicGeoposition
    { Latitude = 47.610, Longitude = -122.342 }),
    NormalizedAnchorPoint = new Point(0.5, 1.0),
    ZIndex = 0,
    Title = "Pike Place Market"
};

myMap.MapElements.Add(pikePlaceIcon);
```

引き続き同じアプローチを使うこともできますが、その場合は新しいマップ レイヤー モデルの利点が活かされません。 要素をレイヤーにグループ化すると、各レイヤーを互いに独立して操作できます。 たとえば、各レイヤーには独自のイベント セットがあるため、特定のレイヤーのイベントに応答し、そのイベントに固有の操作を実行することができます。

また、XAML を直接 [MapLayer](/uwp/api/windows.ui.xaml.controls.maps.maplayer) にバインドすることもできます。 これは [MapElements](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.MapElements) コレクションを使う場合にはできないことです。

これを実現するには、1 つの方法として、ビュー モデル クラス、XAML ページの分離コード、および XAML ページを使います。

### <a name="view-model-class"></a>ビュー モデル クラス

```csharp
public class LandmarksViewModel
{
    public ObservableCollection<MapLayer> LandmarkLayer
        { get; } = new ObservableCollection<MapLayer>();

    public LandmarksViewModel()
    {
        var MyElements = new List<MapElement>();

        var pikePlaceIcon = new MapIcon
        {
            Location = new Geopoint(new BasicGeoposition
            { Latitude = 47.610, Longitude = -122.342 }),
            Title = "Pike Place Market"
        };

        MyElements.Add(pikePlaceIcon);

        var LandmarksLayer = new MapElementsLayer
        {
            ZIndex = 1,
            MapElements = MyElements
        };

        LandmarkLayer.Add(LandmarksLayer);         
    }

```

### <a name="code-behind-a-xaml-page"></a>XAML ページの分離コード

ビュー モデル クラスを分離コード ページに結び付けます。

```csharp
public LandmarksViewModel ViewModel { get; set; }

public myMapPage()
{
    this.InitializeComponent();
    this.ViewModel = new LandmarksViewModel();
}
```

### <a name="xaml-page"></a>XAML ページ

XAML ページで、レイヤーを返すビュー モデル クラスのプロパティにバインドします。

```XML
<maps:MapControl
    x:Name="myMap" TransitFeaturesVisible="False" Loaded="MyMap_Loaded" Grid.Row="2"
    MapServiceToken="Your token" Layers="{x:Bind ViewModel.LandmarkLayer}"/>
```

## <a name="related-topics"></a>関連トピック

* [Bing Maps Developer Center](https://www.bingmapsportal.com/)
* [UWP の地図のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl)
* [地図の設計ガイドライン](./display-maps.md)
* [ビルド2015ビデオ: Windows アプリでの電話、タブレット、および PC でのマップと場所の活用](https://channel9.msdn.com/Events/Build/2015/2-757)
* [UWP の交通情報アプリのサンプル](https://github.com/Microsoft/Windows-appsample-trafficapp)
* [**MapIcon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapIcon)
* [**MapPolygon**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapPolygon)
* [**MapPolyline**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapPolyline)