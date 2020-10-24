---
title: UWP バージョンの選択
description: Microsoft Visual Studio で UWP アプリを作成するときは、ターゲットのバージョンを選択できます。 ここでは、UWP バージョンによる違いと、新しいプロジェクトや既存のプロジェクトで選択したバージョンを構成する方法について説明します。
ms.date: 5/12/2019
ms.topic: article
keywords: windows 10, uwp, バージョン, 作成, バージョン, windows, 選択, 更新, 更新プログラム
ms.assetid: a8b7830f-4929-44c6-90be-91f38be5f364
ms.localizationpriority: medium
f1_keywords:
- UniversalProjects.TargetPlatformWizardPicker
dev_langs:
- csharp
- cppwinrt
- cpp
- vb
ms.openlocfilehash: 1987ad1267b3a48c0488e2d0af985f316097d3e2
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173806"
---
# <a name="choose-a-uwp-version"></a>UWP バージョンの選択

Windows 10 の各バージョンでは、新機能や強化された機能が UWP プラットフォームに提供されます。 Microsoft Visual Studio で UWP アプリを作成するときは、ターゲットのバージョンを選択できます。 [.NET Standard 2.0](/dotnet/standard/net-standard) を使うプロジェクトには、ビルド 16299 以降の**最小バージョン**が必要です。

> [!WARNING]
> Visual Studio の現行バージョンで作成された UWP プロジェクトは、Visual Studio 2015 では開くことができません。

