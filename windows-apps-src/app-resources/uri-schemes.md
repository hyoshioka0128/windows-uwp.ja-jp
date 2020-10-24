---
Description: アプリのパッケージ、アプリのデータ フォルダー、またはクラウドからのファイルを参照するために使用できる URI (Uniform Resource Identifier) スキームはいくつかあります。 また、URI スキームを使用して、アプリのリソース ファイル (.resw) から読み込まれた文字列を参照することもできます。
title: URI スキーム
template: detail.hbs
ms.date: 10/16/2017
ms.topic: article
keywords: Windows 10, UWP, リソース, 画像, アセット, MRT, 修飾子
ms.localizationpriority: medium
ms.openlocfilehash: 2f5bf063c12362fe26e3810e6153b857b7c1a2e4
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89170526"
---
# <a name="uri-schemes"></a>URI スキーム

アプリのパッケージ、アプリのデータ フォルダー、またはクラウドからのファイルを参照するために使用できる URI (Uniform Resource Identifier) スキームはいくつかあります。 また、URI スキームを使用して、アプリのリソース ファイル (.resw) から読み込まれた文字列を参照することもできます。 これらの URI スキームは、コード、XAML マークアップ、アプリ パッケージ マニフェスト、またはタイル/トースト通知テンプレートで使用できます。

## <a name="common-features-of-the-uri-schemes"></a>URI スキームの一般的な機能

