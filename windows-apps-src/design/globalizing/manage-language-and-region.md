---
Description: このトピックでは、用語のユーザー プロファイルの言語の一覧、アプリ マニフェストの言語の一覧、およびアプリ ランタイム言語の一覧を定義します。 これらの用語は、この機能領域のこのトピックおよびその他のトピックで使用しますので、意味を把握しておくことが重要です。
title: ユーザー プロファイルの言語とアプリ マニフェストの言語について
ms.assetid: 22D3A937-736A-4121-8285-A55DED56E594
template: detail.hbs
ms.date: 11/08/2017
ms.topic: article
keywords: Windows 10, UWP, グローバリゼーション, ローカライズの可否, ローカライズ
ms.localizationpriority: medium
ms.openlocfilehash: d782e8cd64cb976df964c72199964c1d349d527e
ms.sourcegitcommit: b034650b684a767274d5d88746faeea373c8e34f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57605577"
---
# <a name="understand-user-profile-languages-and-app-manifest-languages"></a>ユーザー プロファイルの言語とアプリ マニフェストの言語について
Windows ユーザーは、**[設定]** > **[時刻と言語]** > **[地域と言語]** の順に移動して、優先される表示言語の順序指定された一覧を構成するか、または優先される 1 つの表示言語を構成できます。 言語には場合によっては地域バリアントがあります。 たとえば、スペインで話されるスペイン語、メキシコで話されるスペイン語、米国で話されるスペイン語などを選ぶことができます。

また、**[設定]** > **[時刻と言語]** > **[地域と言語]** では、言語とは別に世界中の場所 (地域と呼ばれます) を指定できます。 表示言語 (および地域バリアント) の設定は地域の設定を決定するものではありません。その逆も同様です。 たとえば、現在フランスに住んでいるユーザーが、優先される Windows 表示言語としてスペイン語 (メキシコ) を選択している場合があります。

