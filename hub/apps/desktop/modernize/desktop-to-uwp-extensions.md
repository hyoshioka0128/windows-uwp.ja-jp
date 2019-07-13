---
Description: 拡張機能を使用すると、あらかじめ定義された方法で Windows 10 にパッケージ デスクトップ アプリを統合できます。
title: Windows 10 と UWP (デスクトップ ブリッジ) のパッケージ化されたデスクトップ アプリケーションを統合します。
ms.date: 04/18/2018
ms.topic: article
keywords: windows 10, uwp
ms.assetid: 0a8cedac-172a-4efd-8b6b-67fd3667df34
ms.author: mcleans
author: mcleanbyron
ms.localizationpriority: medium
ms.openlocfilehash: 38a5a6fae3e6477321a8879a50dff21e10fd92e2
ms.sourcegitcommit: 48ca9c99b52f93a805d5afeb7045ba4bf6597371
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2019
ms.locfileid: "67622945"
---
# <a name="integrate-your-packaged-desktop-app-with-windows-10-and-uwp"></a>Windows 10 と UWP パッケージ化されたデスクトップ アプリに統合します。

場合する[MSIX コンテナーでデスクトップ アプリケーションをパッケージ化](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)、定義済みの拡張機能を使用して Windows 10 では、パッケージ化されたデスクトップ アプリケーションを統合する拡張機能を使用することができます、[アプリ パッケージ マニフェスト](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/schema-root).

たとえば、拡張機能を使用して、ファイアウォールの例外を作成、ファイルの種類の既定のアプリケーション、アプリケーションを作成またはスタート タイルをポイントして、アプリのパッケージ化されたバージョン。 拡張機能は、アプリのパッケージ マニフェスト ファイルに XML を追加するだけで使用できます。 コードは必要ありません。

この記事では、これらの拡張機能とそれらを使用して実行できるタスクについて説明します。

