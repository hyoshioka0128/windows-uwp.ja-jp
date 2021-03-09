---
title: winget ツールを使用したアプリケーションのインストールと管理
description: winget コマンド ライン ツールを使用すると、開発者は Windows 10 コンピューター上でアプリケーションを検出、インストール、アップグレード、削除、および構成することができます。
ms.date: 10/22/2020
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: 39b48114242c8de1fad80bbf78860644b1c0dcd9
ms.sourcegitcommit: 9842e0e5c369a52594336d2278af877ccf40b049
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102196985"
---
# <a name="use-the-winget-tool-to-install-and-manage-applications"></a>winget ツールを使用したアプリケーションのインストールと管理

[!INCLUDE [preview-note](../../includes/package-manager-preview.md)]

**winget** コマンド ライン ツールを使用すると、開発者は Windows 10 コンピューター上でアプリケーションを検出、インストール、アップグレード、削除、および構成することができます。 このツールは、Windows パッケージ マネージャー サービスに対するクライアント インターフェイスです。

**winget** ツールは現在プレビュー版のため、現時点では、計画されているすべての機能を使用できるわけではありません。

## <a name="install-winget"></a>winget をインストールする

**winget** ツールをインストールするには、いくつかの方法があります。

* **winget** ツールは、[Windows アプリ インストーラー](https://www.microsoft.com/p/app-installer/9nblggh4nns1?ocid=9nblggh4nns1_ORSEARCH_Bing&rtc=1&activetab=pivot:overviewtab)のフライトまたはプレビュー バージョンに含まれています。 **winget** を使用するには、**アプリ インストーラー** のプレビュー バージョンをインストールする必要があります。 早期にアクセスするには、[Windows パッケージ マネージャーの Insider Program](https://aka.ms/AppInstaller_InsiderProgram) にリクエストを送信してください。 フライト リングに参加することで、最新のプレビューの更新情報を確実に確認できます。

* [Windows Insider のフライト リング](https://insider.windows.com)に参加してください。

* [winget リポジトリの Releases ページ](https://github.com/microsoft/winget-cli/releases)にある Windows Desktop App Installer パッケージをインストールします。

> [!NOTE]
> **winget** ツールには、Windows 10 バージョン 1709 (10.0.16299) 以降のバージョンの Windows 10 が必要です。

## <a name="administrator-considerations"></a>管理者に関する考慮事項

インストーラーの動作は、管理者特権で **winget** を実行しているかどうかによって異なる場合があります。

* 管理者特権を使用せずに **winget** を実行している場合、アプリケーションによっては、インストールするために [昇格が必要](https://docs.microsoft.com/windows/security/identity-protection/user-account-control/)になる可能性があります。 インストーラーが実行されると、Windows は、[昇格](https://docs.microsoft.com/windows/security/identity-protection/user-account-control)を求めるメッセージを表示します。 昇格しないことを選択すると、アプリケーションのインストールは失敗します。  

* 管理者コマンド プロンプトで **winget** を実行しているときは、アプリケーションで必要とする場合に [昇格のプロンプト](/windows/security/identity-protection/user-account-control/how-user-account-control-works)は表示されません。 管理者としてコマンド プロンプトを実行しているときは常に注意し、信頼できるアプリケーションのみをインストールしてください。

## <a name="use-winget"></a>winget を使用する

**アプリ インストーラー** をインストールした後、コマンド プロンプトから "winget" と入力して **winget** を実行できます。

最も一般的な使用シナリオの 1 つは、お気に入りのツールを検索してインストールすることです。

1. ツールを[検索](search.md)するには、`winget search <appname>` と入力します。
2. 目的のツールが使用可能であることを確認したら、`winget install <appname>` と入力してツールを[インストール](install.md)できます。 **winget** ツールがインストーラーを起動し、お使いの PC にアプリケーションをインストールします。
    ![winget コマンドライン](images\install.png)

3. install と search に加えて、**winget** には、アプリケーションの [詳細の表示](show.md)、[ソースの変更](source.md)、および [パッケージの検証](validate.md)を可能にする、他のいくつかのコマンドが用意されています。 コマンドの全一覧を表示するには、`winget --help` と入力します。
    ![winget help](images\help.png)

### <a name="commands"></a>コマンド

**winget** ツールの現在のプレビューでは、次のコマンドがサポートされています。

| コマンド | 説明 |
|---------|-------------|
| [hash](hash.md) | インストーラーの SHA256 ハッシュを生成します。 |
| [help](help.md) | **winget** ツール コマンドのヘルプを表示します。 |
| [install](install.md) | 指定されたアプリケーションをインストールします。 |
| [search](search.md) | アプリケーションを検索します。 |
| [show](show.md) | 指定されたアプリケーションの詳細を表示します。 |
| [source](source.md) | **winget** ツールによってアクセスされる Windows パッケージ マネージャーのリポジトリを追加、削除、および更新します。 |
| [validate](validate.md) | Windows パッケージ マネージャー リポジトリに送信するマニフェスト ファイルを検証します。 |

### <a name="options"></a>オプション

**winget** ツールの現在のプレビューでは、次のオプションがサポートされています。

| オプション | 説明 |
|--------------|-------------|
| **-v、--version** | winget の現在のバージョンを返します。 |
| **--info** |  ライセンスとプライバシーに関する声明へのリンクを含む、winget に関するすべての詳細情報を提供します。 |
| **-?、--help** |  winget の追加のヘルプを表示します。 |

## <a name="supported-installer-formats"></a>サポートされているインストーラー形式

**winget** ツールの現在のプレビューでは、次の種類のインストーラーがサポートされています。

* EXE
* MSIX
* MSI

## <a name="scripting-winget"></a>スクリプト作成 winget

複数のアプリケーションをインストールするために、バッチ スクリプトと PowerShell スクリプトを作成できます。

``` CMD
@echo off  
Echo Install Powertoys and Terminal  
REM Powertoys  
winget install Microsoft.Powertoys  
if %ERRORLEVEL% EQU 0 Echo Powertoys installed successfully.  
REM Terminal  
winget install Microsoft.WindowsTerminal  
if %ERRORLEVEL% EQU 0 Echo Terminal installed successfully.   %ERRORLEVEL%
```

> [!NOTE]
> スクリプト化されると、**winget** は、指定された順序でアプリケーションを起動します。 インストーラーが成功または失敗を返すと、**winget** は次のインストーラーを起動します。 インストーラーが別のプロセスを起動すると、途中で **winget** に返される可能性があります。 これにより、前のインストーラーが完了する前に、**winget** は次のインストーラーをインストールします。

## <a name="missing-tools"></a>欠落しているツール

[コミュニティ リポジトリ](../package/repository.md)にツールまたはアプリケーションが含まれていない場合は、[リポジトリ](https://github.com/microsoft/winget-pkgs)にパッケージを送信してください。 お気に入りのツールを追加することで、自分や他のすべてのユーザーが使用できるようになります。

## <a name="customize-winget-settings"></a>winget 設定のカスタマイズ

**winget** コマンド ラインのエクスペリエンスを構成するには、**settings.json** ファイルを変更します。 詳細については、[https://aka.ms/winget-settings](https://aka.ms/winget-settings) を参照してください。 設定はまだ試験的な状態であり、ツールのプレビュー バージョン向けにまだ最終化されていないことに注意してください。

## <a name="open-source-details"></a>オープン ソースの詳細

**winget** ツールは、GitHub のリポジトリ [https://github.com/microsoft/winget-cli/](https://github.com/microsoft/winget-cli/) から入手できるオープン ソース ソフトウェアです。 クライアントを構築するためのソースは、[src フォルダー](https://github.com/microsoft/winget-cli/tree/master/src)にあります。

**winget** のソースは、Visual Studio 2019 C++ ソリューションに含まれています。 ソリューションを正しく構築するには、最新の [Visual Studio と C++ ワークロード](https://visualstudio.microsoft.com/downloads/)をインストールしてください。

GitHub の **winget** ソースに投稿することをお勧めします。 まず、Microsoft CLA に同意して署名する必要があります。