このトピックで説明しているスキームはすべて、正規化とリソース取得について一般的な URI スキーム規則に従っています。 URI の一般的な構文については、[RFC 3986](https://www.ietf.org/rfc/rfc3986.txt) をご覧ください。

すべての URI スキームでは [RFC 3986](https://www.ietf.org/rfc/rfc3986.txt) に従い、URI の機関コンポーネントおよびパス コンポーネントとして階層部分を定義しています。

```syntax
URI         = scheme ":" hier-part [ "?" query ] [ "#" fragment ]
hier-part   = "//" authority path-abempty
            / path-absolute
            / path-rootless
            / path-empty
```

つまり、URI には原則として 3 つのコンポーネントがあります。 URI *スキーム* には、2 つのスラッシュの直後に "*機関*" コンポーネントがあります (空白にすることも可能)。 この直後にあるのが "*パス*" です。 例として URI `http://www.contoso.com/welcome.png` では、スキームが "`http://`"、機関が "`www.contoso.com`"、パスが "`/welcome.png`" です。 別の例として、URI `ms-appx:///logo.png` では、機関コンポーネントが空であり、既定値が使用されています。

フラグメント コンポーネントは、このトピックで説明している URI のスキーム固有の処理では無視されます。 リソースの取得と比較の間、フラグメント コンポーネントは意味を持ちません。 ただし、特定の実装上のレイヤーでは、フラグメントを解釈してセカンダリ リソースを取得することがあります。

すべての IRI コンポーネントの正規化が終了すると、バイトごとの比較が行われます。

## <a name="case-insensitivity-and-normalization"></a>大文字と小文字の区別と正規化

このトピックで説明している URI スキームはすべて、スキームの正規化とリソース取得について一般的な URI 規則 (RFC 3986) に従っています。 これらの URI の正規化された形式では、大文字と小文字が保持され、RFC 3986 の非予約文字がパーセントデコードされます。

このトピックで説明されているすべての URI スキームでは、標準では*スキーム*、*機関*、および*パス*の大文字と小文字が区別されません。それ以外でも、大文字と小文字を区別せずシステムによって処理されます。 **注** そのルールの唯一の例外は、`ms-resource` の*機関*で、大文字と小文字が区別されます。

## <a name="ms-appx-and-ms-appx-web"></a>ms-appx と ms-appx-web

アプリのパッケージに含まれるファイルを参照するには、URI スキーム `ms-appx` または `ms-appx-web` を使用します (「[アプリのパッケージ化](../packaging/index.md)」をご覧ください)。 アプリ パッケージ内のファイルは通常、静的なイメージ ファイル、データ ファイル、コード ファイル、レイアウト ファイルです。 `ms-appx-web` スキームは、`ms-appx` と同じファイルにアクセスしますが、このファイルは Web コンパートメントにあります。 例や詳しい情報については、「[XAML マークアップとコードから画像やその他のアセットを参照する](images-tailored-for-scale-theme-contrast.md#reference-an-image-or-other-asset-from-xaml-markup-and-code)」をご覧ください。

### <a name="scheme-name-ms-appx-and-ms-appx-web"></a>スキーム名 (ms-appx と ms-appx-web)

URI スキーム名は、文字列 "ms-appx" または "ms-appx-web" です。

```xml
ms-appx://
```

```xml
ms-appx-web://
```

### <a name="authority-ms-appx-and-ms-appx-web"></a>機関 (ms-appx と ms-appx-web)

機関は、パッケージ マニフェストで定義されているパッケージ ID 名です。 したがって、URI 形式と IRI (Internationalized Resource Identifier) 形式のどちらでも、パッケージ ID 名で許可されている文字のセットに制限されます。 パッケージ名は、現在動作しているアプリのパッケージ依存グラフ内のいずれかのパッケージの名前にする必要があります。

```xml
ms-appx://Contoso.MyApp/
ms-appx-web://Contoso.MyApp/
```

機関に他の文字が使用されると、取得と比較の処理に失敗します。 機関の既定値は、現在実行中のアプリのパッケージです。

```xml
ms-appx:///
ms-appx-web:///
```

### <a name="user-info-and-port-ms-appx-and-ms-appx-web"></a>ユーザー情報とポート (ms-appx と ms-appx-web)

`ms-appx` スキームは、他の一般的なスキームとは異なり、ユーザー情報やポートのコンポーネントを定義しません。 "@" and ":" は機関の有効な値として許可されていないため、これらが含まれていると参照は失敗します。 以下の処理はそれぞれ失敗となります。

```xml
ms-appx://john@contoso.myapp/default.html
ms-appx://john:password@contoso.myapp/default.html
ms-appx://contoso.myapp:8080/default.html
ms-appx://john:password@contoso.myapp:8080/default.html
```

### <a name="path-ms-appx-and-ms-appx-web"></a>パス (ms-appx と ms-appx-web)

パス コンポーネントは RFC 3986 の一般的な構文に一致し、IRI 内の非 ASCII 文字をサポートします。 パス コンポーネントは、ファイルの論理ファイル パスまたは物理ファイル パスを定義します。 このファイルは、機関で指定されたアプリのアプリ パッケージのインストール先に関連付けられたフォルダー内にあります。

パスが物理パスとファイル名を指している場合は、物理ファイル資産が取得されます。 ただし、このような物理ファイルが見つからなかった場合は、取得中に返される実際のリソースは、実行時のコンテンツ ネゴシエーションを使って決定されます。 この決定は、アプリ、OS、その他のユーザー設定 (言語、表示倍率、テーマ、ハイ コントラスト、その他の実行時コンテキスト) に基づいて行われます。 たとえば、取得される実際のリソース値を決定する際には、アプリの言語、システムのディスプレイ設定、ユーザーのハイ コントラスト設定の組み合わせが考慮されます。

```xml
ms-appx:///images/logo.png
```

上の URI では、実際には次の物理ファイル名を持つ現在のアプリ パッケージ内のファイルが取得されます。

<blockquote>
<pre>
\Images\fr-FR\logo.scale-100_contrast-white.png
</blockquote>
</pre>

もちろん、完全名を直接参照することで、同じ物理ファイルを取得することもできます。

```xaml
<Image Source="ms-appx:///images/fr-FR/logo.scale-100_contrast-white.png"/>
```

パス コンポーネント `ms-appx(-web)` では、一般的な URI と同様、大文字と小文字が区別されます。 ただし、リソースにアクセスする基になるファイル システムが大文字と小文字を区別しない場合 (NTFS など)、リソースの取得は大文字と小文字の区別なく実行されます。

正規化された URI 形式では大文字と小文字が保持され、RFC 3986 の非予約文字がパーセントデコードされます ("%" 記号の後に 2 桁の 16 進数表現)。 文字 "?"、"#"、"/"、"*"、および "" (二重引用符) は、ファイル名やフォルダー名などのデータを表すパスでパーセントエンコードする必要があります。 パーセントエンコードされたすべての文字は、取得前にデコードされます。 したがって、Hello#World.html という名前のファイルを取得するには、この URI を使用します。

```xml
ms-appx:///Hello%23World.html
```

### <a name="query-ms-appx-and-ms-appx-web"></a>クエリ (ms-appx と ms-appx-web)

クエリ パラメーターは、リソースの取得時には無視されます。 正規化されたクエリ パラメーターの形式では大文字と小文字が保持されます。 クエリ パラメーターは、比較時には無視されません。

## <a name="ms-appdata"></a>ms-appdata

アプリのローカル フォルダー、ローミング フォルダー、一時データ フォルダーのアプリ ファイルを参照するには、URI スキーム `ms-appdata` を使用します。 アプリ データ フォルダーについて詳しくは、「[設定と他のアプリ データを保存して取得する](../design/app-settings/store-and-retrieve-app-data.md)」をご覧ください。

URI スキーム `ms-appdata` では、[ms-appx と ms-appx-web](#ms-appx-and-ms-appx-web) で行われるような、実行時のコンテンツ ネゴシエーションは行われません。 ただし、URI 内で物理ファイルの完全名を使用すると、[ResourceContext.QualifierValues](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.QualifierValues) のコンテンツに応答し、アプリ データから適切なアセットを読み込むことができます。

### <a name="scheme-name-ms-appdata"></a>スキーム名 (ms-appdata)

URI スキーム名は、文字列 "ms-appdata" です。

```xml
ms-appdata://
```

### <a name="authority-ms-appdata"></a>機関 (ms-appdata)

機関は、パッケージ マニフェストで定義されているパッケージ ID 名です。 したがって、URI 形式と IRI (Internationalized Resource Identifier) 形式のどちらでも、パッケージ ID 名で許可されている文字のセットに制限されます。 パッケージ名は、現在動作しているアプリ パッケージの名前にする必要があります。

```xml
ms-appdata://Contoso.MyApp/
```

機関に他の文字が使用されると、取得と比較の処理に失敗します。 機関の既定値は、現在実行中のアプリのパッケージです。

```xml
ms-appdata:///
```

### <a name="user-info-and-port-ms-appdata"></a>ユーザー情報とポート (ms-appdata)

`ms-appdata` スキームは、他の一般的なスキームとは異なり、ユーザー情報やポートのコンポーネントを定義しません。 "@" and ":" は機関の有効な値として許可されていないため、これらが含まれていると参照は失敗します。 以下の処理はそれぞれ失敗となります。

```xml
ms-appdata://john@contoso.myapp/local/data.xml
ms-appdata://john:password@contoso.myapp/local/data.xml
ms-appdata://contoso.myapp:8080/local/data.xml
ms-appdata://john:password@contoso.myapp:8080/local/data.xml
```

### <a name="path-ms-appdata"></a>パス (ms-appdata)

パス コンポーネントは RFC 3986 の一般的な構文に一致し、IRI 内の非 ASCII 文字をサポートします。 [Windows.Storage.ApplicationData](/uwp/api/Windows.Storage.ApplicationData?branch=live) の場所には、ローカル ストレージ、ローミング ストレージ、一時状態ストレージの 3 つの予約済みフォルダーがあります。 `ms-appdata` スキームを使用すると、これらの場所にあるファイルとフォルダーへのアクセスが可能になります。 パス コンポーネントの最初のセグメントでは、次の方法で特定のフォルダーを指定する必要があります。 したがって、"hier-part" の "path-empty" 形式は許可されません。

ローカル フォルダーの場合:

```xml
ms-appdata:///local/
```

一時フォルダーの場合:

```xml
ms-appdata:///temp/
```

ローミング フォルダーの場合:

```xml
ms-appdata:///roaming/
```

パス コンポーネント `ms-appdata` では、一般的な URI と同様、大文字と小文字が区別されます。 ただし、リソースにアクセスする基になるファイル システムが大文字と小文字を区別しない場合 (NTFS など)、リソースの取得は大文字と小文字の区別なく実行されます。

正規化された URI 形式では大文字と小文字が保持され、RFC 3986 の非予約文字がパーセントデコードされます ("%" 記号の後に 2 桁の 16 進数表現)。 文字 "?"、"#"、"/"、"*"、および "" (二重引用符) は、ファイル名やフォルダー名などのデータを表すパスでパーセントエンコードする必要があります。 パーセントエンコードされたすべての文字は、取得前にデコードされます。 したがって、Hello#World.html という名前のローカル ファイルを取得するには、この URI を使用します。

```xml
ms-appdata://local/Hello%23World.html
```

最上位のパス セグメントのリソースと ID の取得は、ドットの正規化の後に処理されます (".././b/c")。 したがって、予約済みフォルダーの外側で URI にドットを使うことはできません。 そのため、次の URI は許可されません。

```xml
ms-appdata:///local/../hello/logo.png
```

この URI は (冗長ですが) 許可されます。

```xml
ms-appdata:///local/../roaming/logo.png
```

### <a name="query-ms-appdata"></a>クエリ (ms-appdata)

クエリ パラメーターは、リソースの取得時には無視されます。 正規化されたクエリ パラメーターの形式では大文字と小文字が保持されます。 クエリ パラメーターは、比較時には無視されません。

## <a name="ms-resource"></a>ms-resource

アプリのリソース ファイル (.resw) から読み込まれた文字列を参照するには、URI スキーム `ms-resource` を使用します。 リソース ファイルの例と詳しい情報については、「[UI とアプリ パッケージ マニフェスト内の文字列をローカライズする](localize-strings-ui-manifest.md)」をご覧ください。

### <a name="scheme-name-ms-resource"></a>スキーム名 (ms-resource)

URI スキーム名は、文字列 "ms-resource" です。

```xml
ms-resource://
```

### <a name="authority-ms-resource"></a>機関 (ms-resource)

機関は、パッケージ リソース インデックス (PRI) 内で定義された最上位のリソース マップで、通常はパッケージ マニフェストで定義されたパッケージ ID 名に対応しています。 「 [アプリのパッケージ化](../packaging/index.md)」を参照してください)。 したがって、URI 形式と IRI (Internationalized Resource Identifier) 形式のどちらでも、パッケージ ID 名で許可されている文字のセットに制限されます。 パッケージ名は、現在動作しているアプリのパッケージ依存グラフ内のいずれかのパッケージの名前にする必要があります。

```xml
ms-resource://Contoso.MyApp/
ms-resource://Microsoft.WinJS.1.0/
```

機関に他の文字が使用されると、取得と比較の処理に失敗します。 機関の既定値は、現在実行中のアプリのパッケージ名 (大文字と小文字の区別あり) です。

```xml
ms-resource:///
```

機関では大文字と小文字が区別され、正規化された形式で大文字と小文字が保持されます。 ただし、リソースの参照では大文字と小文字が区別されません。

### <a name="user-info-and-port-ms-resource"></a>ユーザー情報とポート (ms-resource)

`ms-resource` スキームは、他の一般的なスキームとは異なり、ユーザー情報やポートのコンポーネントを定義しません。 "@" and ":" は機関の有効な値として許可されていないため、これらが含まれていると参照は失敗します。 以下の処理はそれぞれ失敗となります。

```xml
ms-resource://john@contoso.myapp/Resources/String1
ms-resource://john:password@contoso.myapp/Resources/String1
ms-resource://contoso.myapp:8080/Resources/String1
ms-resource://john:password@contoso.myapp:8080/Resources/String1
```

### <a name="path-ms-resource"></a>パス (ms-resource)

パスでは、[ResourceMap](/uwp/api/Windows.ApplicationModel.Resources.Core.ResourceMap?branch=live) サブツリー (「[リソース管理システム](/previous-versions/windows/apps/jj552947(v=win.10))」をご覧ください) とサブツリー内の [NamedResource](/uwp/api/Windows.ApplicationModel.Resources.Core.NamedResource?branch=live) の階層の場所が特定されます (「リソース管理システム」をご覧ください)。 これは通常、リソース ファイル (.resw) のファイル名 (拡張子を除く) と、ファイル内の文字列リソースの識別子に対応しています。

例と詳しい情報については、「[UI とアプリ パッケージ マニフェスト内の文字列をローカライズする](localize-strings-ui-manifest.md)」と「[言語、スケール、ハイ コントラストに合わせたタイルとトースト通知のサポート](../design/shell/tiles-and-notifications/tile-toast-language-scale-contrast.md)」をご覧ください。

パス コンポーネント `ms-resource` では、一般的な URI と同様、大文字と小文字が区別されます。 ただし、基になる取得では、 *ignoreCase*がに設定された[comparestringordinal](/windows/desktop/api/winstring/nf-winstring-windowscomparestringordinal)が使用され `true` ます。

正規化された URI 形式では大文字と小文字が保持され、RFC 3986 の非予約文字がパーセントデコードされます ("%" 記号の後に 2 桁の 16 進数表現)。 文字 "?"、"#"、"/"、"*"、および "" (二重引用符) は、ファイル名やフォルダー名などのデータを表すパスでパーセントエンコードする必要があります。 パーセントエンコードされたすべての文字は、取得前にデコードされます。 したがって、という名前のリソースファイルから文字列リソースを取得するには `Hello#World.resw` 、この URI を使用します。

```xml
ms-resource:///Hello%23World/String1
```

### <a name="query-ms-resource"></a>クエリ (ms-resource)

クエリ パラメーターは、リソースの取得時には無視されます。 正規化されたクエリ パラメーターの形式では大文字と小文字が保持されます。 クエリ パラメーターは、比較時には無視されません。 クエリ パラメーターは、大文字と小文字を区別して比較されます。

この URI 解析の上にレイヤー化される特定のコンポーネントの開発者は、適切と思われるクエリ パラメーターを使うこともできます。

## <a name="related-topics"></a>関連トピック

* [Uniform Resource Identifier (URI): 一般的な構文](https://www.ietf.org/rfc/rfc3986.txt)
* [アプリのパッケージ化](../packaging/index.md)
* [XAML マークアップとコードから画像やその他のアセットを参照する](images-tailored-for-scale-theme-contrast.md#reference-an-image-or-other-asset-from-xaml-markup-and-code)
* [設定と他のアプリ データを保存して取得する](../design/app-settings/store-and-retrieve-app-data.md)
* [UI とアプリ パッケージ マニフェスト内の文字列をローカライズする](localize-strings-ui-manifest.md)
* [リソース管理システム](/previous-versions/windows/apps/jj552947(v=win.10))
* [言語、スケール、ハイ コントラストに合わせたタイルとトースト通知のサポート](../design/shell/tiles-and-notifications/tile-toast-language-scale-contrast.md)