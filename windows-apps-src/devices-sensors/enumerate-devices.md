---
ms.assetid: 4311D293-94F0-4BBD-A22D-F007382B4DB8
title: デバイスの列挙
description: 列挙用の名前空間によって、システムに内部接続されているデバイス、外部接続されているデバイス、ワイヤレス プロトコルまたはネットワーク プロトコル経由で検出できるデバイスを検索できます。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 499af7929c67064623e15ee1d475e0f643fafd2b
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89165466"
---
# <a name="enumerate-devices"></a>デバイスの列挙


## <a name="samples"></a>サンプル

利用可能なデバイスすべてを列挙する最も簡単な方法は、(下のセクションで詳しく取り上げられているように) [**FindAllAsync**](/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) コマンドを使用してスナップショットを取ることです。

```CSharp
async void enumerateSnapshot(){
  DeviceInformationCollection collection = await DeviceInformation.FindAllAsync();
}
```

[**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration) API のより高度な使い方を示すサンプルをダウンロードするには、[ここ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/DeviceEnumerationAndPairing)をクリックしてください。

## <a name="enumeration-apis"></a>列挙 API

列挙用の名前空間によって、システムに内部接続されているデバイス、外部接続されているデバイス、ワイヤレス プロトコルまたはネットワーク プロトコル経由で検出できるデバイスを検索できます。 利用可能なデバイスを列挙するために使う API は、[**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration) 名前空間です。 このような API を使う理由は、次のようなものがあります。

-   使用中のアプリケーションに接続したデバイスを検索する。
-   システムに接続したデバイスまたはシステムによって検出されたデバイスの情報を取得する。
-   デバイスの追加、接続、切断、オンラインの状態、またはその他のプロパティを変更時に、アプリで通知を受信する。
-   デバイスの接続、切断、オンライン状態の変更、またはその他のプロパティの変更時に、アプリでバックグラウンド トリガを受信する。

個別のデバイスと、アプリを実行しているシステムが当該のテクノロジをサポートしている場合、これらの API で、次のプロトコルやバスのいずれかを経由してデバイスを列挙できます。 これは包括的なリストではありません。特定のデバイスでは、他のプロトコルがサポートされている可能性があります。

-   物理的に接続されたバス。 これには PCI や USB が含まれます。 たとえば、 **デバイスマネージャー**で確認できるものがあります。
-   [UPnP](/windows/desktop/UPnP/universal-plug-and-play-start-page)
-   デジタル リビング ネットワーク アライアンス (DLNA)
-   [**Discovery And Launch (DIAL)**](/uwp/api/Windows.Media.DialProtocol)
-   [**DNS サービス検出 (DNS-SD)**](/uwp/api/Windows.Networking.ServiceDiscovery.Dnssd)
-   [デバイス上の Web サービス (WSD)](/windows/desktop/WsdApi/wsd-portal)
-   [Bluetooth](/windows/desktop/Bluetooth/bluetooth-start-page)
-   [**Wi-fi ダイレクト**](/uwp/api/Windows.Devices.WiFiDirect)
-   WiGig
-   [**店舗販売時点管理**](/uwp/api/Windows.Devices.PointOfService)

多くの場合、列挙 API の使用について心配する必要はありません。 その理由は、デバイスを使う API の多くが、適切な既定のデバイスを自動的に選択するか、より合理的な列挙 API を提供するためです。 たとえば、[**MediaElement**](/uwp/api/Windows.UI.Xaml.Controls.MediaElement) は既定のオーディオ レンダリング デバイスを自動的に使います。 アプリが既定のデバイスを使うことができる限り、アプリケーションで列挙 API を使用する必要はありません。 列挙 API は、利用可能なデバイスを検出して接続するための一般的で柔軟な方法を提供します。 このトピックでは、デバイスの列挙についての情報を提供し、デバイスを列挙する 4 つの一般的な方法について説明します。

-   [**DevicePicker**](/uwp/api/Windows.Devices.Enumeration.DevicePicker) UI を使う
-   現在システムで検出可能なデバイスのスナップショットを列挙する
-   現在検出可能なデバイスを列挙して変更を監視する
-   バックグラウンド タスクで現在検出可能なデバイスを列挙して変更を監視する

## <a name="deviceinformation-objects"></a>DeviceInformation オブジェクト


