---
title: アプリ パッケージのアーキテクチャ
description: UWP アプリ パッケージを構築するときにどのプロセッサ アーキテクチャを使用するべきかについて説明します。
ms.date: 07/13/2017
ms.topic: article
keywords: Windows 10, UWP, パッケージ化, アーキテクチャ, パッケージの構成
ms.localizationpriority: medium
ms.openlocfilehash: 12de19b78c3aab27a7fbc29dd5e8183de1a0c0be
ms.sourcegitcommit: 51d884c3646ba3595c016e95bbfedb7ecd668a88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821017"
---
# <a name="app-package-architectures"></a>アプリ パッケージのアーキテクチャ

アプリ パッケージは、特定のプロセッサ アーキテクチャで実行するように構成されます。 アーキテクチャを選択することで、アプリを実行するデバイスを指定することになります。 ユニバーサル Windows プラットフォーム (UWP) アプリは、次のアーキテクチャで実行するように構成できます。
- x86
- x64
- ARM
- ARM64

すべてのアーキテクチャを対象にしてアプリ パッケージを構築することを**強く**お勧めします。 1 つのデバイス アーキテクチャを選択から外すと、アプリを実行できるデバイスの種類を制限することになり、アプリを使用できるユーザー数も抑制することになります。

## <a name="windows-10-devices-and-architectures"></a>Windows 10 デバイスとアーキテクチャ

> [!div class="mx-tableFixed"]
| UWP のアーキテクチャ | デスクトップ (x86)      | デスクトップ (x64)      | デスクトップ (ARM)      | モバイル             | Windows Mixed Reality と HoloLens           | Xbox               | IoT Core (デバイス依存) | Surface Hub        |
|------------------|--------------------|--------------------|--------------------|--------------------|--------------------|--------------------|-----------------------------|--------------------|
| x86              | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :x:                | :heavy_check_mark: | :x:                | :heavy_check_mark:          | :heavy_check_mark: |
| x64              | :x:                | :heavy_check_mark: | :x:                | :x:                | :x:                | :heavy_check_mark: | :heavy_check_mark:          | :heavy_check_mark: |
| ARM および ARM64              | :x:                | :x:                | :heavy_check_mark: | :heavy_check_mark: | :x:                | :x:                | :heavy_check_mark:          | :x:                |


これらのアーキテクチャについて詳しく説明しましょう。

### <a name="x86"></a>x86
x86 はほぼすべてのデバイスで実行されるため、一般的に、アプリ パッケージでは x86 を選ぶのが最も安全な構成になります。 Xbox や一部の IoT Core デバイスなど、デバイスの中には x86 構成のアプリ パッケージを実行できないものもあります。 ただし、PC の場合は x86 パッケージが最も安全な選択肢であり、最も広い範囲のデバイスに展開できます。 Windows 10 デバイスの大部分は、引き続き x86 バージョンの Windows を実行しています。

### <a name="x64"></a>x64
この構成は x86 構成に比べると使用される頻度は低くなります。 この構成は、64 ビットバージョンの Windows 10 を採用しているデスクトップ、[Xbox の UWP アプリ](https://docs.microsoft.com/windows/uwp/xbox-apps/system-resource-allocation)、および Intel Joule の Windows 10 IoT Core 向けのものであることに注意してください。

### <a name="arm-and-arm64"></a>ARM および ARM64
ARM 版 Windows 10 構成には、デスクトップ PC、モバイル デバイス、および一部の IoT Core デバイス (Rasperry Pi 2、Raspberry Pi 3、および DragonBoard) が含まれます。 ARM 版 Windows 10 デスクトップ PC が Windows ファミリに新たに加わりました。そのため、UWP アプリ開発者がこれらの PC で最適なエクスペリエンスを実現するには ARM パッケージをストアに提出する必要があります。

>[!NOTE]
> ネイティブ ARM64 プラットフォームを対象とする UWP アプリケーションのビルドするには、Visual Studio 2017 バージョン 15.9 またはそれ以降、または Visual Studio 2019 が必要です。 詳細については、次を参照してください。[このブログの投稿](https://blogs.windows.com/buildingapps/2018/11/15/official-support-for-windows-10-on-arm-development)します。


詳細については、次を参照してください。 [ARM 上の Windows 10](../porting/apps-on-arm.md)します。 [ARM 版 Windows 10](https://channel9.msdn.com/Events/Build/2017/P4171) のデモを確認し、そのしくみを詳しく知るには、この //Build トークをご覧ください。

IoT の特定のトピックについての詳細については、次を参照してください。 [Visual Studio を使用してアプリを展開する](https://developer.microsoft.com/windows/iot/Docs/AppDeployment)します。
