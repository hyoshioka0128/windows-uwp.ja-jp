---
Description: このセクションは、特定の重要な Windows 機能がさまざまなアプリ プラットフォームでどのようにサポートされているかについて、また、コードでこれらの機能の使用を開始する方法について理解するために役立ちます。
title: 機能とテクノロジ
ms.topic: article
ms.date: 05/08/2019
ms.localizationpriority: medium
ms.author: mcleans
author: mcleanbyron
ms.openlocfilehash: c214a31162b64853fd2115170ef1fd7766cafe96
ms.sourcegitcommit: e1104689fc1db5afb85701205c2580663522ee6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86997949"
---
# <a name="features-and-technologies-for-windows-apps"></a>Windows アプリの機能とテクノロジ

構築するアプリやターゲットとするデバイスの種類に関係なく、Windows では、重要なアプリ シナリオの主要な構成要素である多くの機能がサポートされています。 これらの機能の一部は、ユニバーサル Windows プラットフォーム (UWP)、Win32 (Windows API)、その他のアプリ プラットフォームにさまざまな方法で公開されています。 以下の記事は、特定の Windows 機能がさまざまなアプリ プラットフォームでどのようにサポートされているかについて、また、コードでこれらの機能の使用を開始する方法について理解するために役立ちます。

この記事では、UWP、Win32 (Windows API)、WPF、Windows フォームの各アプリ プラットフォームで Windows の重要な機能やテクノロジにアクセスする方法について詳しく説明した記事の一覧を提供します。 各プラットフォームの開発機能の詳細については、次のリソースを参照してください。

