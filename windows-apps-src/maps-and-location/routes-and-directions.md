---
title: 地図へのルートとルート案内の表示
description: MapRouteFinder クラスを使用してルートと方向を取得し、それをユニバーサル Windows プラットフォーム (UWP) アプリの MapControl に表示する方法について説明します。
ms.assetid: BBB4C23A-8F10-41D1-81EA-271BE01AED81
ms.date: 09/20/2017
ms.topic: article
keywords: Windows 10, UWP, ルート, マップ, 位置情報, ルート案内
ms.localizationpriority: medium
ms.openlocfilehash: b015393d81d736e5886793431966d0d91976e80d
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89171756"
---
# <a name="display-routes-and-directions-on-a-map"></a>地図へのルートとルート案内の表示



ルートとルート案内を要求し、アプリで表示します。

>[!Note]
>アプリでの地図の使用について詳しくは、[ユニバーサル Windows プラットフォーム (UWP) の地図サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl)をダウンロードしてください。
>地図表示がアプリの主要機能でない場合は、代わりに Windows マップ アプリを起動することを検討します。 `bingmaps:`、`ms-drive-to:`、`ms-walk-to:` の各 UI スキームを使って、Windows マップ アプリを起動し、特定の地図やターン バイ ターン方式のルート案内を表示することができます。 詳しくは、「[Windows マップ アプリの起動](../launch-resume/launch-maps-app.md)」をご覧ください。

 
## <a name="an-intro-to-maproutefinder-results"></a>MapRouteFinder 結果の概要


ルートとルート案内のクラスがどのように関連するかを次に示します。

* [**MapRouteFinder**](/uwp/api/Windows.Services.Maps.MapRouteFinder) クラスには、ルートとルート案内を取得するメソッドがあります。 これらのメソッドは、 [**Maproutefinderresult**](/uwp/api/Windows.Services.Maps.MapRouteFinderResult)を返します。

* [**MapRouteFinderResult**](/uwp/api/Windows.Services.Maps.MapRouteFinderResult) には [**MapRoute**](/uwp/api/Windows.Services.Maps.MapRoute) オブジェクトが含まれています。 **Maproutefinderresult**の[**Route**](/uwp/api/windows.services.maps.maproutefinderresult.route)プロパティを使用して、このオブジェクトにアクセスします。

* [**MapRoute**](/uwp/api/Windows.Services.Maps.MapRoute) には、[**MapRouteLeg**](/uwp/api/Windows.Services.Maps.MapRouteLeg) オブジェクトのコレクションが含まれています。 **MapRoute** の [**Legs**](/uwp/api/windows.services.maps.maproute.legs) プロパティを通じてこのコレクションにアクセスします。

* 各 [**MapRouteLeg**](/uwp/api/Windows.Services.Maps.MapRouteLeg) には、[**MapRouteManeuver**](/uwp/api/Windows.Services.Maps.MapRouteManeuver) オブジェクトのコレクションが含まれています。 このコレクションには、 **Mapたるテレ**[**の "実行" プロパティを使用**](/uwp/api/windows.services.maps.maprouteleg.maneuvers)してアクセスします。

自動車や徒歩でのルートとルート案内を取得するには、[**MapRouteFinder**](/uwp/api/Windows.Services.Maps.MapRouteFinder) クラスのメソッドを呼び出します。 たとえば、[**GetDrivingRouteAsync**](/uwp/api/windows.services.maps.maproutefinder.getdrivingrouteasync) や [**GetWalkingRouteAsync**](/uwp/api/windows.services.maps.maproutefinder.getwalkingrouteasync) を使用できます。

ルートを要求する場合は、次の指定を行うことができます。

* 始点と終点のみを指定するか、ルートを計算する一連の中間点を指定できます。

    *立寄地*を指定するとルート区間が追加され、各区間に独自の旅程が設定されます。 *立寄地*を指定するには、[**GetDrivingRouteFromWaypointsAsync**](/uwp/api/windows.services.maps.maproutefinder.getwalkingroutefromwaypointsasync) のオーバーロードのいずれかを使います。

    *経由地*は、*立寄地*どうしの間の中間点を定義します。 ルート区間は追加されません。  これらは、通過する必要のあるルート上の中間点を示すだけです。 *経由地*を指定するには、[**GetDrivingRouteFromEnhancedWaypointsAsync**](/uwp/api/windows.services.maps.maproutefinder.getdrivingroutefromenhancedwaypointsasync) のオーバーロードのいずれかを使います。

