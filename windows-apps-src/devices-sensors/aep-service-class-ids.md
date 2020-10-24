---
ms.assetid: 23001DA5-C099-4C02-ACE9-3597F06ECBF4
title: AEP サービス クラス ID
description: アソシエーション エンドポイント (AEP) サービスは、デバイスが特定のプロトコル経由でサポートするサービスのプログラミング コントラクトを提供します。 これらのサービスのいくつかでは、サービスの参照時に使う必要がある識別子が設定されています。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 025db9ae6ed3b7ab2c532ddc140fd5279db58777
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89168616"
---
# <a name="aep-service-class-ids"></a>AEP サービス クラス ID

アソシエーション エンドポイント (AEP) サービスは、デバイスが特定のプロトコル経由でサポートするサービスのプログラミング コントラクトを提供します。 これらのサービスのいくつかでは、サービスの参照時に使う必要がある識別子が設定されています。 これらのコントラクトは、**System.Devices.AepService.ServiceClassId** プロパティで識別されます。 このトピックでは、既知の AEP サービス クラス ID のいくつかを一覧表示します。 AEP サービス クラス ID は、カスタム クラス ID によってプロトコルに適用することもできます。

アプリの開発者は、使用予定の AEP サービスに対するクエリを制限するために、クラス ID に基づいて高度なクエリ構文 (AQS) フィルターを使う必要があります。 これによって、関連サービスへのクエリ結果が制限され、デバイスのパフォーマンス、バッテリ寿命、およびサービス品質が大幅に向上します。 たとえば、アプリケーションでこれらのサービス クラス ID を使って、デバイスを Miracast の同期または DLNA デジタル メディア レンダラー (DMR) として使うことができます。 デバイスとサービスが互いにどのようにやり取りするかについて詳しくは、「[**DeviceInformationKind**](/uwp/api/Windows.Devices.Enumeration.DeviceInformationKind)」をご覧ください。

> **重要な API**
>
> - [**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration)

## <a name="bluetooth-and-bluetooth-le-services"></a>Bluetooth および Bluetooth LE サービス

Bluetooth サービスは、Bluetooth プロトコルまたは Bluetooth LE プロトコルの 2 つのプロトコルのいずれかに分類されます。 これらのプロトコルの識別子は次のとおりです。

- Bluetooth プロトコル ID: {e0cbf06c-cd8b-4647-bb8a-263b43f0f974}
- Bluetooth LE プロトコル ID: {bb7bb05e-5972-42b5-94fc-76eaa7084d49}

Bluetooth プロトコルは複数のサービスをサポートしており、すべてのサービスで同じ基本的なフォーマットを採用しています。 GUID の最初の 4 桁はサービスによって異なりますが、すべての Bluetooth Guid は **0000-0000-1000-8000-00805F9B34FB** で終わります。 たとえば、RFCOMM サービスでは前に 0x0003 が付くため、完全な ID は **00030000-0000-1000-8000-00805F9B34FB** になります。 次の表に、一般的な Bluetooth サービスをいくつか示します。

| [サービス名]                         | GUID                                     |
|--------------------------------------|------------------------------------------|
| RFCOMM                               | **00030000-0000-1000-8000-00805F9B34FB** |
| GATT - アラート通知サービス    | **18110000-0000-1000-8000-00805F9B34FB** |
| GATT - オートメーション IO                 | **18150000-0000-1000-8000-00805F9B34FB** |
| GATT - バッテリ サービス               | **180F0000-0000-1000-8000-00805F9B34FB** |
| GATT - 血圧                | **18100000-0000-1000-8000-00805F9B34FB** |
| GATT - 身体構成              | **181B0000-0000-1000-8000-00805F9B34FB** |
| GATT - 接着状態管理               | **181E0000-0000-1000-8000-00805F9B34FB** |
| GATT - 連続的な血糖値測定 | **181F0000-0000-1000-8000-00805F9B34FB** |
| GATT - 現在のタイム サービス          | **18050000-0000-1000-8000-00805F9B34FB** |
| GATT - サイクリング パワー                 | **18180000-0000-1000-8000-00805F9B34FB** |
| GATT - サイクリングの速度とリズム     | **18160000-0000-1000-8000-00805F9B34FB** |
| GATT - デバイス情報            | **180A0000-0000-1000-8000-00805F9B34FB** |
| GATT - 環境検知         | **181A0000-0000-1000-8000-00805F9B34FB** |
| GATT - 一般アクセス                | **18000000-0000-1000-8000-00805F9B34FB** |
| GATT - 一般属性             | **18010000-0000-1000-8000-00805F9B34FB** |
| GATT - 血糖値                       | **18080000-0000-1000-8000-00805F9B34FB** |
| GATT - 体温計            | **18090000-0000-1000-8000-00805F9B34FB** |
| GATT - 心拍数                    | **180D0000-0000-1000-8000-00805F9B34FB** |
| GATT - ヒューマン インターフェイス デバイス        | **18120000-0000-1000-8000-00805F9B34FB** |
| GATT - 即時アラート               | **18020000-0000-1000-8000-00805F9B34FB** |
| GATT - 屋内位置            | **18210000-0000-1000-8000-00805F9B34FB** |
| GATT - インターネット プロトコル サポート     | **18200000-0000-1000-8000-00805F9B34FB** |
| GATT - リンク消失                     | **18030000-0000-1000-8000-00805F9B34FB** |
| GATT - 場所とナビゲーション       | **18190000-0000-1000-8000-00805F9B34FB** |
| GATT - 次回夏時間変更サービス       | **18070000-0000-1000-8000-00805F9B34FB** |
| GATT - 電話アラート ステータス サービス    | **180E0000-0000-1000-8000-00805F9B34FB** |
| GATT - パルス オキシメーター                | **18220000-0000-1000-8000-00805F9B34FB** |
| GATT - 参照時間更新サービス | **18060000-0000-1000-8000-00805F9B34FB** |
| GATT - ランニングの速度とリズム     | **18140000-0000-1000-8000-00805F9B34FB** |
| GATT - スキャン パラメーター               | **18130000-0000-1000-8000-00805F9B34FB** |
| GATT - 送信電力                      | **18040000-0000-1000-8000-00805F9B34FB** |
| GATT - ユーザー データ                     | **181C0000-0000-1000-8000-00805F9B34FB** |
| GATT - 体重計                  | **181D0000-0000-1000-8000-00805F9B34FB** |