次の表に、Windows 10 で利用できるバージョンを示します。 この表は、Windows 10 でのみサポートされる UWP アプリを作成する場合にだけ適用されることに注意してください。 以前のバージョンの Windows 向けに UWP アプリを開発することはできません。また、目的のバージョンをターゲットにするには、[SDK の適切なビルドをインストール](https://developer.microsoft.com/windows/downloads#_blank)する必要があります。

| バージョン | 説明 |
| --- | --- |
| ビルド 19041 (バージョン 2004) | これは、2020 年 5 月にリリースされた Windows 10 の最新バージョンです。 このリリースの主な新機能は次のとおりです。 </br> \* **WSL2:** Linux 用 Windows サブシステムが新しいアーキテクチャ モデルで更新され、実際の Linux カーネルが Windows 上で実行されるようになりました。 詳細については、「[WSL 2 について](/windows/wsl/wsl2-about)」を参照してください。 </br> \*  **MSIX:** Windows の新機能により、最新の MSIX アプリ パッケージ形式がさらにサポートされるようになりました。これには、含まれているサービスを使用したパッケージ作成やホステッド アプリの作成機能、パッケージ ID を必要とする機能をパッケージ化されていないアプリに含める機能などが含まれます。 詳細については、[MSIX ドキュメント](/windows/msix/overview)に関するページを参照してください。 </br> このリリースの Windows で追加されたこれらの機能や他の多くの機能の詳細については、[デベロッパー センター](https://developer.microsoft.com/windows/windows-10-for-developers)または [Windows 10 の開発者向け新着情報](../whats-new/windows-10-build-19041.md)に関する詳細ページをご覧ください。
| ビルド 18362 (バージョン 1903) | このバージョンの Windows 10 は、2019 年 4 月にリリースされました。 このリリースの主な新機能は次のとおりです。 </br> \* **XAML Islands:** Windows 10 では、非 UWP デスクトップ アプリケーションで UWP コントロールを使用できるようになりました。 WPF、Windows フォーム、または C++ Win32 向けの開発を行う場合、[既存のアプリに Windows 10 UI の最新機能を追加する方法について確認してください](/windows/apps/desktop/modernize/xaml-islands)。 </br> \* **Linux 用 Windows サブシステム:** Windows 内から Linux ファイルに直接アクセスできるようになりました。また、新しいコマンド ライン オプションをいくつか使用できるようになりました。 「[WSL について](/windows/wsl/about.md)」で最新情報を参照してください。 </br> このリリースの Windows で追加されたこれらの機能や他の多くの機能については、[ビルド 18362 の新着情報](../whats-new/windows-10-build-18362.md)に関するページを参照してください。
| ビルド 17763 (バージョン 1809) | このバージョンの Windows 10 は、2018 年 10 月にリリースされました。 **このバージョンの Windows をターゲットにするには、Visual Studio 2017 または Visual Studio 2019 を使用する "_必要がある_" ことに注意してください。** このリリースの主な新機能は次のとおりです。 </br> \* **Windows Machine Learning:** Windows Machine Learning が正式に発表され、最先端の機械学習モデルのサポートと高速な評価などの機能が提供されます。 このプラットフォームについて詳しくは、「[Windows Machine Learning](/windows/ai/)」をご覧ください。 </br> \* **Fluent Design:** メニュー バー、コマンド バーのポップアップ、XAML プロパティのアニメーションなど、新しい機能が Windows 10 に追加されました。 最新情報については、「[Fluent Design の概要](/windows/apps/fluent-design-system)」をご覧ください。 </br> このリリースの Windows で追加されたこれらの機能や他の多くの機能については、[ビルド 17763 の新着情報](../whats-new/windows-10-build-17763.md)に関するページを参照してください。
| ビルド 17134 (バージョン 1803) | このバージョンの Windows 10 は、2018 年 4 月にリリースされました。 **このバージョンの Windows をターゲットにするには、Visual Studio 2017 または Visual Studio 2019 を使用する "_必要がある_" ことに注意してください。** このリリースの主な新機能は次のとおりです。 </br> \* **Fluent Design:** ツリー ビュー、引っ張って更新、ナビゲーション ビューなど、新しい機能が Windows 10 に追加されました。 最新情報については、「[Fluent Design の概要](/windows/apps/fluent-design-system)」をご覧ください。 </br> \* **コンソール UWP アプリ:** C++ /WinRT または /CX の UWP コンソール アプリを作成して、DOS や PowerShell などのコンソール ウィンドウで実行できるようになりました。 </br> このリリースの Windows で追加されたこれらの機能や他の多くの機能については、[ビルド 17134 の新着情報](../whats-new/windows-10-build-17134.md)に関するページを参照してください。
| ビルド 16299 (Fall Creators Update バージョン 1709) | このバージョンの Windows 10 は、2017 年 10 月にリリースされました。 **このバージョンの Windows をターゲットにするには、Visual Studio 2017 または Visual Studio 2019 を使用する "_必要がある_" ことに注意してください。** このリリースの主な新機能は次のとおりです。 </br> \* **.NET Standard 2.0:** .NET API の数が大幅に増えており、お気に入りの NuGet パッケージとサード パーティ製ライブラリが .NET Standard に組み込まれています。 詳しくは、[こちら](/dotnet/standard/net-standard)のドキュメントをご覧ください。 これらの新しい API にアクセスするには、**最小バージョン**をビルド 16299 に設定する必要がある点に注意してください。 </br> \* **Fluent Design:** 照明、深度、視点、および動きを使ってアプリを強化し、重要な UI 要素にユーザーが専念できるようにしています。 </br> \* **条件付き XAML:** プロパティを簡単に設定し、実行時に API があるかどうかに基づいてオブジェクトをインスタンス化できるため、デバイスやバージョン間でアプリをシームレスに実行できるようになります。 </br> このリリースの Windows で追加されたこれらの機能や他の多くの機能については、[Windows 10 の開発者向け新着情報](../whats-new/windows-10-build-16299.md)に関するページを参照してください。
| ビルド 15063 (Creators Update バージョン 1703) | このバージョンの Windows 10 は、2017 年 3 月にリリースされました。 **このバージョンの Windows をターゲットにするには、Visual Studio 2017 または Visual Studio 2019 を使用する "_必要がある_" ことに注意してください**。 このリリースの主な新機能は次のとおりです。  </br> \* **インクの解析:** Windows Ink で、インク ストロークを筆記のストロークか描画のストロークかに分類し、テキスト、図形、基本的なレイアウト構造を認識できるようになりました。 </br> \* **Windows.Ui.Composition API:** アプリ全体でアニメーションを簡単に組み合わせ、適用することができます。 </br> \* **ライブ編集:** アプリの実行中に XAML を編集し、適用される変更内容をリアルタイムで確認できます。 </br> このリリースの Windows で追加されたこれらの機能や他の多くの機能については、[ビルド 15063 の新着情報](../whats-new/windows-10-build-15063.md)に関するページを参照してください。  |
| ビルド 14393 (Anniversary Update バージョン 1607) | このバージョンの Windows 10 は、2016 年 7 月にリリースされました。 このリリースの主な新機能は次のとおりです。 </br> \* **Windows Ink:** InkCanvas と InkToolbar の各コントロールが新しく追加されました。 </br> \* **Cortana API:** 新しい Cortana アクションを使って、Cortana のサポートをアプリの特定の機能と統合できます。 </br> \* **Windows Hello:** Microsoft Edge が Windows Hello をサポートするようになり、Web 開発者が生体認証にアクセスできるようになりました。 </br> このリリースの Windows で追加されたこれらの機能や他の多くの機能については、[ビルド 14393 の新着情報](../whats-new/windows-10-build-14393.md)に関するページを参照してください。  |
| ビルド 10586 (November Update バージョン 1511) | このバージョンの Windows 10 は、2015 年 11 月にリリースされました。 このリリースでは主な新機能として、Microsoft Edge のビデオ通信用 ORTC (オブジェクト リアルタイム通信) APIと、アプリで Windows Hello 顔認証を使うためのプロバイダー API が導入されました。 [このビルドで導入された機能について詳しくは、こちらをご覧ください。](../whats-new/windows-10-build-10586.md) |
| ビルド 10240 (Windows 10 バージョン 1507) | 2015 年 7 月にリリースされた Windows 10 の初期リリース バージョンです。 [このビルドで導入された機能について詳しくは、こちらをご覧ください。](../whats-new/windows-10-build-10240.md) |

一般ユーザー向けのコードを新しく開発する場合、常に最新ビルドの Windows (19041) を使うことを強くお勧めします。 エンタープライズ アプリを開発する場合は、**最小バージョン**で古いバージョンをサポートすることを検討してください。

## <a name="whats-different-in-each-uwp-version"></a>UWP バージョンの比較

連続する各バージョンの Windows 10 に対して、UWP の新しい API や変更された API が用意されています。 各バージョンで追加された具体的な機能については、「[Windows 10 の開発者向け新着情報](../whats-new/windows-10-build-19041.md)」をご覧ください。

すべてのデバイス ファミリとそのバージョン、およびすべての API コントラクトとそのバージョンを列挙したリファレンス トピックについては、「[デバイス ファミリ](/uwp/extension-sdks/)」と「[APIコントラクト](/uwp/extension-sdks/)」をご覧ください。

## <a name="net-api-availability-in-uwp-versions"></a>UWP バージョンでの .NET API の可用性

UWP は、.NET API の限定されたサブセットをサポートしており、それらは、プロジェクトの**ターゲット バージョン**や**最小バージョン**に関係なく使用できます。 [こちらのページで、使用可能な種類について詳しく説明しています](/dotnet/api/index?view=dotnet-uwp-10.0)。

再利用可能なクロスプラットフォーム ライブラリを作成する場合、UWP で .NET Standard がサポートされています。 [.NET Standard のドキュメント](/dotnet/standard/net-standard)で、どの UWP バージョンでどの .NET Standard がサポートされるかについて説明しています。

デスクトップ アプリを開発する場合は、.NET Framework の可用性の詳細について、代わりに [.NET Framework のバージョンと依存関係](/dotnet/framework/migration-guide/versions-and-dependencies)に関するページをご覧ください。

## <a name="choose-which-version-to-use-for-your-app"></a>アプリで使用するバージョンの選択

Visual Studio の **[新しいユニバーサル Windows プロジェクト]** ダイアログで、 **[ターゲット バージョン]** と **[最小バージョン]** を選択できます。 また、アプリの **[プロパティ]** にある*アプリケーション* セクションで、UWP アプリの **[ターゲット バージョン]** と **[最小バージョン]** を変更することもできます。

* **[ターゲット バージョン]** 。 アプリの実行環境として想定している Windows 10 のバージョン。 この設定により、プロジェクト ファイルの *TargetPlatformVersion* が設定されます。 またアプリ パッケージ マニフェスト内の *TargetDeviceFamily@MaxVersionTested* 属性の値が設定されます。 選択した値に基づいて、プロジェクトがターゲットとする UWP プラットフォームのバージョンが指定され、アプリで使用可能な API のセットが決まります。したがって、可能な限り新しいバージョンを選択することをお勧めします。 アプリ パッケージ マニフェストの詳細と、TargetDeviceFamily を手動で構成する場合のガイドラインについては、「[TargetDeviceFamily](/uwp/schemas/appxpackage/uapmanifestschema/element-targetdevicefamily)」をご覧ください。
* **[最小バージョン]** 。 アプリの基本機能をサポートするために必要な Windows 10 の最も古いバージョン。 この設定により、プロジェクト ファイルの *TargetPlatformMinVersion* が設定されます。 またアプリ パッケージ マニフェスト内の *TargetDeviceFamily@MinVersion* 属性の値が設定されます。 選択した値に基づいて、プロジェクトが動作できる UWP プラットフォームの最小バージョンが指定されます。

これらの設定は、アプリが **[最小バージョン]** から **[ターゲット バージョン]** までのすべてのバージョンで動作することの宣言となります。 これら 2 つが同じバージョンである場合は、特に問題はありません。 これらが異なる場合は、次の点に注意が必要です。

* コードでは、 **[最小バージョン]** で指定されたバージョンに含まれているすべての API を自由に (つまり、条件チェックなしに) 呼び出すことができます。
* 必ず **[最小バージョン]** を実行するデバイスでコードをテストして、 **[ターゲット バージョン]** のみに存在する API を必要とすることなく動作することを確認してください。
* プロジェクトのコンパイルに使用するすべての参照 (コントラクト winmds) は、 **[ターゲット バージョン]** の値によって特定されます。 しかしそれらの参照により、( **[最小バージョン]** で) サポートを宣言したデバイスに存在しない API への呼び出しを含むコードもコンパイルできます。 したがって、 **[最小バージョン]** の後に導入されたすべての API は、アダプティブ コード経由で呼び出す必要があります。 アダプティブ コードについて詳しくは、「[バージョン アダプティブ コード](../debug-test-perf/version-adaptive-code.md)」をご覧ください。