* [UWP のドキュメント](/windows/uwp/index)
* [Win32 (Windows API) のドキュメント](/windows/desktop/index)
* [WPF のドキュメント](https://docs.microsoft.com/dotnet/framework/wpf/index)
* [Windows フォームのドキュメント](https://docs.microsoft.com/dotnet/framework/winforms/index)

## <a name="key-windows-features-and-technologies"></a>重要な Windows の機能とテクノロジ

以下のセクションでは、最新の魅力的なエクスペリエンスを顧客に提供するために利用できる、いくつかの重要な Windows の機能とテクノロジについて説明します。

### <a name="windows-ink"></a>Windows Ink

![Surface ペン](images/hero-small.png)  

Windows Ink プラットフォームでペン デバイスを使うと、自然な形でデジタルの手書きノート、描画、コメントを作れます。 このプラットフォームは、デジタイザー入力のインク データとしてのキャプチャ、インク データの生成、インク データの管理、出力デバイスのインク ストロークとしてのインク データのレンダリング、手書き認識によるインクからテキストへの変換をサポートします。

Windows アプリで Windows Ink を使用するさまざまな方法の詳細については、「[Windows Ink](/windows/uwp/design/input/pen-and-stylus-interactions)」を参照してください。

### <a name="speech-interactions"></a>音声操作

![SGRS 文法ファイルに基づく制約の場合の、最初の認識画面](images/speech-listening-initial.png)

![SGRS 文法ファイルに基づく制約の場合の、最終的な認識画面](images/speech-listening-complete.png)

Windows には、音声認識や音声合成 (TTS: text-to-speech) をアプリのユーザー エクスペリエンスに直接統合するための多くの方法が用意されています。 音声機能は、ユーザーがアプリを楽しく確実に操作できる手段になります。音声機能によって、キーボード、マウス、タッチ、ジェスチャを補完することも、場合によってはこれらの代替として使うこともできます。

Windows アプリで音声操作を使用するさまざまな方法の詳細については、「[Windows 10 の音声、音声、および会話](speech.md)」を参照してください。

### <a name="windows-ai"></a>Windows AI

![Windows AI](images/windows-ai.png)

Microsoft では、Windows アプリケーションを強化するために使用できる、さまざまな AI ソリューションを提供しています。 Windows Machine Learning を使用すると、トレーニング済みの機械学習モデルをアプリに統合し、デバイス上でローカルに実行することができます。 Windows Vision Skills を使用すると、事前に構築されたライブラリを使用して、一般的な画像処理タスクを実行したり、独自のカスタム ソリューションを作成したりできます。 DirectML は、ハードウェアを最大限に活用するための、DirectX スタイルの低レベル API を提供します。

Windows アプリに AI を統合するさまざまな方法の詳細については、「[Windows AI](https://docs.microsoft.com/windows/ai/)」を参照してください。

## <a name="features-and-technologies-by-platform"></a>プラットフォーム別の機能とテクノロジ

以下のセクションのリンクは、Windows の中核的な機能やテクノロジを、Microsoft の主要なアプリ プラットフォームである UWP、Win32 (Windows API)、WPF、および Windows フォームから統合する方法について調べるために役立ちます。

### <a name="user-interface-and-accessibility"></a>ユーザー インターフェイスとアクセシビリティ

|  UWP  |  Win32 (Windows API) |  WPF  |  Windows フォーム  |
|-------|----------------------|-------|-----------------|
| [設計](/windows/uwp/design/basics/)<br/><br/>[レイアウト](/windows/uwp/design/layout/)<br/><br/>[コントロール](/windows/uwp/design/controls-and-patterns/)<br/><br/>[入力](/windows/uwp/design/input/)<br/><br/>[タイル](/windows/uwp/design/shell/tiles-and-notifications/creating-tiles)<br/><br/>[ビジュアル レイヤー](/windows/uwp/composition/visual-layer)<br/><br/>[XAML プラットフォーム](/windows/uwp/xaml-platform/)<br/><br/>[起動、再開、バックグラウンド タスク](/windows/uwp/launch-resume/)<br/><br/>[Windows のアクセシビリティ](/windows/uwp/design/accessibility/accessibility)<br/><br/>[音声操作](https://docs.microsoft.com/windows/uwp/design/input/speech-interactions)<br/><br/> |  [デスクトップ ユーザー インターフェイス](/windows/desktop/windows-application-ui-development)<br/><br/>[デスクトップ環境とシェル](/windows/desktop/user-interface)<br/><br/>[Windows コントロール](/windows/desktop/controls/window-controls)<br/><br/>[デスクトップ アプリケーションの UWP コントロール (XAML Islands)](/windows/apps/desktop/modernize/xaml-islands)<br/><br/>[デスクトップ アプリでの UWP ビジュアル レイヤー](/windows/apps/desktop/modernize/visual-layer-in-desktop-apps)<br/><br/>[Windows とメッセージ](/windows/desktop/winmsg/windowing)<br/><br/>[メニューとその他のリソース](/windows/desktop/menurc/resources)<br/><br/>[高 DPI](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)<br/><br/>[アクセシビリティ](/windows/desktop/accessibility)<br/><br/>[Microsoft Speech Platform - ソフトウェア開発キット (SDK) (バージョン 11)](https://www.microsoft.com/download/details.aspx?id=27226)<br/><br/>[Microsoft Speech SDK バージョン 5.1](https://www.microsoft.com/download/details.aspx?id=10121)<br/><br/>  |  [WPF のウィンドウ](https://docs.microsoft.com/dotnet/framework/wpf/app-development/windows-in-wpf-applications)<br/><br/>[ナビゲーションの概要](https://docs.microsoft.com/dotnet/framework/wpf/app-development/navigation-overview)<br/><br/>[WPF の XAML](https://docs.microsoft.com/dotnet/framework/wpf/advanced/xaml-in-wpf)<br/><br/>[コントロール](https://docs.microsoft.com/dotnet/framework/wpf/controls/)<br/><br/>[ビジュアル層のプログラミング](https://docs.microsoft.com/dotnet/framework/wpf/graphics-multimedia/visual-layer-programming)<br/><br/>[入力](https://docs.microsoft.com/dotnet/framework/wpf/advanced/input-wpf)<br/><br/>[アクセシビリティ](https://docs.microsoft.com/dotnet/framework/ui-automation/)<br/><br/>[.NET Framework 用 System.Speech プログラミング ガイド](https://docs.microsoft.com/previous-versions/office/developer/speech-technologies/hh361625(v=office.14))<br/><br/>  | [Windows フォームの作成](https://docs.microsoft.com/dotnet/framework/winforms/creating-a-new-windows-form)<br/><br/>[コントロール](https://docs.microsoft.com/dotnet/framework/winforms/controls/)<br/><br/>[ダイアログ ボックス](https://docs.microsoft.com/dotnet/framework/winforms/dialog-boxes-in-windows-forms)<br/><br/>[ユーザー入力](https://docs.microsoft.com/dotnet/framework/winforms/user-input-in-windows-forms)<br/><br/>[Windows フォームのアクセシビリティ](https://docs.microsoft.com/dotnet/framework/winforms/advanced/windows-forms-accessibility)<br/><br/>[.NET Framework 用 System.Speech プログラミング ガイド](https://docs.microsoft.com/previous-versions/office/developer/speech-technologies/hh361625(v=office.14))<br/><br/> |

### <a name="audio-video-and-graphics"></a>オーディオ、ビデオ、グラフィックス

|  UWP  |  Win32 (Windows API) |  WPF  |  Windows フォーム  |
|-------|----------------------|-------|-----------------|
| [オーディオ、ビデオ、およびカメラ](/windows/uwp/audio-video-camera/)<br/><br/>[メディア再生](/windows/uwp/audio-video-camera/media-playback/)<br/><br/>[ビジュアル レイヤー](/windows/uwp/composition/visual-layer)<br/><br/>[XAML プラットフォーム](/windows/uwp/xaml-platform/) |  [オーディオとビデオ](/windows/desktop/audio-and-video)<br/><br/>[グラフィックスとゲーミング](/windows/desktop/graphics-and-multimedia)<br/><br/>[DirectX](/windows/desktop/getting-started-with-directx-graphics)<br/><br/>[Direct2D](/windows/desktop/direct2d/direct2d-portal)<br/><br/>[Direct3D](/windows/desktop/direct3d)<br/><br/>[Windows GDI](/windows/desktop/gdi/windows-gdi)<br/><br/>[GDI+](/windows/desktop/gdiplus/-gdiplus-gdi-start)  |  [グラフィックス](https://docs.microsoft.com/dotnet/framework/wpf/graphics-multimedia/graphics)<br/><br/>[マルチメディア](https://docs.microsoft.com/dotnet/framework/wpf/graphics-multimedia/multimedia-overview)  |  [グラフィックスと描画](https://docs.microsoft.com/dotnet/framework/winforms/advanced/graphics-and-drawing-in-windows-forms)<br/><br/>[SoundPlayer クラス](https://docs.microsoft.com/dotnet/framework/winforms/controls/soundplayer-class-overview)  |

### <a name="data-access-and-app-resources"></a>データ アクセスとアプリ リソース

|  UWP  |  Win32 (Windows API) |  WPF  |  Windows フォーム  |
|-------|----------------------|-------|-----------------|
| [データ アクセス](/windows/uwp/data-access/)<br/><br/>[データ バインディング](/windows/uwp/data-binding/)<br/><br/>[ファイル、フォルダー、およびライブラリ](/windows/uwp/files/)<br/><br/>[アプリ リソース](/windows/uwp/app-resources/) |  [データ アクセスとストレージ](/windows/desktop/data-access-and-storage)<br/><br/>[ローカル ファイル システム](/windows/desktop/fileio/file-systems)<br/><br/>[リソースの概要](/windows/desktop/menurc/resources-overviews)</li>  |  [データとモデリング](https://docs.microsoft.com/dotnet/framework/data/)<br/><br/>[データ バインディング](https://docs.microsoft.com/dotnet/framework/wpf/data/data-binding-wpf)<br/><br/>[.NET アプリのリソース](https://docs.microsoft.com/dotnet/framework/resources/)<br/><br/>[アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル](https://docs.microsoft.com/dotnet/framework/wpf/app-development/wpf-application-resource-content-and-data-files)  |  [データとモデリング](https://docs.microsoft.com/dotnet/framework/data/)<br/><br/>[データ バインディング](https://docs.microsoft.com/dotnet/framework/winforms/windows-forms-data-binding)<br/><br/>[.NET アプリのリソース](https://docs.microsoft.com/dotnet/framework/resources/)<br/><br/>[アプリケーションの設定](https://docs.microsoft.com/dotnet/framework/winforms/advanced/application-settings-for-windows-forms)  |

### <a name="devices-documents-and-printing"></a>デバイス、ドキュメント、印刷

|  UWP  |  Win32 (Windows API) |  WPF  |  Windows フォーム  |
|-------|----------------------|-------|-----------------|
| [デバイス機能を有効にする](/windows/uwp/devices-sensors/enable-device-capabilities)<br/><br/>[デバイスの列挙](/windows/uwp/devices-sensors/enumerate-devices)<br/><br/>[センサー](/windows/uwp/devices-sensors/sensors)<br/><br/>[Bluetooth](/windows/uwp/devices-sensors/bluetooth)<br/><br/>[印刷とスキャン](/windows/uwp/devices-sensors/printing-and-scanning)<br/><br/>[NFC](/windows/uwp/devices-sensors/nfc) | [センサー API](/windows/desktop/sensorsapi/portal)<br/><br/>[印刷](/desktop/printdocs/printdocs-printing)<br/><br/>[UPnP API](/desktop/upnp/universal-plug-and-play-start-page) |  [印刷および印刷システムの管理](https://docs.microsoft.com/dotnet/framework/wpf/advanced/printing-and-print-system-management)  |  [印刷のサポート](https://docs.microsoft.com/dotnet/framework/winforms/advanced/windows-forms-print-support)  |

### <a name="system-network-and-power"></a>システム、ネットワーク、電源

|  UWP  |  Win32 (Windows API) |  WPF  |  Windows フォーム  |
|-------|----------------------|-------|-----------------|
| [デバイスの列挙](/windows/uwp/devices-sensors/enumerate-devices)<br/><br/>[バッテリー情報の取得](/windows/uwp/devices-sensors/get-battery-info)<br/><br/>[スレッド化と非同期プログラミング](/windows/uwp/threading-async/)<br/><br/>[ネットワークと Web サービス](/windows/uwp/networking/) | [システム サービス](/windows/desktop/system-services)<br/><br/>[メモリ管理](/windows/desktop/memory/memory-management)<br/><br/>[電源管理](/windows/desktop/power/power-management-portal)<br/><br/>[プロセスとスレッド](/windows/desktop/procthread/processes-and-threads)<br/><br/>[ネットワークとインターネット](/windows/desktop/networking)<br/><br/>[Windows システム情報](/windows/desktop/sysinfo/windows-system-information) |  [スレッド モデル](https://docs.microsoft.com/dotnet/framework/wpf/advanced/threading-model)<br/><br/>[.NET Framework のネットワーク プログラミング](https://docs.microsoft.com/dotnet/framework/network-programming/)  |  [システム情報](https://docs.microsoft.com/dotnet/framework/winforms/advanced/system-information-and-windows-forms)<br/><br/>[電源管理](https://docs.microsoft.com/dotnet/framework/winforms/advanced/power-management-in-windows-forms)<br/><br/>[.NET Framework のネットワーク プログラミング](https://docs.microsoft.com/dotnet/framework/network-programming/)<br/><br/>[Windows フォームのネットワーク](https://docs.microsoft.com/dotnet/framework/winforms/advanced/networking-in-windows-forms-applications)  |

### <a name="debugging-and-performance"></a>デバッグとパフォーマンス

|  UWP  |  Win32 (Windows API) |  WPF と Windows フォーム  |
|-------|----------------------|-------|-----------------|
| [デバッグ、テスト、パフォーマンス](/windows/uwp/debug-test-perf)<br/><br/>[UWP アプリの展開とデバッグ](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps)<br/><br/>[Windows アプリ認定キット](/windows/uwp/debug-test-perf/windows-app-certification-kit)<br/><br/>[パフォーマンス](/windows/uwp/debug-test-perf/performance-and-xaml-ui)| [デバッグとエラー処理](https://docs.microsoft.com/windows/win32/debugging-and-error-handling)<br/><br/>[Windows 用デバッグ ツール](https://docs.microsoft.com/windows-hardware/drivers/debugger/)<br/><br/>[Windows イベント トレーシング (ETW)](https://docs.microsoft.com/windows/win32/etw/event-tracing-portal)<br/><br/>[.NET TraceProcessing API](/windows/apps/trace-processing/)<br/><br/>[TraceLogging](https://docs.microsoft.com/windows/win32/tracelogging/trace-logging-portal)<br/><br/>[パフォーマンス カウンター](https://docs.microsoft.com/windows/win32/perfctrs/performance-counters-portal) |  [デバッグ、トレース、およびプロファイリング](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/)<br/><br/>[アプリケーションのトレースとインストルメント](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)<br/><br/>[マネージド デバッグ アシスタントによるエラーの診断](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants)<br/><br/>[ランタイム プロファイリング](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/runtime-profiling)<br/><br/>[パフォーマンス カウンター](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/performance-counters)<br/><br/>[Windows フォームの ClickOnce 配置](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)  |

### <a name="packaging-and-deployment"></a>パッケージ化と配置

|  UWP  |  Win32 (Windows API) |  WPF  |  Windows フォーム  |
|-------|----------------------|-------|-----------------|
| [アプリのパッケージ化](/windows/uwp/packaging/)<br/><br/>[MSIX](https://docs.microsoft.com/windows/msix/)<br/><br/>[アプリ パッケージ マニフェスト スキーマ](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/schema-root) | [Windows デスクトップ アプリのパッケージ化 (MSIX)](/windows/msix/desktop/desktop-to-uwp-root)<br/><br/>[アプリケーションのインストールとサービス](/windows/desktop/application-installing-and-servicing)<br/><br/>[Windows インストーラー](/windows/desktop/msi/windows-installer-portal) |  [Windows デスクトップ アプリのパッケージ化 (MSIX)](/windows/msix/desktop/desktop-to-uwp-root)<br/><br/>[.NET Framework およびアプリケーションの配置](https://docs.microsoft.com/dotnet/framework/deployment/)<br/><br/>[WPF アプリケーションの配置](https://docs.microsoft.com/dotnet/framework/wpf/app-development/deploying-a-wpf-application-wpf)  |  [Windows デスクトップ アプリのパッケージ化 (MSIX)](/windows/msix/desktop/desktop-to-uwp-root)<br/><br/>[.NET Framework およびアプリケーションの配置](https://docs.microsoft.com/dotnet/framework/deployment/)<br/><br/>[Windows フォームの ClickOnce 配置](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)  |