UWP アプリの場合、言語は [BCP-47 言語タグ](https://go.microsoft.com/fwlink/p/?linkid=227302)として表示されます。 たとえば、BCP-47 言語タグ "en-US" は **[設定]** の英語 (米国)に対応しています。 適切な UWP API は、BCP-47 言語タグの文字列表現を受け入れて返します。

「[IANA 言語サブタグ レジストリ](https://go.microsoft.com/fwlink/p/?linkid=227303)」も参照してください。

次の 3 つのセクションでは、"ユーザー プロファイルの言語の一覧"、"アプリ マニフェストの言語の一覧"、"アプリの実行時の言語の一覧" という用語を定義します。 これらの用語は、この機能領域のこのトピックおよびその他のトピックで使用しますので、意味を把握しておくことが重要です。

## <a name="user-profile-language-list"></a>ユーザー プロファイルの言語の一覧
ユーザー プロファイルの言語の一覧は、**[設定]** > **[時刻と言語]** > **[地域と言語]** > **[言語]** でユーザーによって構成された一覧の名前です。 コードでは、[**GlobalizationPreferences.Languages**](/uwp/api/windows.system.userprofile.globalizationpreferences.Languages) プロパティを使用して、読み取り専用の文字列一覧としてユーザー プロファイルの言語の一覧にアクセスできます。この一覧では、各文字列は "en-US" または "ja-JP" などの単一の [BCP-47 言語タグ](https://go.microsoft.com/fwlink/p/?linkid=227302) です。

```csharp
    IReadOnlyList<string> userLanguages = Windows.System.UserProfile.GlobalizationPreferences.Languages;
```

## <a name="app-manifest-language-list"></a>アプリ マニフェストの言語の一覧
アプリ マニフェストの言語の一覧は、アプリでサポートを宣言している (または宣言する) 言語の一覧です。 この一覧は、ローカライズまで開発ライフサイクルを通じてアプリを進行させるにつれて大きくなります。

一覧はコンパイル時に決定されますが、決定方法を正確に制御するための 2 つのオプションがあります。 1 つ目のオプションは、Visual Studio でプロジェクト内のファイルから一覧を決定する方法です。 これを行うには、まずアプリのパッケージ マニフェスト ソース ファイル (`Package.appxmanifest`) の **[アプリケーション]** タブでアプリの**既定の言語**を設定します。 次に、同じファイルにこの構成が含まれていることを確認します (既定では含まれています)。

```xml
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
```

ビルドされたアプリ パッケージ マニフェスト ファイル (`AppxManifest.xml`) を Visual Studio が生成するたびに、ソース ファイル内の単一の `Resource` 要素をプロジェクトに含まれる統合したすべての言語修飾子に展開します (「[言語、スケール、ハイ コントラスト、その他の修飾子用にリソースを調整する](../../app-resources/tailor-resources-lang-scale-contrast.md)」を参照)。 たとえば、ローカライズを開始して、文字列、イメージ、またはフォルダー名またはファイル名に "en-US"、"ja-JP"、"fr-FR" が含まれるファイル リソースがある場合、作成された `AppxManifest.xml` ファイルには次の内容が含まれます (一覧の最初のエントリは設定した既定の言語です)。

```xml
  <Resources>
    <Resource Language="EN-US" />
    <Resource Language="JA-JP" />
    <Resource Language="FR-FR" />
  </Resources>
```

もう 1 つのオプションは、アプリ パッケージ マニフェスト ソース ファイル (`Package.appxmanifest`) 内の単一の "x-generate" `<Resource>` 要素を `<Resource>` 要素の展開時のリストで置き換える方法です (既定の言語を最初に表示するように注意してください)。 このオプションの方がメンテナンス作業が多くなりますが、カスタム ビルド システムを使用する場合には適切なオプションです。

まず、アプリ マニフェストの言語の一覧には 1 つの言語のみが含められます。 たとえば en-US です。 ただし、最終的にマニフェストを手動で構成するか、または翻訳済みのリソースをプロジェクトに追加すると、リストは大きくなります。

アプリが Microsoft Store にある場合、アプリ マニフェストの言語の一覧の言語は、ユーザーに表示される言語になります。 特に Microsoft Store でサポートされる BCP-47 言語タグの一覧については、「[サポートされている言語](../../publish/supported-languages.md)」を参照してください。

コードでは、[**ApplicationLanguages.ManifestLanguages**](/uwp/api/windows.globalization.applicationlanguages.ManifestLanguages) プロパティを使用して、読み取り専用の文字列一覧としてアプリ マニフェストの言語の一覧にアクセスできます。この一覧では、各文字列は単一の BCP-47 言語タグです。

```csharp
    IReadOnlyList<string> userLanguages = Windows.Globalization.ApplicationLanguages.ManifestLanguages;
```

## <a name="app-runtime-language-list"></a>アプリの実行時の言語の一覧
関連する 3 つ目の言語の一覧は、前述した 2 つの一覧の共通部分です。 実行時に、アプリでサポートを宣言している言語の一覧 (アプリ マニフェストの言語の一覧) は、ユーザーが基本設定を宣言した言語の一覧 (ユーザー プロファイルの言語の一覧) と比較されます。 アプリの実行時の言語の一覧はこの共通部分に設定されるか (共通部分が空でない場合)、またはアプリの既定の言語に設定されます (共通部分が空である場合)。

具体的には、アプリの実行時の言語の一覧は次の項目で構成されています。

1.  **(オプション) 第 1 言語の上書き**。 [  **PrimaryLanguageOverride**](/uwp/api/Windows.Globalization.ApplicationLanguages.PrimaryLanguageOverride) は、独自の独立した言語選択をユーザーに提示するアプリや、既定の言語選択を無効にしなければならない重大な理由があるアプリで利用できる、シンプルな上書き設定です。 詳細については、「[アプリ リソースとローカライズのサンプルに関するページ](https://go.microsoft.com/fwlink/p/?linkid=231501)」を参照してください。
2.  **アプリでサポートされるユーザーの言語**。 これは、アプリ マニフェストの言語の一覧でフィルター処理されたユーザー プロファイルの言語の一覧です。 アプリでサポートされる言語でユーザーの言語をフィルター処理することで、ソフトウェア開発キット (SDK)、クラス ライブラリ、依存性のあるフレームワーク パッケージ、そのアプリの間で一貫性が保たれます。
3.  **1 と 2 が空の場合、アプリでサポートされる既定または最初の言語**。 ユーザー プロファイルの言語の一覧に、アプリでサポートされる言語が含まれない場合は、アプリで最優先にサポートされる言語がアプリの実行時の言語として選ばれます。

コードでは、[ResourceContext.QualifierValues](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.QualifierValues) プロパティを使用して、BCP-47 言語タグのセミコロンで区切られた一覧を含む文字列の形式でアプリの実行時の言語の一覧にアクセスできます。

```csharp
    string runtimeLanguages = Windows.ApplicationModel.Resources.Core.ResourceContext.GetForCurrentView().QualifierValues["Language"];
```

文字列の読み取り専用の一覧としてアクセスすることもできます。各文字列には単一の BCP-47 言語タグが含まれます。 [  **ResourceContext.Languages**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.Languages) プロパティまたは [**ApplicationLanguages.Languages**](/uwp/api/windows.globalization.applicationlanguages.Languages) プロパティを使用してこれを行うことができます。

```csharp
    IReadOnlyList<string> runtimeLanguages = Windows.ApplicationModel.Resources.Core.ResourceContext.GetForCurrentView().Languages;

    runtimeLanguages = Windows.Globalization.ApplicationLanguages.Languages;
```

アプリのランタイムの言語の一覧により、Windows がアプリ用に読み込むリソースが決定されます。また、日付、時刻、数値、他のコンポーネントの書式設定に使われる言語が決定されます。 「[日付、時刻、数値の形式のグローバル化](use-global-ready-formats.md)」を参照してください。

**注** ユーザー プロファイルの言語とアプリ マニフェストの言語が互いの地域バリアントである場合、ユーザーの地域バリアントがアプリの実行時の言語として使用されます。 たとえば、ユーザーが en-GB を選んだがアプリでは en-US がサポートされるという場合、アプリの実行時の言語は en-GB になります。 この結果、日付、時刻、数値の形式はユーザーの期待 (en-GB) により近いものとなりますが、(言語の対応付けにより) ローカライズ リソースはアプリのサポート言語 (en-US) で読み込まれます。

## <a name="qualify-resource-files-with-their-language"></a>ユーザーの言語によるリソース ファイルの修飾
言語リソース修飾子でリソース ファイルまたはそのフォルダーに名前を付けます。 リソース修飾子の詳細については、「[言語、スケール、ハイ コントラスト、その他の修飾子用にリソースを調整する](../../app-resources/tailor-resources-lang-scale-contrast.md)」を参照してください)。 リソース ファイルは、イメージ (またはその他の資産) を指定できますか、または、リソース コンテナー ファイルをなどあることができます、 *.resw*テキスト文字列を格納しています。

**注**アプリの既定の言語であってもリソースは、language 修飾子を指定する必要があります。 たとえば、アプリの既定の言語が英語 (米国) の場合は、修飾として資産`\Assets\Images\en-US\logo.png`します。

- Windows では、EN-US、EN-GB などの地域のバリアントを含む複雑な一致を実行します。 適切なリージョンのサブ タグが含まれます。 「[リソース管理システムでの言語タグの照合の仕組み](../../app-resources/how-rms-matches-lang-tags.md)」を参照してください。
- 言語の定義を抑制するスクリプトの値がない場合は、修飾子で言語スクリプトのサブ タグを指定します。 たとえば、ZH-CN、ZH-TW ではなく使用 Zh-hant、zh-tw が Hant-ありますまたは Zh-hans (詳細については、次を参照してください。、 [IANA 言語サブタグ レジストリ](https://go.microsoft.com/fwlink/p/?linkid=227303))。
- 1 つの標準言語がある言語では、リージョンの修飾子を含める必要はありません。 たとえば、JA-JP ではなく、ja を使用します。
- 一部のツールやその他のコンポーネント (機械翻訳など) では、データの理解に役立つ地域言語情報など特定の言語タグを探す場合があります。

### <a name="not-all-resources-need-to-be-localized"></a>すべてのリソースをローカライズする必要があります。

ローカライズしないすべてのリソースに必要な場合があります。

- 少なくとも既定の言語ですべてのリソースの存在を確認します。
- 一部のリソースのサブセットが密接に関連する言語 (部分的なローカライズ) で十分です。 たとえば、アプリの完全なリソースのセットがスペイン語で用意されている場合、アプリの UI でカタルニア語にローカライズされていないものがある可能性があります。 カタルニア語とし、スペイン語を話すユーザー用カタルニア語では使用できないリソースがスペイン語で表示されます。
- 一部のリソースは、特定の言語では、ほとんどの一般的なリソースへの他のリソース マップの中に例外を必要があります。 この場合、未確定の言語タグ 'und' を持つすべての言語で使用するためのリソースをマークします。 Windows がワイルドカードとして 'und' 言語タグを解釈 (のような '\*')、その他の特定の一致の後に最上位のアプリの言語と一致するのです。 たとえば、いくつかのリソース (要素の幅など) がフィンランド語では異なっていて、残りのリソースはすべての言語で同じであれば、フィンランド語のリソースはフィンランド語の言語タグでマークし、残りは 'und' でマークする必要があります。
- フォントまたはテキストの高さなどの言語スクリプトに基づいてリソースが指定されたスクリプトを使用して、未確定の言語タグを使用します。 ' und -&lt;スクリプト&gt;'。 たとえば、ラテン語フォントの場合は `und-Latn\\fonts.css` を使い、キリル語フォントの場合は `und-Cryl\\fonts.css` を使います。

## <a name="set-the-http-accept-language-request-header"></a>HTTP Accept-Language 要求ヘッダーの設定
呼び出す Web サービスがアプリと同じ程度ローカライズされているかどうかを検討します。 通常の Web 要求と XMLHttpRequest (XHR) で UWP アプリとデスクトップ アプリから行われた HTTP 要求では、標準の HTTP Accept-Language 要求ヘッダーが使われます。 既定では、HTTP ヘッダーは、ユーザー プロファイルの言語の一覧に設定されます。 この一覧内の各言語は、言語と重み付け (q) のニュートラルを含むようにさらに拡張されます。 たとえば、fr-FR と en-US のユーザーの言語一覧では、HTTP Accept-Language 要求ヘッダーは "fr-FR, fr, en-US, en ("fr-FR,fr;q=0.8,en-US;q=0.5,en;q=0.3")" となります。 ただし、たとえば天気予報アプリで UI がフランス語 (フランス) で表示されていて、ユーザーの優先順位一覧の中で最上位にリストされている言語がドイツ語の場合、アプリ内で整合性を維持するために、サービスからフランス語 (フランス) を明示的に要求する必要があります。

## <a name="apis-in-the-windowsglobalization-namespace"></a>Windows.Globalization 名前空間の API
通常、[**Windows.Globalization**](/uwp/api/windows.globalization?branch=live) 名前空間の API は、アプリの実行時の言語の一覧を使って言語を判断します。 どの言語にも対応する形式が存在しない場合は、ユーザー ロケールが使われます。 これはシステム クロックに使われているものと同じロケールです。 ユーザー ロケールは**設定** > **時刻と言語** > **地域と言語** >  **追加の日付、時刻、および地域の設定** > **リージョン。日付、時刻、または数値の形式を変更する**します。 **Windows.Globalization** API には、アプリの実行時の言語の一覧の代わりに使う言語の一覧を指定するための上書きもあります。

[  **Language**](/uwp/api/windows.globalization.language?branch=live) クラスを使うと、言語のスクリプト、表示名、本来の名称などの、特定の言語についての詳細も調べることができます。

## <a name="use-geographic-region-when-appropriate"></a>必要に応じて、地理的な地域を使う
**[設定]** > **[時刻と言語]** > **[地域と言語]** > **[国/地域]** で、自分の地域として世界中の場所を指定できます。 ユーザーに表示するコンテンツの選択方法として、言語ではなく、この設定を使うことができます。 たとえば、ニュース アプリは、既定では、この地域のコンテンツを表示します。

コードでは、[**GlobalizationPreferences.HomeGeographicRegion**](/uwp/api/windows.system.userprofile.globalizationpreferences.HomeGeographicRegion) プロパティを使ってこの設定にアクセスできます。

[  **GeographicRegion**](/uwp/api/windows.globalization.geographicregion?branch=live) クラスを使うと、地域の表示名、本来の名称、使用通貨などの、特定地域についての詳細を調べることができます

## <a name="examples"></a>例
次の表は、言語と地域の各設定によってアプリの UI に表示されるものの例を示しています。

<table border="1">
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">アプリ マニフェストの言語の一覧</th>
<th align="left">ユーザー プロファイルの言語の一覧</th>
<th align="left">アプリの第 1 言語の上書き (オプション)</th>
<th align="left">アプリの実行時の言語の一覧</th>
<th align="left">アプリでユーザーに表示されるもの</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">英語 (英国) (既定)、ドイツ語 (ドイツ)</td>
<td align="left">英語 (英国)</td>
<td align="left">なし</td>
<td align="left">英語 (英国)</td>
<td align="left">UI の場合:英語 (英国)<br>日付/時間/数字:英語 (英国)</td>
</tr>
<tr>
<td align="left">ドイツ語 (ドイツ) (既定)、フランス語 (フランス)、イタリア語 (イタリア)</td>
<td align="left">フランス語 (オーストリア)</td>
<td align="left">なし</td>
<td align="left">フランス語 (オーストリア)</td>
<td align="left">UI の場合:フランス語 (フランス) (フランス語 (オーストリア) からフォールバック)<br>日付/時間/数字:フランス語 (オーストリア)</td>
</tr>
<tr>
<td align="left">英語 (米国) (既定)、フランス語 (フランス)、英語 (英国)</td>
<td align="left">英語 (カナダ)、フランス語 (カナダ)</td>
<td align="left">なし</td>
<td align="left">英語 (カナダ)、フランス語 (カナダ)</td>
<td align="left">UI の場合:英語 (米国) (英語 (カナダ) からフォールバック)<br>日付/時間/数字:英語 (カナダ)</td>
</tr>
<tr>
<td align="left">スペイン語 (スペイン) (既定)、スペイン語 (メキシコ)、スペイン語 (ラテン アメリカ)、ポルトガル語 (ブラジル)</td>
<td align="left">英語 (米国)</td>
<td align="left">なし</td>
<td align="left">スペイン語 (スペイン)</td>
<td align="left">UI の場合:スペイン語 (スペイン) (英語の使用可能なフォールバックなしから既定を使用)<br>日付/時刻/数値: スペイン語 (スペイン)</td>
</tr>
<tr>
<td align="left">カタルニア語 (既定)、スペイン語 (スペイン)、フランス語 (フランス)</td>
<td align="left">カタルニア語、フランス語 (フランス)</td>
<td align="left">なし</td>
<td align="left">カタルニア語、フランス語 (フランス)</td>
<td align="left">UI の場合:カタルニア語といくつかのフランス語 (フランス) ほとんどの場合、すべての文字列がカタルニア語では<br>日付/時間/数字:カタルニア語</td>
</tr>
<tr>
<td align="left">英語 (英国) (既定)、フランス語 (フランス)、ドイツ語 (ドイツ)</td>
<td align="left">ドイツ語 (ドイツ)、英語 (英国)</td>
<td align="left">英語 (英国) (アプリの UI でユーザーによって選ばれる)</td>
<td align="left">英語 (英国)、ドイツ語 (ドイツ)</td>
<td align="left">UI の場合:英語 (GB) (言語の上書き)<br>日付/時刻/数値: 英語 (英国)</td>
</tr>
</tbody>
</table>

>[!NOTE]
> Microsoft で使用される標準の国/地域コードの一覧は、次を参照してください。、[公式の国/地域一覧](https://globalready.azurewebsites.net/marketreadiness/OfficialCountryregion)します。

## <a name="important-apis"></a>重要な API
* [GlobalizationPreferences.Languages](/uwp/api/windows.system.userprofile.globalizationpreferences.Languages)
* [ApplicationLanguages.ManifestLanguages](/uwp/api/windows.globalization.applicationlanguages.ManifestLanguages)
* [PrimaryLanguageOverride](/uwp/api/Windows.Globalization.ApplicationLanguages.PrimaryLanguageOverride)
* [ResourceContext.QualifierValues](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.QualifierValues)
* [ResourceContext.Languages](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.Languages)
* [ApplicationLanguages.Languages](/uwp/api/windows.globalization.applicationlanguages.Languages)
* [Windows.Globalization](/uwp/api/windows.globalization?branch=live)
* [言語](/uwp/api/windows.globalization.language?branch=live)
* [GlobalizationPreferences.HomeGeographicRegion](/uwp/api/windows.system.userprofile.globalizationpreferences.HomeGeographicRegion)
* [GeographicRegion](/uwp/api/windows.globalization.geographicregion?branch=live)

## <a name="related-topics"></a>関連トピック
* [Bcp-47 言語タグ](https://go.microsoft.com/fwlink/p/?linkid=227302)
* [IANA 言語サブタグ レジストリ](https://go.microsoft.com/fwlink/p/?linkid=227303)
* [言語、スケール、ハイ コントラスト、その他の修飾子用にリソースを調整する](../../app-resources/tailor-resources-lang-scale-contrast.md)
* [サポートされている言語](../../publish/supported-languages.md)
* [日付/時間/数字形式をグローバル化します。](use-global-ready-formats.md)
* [リソース管理システムでの言語タグの照合の仕組み](../../app-resources/how-rms-matches-lang-tags.md)

## <a name="samples"></a>サンプル
* [アプリケーション リソースとローカリゼーション サンプル](https://go.microsoft.com/fwlink/p/?linkid=231501)