列挙 API の操作では、[**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトを頻繁に使う必要があります。 これらのオブジェクトには、デバイスに関する利用可能な情報のほとんどが含まれています。 次の表は、ユーザーが関心を持つ **DeviceInformation** プロパティのいくつかを紹介しています。 詳細な一覧については、 **Deviceinformation**のリファレンスページを参照してください。

| プロパティ                         | 備考                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DeviceInformation.Id**         | これはデバイス固有の識別子であり、文字列変数として提供されます。 多くの場合、これは、あるメソッドから別のメソッドに渡すためだけの不透明な値であり、ユーザーが関心を持つ特定のデバイスを示します。 このプロパティと **DeviceInformation.Kind** プロパティは、アプリを終了し、再度アプリを開くときに使うこともできます。 これにより、確実に同じ [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトを回復して再び使うことができます。 |
| **DeviceInformation.Kind**       | [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトで表されるデバイス オブジェクトの種類を示します。 これは、デバイスのカテゴリでも種類でもありません。 1 つのデバイスを、種類の異なる複数の **DeviceInformation** オブジェクトで表すことができます。 このプロパティに指定できる値とそれらの相互関係については、[**DeviceInformationKind**](/uwp/api/windows.devices.enumeration.deviceinformationkind) をご覧ください。                           |
| **DeviceInformation.Properties** | このプロパティ バッグには、[**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトについて要求される情報が含まれています。 最も一般的なプロパティは、[**DeviceInformation.Name**](/uwp/api/windows.devices.enumeration.deviceinformation.name) のように、**DeviceInformation** オブジェクトのプロパティとして簡単に参照されます。 詳しくは、「[デバイス情報のプロパティ](device-information-properties.md)」をご覧ください。                                                                |

 

## <a name="devicepicker-ui"></a>DevicePicker UI


[**DevicePicker**](/uwp/api/Windows.Devices.Enumeration.DevicePicker) は、Windows から提供されるコントロールであり、ユーザーが一覧からデバイスを選択できるようにする小さな UI を作成します。 **DevicePicker** ウィンドウは、いくつかの方法でカスタマイズできます。

-   UI に表示されるデバイスは、[**SupportedDeviceSelectors**](/uwp/api/windows.devices.enumeration.devicepickerfilter.supporteddeviceselectors)、[**SupportedDeviceClasses**](/uwp/api/windows.devices.enumeration.devicepickerfilter.supporteddeviceclasses)、または両方を [**DevicePicker.Filter**](/uwp/api/windows.devices.enumeration.devicepicker.filter) に追加することで制御できます。 多くの場合、セレクターまたはクラスを 1 つ追加するだけですが、2 つ以上必要な場合は、複数を追加できます。 複数のセレクターまたはクラスを追加する場合は、OR ロジック関数を使ってそれらを結び付けます。
-   デバイスから取得するプロパティを指定できます。 これを行うには、プロパティを [**Devicepicker. RequestedProperties**](/uwp/api/windows.devices.enumeration.devicepicker.requestedproperties)に追加します。
-   [**Appearance**](/uwp/api/windows.devices.enumeration.devicepicker.appearance) を使って、[**DevicePicker**](/uwp/api/Windows.Devices.Enumeration.DevicePicker) の外観を変更できます。
-   [**DevicePicker**](/uwp/api/Windows.Devices.Enumeration.DevicePicker) を表示するときに、そのサイズと場所を指定できます。

[**DevicePicker**](/uwp/api/Windows.Devices.Enumeration.DevicePicker) を表示すると、デバイスの追加、削除、更新に合わせて、UI の内容が自動的に更新されます。

**メモ**   [**Devicepicker**](/uwp/api/Windows.Devices.Enumeration.DevicePicker)を使用して[**deviceinformationkind**](/uwp/api/windows.devices.enumeration.deviceinformationkind)を指定することはできません。 特定の **DeviceInformationKind** のデバイスが必要な場合は、[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) を作成して独自の UI を提供する必要があります。

 

キャスト メディア コンテンツと DIAL を使う場合は、それぞれに独自のピッカーが用意されています。 [**CastingDevicePicker**](/uwp/api/Windows.Media.Casting.CastingDevicePicker) と [**DialDevicePicker**](/uwp/api/Windows.Media.DialProtocol.DialDevicePicker) です。

## <a name="enumerate-a-snapshot-of-devices"></a>ネットワークのスナップショットの列挙


[**DevicePicker**](/uwp/api/Windows.Devices.Enumeration.DevicePicker) がニーズに合わず、より柔軟な方法が必要になることがあります。 たとえば、独自の UI を作成する場合や、ユーザーに UI を表示せずにデバイスを列挙する場合などが考えられます。 そのような場合は、デバイスのスナップショットを列挙することができます。 そのためには、システムに現在接続されているデバイスやシステムとペアリングされているデバイスを調べます。 ただし、この方法では、利用可能なデバイスのスナップショットが確認されるだけであるため、一覧を列挙した後に接続されたデバイスは検出できないことに注意する必要があります。 デバイスが更新または削除された場合に通知を受け取ることもできません。 注意すべき潜在的なもう 1 つのデメリットは、この方法では列挙がすべて完了するまで結果が表示されないことです。 このため、**AssociationEndpoint** オブジェクト、**AssociationEndpointContainer** オブジェクト、または **AssociationEndpointService** オブジェクトに関心がある場合は、この方法を使うべきではありません。これらのオブジェクトは、ネットワーク プロトコルまたはワイヤレス プロトコル経由で検出されるからです。 これを完了するには最長で 30 秒かかります。 このような場合は、[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) オブジェクトを使って利用可能なデバイスを列挙する必要があります。

デバイスのスナップショットを列挙するには、[**FindAllAsync**](/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) メソッドを使います。 このメソッドは、列挙プロセス全体が完了するまで待ってから、すべての結果を 1 つの [**DeviceInformationCollection**](/uwp/api/windows.devices.enumeration.deviceinformationcollection) オブジェクトとして返します。 このメソッドには、結果をフィルター処理し、目的のデバイスに合わせてその結果を絞り込むためのいくつかのオプションを提供するオーバーロードもあります。 オーバーロードを使うには、[**DeviceClass**](/uwp/api/Windows.Devices.Enumeration.DeviceClass) を指定するか、デバイス セレクターを渡します。 デバイス セレクターとは、列挙するデバイスを指定する AQS 文字列です。 詳細については、「 [デバイスセレクターを構築する](build-a-device-selector.md)」を参照してください。

デバイスの列挙スナップショットの例を以下に示します。



結果を絞り込むだけでなく、デバイスから取得するプロパティも指定できます。 その場合、指定したプロパティが、コレクションで返される各 [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトのプロパティ バックで利用可能になります。 すべてのデバイスの種類ですべてのプロパティを使うことができるわけではないことに注意してください。 デバイスの種類に使用できるプロパティについては、「 [デバイス情報のプロパティ](device-information-properties.md)」を参照してください。



## <a name="enumerate-and-watch-devices"></a>デバイスの列挙と監視


デバイスをより強力かつ柔軟な方法で列挙するには、[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) を作成します。 この方法では、デバイスを列挙するときの柔軟性が最も高くなります。 現在存在するデバイスを列挙できるだけでなく、デバイス セレクターに一致するデバイスの追加、削除、プロパティの変更が行われた場合に通知を受け取ることもできます。 **DeviceWatcher** を作成するときにデバイス セレクターを指定します。 デバイス セレクターについて詳しくは、「[デバイス セレクターのビルド](build-a-device-selector.md)」をご覧ください。 ウォッチャーを作成すると、指定した条件に一致するデバイスについて次の通知を受け取れるようになります。

-   新しいデバイスが追加された場合の追加通知。
-   目的のプロパティが変更された場合の更新通知。
-   デバイスが使えなくなった場合やフィルターに一致しなくなった場合の削除通知。

ほとんどの場合、[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) を使うときは、デバイスの一覧を維持して、ウォッチャーが監視対象のデバイスから更新を受け取るのに合わせてその一覧への追加、一覧からの項目の削除、または項目の更新を行います。 更新通知を受け取ると、更新された情報を [**DeviceInformationUpdate**](/uwp/api/windows.devices.enumeration.deviceinformationupdate) オブジェクトとして利用できるようになります。 デバイスの一覧を更新するには、まず、変更された [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) を見つけます。 次に、そのオブジェクトの [**Update**](/uwp/api/windows.devices.enumeration.deviceinformation.update) メソッドを呼び出して、**DeviceInformationUpdate** オブジェクトを渡します。 これは、**DeviceInformation** オブジェクトを自動的に更新できる便利な関数です。

[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) では、デバイスが追加されたり変更されたりすると通知が送られてくるため、対象のオブジェクトが **AssociationEndpoint**、**AssociationEndpointContainer**、または **AssociationEndpointService** である場合はこの方法でデバイスを列挙することをお勧めします。これらのオブジェクトは、ネットワーク プロトコルまたはワイヤレス プロトコル経由で列挙されるからです。

[**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) を作成するには、いずれかの [**CreateWatcher**](/uwp/api/windows.devices.enumeration.deviceinformation.createwatcher) メソッドを使います。 これらのメソッドは、目的のデバイスを指定できるようにオーバーロードされています。 オーバーロードを使うには、[**DeviceClass**](/uwp/api/Windows.Devices.Enumeration.DeviceClass) を指定するか、デバイス セレクターを渡します。 デバイス セレクターとは、列挙するデバイスを指定する AQS 文字列です。 詳細については、「 [デバイスセレクターを構築する](build-a-device-selector.md)」を参照してください。 デバイスから取得する目的のプロパティを指定することもできます。 その場合、指定したプロパティが、コレクションで返される各 [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトのプロパティ バックで利用可能になります。 すべてのデバイスの種類ですべてのプロパティを使うことができるわけではないことに注意してください。 どのデバイスの種類でどのプロパティを使うことができるかについては、「[デバイス情報プロパティ](device-information-properties.md)」をご覧ください。

## <a name="watch-devices-as-a-background-task"></a>バックグラウンド タスクによるデバイスの監視


バックグラウンド タスクによるデバイスの監視は、上で説明した [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) を作成する方法によく似ています。 実際、最初に前のセクションの説明に従って通常の **DeviceWatcher** オブジェクトを作成する必要があります。 オブジェクトを作成したら、[**DeviceWatcher.Start**](/uwp/api/windows.devices.enumeration.devicewatcher.start) の代わりに [**GetBackgroundTrigger**](/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) を使います。 **GetBackgroundTrigger** を呼び出すときに目的の通知 (追加、削除、更新) を指定する必要があります。 更新または削除を要求する際には追加も要求する必要があります。 トリガーを登録すると、すぐにバックグラウンドで **DeviceWatcher** の実行が開始されます。 それ以降、条件に一致する新しい通知を受け取るたびに、バックグラウンド タスクがアプリケーションをトリガーして、前回のトリガー以降の最新の変更が提供されます。

**重要**   [**DeviceWatcherTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceWatcherTrigger)が最初にアプリケーションをトリガーするのは、ウォッチャーが**EnumerationCompleted**状態に達したときです。 したがって、そのときには最初の結果がすべて含まれます。 その後にアプリケーションがトリガーされるときには、前回のトリガー以降に発生した追加、更新、削除の通知のみが含まれます。 最初の結果が一度に 1 つずつ送られるのではなく、**EnumerationCompleted** に達した後にまとめて送られるため、フォアグラウンドの [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) オブジェクトとは若干異なります。

 

ワイヤレス プロトコルの中には、バックグラウンドでスキャンするときにはフォアグラウンドでスキャンするときと動作が異なるものや、そもそもバックグラウンドでのスキャンをサポートしていないものもあります。 バックグラウンド スキャンについては 3 つの可能性があります。 次の表は、それらの可能性と、そのアプリケーションに対する影響を示しています。 たとえば、Bluetooth と Wi-fi Direct ではバックグラウンドスキャンがサポートされていないため、拡張機能によって [**DeviceWatcherTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceWatcherTrigger)はサポートされません。

| 動作                                  | 影響                                                                                                                                  |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| バックグラウンドでも同じ動作               | なし                                                                                                                                    |
| バックグラウンドで可能なのはパッシブ スキャンのみ | パッシブ スキャンが行われるまで待つことになるため、デバイスの検出に時間がかかる場合があります。                                                           |
| バックグラウンド スキャンはサポートされていない            | [**DeviceWatcherTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceWatcherTrigger) でデバイスが検出されず、更新も報告されません。 |

 

バックグラウンド タスクとしてのスキャンをサポートしていないプロトコルが [**DeviceWatcherTrigger**](/uwp/api/Windows.ApplicationModel.Background.DeviceWatcherTrigger) に含まれていてもトリガーは機能しますが、 そのプロトコルで更新や結果を取得することはできません。 その他のプロトコルやデバイスの更新は通常どおりに検出されます。

## <a name="using-deviceinformationkind"></a>DeviceInformationKind の使用


ほとんどの場合、[**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトの [**DeviceInformationKind**](/uwp/api/windows.devices.enumeration.deviceinformationkind) を気にする必要はありません。 お使いのデバイス API で返されるデバイス セレクターでは、多くの場合、その API で使うための正しい種類のデバイス オブジェクトが取得されることが保証されているからです。 しかし、デバイスの **DeviceInformation** を取得する際に、対応するデバイス API がなく、デバイス セレクターを取得できない場合もあります。 そのような場合は、独自のセレクターを作成する必要があります。 たとえば、Web Services on Devices には専用の API がありませんが、[**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration) API を使ってそれらのデバイスを検出し、情報を取得できます。その後、ソケット API でそれらを使うことができます。

独自のデバイス セレクターを作成してデバイス オブジェクトを列挙する場合は、[**DeviceInformationKind**](/uwp/api/windows.devices.enumeration.deviceinformationkind) の理解が重要になります。 使用可能なすべての種類と、それらの相互関係については、**DeviceInformationKind** のリファレンス ページをご覧ください。 **DeviceInformationKind** の最も一般的な使い方の 1 つでは、クエリをデバイス セレクターと組み合わせて送信するときに、検索するデバイスの種類を指定するために使います。 これにより、指定した **DeviceInformationKind** と一致するデバイスのみを確実に列挙します。 たとえば、**DeviceInterface** オブジェクトを検索してから、親 **Device** オブジェクトの情報を取得するクエリを実行します。 その親オブジェクトには詳細情報が含まれる場合があります。

[**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトのプロパティ バッグ内で利用可能なプロパティは、デバイスの [**DeviceInformationKind**](/uwp/api/windows.devices.enumeration.deviceinformationkind) に応じて異なる場合があることに注意することが重要です。 特定の種類でしか使うことのできないプロパティもあります。 プロパティと種類の関係について詳しくは、「[デバイス情報プロパティ](device-information-properties.md)」をご覧ください。 したがって、上の例では、親 **Device** を検索すると、**DeviceInterface** デバイス オブジェクトでは利用できなかった詳細情報にアクセスできるようになります。 このため、AQS フィルター文字列を作成するときには、要求するプロパティが列挙する **DeviceInformationKind** オブジェクトで利用可能かどうかを確認することが重要です。 フィルターの作成について詳しくは、「[デバイス セレクターのビルド](build-a-device-selector.md)」をご覧ください。

**AssociationEndpoint** オブジェクト、**AssociationEndpointContainer** オブジェクト、または **AssociationEndpointService** オブジェクトを列挙する場合、ワイヤレス プロトコルまたはネットワーク プロトコル経由で列挙することになります。 この状況では、[**FindAllAsync**](/uwp/api/windows.devices.enumeration.deviceinformation.findallasync) を使わずに、[**CreateWatcher**](/uwp/api/windows.devices.enumeration.deviceinformation.createwatcher) を使うことをお勧めします。 その理由は、ネットワーク経由で検索すると、[**EnumerationCompleted**](/uwp/api/windows.devices.enumeration.devicewatcher.enumerationcompleted) が生成されるまで、検索操作が 10 秒以上タイムアウトされないことが頻発するためです。 **FindAllAsync** は、**EnumerationCompleted** がトリガーされるまでその操作を完了しません。 [**DeviceWatcher**](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher) を使う場合は、**EnumerationCompleted** が呼び出されるタイミングに関係なく、リアルタイムに近い結果を取得できます。

## <a name="save-a-device-for-later-use"></a>後で使うためにデバイスを保存する


すべての [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトが、[**DeviceInformation.Id**](/uwp/api/windows.devices.enumeration.deviceinformation.id) と [**DeviceInformation.Kind**](/uwp/api/windows.devices.enumeration.deviceinformation.kind) の 2 つの情報を組み合わせて個別に識別されています。 この 2 つの情報を手元に残しておくと、**DeviceInformation** オブジェクトが失われたとしても、この情報を [**CreateFromIdAsync**](/uwp/api/windows.devices.enumeration.deviceinformation.createfromidasync) に渡して再び作成することができます。 この場合、アプリと統合するデバイスのユーザー設定を保存できます。


 

 