* 最適化を指定できます (例: 距離を最短にする)。

* 制限を指定できます (例: 高速道路を回避する)。

## <a name="display-directions"></a>ルート案内の表示

[**MapRouteFinderResult**](/uwp/api/Windows.Services.Maps.MapRouteFinderResult) オブジェクトには [**MapRoute**](/uwp/api/Windows.Services.Maps.MapRoute) オブジェクトが含まれており、[**Route**](/uwp/api/windows.services.maps.maproutefinderresult.route) プロパティを使ってアクセスできます。

計算された [**MapRoute**](/uwp/api/Windows.Services.Maps.MapRoute) には、ルートの移動にかかる時間、ルートの距離、およびルートの区間を含む [**MapRouteLeg**](/uwp/api/Windows.Services.Maps.MapRouteLeg) オブジェクトのコレクションを提供するプロパティがあります。 各 **MapRouteLeg** オブジェクトには、[**MapRouteManeuver**](/uwp/api/Windows.Services.Maps.MapRouteManeuver) オブジェクトのコレクションが含まれています。 **MapRouteManeuver** オブジェクトにはルート案内が含まれており、[**InstructionText**](/uwp/api/windows.services.maps.maproutemaneuver.instructiontext) プロパティを使ってアクセスできます。

>[!IMPORTANT]
>マップ サービスを使用する前に、マップ認証キーを指定する必要があります。 詳しくは、「[マップ認証キーの要求](authentication-key.md)」をご覧ください。

 

```csharp
using System;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.Services.Maps;
using Windows.Devices.Geolocation;
...
private async void button_Click(object sender, RoutedEventArgs e)
{
   // Start at Microsoft in Redmond, Washington.
   BasicGeoposition startLocation = new BasicGeoposition() {Latitude=47.643,Longitude=-122.131};

   // End at the city of Seattle, Washington.
   BasicGeoposition endLocation = new BasicGeoposition() {Latitude = 47.604,Longitude= -122.329};

   // Get the route between the points.
   MapRouteFinderResult routeResult =
         await MapRouteFinder.GetDrivingRouteAsync(
         new Geopoint(startLocation),
         new Geopoint(endLocation),
         MapRouteOptimization.Time,
         MapRouteRestrictions.None);

   if (routeResult.Status == MapRouteFinderStatus.Success)
   {
      System.Text.StringBuilder routeInfo = new System.Text.StringBuilder();

      // Display summary info about the route.
      routeInfo.Append("Total estimated time (minutes) = ");
      routeInfo.Append(routeResult.Route.EstimatedDuration.TotalMinutes.ToString());
      routeInfo.Append("\nTotal length (kilometers) = ");
      routeInfo.Append((routeResult.Route.LengthInMeters / 1000).ToString());

      // Display the directions.
      routeInfo.Append("\n\nDIRECTIONS\n");

      foreach (MapRouteLeg leg in routeResult.Route.Legs)
      {
         foreach (MapRouteManeuver maneuver in leg.Maneuvers)
         {
            routeInfo.AppendLine(maneuver.InstructionText);
         }
      }

      // Load the text box.
      tbOutputText.Text = routeInfo.ToString();
   }
   else
   {
      tbOutputText.Text =
            "A problem occurred: " + routeResult.Status.ToString();
   }
}
```

この例では、`tbOutputText` テキスト ボックスに次の結果が表示されます。

``` syntax
Total estimated time (minutes) = 18.4833333333333
Total length (kilometers) = 21.847

DIRECTIONS
Head north on 157th Ave NE.
Turn left onto 159th Ave NE.
Turn left onto NE 40th St.
Turn left onto WA-520 W.
Enter the freeway WA-520 from the right.
Keep left onto I-5 S/Portland.
Keep right and leave the freeway at exit 165A towards James St..
Turn right onto James St.
You have reached your destination.
```

## <a name="display-routes"></a>ルートの表示


[**MapControl**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) に [**MapRoute**](/uwp/api/Windows.Services.Maps.MapRoute) を表示するには、**MapRoute** を使って [**MapRouteView**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapRouteView) を構成します。 次に、 **Maprouteview**を**Mapcontrol**の[**route**](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.routes)コレクションに追加します。

