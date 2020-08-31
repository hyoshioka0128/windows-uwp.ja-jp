---
ms.assetid: 3aeddb83-5314-447b-b294-9fc28273cd39
description: Microsoft Advertising SDK をインストールして、Windows 10 用のユニバーサル Windows プラットフォーム (UWP) アプリに広告を表示する方法について説明します。
title: Microsoft Advertising SDK のインストール
ms.date: 02/18/2020
ms.topic: article
keywords: Windows 10, UWP, 広告, 宣伝, インストール, SDK, Advertising ライブラリ
ms.localizationpriority: medium
ms.openlocfilehash: d5c5c18c41996c5d46c261f351a900fea2532a93
ms.sourcegitcommit: 45dec3dc0f14934b8ecf1ee276070b553f48074d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094671"
---
# <a name="install-the-microsoft-advertising-sdk"></a>Microsoft Advertising SDK のインストール

>[!WARNING]
> 2020年6月1日から、Microsoft Ad 収益化 platform for Windows UWP アプリがシャットダウンされます。 [詳細情報](https://social.msdn.microsoft.com/Forums/windowsapps/en-US/db8d44cb-1381-47f7-94d3-c6ded3fea36f/microsoft-ad-monetization-platform-shutting-down-june-1st?forum=aiamgr)

Windows 10 用の UWP アプリで広告を表示するには、[Microsoft Advertising SDK](https://marketplace.visualstudio.com/items?itemName=AdMediator.MicrosoftAdvertisingSDK) をインストールします。 この SDK は、Visual Studio 2015 およびそれ以降のバージョンの拡張機能です。

> [!NOTE]
> JavaScript/HTML UWP アプリを開発していて、Windows 10 SDK バージョン 10.0.14393 (記念日更新) 以降がインストールされている場合は、 [WinJS](https://github.com/winjs/winjs) ライブラリもインストールする必要があります。 このライブラリは以前のバージョンの Windows 10 SDK に含まれていましたが、Windows 10 SDK バージョン 10.0.14393 (Anniversary Update) 以降ではこのライブラリを別個にインストールする必要があります。

<span id="install-msi" />

## <a name="install-via-msi"></a>MSI によるインストール

MSI インストーラーを使って Microsoft Advertising SDK をインストールするには

1.  Visual Studio のすべてのインスタンスを閉じます。

2. Microsoft Advertising SDK、Universal Ad Client SDK、Ad Mediator 拡張、または Microsoft Store Engagement and Monetization SDK の以前のバージョンを以前にインストールしていた場合は、これらの SDK のバージョンをアンインストールします。 必要に応じて、**コマンド プロンプト** ウィンドウを開き、次のコマンドを実行して、Visual Studio と共にインストールされている可能性があり、コンピューター上のインストールされているプログラムの一覧には表示されない可能性がある、古い広告 SDK のバージョンをすべて削除します。
    ```console
    MsiExec.exe /x{5C87A4DB-31C7-465E-9356-71B485B69EC8}
    MsiExec.exe /x{6AB13C21-C3EC-46E1-8009-6FD5EBEE515B}
    MsiExec.exe /x{6AC81125-8485-463D-9352-3F35A2508C11}
    ```

3.  [Microsoft Advertising SDK](https://marketplace.visualstudio.com/items?itemName=AdMediator.MicrosoftAdvertisingSDK) をダウンロードしてインストールします。 インストールには数分かかることがあります。 確実に処理が完了するまでお待ちください。

4.  Visual Studio を再起動します。

5.  以前のバージョンの Microsoft Advertising SDK、Universal Ad Client SDK、Microsoft Store Engagement and Monetization SDK の Advertising ライブラリを参照する既存のプロジェクトがある場合には、Visual Studio でプロジェクトを開き、プロジェクトをクリーンしてリビルドすることをお勧めします (**ソリューション エクスプ ローラー**でプロジェクト ノードを右クリックして、**[クリーン]** を選択し、次にもう一度プロジェクト ノードを右クリックして、**[リビルド]** を選択します)。

  または、プロジェクトで初めて Microsoft Advertising SDK を使う場合には、[Microsoft Advertising SDK への参照を追加](#reference)することができます。

<span id="install-nuget" />

## <a name="install-via-nuget"></a>NuGet によるインストール

NuGet を使って特定の UWP プロジェクトに Microsoft Advertising SDK をインストールするには:

1.  Visual Studio のすべてのインスタンスを閉じます。

2.  Microsoft Advertising SDK、Universal Ad Client SDK、Ad Mediator 拡張、または Microsoft Store Engagement and Monetization SDK の以前のバージョンを以前にインストールしていた場合は、これらの SDK のバージョンをアンインストールします。 必要に応じて、**コマンド プロンプト** ウィンドウを開き、次のコマンドを実行して、Visual Studio と共にインストールされている可能性があり、コンピューター上のインストールされているプログラムの一覧には表示されない可能性がある、古い広告 SDK のバージョンをすべて削除します。
    ```console
    MsiExec.exe /x{5C87A4DB-31C7-465E-9356-71B485B69EC8}
    MsiExec.exe /x{6AB13C21-C3EC-46E1-8009-6FD5EBEE515B}
    MsiExec.exe /x{6AC81125-8485-463D-9352-3F35A2508C11}
    ```

3.  Visual Studio を起動し、Microsoft Advertising SDK を使用するプロジェクトを開きます。
    > [!NOTE]
    > プロジェクトに SDK の以前の MSI インストールからのライブラリの参照が既に含まれている場合は、これらの参照をプロジェクトから削除します。 これらの参照は、参照先のライブラリが前の手順で削除されたため、その隣に警告アイコンが表示されます。

4. Visual Studio で、**[プロジェクト]** と **[NuGet パッケージの管理]** をクリックします。

5. 検索ボックスに、「**Microsoft.Advertising.XAML**」(XAML プロジェクト用) または「**Microsoft.Advertising.JS**」(JavaScript/HTML プロジェクト用) と入力し、対応するパッケージをインストールします。 パッケージのインストールが完了したら、ソリューションを保存します。
    > [!NOTE]
    > **[出力]** ウィンドウに、指定されたパスが長すぎることを示す*インストール パッケージ* エラーが表示されたとき、場合によっては、NuGet を構成して、既定の場所よりも短いパスで示される別の場所にパッケージを展開する必要があります。 これを行うには、`repositoryPath` 値をコンピューターの nuget.config ファイルに追加し、それを短いフォルダーのパスに割り当て、そこに NuGet パッケージが展開されるようにします。 詳しくは、NuGet ドキュメントの[この記事](https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior)をご覧ください。 または、Visual Studio プロジェクトを短いパスを持つ別のフォルダーに移動してみることができます。

6. ソリューションを閉じ、再度開きます。

7.  プロジェクトが NuGet によりインストールされた以前のバージョンの Microsoft Advertising SDK のライブラリを既に参照している場合で、プロジェクトを SDK の新しいリリースに更新する場合には、プロジェクトをクリーンしてリビルドすることをお勧めします (**ソリューション エクスプローラー**でプロジェクト ノードを右クリックして、**[クリーン]** を選択し、次にもう一度プロジェクト ノードを右クリックして、**[リビルド]** を選択します)。

  または、プロジェクトで初めて Microsoft Advertising SDK を使う場合には、[Microsoft Advertising SDK への参照を追加](#reference)することができます。

<span id="reference" />

## <a name="add-a-reference-to-the-microsoft-advertising-sdk"></a>Microsoft Advertising SDK への参照を追加する

Microsoft Advertising SDK をインストールした後、次の手順に従ってプロジェクト内の SDK を参照すると、アドバタイズ API を使用できます。

1. Visual Studio でプロジェクトを開きます。
    > [!NOTE]
    > プロジェクトのターゲットが **[Any CPU]** (任意の CPU) になっている場合は、アーキテクチャ固有のビルド出力 (たとえば、**[x86]**) を使うようにプロジェクトを更新します。 プロジェクトのターゲットが **[Any CPU]** (任意の CPU) になっていると、次の手順で Microsoft Advertising SDK への参照を正常に追加できません。 詳しくは、「[プロジェクトのターゲットを "Any CPU" に設定すると参照エラーが発生する](known-issues-for-the-advertising-libraries.md#reference_errors)」をご覧ください。

2. **ソリューション エクスプローラー**で、**[参照設定]** を右クリックし、**[参照の追加]** を選択します。

3. **[参照マネージャー]** で **[ユニバーサル Windows]** を展開して **[拡張機能]** をクリックし、**[Microsoft Advertising XAML for XAML]** (XAML アプリの場合) または **[Microsoft Advertising SDK for JavaScript]** (JavaScript と HTML を使って構築されたアプリの場合) の横にあるチェック ボックスをオンにします。

4.  **[参照マネージャー]** で、[OK] をクリックします。

アドバタイズ API を使い始める方法を示すチュートリアルでは、次の記事をご覧ください。

* [スポット広告](interstitial-ads.md)
* [ネイティブ広告](native-ads.md)
* [XAML および .NET の AdControl](adcontrol-in-xaml-and--net.md)
* [HTML 5 および Javascript での AdControl](adcontrol-in-html-5-and-javascript.md)

<span id="framework" />

## <a name="understanding-framework-packages-in-the-microsoft-advertising-sdk"></a>Microsoft Advertising SDK のフレームワーク パッケージについて

(UWP アプリ用) [Microsoft Advertising SDK](https://marketplace.visualstudio.com/items?itemName=AdMediator.MicrosoftAdvertisingSDK) の Microsoft.Advertising.dll ライブラリは、*フレームワーク パッケージ*として構成されています。 このライブラリには、[Microsoft.Advertising](https://docs.microsoft.com/uwp/api/microsoft.advertising) のアドバタイズ API と [Microsoft.Advertising.WinRT.UI](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui) 名前空間が含まれます。

このライブラリはフレームワーク パッケージであるため、このライブラリを使用するバージョンのアプリをユーザーがインストールすると、このライブラリは、修正されてパフォーマンスが向上した新しいバージョンのライブラリが公開されるたびに、ユーザーのデバイスで Windows Update によって自動的に更新されます。 これにより、利用できる最新バージョンのライブラリがユーザーのデバイスに確実にインストールされます。

このライブラリに新しい API や機能が導入された新しいバージョンの SDK がリリースされた場合は、これらの機能を使用するために最新バージョンの SDK をインストールする必要があります。 このシナリオでは、更新されたアプリをストアに公開する必要もあります。