利用可能な Bluetooth サービスの完全な一覧については、 [GATT services の仕様](https://www.bluetooth.com/specifications/gatt/services/)を参照してください。 また、[**GattServiceUuids**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattServiceUuids) API を使って一般的な GATT サービスをいくつか取得することもできます。

## <a name="custom-bluetooth-le-services"></a>Bluetooth LE のカスタム サービス

Bluetooth LE のカスタム サービスは、次のプロトコル識別子を使います。{bb7bb05e-5972-42b5-94fc76eaa7084d49}

カスタム プロファイルは、独自に定義された GUID を使って定義します。 このカスタム GUID は、**System.Devices.AepService.ServiceClassId** に対して使う必要があります。

## <a name="upnp-services"></a>UPnP サービス

UPnP サービスは、次のプロトコル識別子を使います。{0e261de4-12f0-46e6-91ba-428607ccef64}

一般的に、すべての UPnP サービスでは、RFC 4122 で定義されたアルゴリズムを使い、サービスの名前が GUID にハッシュされています。 次の表では、Windows で定義されている一般的な UPnP サービスのいくつかを紹介します。

| [サービス名]                       | GUID                                      |
|------------------------------------|-------------------------------------------|
| [ODBC 入力元エディター]                 | **ba36014c-b51f-51cc-bf71-1ad779ced3c6**  |
| AV トランスポート                       | **deeacb78-707a-52df-b1c6-6f945e7e25bf**  |
| レンダリング制御                  | **cc7fe721-a3c7-5a14-8c49-4419dc895513**  |
| レイヤー 3 転送                 | **97d477fa-f403-577b-a714-b29a9007797f**  |
| WAN 共通インターフェイス構成 | **e4c1c624-c3c4-5104-b72e-ac425d9d157c**  |
| WAP IP 接続                  | **e4ac1c23-b5ac-5c27-8814-6bd837d8832c**  |
| WFA WLAN の構成             | **23d5f7db-747f-5099-8f21-3ddfd0c3c688**  |
| プリンターの拡張                   | **fb9074da-3d9f-5384-922e-9978ae51ef0c**  |
| プリンターの基本                      | **5d2a7252-d45c-5158-87a4-05212da327e1**  |
| メディア受信機レジスタ           | **0b4a2add-d725-5198-b2ba-852b8bf8d183**  |
| コンテンツ ディレクトリ                  | **89e701dd-0597-5279-a31c-235991d0db1c**  |
| DIAL                               | **085dfa4a-3948-53c7-a0d7-16d8ec26b29b**  |

## <a name="wsd-services"></a>WSD サービス

WSD サービスは、次のプロトコル識別子を使います。{782232aa-a2f9-4993-971b-aedc551346b0}

一般的に、すべての WSD サービスでは、RFC 4122 で定義されたアルゴリズムを使い、サービスの名前が GUID にハッシュされています。 次の表では、Windows で定義されている一般的な WSD サービスのいくつかを紹介します。

| [サービス名] | GUID                                     |
|--------------|------------------------------------------|
| [プリンター]      | **65dca7bd-2611-583e-9a12-ad90f47749cf** |
| スキャナー      | **56ec8b9e-0237-5cae-aa3f-d322dd2e6c1e** |

## <a name="aqs-sample"></a>AQS サンプル

この AQS は、DIAL をサポートするすべての UPnP **AssociationEndpointService** オブジェクトに対してフィルターを実行します。 この場合、[**DeviceInformationKind**](/uwp/api/Windows.Devices.Enumeration.DeviceInformationKind) は **AsssociationEndpointService** に設定されています。

``` syntax
System.Devices.AepService.ProtocolId:="{0e261de4-12f0-46e6-91ba-428607ccef64}" AND
System.Devices.AepService.ServiceClassId:="{085DFA4A-3948-53C7-A0D7-16D8EC26B29B}"
```