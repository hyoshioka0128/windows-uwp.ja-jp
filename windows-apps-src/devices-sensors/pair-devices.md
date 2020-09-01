---
ms.assetid: F8A741B4-7A6A-4160-8C5D-6B92E267E6EA
title: デバイスのペアリング
description: 一部のデバイスは、使う前にペアリングする必要があります。 Windows.Devices.Enumeration 名前空間では、デバイスをペアリングするための 3 つの異なる方法がサポートされています。
ms.date: 04/19/2019
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d3fff5a8868cfe29c944336a33c8b6554b74ebf4
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89175446"
---
# <a name="pair-devices"></a>デバイスのペアリング



**重要な API**

- [**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration)

一部のデバイスは、使う前にペアリングする必要があります。 [**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration) 名前空間では、デバイスをペアリングするための 3 つの異なる方法がサポートされています。

-   自動ペアリング
-   基本ペアリング
-   カスタム ペアリング

**ヒント**   一部のデバイスは、使用するためにペアリングする必要がありません。 これについては、自動ペアリングに関するセクションで説明します。

 

## <a name="automatic-pairing"></a>自動ペアリング


アプリケーションでデバイスを使いたいが、デバイスがペアリングされているかどうかは重要でない場合があります。 単に、デバイスに関連付けられている機能を使用できるようにする場合です。 たとえば、アプリで Web カメラからイメージをキャプチャするだけの場合、必ずしもデバイス自体ではなく、イメージのキャプチャだけが重要となります。 対象のデバイスで使用できるデバイス API がある場合は、自動ペアリングが該当します。

この場合は、単にデバイスに関連付けられている API を使い、必要に応じて呼び出しを行い、必要になる可能性のあるペアリングをシステムが処理することを信頼します。 機能を使うためにペアリングする必要がないデバイスもあります。 デバイスをペアリングする必要がない場合、デバイス API はバックグラウンドでペアリング アクションを処理するため、アプリにその機能を統合する必要はありません。 アプリには、特定のデバイスがペアリングされているかや、ペアリングする必要があるかどうかに関する情報がありませんが、それでもデバイスにアクセスし、その機能を使うことができます。

## <a name="basic-pairing"></a>基本ペアリング


基本ペアリングは、アプリケーションがデバイスのペアリングを試行するために [**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration) API を使うときに行われます。 このシナリオでは、Windows にペアリングの試行とその処理を許可します。 ユーザーの操作が必要な場合は、Windows によって処理されます。 また、デバイスのペアリングが必要な場合や、自動ペアリングを試行する、関連するデバイス API がない場合も、基本ペアリングを使用します。 単に、デバイスを使用できるようにする場合でも、最初にペアリングする必要があります。