> [!NOTE]
> この記事で説明されている機能では、お客様のデスクトップ アプリケーションの Windows アプリ パッケージを作成することが必要です。 これはまだ完了していない場合を参照してください。[デスクトップ アプリケーションをパッケージ化](https://docs.microsoft.com/windows/msix/desktop/desktop-to-uwp-root)します。

## <a name="transition-users-to-your-app"></a>ユーザーをアプリに移行する

ユーザーによってパッケージ アプリが使用されるように、移行を促します。

* [既存のスタート タイルとタスク バー ボタンをポイントして、パッケージ アプリ](#point)
* [デスクトップ アプリではなくファイルを開き、パッケージ化されたアプリケーションを作成します。](#make)
* [ファイルの種類のセット、パッケージ化されたアプリケーションに関連付ける](#associate)
* [特定のファイルの種類のファイルのコンテキスト メニューにオプションを追加します。](#add)
* [URL を使用して直接特定の種類のファイルを開く](#open)

<a id="point" />

### <a name="point-existing-start-tiles-and-taskbar-buttons-to-your-packaged-app"></a>既存のスタート タイルとタスク バー ボタンの参照先をパッケージ アプリに設定する

ユーザーによって、デスクトップ アプリがタスク バーまたはスタート メニューにピン留めされている可能性があります。 これらのショートカットの参照先を新しいパッケージ アプリに変更できます。

#### <a name="xml-namespace"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.desktopAppMigration">
    <DesktopAppMigration>
        <DesktopApp AumId="[your_app_aumid]" />
        <DesktopApp ShortcutPath="[path]" />
    </DesktopAppMigration>
</Extension>

```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-rescap3-desktopappmigration)をご覧ください。

|Name | 説明 |
|-------|-------------|
|Category |常に ``windows.desktopAppMigration`` です。
|AumID |パッケージ アプリのアプリケーション ユーザー モデル ID。 |
|ShortcutPath |アプリのデスクトップ バージョンを起動する .lnk ファイルへのパス。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:rescap3="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3"
  IgnorableNamespaces="rescap3">
  <Applications>
    <Application>
      <Extensions>
        <rescap3:Extension Category="windows.desktopAppMigration">
          <rescap3:DesktopAppMigration>
            <rescap3:DesktopApp AumId="[your_app_aumid]" />
            <rescap3:DesktopApp ShortcutPath="%USERPROFILE%\Desktop\[my_app].lnk" />
            <rescap3:DesktopApp ShortcutPath="%APPDATA%\Microsoft\Windows\Start Menu\Programs\[my_app].lnk" />
            <rescap3:DesktopApp ShortcutPath="%PROGRAMDATA%\Microsoft\Windows\Start Menu\Programs\[my_app_folder]\[my_app].lnk"/>
         </rescap3:DesktopAppMigration>
        </rescap3:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a>関連するサンプル

[WPF ピクチャ ビューアーの移行/移行/アンインストール](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="make" />

### <a name="make-your-packaged-application-open-files-instead-of-your-desktop-app"></a>デスクトップ アプリではなくファイルを開き、パッケージ化されたアプリケーションを作成します。

ユーザーが特定の種類のデスクトップ バージョンのアプリを開く代わりにファイルの既定で、新しいパッケージ化されたアプリケーションを開くことを確認することができます。

これを行うには、ファイルの関連付けを継承するために、関連付けされている各アプリケーションの[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) を指定します。

#### <a name="xml-namespaces"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
<FileTypeAssociation Name="[AppID]">
         <MigrationProgIds>
            <MigrationProgId>"[ProgID]"</MigrationProgId>
        </MigrationProgIds>
    </FileTypeAssociation>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 この ID は、ファイルの種類の関連付けによって関連付けられたハッシュ対象の[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) を生成するために内部で使用されます。 この ID を使って、アプリの今後のバージョンで変更を管理することができます。 |
|MigrationProgId |[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids)アプリケーション、コンポーネント、およびファイルの関連付けを継承するデスクトップ アプリケーションのバージョンをについて説明します。|

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:rescap3="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3"
  IgnorableNamespaces="uap3, rescap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <rescap3:MigrationProgIds>
              <rescap3:MigrationProgId>Foo.Bar.1</rescap3:MigrationProgId>
              <rescap3:MigrationProgId>Foo.Bar.2</rescap3:MigrationProgId>
            </rescap3:MigrationProgIds>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a>関連するサンプル

[WPF ピクチャ ビューアーの移行/移行/アンインストール](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="associate" />

### <a name="associate-your-packaged-application-with-a-set-of-file-types"></a>ファイルの種類のセット、パッケージ化されたアプリケーションに関連付ける

パッケージ化されたアプリケーションは、ファイル拡張子に関連付けられていることができます。 ユーザーがファイルを右クリックし、選択した場合、**プログラムから開く**オプション、推奨事項の一覧で、アプリケーションが表示されます。

#### <a name="xml-namespace"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[file extension]"</FileType>
        </SupportedFileTypes>
    </FileTypeAssociation>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 この ID は、ファイルの種類の関連付けによって関連付けられたハッシュ対象の[プログラム識別子 (ProgID)](https://docs.microsoft.com/windows/desktop/shell/fa-progids) を生成するために内部で使用されます。 この ID を使って、アプリの今後のバージョンで変更を管理することができます。   |
|FileType |アプリでサポートされているファイル拡張子。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap, uap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap:SupportedFileTypes>
            <uap:FileType>.txt</uap:FileType>
            <uap:FileType>.avi</uap:FileType>
            </uap:SupportedFileTypes>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a>関連するサンプル

[WPF ピクチャ ビューアーの移行/移行/アンインストール](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="add" />

### <a name="add-options-to-the-context-menus-of-files-that-have-a-certain-file-type"></a>特定の種類のファイルのコンテキスト メニューにオプションを追加する

ほとんどの場合、ユーザーはファイルをダブルクリックして開きます。 ユーザーがファイルを右クリックすると、さまざまなオプションが表示されます。

このメニューには、オプションを追加できます。 これらのオプションを使用すると、ファイルの印刷、編集、プレビューなど、ファイルの操作を別の方法で行うことができます。

#### <a name="xml-namespaces"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedVerbs>
           <Verb Id="[ID]" Extended="[Extended]" Parameters="[parameters]">"[verb label]"</Verb>
        </SupportedVerbs>
    </FileTypeAssociation>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category | 常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 |
|Verb |エクスプローラーのコンテキスト メニューに表示される名前です。 この文字列は、```ms-resource``` を使用してローカライズできます。|
|Id |動詞の一意の ID。 アプリケーションが UWP アプリの場合、ユーザーの選択を適切に処理できるように、アクティブ化イベントの引数の一部としてアプリに渡されます。 アプリケーションが完全に信頼されているパッケージ アプリの場合は、パラメーターを受け取った代わりに (次の箇条書きを参照してください)。 |
|Parameters |動詞に関連付けられている引数のパラメーターと値のリスト。 アプリケーションが完全に信頼されているパッケージ アプリの場合は、これらのパラメーターは、アプリケーションがアクティブになるイベント引数としてアプリケーションに渡されます。 複数のアクティブ化の動詞に基づくアプリケーションの動作をカスタマイズすることができます。 変数にファイル パスが含まれる可能性がある場合は、パラメーター値を引用符で囲みます。 これにより、パスにスペースが含まれている場合に発生する問題を回避できます。 アプリケーションが UWP アプリの場合は、パラメーターを渡すことはできません。 アプリは、代わりに ID を受け取ります (前の項目を参照してください)。|
|Extended |ユーザーが **Shift** キーを押しながらファイルを右クリックすることでコンテキスト メニューを表示した場合にのみ表示される動詞を指定します。 この属性は省略可能であり、指定されていない場合の既定値は **False** (常に動詞を表示する) です。 この動作は各動詞について個別に指定します ("開く" は例外で、常に **False**)。|

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"

  IgnorableNamespaces="uap, uap2, uap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap2:SupportedVerbs>
              <uap3:Verb Id="Edit" Parameters="/e &quot;%1&quot;">Edit</uap3:Verb>
              <uap3:Verb Id="Print" Extended="true" Parameters="/p &quot;%1&quot;">Print</uap3:Verb>
            </uap2:SupportedVerbs>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

#### <a name="related-sample"></a>関連するサンプル

[WPF ピクチャ ビューアーの移行/移行/アンインストール](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/DesktopAppTransition)

<a id="open" />

### <a name="open-certain-types-of-files-directly-by-using-a-url"></a>URL を使用して特定の種類のファイルを直接開く

ユーザーが特定の種類のデスクトップ バージョンのアプリを開く代わりにファイルの既定で、新しいパッケージ化されたアプリケーションを開くことを確認することができます。

#### <a name="xml-namespaces"></a>XML 名前空間

* http:\//schemas.microsoft.com/appx/manifest/uap/windows10
* http:\//schemas.microsoft.com/appx/manifest/uap/windows10/3"

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]" UseUrl="true" Parameters="%1">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
    </FileTypeAssociation>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 |
|UseUrl |URL ターゲットから直接ファイルを開くかどうかを示します。 この値を設定しない場合は、システムを使用して URL 原因、最初のダウンロード ファイルをローカル ファイルを開くアプリケーションでしようとします。 |
|Parameters |省略可能なパラメーター。 |
|FileType |関連するファイル拡張子。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap, uap3">
  <Applications>
      <Application>
        <Extensions>
          <uap:Extension Category="windows.fileTypeAssociation">
            <uap3:FileTypeAssociation Name="documenttypes" UseUrl="true" Parameters="%1">
              <uap:SupportedFileTypes>
                <uap:FileType>.txt</uap:FileType>
                <uap:FileType>.doc</uap:FileType>
              </uap:SupportedFileTypes>
            </uap3:FileTypeAssociation>
          </uap:Extension>
        </Extensions>
      </Application>
    </Applications>
</Package>
```

## <a name="perform-setup-tasks"></a>セットアップ タスクを実行する

* [アプリがファイアウォールの例外を作成します。](#rules)
* [パッケージの任意のフォルダーに、DLL ファイルに配置します。](#load-paths)

<a id="rules" />

### <a name="create-firewall-exception-for-your-app"></a>アプリのファイアウォール例外を作成する

アプリケーションは、ポート経由の通信を必要とする場合は、ファイアウォールの例外の一覧にアプリケーションを追加できます。

#### <a name="xml-namespace"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.firewallRules">
  <FirewallRules Executable="[executable file name]">
    <Rule
      Direction="[Direction]"
      IPProtocol="[Protocol]"
      LocalPortMin="[LocalPortMin]"
      LocalPortMax="LocalPortMax"
      RemotePortMin="RemotePortMin"
      RemotePortMax="RemotePortMax"
      Profile="[Profile]"/>
  </FirewallRules>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-firewallrules)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |いつも ``windows.firewallRules``|
|Executable |ファイアウォールの例外の一覧に追加する実行可能ファイルの名前。 |
|Direction |規則が受信規則か送信規則かを示します。 |
|IPProtocol |通信プロトコル。 |
|LocalPortMin |ローカル ポート番号の範囲を示すポート番号の下限。 |
|LocalPortMax |ローカル ポート番号の範囲を示すポート番号の上限。 |
|RemotePortMax |リモート ポート番号の範囲を示すポート番号の下限。 |
|RemotePortMax |リモート ポート番号の範囲を示すポート番号の上限。 |
|Profile |ネットワークの種類。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="desktop2">
  <Extensions>
    <desktop2:Extension Category="windows.firewallRules">
      <desktop2:FirewallRules Executable="Contoso.exe">
          <desktop2:Rule Direction="in" IPProtocol="TCP" Profile="all"/>
          <desktop2:Rule Direction="in" IPProtocol="UDP" LocalPortMin="1337" LocalPortMax="1338" Profile="domain"/>
          <desktop2:Rule Direction="in" IPProtocol="UDP" LocalPortMin="1337" LocalPortMax="1338" Profile="public"/>
          <desktop2:Rule Direction="out" IPProtocol="UDP" LocalPortMin="1339" LocalPortMax="1340" RemotePortMin="15"
                         RemotePortMax="19" Profile="domainAndPrivate"/>
          <desktop2:Rule Direction="out" IPProtocol="GRE" Profile="private"/>
      </desktop2:FirewallRules>
  </desktop2:Extension>
</Extensions>
</Package>
```

<a id="load-paths" />

### <a name="place-your-dll-files-into-any-folder-of-the-package"></a>DLL ファイルをパッケージの任意のフォルダーに配置します。

拡張機能を使ってそれらのフォルダーを指定します。 これにより、システムは配置したファイルを見つけて読み込むことができます。 この拡張機能は、 _%PATH%_ 環境変数の置き換えと考えてください。

この拡張機能を使わない場合、システムはプロセスのパッケージの依存関係グラフ、パッケージ ルート フォルダー、システム ディレクトリ ( _%SystemRoot%\system32_) の順で検索します。 詳しくは、[Windows アプリの検索順序に関するページ](https://docs.microsoft.com/windows/desktop/Dlls/dynamic-link-library-search-order)をご覧ください。

各パッケージには、これらの拡張機能を 1 つだけ含めることができます。 つまり、1 つをメイン パッケージに追加し、他の拡張機能は[オプション パッケージと関連するセット](https://docs.microsoft.com/windows/uwp/packaging/optional-packages)それぞれに 1 つずつ追加できます。

#### <a name="xml-namespace"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/uap/windows10/6

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

アプリケーション マニフェストのパッケージ レベルでこの拡張機能を宣言します。

```XML
<Extension Category="windows.loaderSearchPathOverride">
  <LoaderSearchPathOverride>
    <LoaderSearchPathEntry FolderPath="[path]"/>
  </LoaderSearchPathOverride>
</Extension>

```

|Name | 説明 |
|-------|-------------|
|Category |常に ``windows.loaderSearchPathOverride`` です。
|FolderPath | dll ファイルが含まれているフォルダーのパス。 パッケージのルート フォルダーの相対パスを指定します。 1 つの拡張機能で最大 5 つのパスを指定できます。 システムがパッケージのルート フォルダーにあるファイルを検索するようにする場合、これらのパスのいずれかに空の文字列を使用します。 重複するパスを含めないでください。パスの先頭と末尾にスラッシュや円記号を使わないでください。 <br><br> システムはサブフォルダーを検索しないため、システムが読み込む DLL ファイルが含まれている各フォルダーを明示的に一覧表示してください。|

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/6"
  IgnorableNamespaces="uap6">
  ...
    <Extensions>
      <uap6:Extension Category="windows.loaderSearchPathOverride">
        <uap6:LoaderSearchPathOverride>
          <uap6:LoaderSearchPathEntry FolderPath=""/>
          <uap6:LoaderSearchPathEntry FolderPath="folder1/subfolder1"/>
          <uap6:LoaderSearchPathEntry FolderPath="folder2/subfolder2"/>
        </uap6:LoaderSearchPathOverride>
      </uap6:Extension>
    </Extensions>
...
</Package>
```

## <a name="integrate-with-file-explorer"></a>エクスプローラーに統合する

ユーザーが慣れた方法でファイルを整理し操作できるようになります。

* [ユーザーの選択し、同時に複数のファイルを開くときに、アプリケーションの動作を定義します。](#define)
* [ファイル エクスプ ローラー内でサムネイル画像のファイルの内容を表示します。](#show)
* [ファイル エクスプ ローラーのプレビュー ウィンドウにファイルの内容を表示します。](#preview)
* [ファイル エクスプ ローラーで、[種類] 列を使用して、ユーザーがファイルをグループ化を有効にします。](#enable)
* [検索、インデックス、プロパティ ダイアログ ボックス、および詳細ウィンドウにファイルのプロパティを使用できるように](#make-file-properties)
* [ファイルの種類のコンテキスト メニュー ハンドラーを指定します。](#context-menu)
* [クラウド サービスからのファイルをファイル エクスプ ローラーに表示](#cloud-files)

<a id="define" />

### <a name="define-how-your-application-behaves-when-users-select-and-open-multiple-files-at-the-same-time"></a>ユーザーの選択し、同時に複数のファイルを開くときに、アプリケーションの動作を定義します。

ユーザーが同時に複数のファイルを開いたときに、アプリケーションの動作を指定します。

#### <a name="xml-namespaces"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]" MultiSelectModel="[SelectionModel]">
        <SupportedVerbs>
            <Verb Id="Edit" MultiSelectModel="[SelectionModel]">Edit</Verb>
        </SupportedVerbs>
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 |
|MultiSelectModel |下を参照 |
|FileType |関連するファイル拡張子。 |

**MultSelectModel**

パッケージ デスクトップ アプリには、通常のデスクトップ アプリと同じ 3 つのオプションがあります。

* ``Player`` :アプリケーションは、1 回をアクティブ化されます。 すべての選択したファイルは、引数のパラメーターとしてアプリケーションに渡されます。
* ``Single`` :アプリケーションは、選択した最初のファイルの 1 つの時間をアクティブ化されます。 その他のファイルは無視されます。
* ``Document`` :選択したファイルごとに、アプリケーションの新しい、個別のインスタンスがアクティブ化されます。

 ファイルの種類やアクションごとに、さまざまな環境設定項目を設定できます。 たとえば、*Documents* は *Document* モードで開き、*Images* は *Player* モードで開くことができます。

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap, uap2, uap3">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="myapp" MultiSelectModel="Document">
            <uap2:SupportedVerbs>
              <uap3:Verb Id="Edit" MultiSelectModel="Player">Edit</uap3:Verb>
              <uap3:Verb Id="Preview" MultiSelectModel="Document">Preview</uap3:Verb>
            </uap2:SupportedVerbs>
            <uap:SupportedFileTypes>
              <uap:FileType>.txt</uap:FileType>
            </uap:SupportedFileTypes>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

ユーザーが 15 個以下のファイルを開いた場合、**MultiSelectModel** 属性の既定値は *Player* になります。 それ以外の場合、既定値は *Document* です。 UWP アプリは常に *Player* として起動されます。

<a id="show" />

### <a name="show-file-contents-in-a-thumbnail-image-within-file-explorer"></a>エクスプ ローラーでサムネイル画像のファイル内容を表示する

ファイルが中アイコン、大アイコン、特大アイコンで表示された場合に、ファイル内容のサムネイル画像をユーザーが確認できるようにします。

#### <a name="xml-namespace"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
        <ThumbnailHandler
            Clsid  ="[Clsid  ]" />
    </FileTypeAssociation>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 |
|FileType |関連するファイル拡張子。 |
|Clsid   |アプリのクラス ID。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="uap, uap2, uap3, desktop2">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap2:SupportedFileTypes>
              <uap:FileType>.bar</uap:FileType>
            </uap2:SupportedFileTypes>
            <desktop2:ThumbnailHandler
              Clsid  ="20000000-0000-0000-0000-000000000001"  />
            </uap3:FileTypeAssociation>
         </uap::Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="preview" />

### <a name="show-file-contents-in-the-preview-pane-of-file-explorer"></a>エクスプローラーのプレビュー ウィンドウにファイル内容を表示する

エクスプローラーのプレビュー ウィンドウで、ユーザーがファイルの内容をプレビューできるようにします。

#### <a name="xml-namespace"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/2
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
        <DesktopPreviewHandler Clsid  ="[Clsid  ]" />
    </FileTypeAssociation>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 |
|FileType |関連するファイル拡張子。 |
|Clsid   |アプリのクラス ID。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="uap, uap2, uap3, desktop2">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap2SupportedFileTypes>
              <uap:FileType>.bar</uap:FileType>
                </uap2SupportedFileTypes>
              <desktop2:DesktopPreviewHandler Clsid ="20000000-0000-0000-0000-000000000001" />
           </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="enable" />

### <a name="enable-users-to-group-files-by-using-the-kind-column-in-file-explorer"></a>ユーザーがエクスプローラーの [種類] 列を使用してファイルをグループ化できるようにする

ファイルの種類に関する 1 つまたは複数の定義済みの値を **Kind** フィールドに関連付けることができます。

ユーザーはエクスプローラーでこのフィールドを使用して、ファイルをグループ化できます。 また、このフィールドは、システム コンポーネントによって、インデックス作成などのさまざまな目的にも使用されます。

**Kind** フィールドの詳細と、このフィールドに使用できる値については、「[種類名の使用](https://docs.microsoft.com/windows/desktop/properties/building-property-handlers-user-friendly-kind-names)」をご覧ください。

#### <a name="xml-namespaces"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fileTypeAssociation">
    <FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>"[FileExtension]"</FileType>
        </SupportedFileTypes>
        <KindMap>
            <Kind value="[KindValue]">
        </KindMap>
    </FileTypeAssociation>
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 |
|FileType |関連するファイル拡張子。 |
|value |有効な [Kind 値](https://docs.microsoft.com/windows/desktop/properties/building-property-handlers-user-friendly-kind-names)。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:rescap="http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities/3"
  IgnorableNamespaces="uap, rescap">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
           <uap:FileTypeAssociation Name="Contoso">
             <uap:SupportedFileTypes>
               <uap:FileType>.m4a</uap:FileType>
               <uap:FileType>.mta</uap:FileType>
             </uap:SupportedFileTypes>
             <rescap:KindMap>
               <rescap:Kind value="Item">
               <rescap:Kind value="Communications">
               <rescap:Kind value="Task">
             </rescap:KindMap>
          </uap:FileTypeAssociation>
      </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="make-file-properties" />

### <a name="make-file-properties-available-to-search-index-property-dialogs-and-the-details-pane"></a>ファイルのプロパティを検索、インデックス、プロパティ ダイアログ、詳細ウィンドウに利用できるようにする

#### <a name="xml-namespace"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10
* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<uap:Extension Category="windows.fileTypeAssociation">
    <uap:FileTypeAssociation Name="[AppID]">
        <SupportedFileTypes>
            <FileType>.bar</FileType>
        </SupportedFileTypes>
        <DesktopPropertyHandler Clsid ="[Clsid]"/>
    </uap:FileTypeAssociation>
</uap:Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fileTypeAssociation`` です。
|Name |アプリの一意の ID。 |
|FileType |関連するファイル拡張子。 |
|Clsid  |アプリのクラス ID。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="uap, uap3, desktop2">
  <Applications>
    <Application>
      <Extensions>
        <uap:Extension Category="windows.fileTypeAssociation">
          <uap3:FileTypeAssociation Name="Contoso">
            <uap:SupportedFileTypes>
              <uap:FileType>.bar</uap:FileType>
            </uap:SupportedFileTypes>
            <desktop2:DesktopPropertyHandler Clsid ="20000000-0000-0000-0000-000000000001"/>
          </uap3:FileTypeAssociation>
        </uap:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="context-menu" />

### <a name="specify-a-context-menu-handler-for-a-file-type"></a>ファイルの種類のコンテキスト メニュー ハンドラーを指定します。

お客様のデスクトップ アプリケーションが定義されている場合、[コンテキスト メニュー ハンドラー](https://docs.microsoft.com/windows/desktop/shell/context-menu-handlers)、メニュー ハンドラーを登録するこの拡張機能を使用します。

#### <a name="xml-namespaces"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/foundation/windows10
* http://schemas.microsoft.com/appx/manifest/desktop/windows10/4

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extensions>
    <com:Extension Category="windows.comServer">
        <com:ComServer>
            <com:SurrogateServer AppId="[AppID]" DisplayName="[DisplayName]">
                <com:Class Id="[Clsid]" Path="[Path]" ThreadingModel="[Model]"/>
            </com:SurrogateServer>
        </com:ComServer>
    </com:Extension>
    <desktop4:Extension Category="windows.fileExplorerContextMenus">
        <desktop4:FileExplorerContextMenus>
            <desktop4:ItemType Type="[Type]">
                <desktop4:Verb Id="[ID]" Clsid="[Clsid]" />
            </desktop4:ItemType>
        </desktop4:FileExplorerContextMenus>
    </desktop4:Extension>
</Extensions>
```

ここで、完全なスキーマの参照を検索: [com:ComServer](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-com-comserver)と[desktop4:FileExplorerContextMenus](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop4-fileexplorercontextmenus)します。

#### <a name="instructions"></a>手順

コンテキスト メニュー ハンドラーを登録するには、次の手順に従います。

1. デスクトップ アプリケーションでは、実装、[コンテキスト メニュー ハンドラー](https://docs.microsoft.com/windows/desktop/shell/context-menu-handlers)実装することによって、 [IExplorerCommand](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommand)または[IExplorerCommandState](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommandstate)インターフェイス。 サンプルについては、次を参照してください。、 [ExplorerCommandVerb](https://github.com/microsoft/Windows-classic-samples/tree/master/Samples/Win7Samples/winui/shell/appshellintegration/ExplorerCommandVerb)コード サンプル。 実装オブジェクトのそれぞれのクラス GUID を定義することを確認します。 たとえば、次のコードは実装のクラス ID を定義します。 [IExplorerCommand](https://docs.microsoft.com/windows/desktop/api/shobjidl_core/nn-shobjidl_core-iexplorercommand)します。

    ```cpp
    class __declspec(uuid("d0c8bceb-28eb-49ae-bc68-454ae84d6264")) CExplorerCommandVerb;
    ```

2. パッケージ マニフェストで指定、 [com:ComServer](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-com-comserver)コンテキスト メニュー ハンドラーの実装のクラス ID を持つサロゲートの COM サーバーを登録するアプリケーションの拡張機能。

    ```xml
    <com:Extension Category="windows.comServer">
        <com:ComServer>
            <com:SurrogateServer AppId="d0c8bceb-28eb-49ae-bc68-454ae84d6264" DisplayName="ContosoHandler">
                <com:Class Id="d0c8bceb-28eb-49ae-bc68-454ae84d6264" Path="ExplorerCommandVerb.dll" ThreadingModel="STA"/>
            </com:SurrogateServer>
        </com:ComServer>
    </com:Extension>
    ```

2. パッケージ マニフェストで指定、 [desktop4:FileExplorerContextMenus](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop4-fileexplorercontextmenus)コンテキスト メニュー ハンドラーの実装を登録するアプリケーションの拡張機能。

    ```xml
    <desktop4:Extension Category="windows.fileExplorerContextMenus">
        <desktop4:FileExplorerContextMenus>
            <desktop4:ItemType Type=".rar">
                <desktop4:Verb Id="Command1" Clsid="d0c8bceb-28eb-49ae-bc68-454ae84d6264" />
            </desktop4:ItemType>
        </desktop4:FileExplorerContextMenus>
    </desktop4:Extension>
    ```

#### <a name="example"></a>例

```XML
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:desktop4="http://schemas.microsoft.com/appx/manifest/desktop/windows10/4"
  IgnorableNamespaces="desktop4">
  <Applications>
    <Application>
      <Extensions>
        <com:Extension Category="windows.comServer">
          <com:ComServer>
            <com:SurrogateServer AppId="d0c8bceb-28eb-49ae-bc68-454ae84d6264" DisplayName="ContosoHandler"">
              <com:Class Id="Id="d0c8bceb-28eb-49ae-bc68-454ae84d6264" Path="ExplorerCommandVerb.dll" ThreadingModel="STA"/>
            </com:SurrogateServer>
          </com:ComServer>
        </com:Extension>
        <desktop4:Extension Category="windows.fileExplorerContextMenus">
          <desktop4:FileExplorerContextMenus>
            <desktop4:ItemType Type=".contoso">
              <desktop4:Verb Id="Command1" Clsid="d0c8bceb-28eb-49ae-bc68-454ae84d6264" />
            </desktop4:ItemType>
          </desktop4:FileExplorerContextMenus>
        </desktop4:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="cloud-files" />

### <a name="make-files-from-your-cloud-service-appear-in-file-explorer"></a>クラウド サービスのファイルがエクスプローラーに表示されるようにする

アプリに実装するハンドラーを登録する ユーザーがエクスプローラーでクラウド ベースのファイルを右クリックしたときに表示されるコンテキスト メニュー オプションを追加することもできます。

#### <a name="xml-namespace"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.cloudfiles" >
    <CloudFiles IconResource="[Icon]">
        <CustomStateHandler Clsid ="[Clsid]"/>
        <ThumbnailProviderHandler Clsid ="[Clsid]"/>
        <ExtendedPropertyhandler Clsid ="[Clsid]"/>
        <CloudFilesContextMenus>
            <Verb Id ="Command3" Clsid= "[GUID]">[Verb Label]</Verb>
        </CloudFilesContextMenus>
    </CloudFiles>
</Extension>

```

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.cloudfiles`` です。
|iconResource |クラウド ファイル プロバイダー サービスを表すアイコン。 このアイコンは、エクスプローラーのナビゲーション ウィンドウに表示されます。  ユーザーは、このアイコンを選んでクラウド サービスのファイルを表示します。 |
|CustomStateHandler Clsid |CustomStateHandler を実装するアプリケーションのクラス ID。 システムは、このクラス ID を使ってクラウド ファイルのカスタム状態と列を要求します。 |
|ThumbnailProviderHandler Clsid |ThumbnailProviderHandler を実装するアプリケーションのクラス ID。 システムは、このクラス ID を使ってクラウド ファイルの縮小版イメージを要求します。 |
|ExtendedPropertyHandler Clsid |ExtendedPropertyHandler を実装するアプリケーションのクラス ID。  システムは、このクラス ID を使ってクラウド ファイルの拡張プロパティを要求します。 |
|Verb |クラウド サービスによって提供されるファイルのエクスプローラー コンテキスト メニューに表示される名前です。 |
|Id |動詞の一意の ID。 |

#### <a name="example"></a>例

```XML
<Package
    xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
    IgnorableNamespaces="desktop">
  <Applications>
    <Application>
      <Extensions>
        <Extension Category="windows.cloudfiles" >
            <CloudFiles IconResource="images\Wide310x150Logo.png">
                <CustomStateHandler Clsid ="20000000-0000-0000-0000-000000000001"/>
                <ThumbnailProviderHandler Clsid ="20000000-0000-0000-0000-000000000001"/>
                <ExtendedPropertyhandler Clsid ="20000000-0000-0000-0000-000000000001"/>
                <desktop:CloudFilesContextMenus>
                    <desktop:Verb Id ="keep" Clsid=
                       "20000000-0000-0000-0000-000000000001">
                       Always keep on this device</desktop:Verb>
                </desktop:CloudFilesContextMenus>
            </CloudFiles>
          </Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="start" />

## <a name="start-your-application-in-different-ways"></a>さまざまな方法でアプリケーションを起動します。

* [プロトコルを使用して、アプリケーションを開始します。](#protocol)
* [エイリアスを使用して、アプリケーションを起動します。](#alias)
* [ユーザーが Windows にログインすると、実行可能ファイルを開始します。](#executable)
* [ユーザーが各自の PC にデバイスを接続するときのアプリケーションの起動を有効にします。](#autoplay)
* [Microsoft Store から更新プログラムを受信した後に自動的に再起動します。](#updates)

<a id="protocol" />

### <a name="start-your-application-by-using-a-protocol"></a>プロトコルを使用して、アプリケーションを開始します。

プロトコルの関連付けによって、他のプログラムやシステム コンポーネントがパッケージ アプリと相互運用できるようにします。 プロトコルを使用して、パッケージ化されたアプリケーションが開始されると、それに従って動作できるように、アクティブ化イベントの引数を渡す特定のパラメーターを指定できます。 パラメーターは、完全に信頼できるパッケージ アプリでのみサポートされています。 UWP アプリでは、パラメーターを使用できません。

#### <a name="xml-namespace"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/uap/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension
    Category="windows.protocol">
  <Protocol
      Name="[Protocol name]"
      Parameters="[Parameters]" />
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-protocol)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.protocol`` です。
|Name |プロトコルの名前。 |
|Parameters |パラメーターと、アプリケーションがアクティブになるイベントの引数として、アプリケーションに渡す値の一覧。 変数にファイル パスが含まれる可能性がある場合は、パラメーター値を引用符で囲みます。 これにより、パスにスペースが含まれている場合に発生する問題を回避できます。 |

### <a name="example"></a>例

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  IgnorableNamespaces="uap3">
  <Applications>
    <Application>
      <Extensions>
         <uap3:Extension
                Category="windows.appExecutionAlias"
                Executable="exes\launcher.exe"
                EntryPoint="Windows.FullTrustApplication">
            <uap3:AppExecutionAlias>
                <desktop:ExecutionAlias Alias="Contoso.exe" />
            </uap3:AppExecutionAlias>
        </uap3:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="alias" />

### <a name="start-your-application-by-using-an-alias"></a>エイリアスを使用して、アプリケーションを起動します。

ユーザーおよびその他のプロセスは、アプリへの完全パスを指定するのにことがなく、アプリケーションを開始するのにエイリアスを使用できます。 そのエイリアス名を指定できます。

#### <a name="xml-namespaces"></a>XML 名前空間

* http://schemas.microsoft.com/appx/manifest/uap/windows10/3
* http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension
    Category="windows.appExecutionAlias"
    Executable="[ExecutableName]"
    EntryPoint="Windows.FullTrustApplication">
    <AppExecutionAlias>
        <desktop:ExecutionAlias Alias="[AliasName]" />
    </AppExecutionAlias>
</Extension>
```

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.appExecutionAlias`` です。
|Executable |エイリアスが呼び出されたときに起動する実行可能ファイルの相対パス。 |
|Alias |アプリの短い名前。 常に、拡張子 ".exe" で終わっている必要があります。 パッケージ内のアプリケーションごとにアプリの実行エイリアスは 1 つだけ指定できます。 複数のアプリで同じエイリアスが登録されている場合、システムは最後に登録されたアプリを呼び出します。したがって、他のアプリが上書きする可能性が低い一意のエイリアスを選んでください。
|

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3"
  xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
  IgnorableNamespaces="uap3, desktop">
  <Applications>
    <Application>
      <Extensions>
        <uap3:Extension
          Category="windows.protocol">
          <uap3:Protocol
            Name="myapp-cmd"
            Parameters="/p &quot;%1&quot;" />
        </uap3:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
 
...
</Package>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap-filetypeassociation)をご覧ください。

<a id="executable" />

### <a name="start-an-executable-file-when-users-log-into-windows"></a>ユーザーが Windows にログオンしたときに実行可能ファイルを起動する

スタートアップ タスクでは、ユーザーがログオンするたびに自動的に実行可能ファイルを実行するアプリケーションを許可します。

> [!NOTE]
> ユーザーは、このスタートアップ タスクを登録するには少なくとも 1 回のアプリケーションの起動を持ちます。

アプリケーションでは、複数のスタートアップ タスクを宣言できます。 各タスクは独立して起動されます。 すべてのスタートアップ タスクは、タスク マネージャーの **[スタートアップ]** タブに、アプリのマニフェストで指定した名前とアプリのアイコンを使って表示されます。 タスク マネージャーによって、タスクの起動への影響が自動的に分析されます。

ユーザーは、タスク マネージャーを使用して、アプリのスタートアップ タスクを手動で無効にすることができます。 ユーザーがタスクを無効にした場合、プログラムでタスクを再度有効にすることはできません。

#### <a name="xml-namespace"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension
    Category="windows.startupTask"
    Executable="[ExecutableName]"
    EntryPoint="Windows.FullTrustApplication">
  <StartupTask
      TaskId="[TaskID]"
      Enabled="true"
      DisplayName="[DisplayName]" />
</Extension>
```

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.startupTask`` です。|
|Executable |起動する実行可能ファイルへの相対パス。 |
|TaskId |タスクの一意の識別子。 この識別子を使用して、アプリケーション Api を呼び出すこと、 [Windows.ApplicationModel.StartupTask](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.StartupTask)クラスをプログラムで有効または、スタートアップ タスクを無効にします。 |
|有効 |初めて起動したタスクを有効にするか、無効にするかを指定します。 有効になっているタスクは、(ユーザーが無効にしていない限り) 次回ユーザーがログオンするときに実行されます。 |
|DisplayName |タスク マネージャーに表示されるタスクの名前。 この文字列は、```ms-resource``` を使用してローカライズできます。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10"
  IgnorableNamespaces="desktop">
  <Applications>
    <Application>
      <Extensions>
        <desktop:Extension
          Category="windows.startupTask"
          Executable="bin\MyStartupTask.exe"
          EntryPoint="Windows.FullTrustApplication">
        <desktop:StartupTask
          TaskId="MyStartupTask"
          Enabled="true"
          DisplayName="My App Service" />
        </desktop:Extension>
      </Extensions>
    </Application>
  </Applications>
 </Package>
```

<a id="autoplay" />

### <a name="enable-users-to-start-your-application-when-they-connect-a-device-to-their-pc"></a>ユーザーが各自の PC にデバイスを接続するときのアプリケーションの起動を有効にします。

自動再生は、ユーザーが各自の PC にデバイスを接続するときに、オプションとして、アプリケーションを表示できます。

#### <a name="xml-namespace"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/desktop/windows10/3

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.autoPlayHandler">
  <AutoPlayHandler>
    <InvokeAction ActionDisplayName="[action string]" ProviderDisplayName="[name of your app/service]">
      <Content ContentEvent="[Content event]" Verb="[any string]" DropTargetHandler="[Clsid]" />
      <Content ContentEvent="[Content event]" Verb="[any string]" Parameters="[Initialization parameter]"/>
      <Device DeviceEvent="[Device event]" HWEventHandler="[Clsid]" InitCmdLine="[Initialization parameter]"/>
    </InvokeAction>
  </AutoPlayHandler>
```

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.autoPlayHandler`` です。
|ActionDisplayName |ユーザーが PC に接続するデバイスで実行できるアクションを表す文字列です (例。「ファイルのインポート」または「ビデオを再生」)。 |
|ProviderDisplayName | アプリケーションまたはサービスを表す文字列です (例。「Contoso ビデオ プレーヤー」)。 |
|ContentEvent |ユーザーに ``ActionDisplayName`` と ``ProviderDisplayName`` をプロンプト表示する原因となるコンテンツ イベントの名前。 コンテンツ イベントは、カメラのメモリ カード、サム ドライブ、DVD などのボリューム デバイスが PC に挿入されたときに発生します。 これらのイベントの詳しい一覧については、[ここ](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference)をご覧ください。  |
|Verb |動詞の設定は、選択したオプションのアプリケーションに渡される値を識別します。 自動再生のイベントの起動アクションは複数指定できます。また、[動詞] 設定を使って、ユーザーがアプリで選んだアクションを確認できます。 アプリに渡される起動イベント引数の verb プロパティを調べることでユーザーが選んだオプションを確認できます。 [動詞] 設定には任意の値を使うことができます。ただし、予約されている open を除きます。 |
|DropTargetHandler |実装するアプリケーションのクラス ID、 [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017)インターフェイス。 リムーバブル メディアのファイルは、[IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) 実装の [Drop](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget.drop?view=visualstudiosdk-2017#Microsoft_VisualStudio_OLE_Interop_IDropTarget_Drop_Microsoft_VisualStudio_OLE_Interop_IDataObject_System_UInt32_Microsoft_VisualStudio_OLE_Interop_POINTL_System_UInt32__) メソッドに渡されます。  |
|Parameters |すべてのコンテンツ イベントで [IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) インターフェイスを実装する必要はありません。 どのコンテンツ イベントにも、[IDropTarget](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.idroptarget?view=visualstudiosdk-2017) インターフェイスを実装する代わりにコマンド ライン パラメーターを指定することができます。 これらのイベントでは、自動再生がこれらのコマンド ライン パラメーターを使用してアプリケーションを起動します。 アプリの初期化コードでそれらのパラメーターを解析して、自動再生によって起動したかどうかを判断し、カスタム実装を提供することができます。 |
|DeviceEvent |ユーザーに ``ActionDisplayName`` と ``ProviderDisplayName`` をプロンプト表示する原因となるデバイス イベントの名前。 デバイス イベントは、デバイスが PC に接続されると発生します。 デバイス イベントの先頭は文字列 ``WPD`` です。一覧については[ここ](https://docs.microsoft.com/windows/uwp/launch-resume/auto-launching-with-autoplay#autoplay-event-reference)をご覧ください。 |
|HWEventHandler |実装するアプリケーションのクラス ID、 [IHWEventHandler](https://docs.microsoft.com/windows/desktop/api/shobjidl/nn-shobjidl-ihweventhandler)インターフェイス。 |
|InitCmdLine |[IHWEventHandler](https://docs.microsoft.com/windows/desktop/api/shobjidl/nn-shobjidl-ihweventhandler) インターフェイスの [Initialize](https://docs.microsoft.com/windows/desktop/api/shobjidl/nf-shobjidl-ihweventhandler-initialize) メソッドに渡す文字列パラメーター。 |

### <a name="example"></a>例

```XML
<Package
  xmlns:desktop3="http://schemas.microsoft.com/appx/manifest/desktop/windows10/3"
  IgnorableNamespaces="desktop3">
  <Applications>
    <Application>
      <Extensions>
        <desktop3:Extension Category="windows.autoPlayHandler">
          <desktop3:AutoPlayHandler>
            <desktop3:InvokeAction ActionDisplayName="Import my files" ProviderDisplayName="ms-resource:AutoPlayDisplayName">
              <desktop3:Content ContentEvent="ShowPicturesOnArrival" Verb="show" DropTargetHandler="CD041BAE-0DEA-4472-9B7B-C98043D26EA8"/>
              <desktop3:Content ContentEvent="PlayVideoFilesOnArrival" Verb="play" Parameters="%1" />
              <desktop3:Device DeviceEvent="WPD\ImageSource" HWEventHandler="CD041BAE-0DEA-4472-9B7B-C98043D26EA8" InitCmdLine="/autoplay"/>
            </desktop3:InvokeAction>
          </desktop3:AutoPlayHandler>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="updates" />

### <a name="restart-automatically-after-receiving-an-update-from-the-microsoft-store"></a>Microsoft Store から更新プログラムを受信した後、自動的に再起動する

ユーザーに更新プログラムをインストールするときに、アプリケーションが開いている場合、アプリケーションを閉じます。

そのアプリケーションの場合、更新された後で再起動が完了すると、呼び出し、 [RegisterApplicationRestart](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-registerapplicationrestart)を再起動するすべてのプロセス内の関数。

各アクティブなウィンドウ、アプリケーションでの受信、 [WM_QUERYENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-queryendsession)メッセージ。 この時点で、アプリケーションを呼び出すことができます、 [RegisterApplicationRestart](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-registerapplicationrestart)必要な場合は、コマンドラインを更新するには、もう一度関数。

アプリケーション内のアクティブな各ウィンドウが受信すると、 [WM_ENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-endsession)メッセージ、アプリケーションがデータを保存およびシャット ダウンします。

>[!NOTE]
また、アクティブなウィンドウが表示される、 [WM_CLOSE](https://docs.microsoft.com/windows/desktop/winmsg/wm-close)メッセージ、アプリケーションが処理しない場合、 [WM_ENDSESSION](https://docs.microsoft.com/windows/desktop/Shutdown/wm-endsession)メッセージ。

この時点で、アプリケーションが、独自のプロセスを終了する 30 秒を持っているか、プラットフォームは、これらを強制的に終了します。

更新プログラムが完了した後、アプリケーションを再起動します。

## <a name="work-with-other-applications"></a>他のアプリケーションと連携する

他のアプリとの統合、他のプロセスの開始、情報の共有が可能です。

* [印刷をサポートするアプリケーションで印刷のターゲットとして表示される、アプリケーションを作成します。](#printing)
* [その他の Windows アプリケーションでのフォントの共有](#fonts)
* [ユニバーサル Windows プラットフォーム (UWP) アプリからの Win32 プロセスを開始します。](#win32-process)

<a id="printing" />

### <a name="make-your-application-appear-as-the-print-target-in-applications-that-support-printing"></a>印刷をサポートするアプリケーションで印刷のターゲットとして表示される、アプリケーションを作成します。

ユーザーは、メモ帳などの別のアプリケーションからデータを印刷する場合、アプリケーションの利用可能な印刷ターゲット アプリの一覧で印刷のターゲットとして表示を行うことができます。

XML Paper Specification (XPS) 形式で印刷データを受信するようにアプリケーションを変更する必要があります。

#### <a name="xml-namespaces"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.appPrinter">
    <AppPrinter
        DisplayName="[DisplayName]"
        Parameters="[Parameters]" />
</Extension>
```

完全なスキーマ リファレンスについては、[こちら](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-desktop2-appprinter)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.appPrinter`` です。
|DisplayName |アプリの印刷先一覧に表示する名前。 |
|Parameters |アプリケーションに要求を正しく処理するために必要な任意のパラメーター。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:desktop2="http://schemas.microsoft.com/appx/manifest/desktop/windows10/2"
  IgnorableNamespaces="desktop2">
  <Applications>
  <Application>
    <Extensions>
      <desktop2:Extension Category="windows.appPrinter">
        <desktop2:AppPrinter
          DisplayName="Send to Contoso"
          Parameters="/insertdoc %1" />
      </desktop2:Extension>
    </Extensions>
  </Application>
</Applications>
</Package>
```

この拡張機能を使用するサンプルについては、[こちら](https://github.com/Microsoft/DesktopBridgeToUWP-Samples/tree/master/Samples/PrintToPDF)をご覧ください。

<a id="fonts" />

### <a name="share-fonts-with-other-windows-applications"></a>他の Windows アプリケーションとフォントを共有する

他の Windows アプリケーションとカスタム フォントを共有できます。

#### <a name="xml-namespaces"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/desktop/windows10/2

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.sharedFonts">
    <SharedFonts>
      <Font File="[FontFile]" />
    </SharedFonts>
  </Extension>
```

完全なスキーマ リファレンスについては、[こちら](/uwp/schemas/appxpackage/uapmanifestschema/element-uap4-sharedfonts)をご覧ください。

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.sharedFonts`` です。
|File |共有するフォントが格納されたファイル。 |

#### <a name="example"></a>例

```XML
<Package
  xmlns:uap4="http://schemas.microsoft.com/appx/manifest/uap/windows10/4"
  IgnorableNamespaces="uap4">
  <Applications>
    <Application>
      <Extensions>
        <uap4:Extension Category="windows.sharedFonts">
          <uap4:SharedFonts>
            <uap4:Font File="Fonts\JustRealize.ttf" />
            <uap4:Font File="Fonts\JustRealizeBold.ttf" />
          </uap4:SharedFonts>
        </uap4:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

<a id="win32-process" />

### <a name="start-a-win32-process-from-a-universal-windows-platform-uwp-app"></a>ユニバーサル Windows プラットフォーム (UWP) アプリから Win32 プロセスを開始する

完全信頼で実行される Win32 プロセスを開始します。

#### <a name="xml-namespaces"></a>XML 名前空間

http://schemas.microsoft.com/appx/manifest/desktop/windows10

#### <a name="elements-and-attributes-of-this-extension"></a>この拡張機能の要素と属性

```XML
<Extension Category="windows.fullTrustProcess" Executable="[executable file]">
  <FullTrustProcess>
    <ParameterGroup GroupId="[GroupID]" Parameters="[Parameters]"/>
  </FullTrustProcess>
</Extension>
```

|Name |説明 |
|-------|-------------|
|Category |常に ``windows.fullTrustProcess`` です。
|GroupID |実行可能ファイルに渡すパラメーターのセットを識別するための文字列。 |
|Parameters |実行可能ファイルに渡すパラメーター。 |

#### <a name="example"></a>例

```XML
<Package xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
         xmlns:rescap=
"http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities"
         xmlns:desktop="http://schemas.microsoft.com/appx/manifest/desktop/windows10">
  ...
  <Capabilities>
      <rescap:Capability Name="runFullTrust"/>
  </Capabilities>
  <Applications>
    <Application>
      <Extensions>
          <desktop:Extension Category="windows.fullTrustProcess" Executable="fulltrustprocess.exe">
              <desktop:FullTrustProcess>
                  <desktop:ParameterGroup GroupId="SyncGroup" Parameters="/Sync"/>
                  <desktop:ParameterGroup GroupId="OtherGroup" Parameters="/Other"/>
              </desktop:FullTrustProcess>
           </desktop:Extension>
      </Extensions>
    </Application>
  </Applications>
</Package>
```

この拡張機能をすべてのデバイスで動作するユニバーサル Windows プラットフォームのユーザー インターフェイスを作成する場合に便利ですが完全信頼で実行を継続する Win32 アプリケーションのコンポーネントをします。

Win32 アプリの Windows アプリ パッケージを作成します。 そのうえで、この拡張機能を UWP アプリのパッケージ ファイルに追加してください。 この拡張機能では、Windows アプリ パッケージの実行可能ファイルを起動することを示します。  UWP アプリと Win32 アプリの間でやり取りを行うには、1 つまたは複数の[アプリ サービス](/windows/uwp/launch-resume/app-services.md)を設定します。 このシナリオについては詳しくは、[こちら](https://blogs.msdn.microsoft.com/appconsult/2016/12/19/desktop-bridge-the-migrate-phase-invoking-a-win32-process-from-a-uwp-app/)をご覧ください。

## <a name="next-steps"></a>次のステップ

**質問の回答を検索**

ご質問がある場合は、 Stack Overflow でお問い合わせください。 Microsoft のチームでは、これらの[タグ](https://stackoverflow.com/questions/tagged/project-centennial+or+desktop-bridge)をチェックしています。 [こちら](https://social.msdn.microsoft.com/Forums/en-US/home?filter=alltypes&sort=relevancedesc&searchTerm=%5BDesktop%20Converter%5D)から質問することもできます。

**ご意見や機能を提案します。**

[UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/161895-desktop-bridge-centennial) のページをご覧ください。