>[!IMPORTANT]
>マップ サービスまたはマップ コントロールを使用する前に、マップ認証キーを指定する必要があります。 詳しくは、「[マップ認証キーの要求](authentication-key.md)」をご覧ください。

 

```csharp
using System;
using Windows.Devices.Geolocation;
using Windows.Services.Maps;
using Windows.UI;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Maps;
...
private async void ShowRouteOnMap()
{
   // Start at Microsoft in Redmond, Washington.
   BasicGeoposition startLocation = new BasicGeoposition() { Latitude = 47.643, Longitude = -122.131 };

   // End at the city of Seattle, Washington.
   BasicGeoposition endLocation = new BasicGeoposition() { Latitude = 47.604, Longitude = -122.329 };


   // Get the route between the points.
   MapRouteFinderResult routeResult =
         await MapRouteFinder.GetDrivingRouteAsync(
         new Geopoint(startLocation),
         new Geopoint(endLocation),
         MapRouteOptimization.Time,
         MapRouteRestrictions.None);

   if (routeResult.Status == MapRouteFinderStatus.Success)
   {
      // Use the route to initialize a MapRouteView.
      MapRouteView viewOfRoute = new MapRouteView(routeResult.Route);
      viewOfRoute.RouteColor = Colors.Yellow;
      viewOfRoute.OutlineColor = Colors.Black;

      // Add the new MapRouteView to the Routes collection
      // of the MapControl.
      MapWithRoute.Routes.Add(viewOfRoute);

      // Fit the MapControl to the route.
      await MapWithRoute.TrySetViewBoundsAsync(
            routeResult.Route.BoundingBox,
            null,
            Windows.UI.Xaml.Controls.Maps.MapAnimationKind.None);
   }
}
```

この例では、 **Mapwithroute**という名前の[**mapcontrol**](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl)に次のコードが表示されます。

![ルートが表示されたマップ コントロール。](images/routeonmap.png)

同じ例を使って、2 つの*立寄地*の間に 1 つの*経由地*を指定するバージョンを次に示します。

```csharp
using System;
using Windows.Devices.Geolocation;
using Windows.Services.Maps;
using Windows.UI;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Maps;
...
private async void ShowRouteOnMap()
{
  Geolocator locator = new Geolocator();
  locator.DesiredAccuracyInMeters = 1;
  locator.PositionChanged += Locator_PositionChanged;

  BasicGeoposition point1 = new BasicGeoposition() { Latitude = 47.649693, Longitude = -122.144908 };
  BasicGeoposition point2 = new BasicGeoposition() { Latitude = 47.6205, Longitude = -122.3493 };
  BasicGeoposition point3 = new BasicGeoposition() { Latitude = 48.649693, Longitude = -122.144908 };

  // Get Driving Route from point A  to point B thru point C
  var path = new List<EnhancedWaypoint>();

  path.Add(new EnhancedWaypoint(new Geopoint(point1), WaypointKind.Stop));
  path.Add(new EnhancedWaypoint(new Geopoint(point2), WaypointKind.Via));
  path.Add(new EnhancedWaypoint(new Geopoint(point3), WaypointKind.Stop));

  MapRouteFinderResult routeResult =  await MapRouteFinder.GetDrivingRouteFromEnhancedWaypointsAsync(path);

  if (routeResult.Status == MapRouteFinderStatus.Success)
  {
      MapRouteView viewOfRoute = new MapRouteView(routeResult.Route);
      viewOfRoute.RouteColor = Colors.Yellow;
      viewOfRoute.OutlineColor = Colors.Black;

      myMap.Routes.Add(viewOfRoute);

      await myMap.TrySetViewBoundsAsync(
            routeResult.Route.BoundingBox,
            null,
            Windows.UI.Xaml.Controls.Maps.MapAnimationKind.None);
  }
}
```

## <a name="related-topics"></a>関連トピック

* [Bing Maps Developer Center](https://www.bingmapsportal.com/)
* [UWP の地図のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MapControl)
* [地図の設計ガイドライン](./display-maps.md)
* [ビルド2015ビデオ: Windows アプリでの電話、タブレット、および PC でのマップと場所の活用](https://channel9.msdn.com/Events/Build/2015/2-757)
* [UWP の交通情報アプリのサンプル](https://github.com/Microsoft/Windows-appsample-trafficapp)