基本ペアリングを試行するためには、対象のデバイス用の [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトを最初に入手する必要があります。 オブジェクトを入手したら、[**DeviceInformation.Pairing**](/uwp/api/windows.devices.enumeration.deviceinformation.pairing) プロパティを操作します。これは、[**DeviceInformationPairing**](/uwp/api/windows.devices.enumeration.deviceinformation.pairing) オブジェクトです。 ペアリングを試みるには、[**DeviceInformationPairing.PairAsync**](/uwp/api/windows.devices.enumeration.deviceinformationpairing.pairasync) を呼び出します。 ペアリング アクションの完了を試みる時間をアプリに与えるために、結果を **await** する必要があります。 ペアリング アクションの結果が返され、エラーが返されない限り、デバイスはペアリングされます。

基本ペアリングを使っている場合は、デバイスのペアリング状態に関する追加情報にもアクセスできます。 たとえば、ペアリング状態 ([**IsPaired**](/uwp/api/Windows.Devices.Enumeration.DeviceInformationPairing.IsPaired)) と、デバイスがペアリングできるかどうか ([**CanPair**](/uwp/api/Windows.Devices.Enumeration.DeviceInformationPairing.CanPair)) がわかります。 これらはどちらも [**DeviceInformationPairing**](/uwp/api/windows.devices.enumeration.deviceinformation.pairing) オブジェクトのプロパティです。 自動ペアリングを使っている場合、該当する [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトを入手しない限り、この情報にアクセスできない可能性があります。

## <a name="custom-pairing"></a>カスタム ペアリング


カスタム ペアリングでは、アプリでペアリング プロセスを処理できます。 これにより、アプリはペアリング プロセス用にサポートされている [**DevicePairingKinds**](/uwp/api/Windows.Devices.Enumeration.DevicePairingKinds) を指定できます。 必要に応じて、ユーザーと対話する独自のユーザー インターフェイスも作成します。 ペアリング プロセスの進行に対するアプリの影響を少し高めたり、独自のペアリング ユーザー インターフェイスを表示するときに、カスタム ペアリングを使います。

カスタム ペアリングを実装するためには、基本ペアリングと同じように、対象のデバイス用の [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトを入手する必要があります。 ただし、重要な特定のプロパティは [**DeviceInformation.Pairing.Custom**](/uwp/api/windows.devices.enumeration.deviceinformationpairing.custom) になります。 これにより、[**DeviceInformationCustomPairing**](/uwp/api/windows.devices.enumeration.deviceinformationcustompairing) オブジェクトを取得できます。 すべての [**DeviceInformationCustomPairing.PairAsync**](/uwp/api/windows.devices.enumeration.deviceinformationcustompairing.pairasync) メソッドでは、[**DevicePairingKinds**](/uwp/api/Windows.Devices.Enumeration.DevicePairingKinds) パラメーターを含める必要があります。 これは、デバイスのペアリングを試みるためにユーザーが必要とするアクションを示します。 ユーザーが実行する必要があるアクションとその種類について詳しくは、**DevicePairingKinds** のリファレンス ページをご覧ください。 基本ペアリングと同様に、ペアリング アクションの完了を試みる時間をアプリに与えるために、結果を **await** する必要があります。 ペアリング アクションの結果が返され、エラーが返されない限り、デバイスはペアリングされます。

カスタム ペアリングをサポートするため、[**PairingRequested**](/uwp/api/windows.devices.enumeration.deviceinformationcustompairing.pairingrequested) イベントのハンドラーを作成する必要があります。 このハンドラーでは、カスタム ペアリング シナリオで使われる可能性のあるすべての異なる [**DevicePairingKinds**](/uwp/api/Windows.Devices.Enumeration.DevicePairingKinds) を必ず考慮する必要があります。 実行する適切なアクションは、イベント引数の一部として提供される **DevicePairingKinds** によって異なります。

カスタム ペアリングは常にシステム レベルの操作であることを認識することが重要です。 このため、デスクトップまたは Windows Phone を操作している場合、ペアリングが発生するときに、システム ダイアログが常にユーザーに表示されます。 これは、これらの両方のプラットフォームが、ユーザーの同意を必要とするユーザー エクスペリエンスを発生させるためです。 このダイアログは自動的に生成されるため、これらのプラットフォームを使用中に **ConfirmOnly** の [**DevicePairingKinds**](/uwp/api/Windows.Devices.Enumeration.DevicePairingKinds) を選ぶ場合に、独自のダイアログを作る必要はありません。 他の **DevicePairingKinds** については、特定の **DevicePairingKinds** 値に応じて、いくつかの特別な処理を実行する必要があります。 さまざまな **DevicePairingKinds** の値のカスタム ペアリングを処理する方法の例については、サンプルをご覧ください。

Windows 10 バージョン1903以降では、新しい**DevicePairingKinds**がサポートされて**います。** この値は、アプリがペアリングされたデバイスで認証を行うために、ユーザーのユーザー名とパスワードを要求する必要があることを意味します。 この場合に対処するには、 **PairingRequested**イベントハンドラーのイベント引数の[**Acceptwithpasswordcredential**](/uwp/api/windows.devices.enumeration.devicepairingrequestedeventargs.acceptwithpasswordcredential?branch=release-19h1#Windows_Devices_Enumeration_DevicePairingRequestedEventArgs_AcceptWithPasswordCredential_Windows_Security_Credentials_PasswordCredential_)メソッドを呼び出して、ペアリングを受け入れます。 ユーザー名とパスワードをパラメーターとしてカプセル化する [**Passwordcredential**](/uwp/api/windows.security.credentials.passwordcredential) オブジェクトを渡します。 リモートデバイスのユーザー名とパスワードは、ローカルでサインインしているユーザーの資格情報とは異なる場合があることに注意してください。

## <a name="unpairing"></a>ペアリング解除


デバイスのペアリング解除が該当するのは、上記で説明した基本ペアリングまたはカスタム ペアリングのシナリオのみです。 自動ペアリングを使っている場合、アプリはデバイスのペアリング状態を記憶しないため、ペアリング解除する必要はありません。 それでもデバイスをペアリング解除する場合のプロセスは、実装するのが基本ペアリングまたはカスタム ペアリングかにかかわらず同じです。 これは、追加情報を提供したり、ペアリング解除プロセスにかかわったりする必要がないためです。

デバイスをペアリング解除する最初の手順は、ペアリング解除するデバイスの [**DeviceInformation**](/uwp/api/Windows.Devices.Enumeration.DeviceInformation) オブジェクトを入手することです。 次に、[**DeviceInformation.Pairing**](/uwp/api/windows.devices.enumeration.deviceinformation.pairing) プロパティを取得し、[**DeviceInformationPairing.UnpairAsync**](/uwp/api/windows.devices.enumeration.deviceinformationpairing.unpairasync) を呼び出す必要があります。 ペアリングと同様に、結果を **await** します。 ペアリング解除アクションの結果が返され、エラーが返されない限り、デバイスはペアリング解除されます。

## <a name="sample"></a>サンプル


[**Windows. デバイスの列挙**](/uwp/api/Windows.Devices.Enumeration)api の使用方法を示すサンプルをダウンロードするには、[ここ](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/DeviceEnumerationAndPairing)をクリックしてください。

 

 