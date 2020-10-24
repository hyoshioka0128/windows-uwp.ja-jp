---
description: このトピックでは、修飾子の一般概念、使用方法、各修飾子名の目的について説明します。
title: 言語、スケール、ハイ コントラスト、その他の修飾子用にリソースを調整する
template: detail.hbs
ms.date: 10/10/2017
ms.topic: article
keywords: Windows 10, UWP, リソース, 画像, アセット, MRT, 修飾子
ms.localizationpriority: medium
ms.openlocfilehash: 59f0b636384ba133e985f0704e2033c1acc5f15e
ms.sourcegitcommit: efa5f793607481dcae24cd1b886886a549e8d6e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412016"
---
# <a name="tailor-your-resources-for-language-scale-high-contrast-and-other-qualifiers"></a>言語、スケール、ハイ コントラスト、その他の修飾子用にリソースを調整する

このトピックでは、リソース修飾子の一般概念、使用方法、各修飾子名の目的について説明します。 すべての使用可能な修飾子値の参照テーブルについては、「 [**QualifierValues**](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.QualifierValues) 」を参照してください。

アプリでは、表示言語、ハイ コントラスト設定、[表示倍率](../design/layout/screen-sizes-and-breakpoints-for-responsive-design.md#effective-pixels-and-scale-factor)などのランタイム コンテキストに合わせて調整されたアセットやリソースを読み込むことができます。 これを行うには、リソースのフォルダーまたはファイルの名前を、これらのコンテキストに対応した修飾子の名前と値に一致させます。 たとえば、ハイ コントラスト モードでは別のセットのイメージ アセットをアプリに読み込む、ということもできます。

アプリのローカライズの価値提案の詳細については、「[グローバリゼーションとローカライズ](../design/globalizing/globalizing-portal.md)」をご覧ください。

## <a name="qualifier-name-qualifier-value-and-qualifier"></a>修飾子名、修飾子の値、修飾子

修飾子名は、一連の修飾子の値にマップされるキーです。 修飾子の名前と修飾子の値を次に示します。

| Context | 修飾子名 | 修飾子の値 |
| :--------------- | :--------------- | :--------------- |
| ハイ コントラスト設定 | contrast | standard、high、black、white |

修飾子は、修飾子名と修飾子の値を組み合わせて作成します。 `<qualifier name>-<qualifier value>` 修飾子の形式を指定します。 `contrast-standard` 修飾子の例を次に示します。

ハイ コントラストの場合、修飾子のセットは `contrast-standard`、`contrast-high`、`contrast-black`、`contrast-white` になります。 修飾子名と修飾子の値では、大文字と小文字が区別されません。 たとえば、`contrast-standard` と `Contrast-Standard` は同じ修飾子であると見なされます。

## <a name="use-qualifiers-in-folder-names"></a>修飾子をフォルダー名に使用する

アセット ファイルが含まれるフォルダーに、修飾子を使用して名前を付ける例を次に示します。 修飾子ごとに複数のアセット ファイルがある場合は、フォルダー名に修飾子を使用します。 これにより、フォルダー レベルで一度だけ修飾子を設定すると、この修飾子がフォルダー内のすべての項目に適用されます。

```console
\Assets\Images\contrast-standard\<logo.png, and other image files>
\Assets\Images\contrast-high\<logo.png, and other image files>
\Assets\Images\contrast-black\<logo.png, and other image files>
\Assets\Images\contrast-white\<logo.png, and other image files>
```

上の例のようにフォルダーの名前を付けた場合、アプリはハイ コントラスト設定を使用して、適切な修飾子名が適用されたフォルダーからリソース ファイルを読み込みます。 このため、設定が [ハイ コントラスト 黒] であれば、`\Assets\Images\contrast-black` フォルダー内のリソース ファイルが読み込まれます。 設定が [なし] (コンピューターがハイ コントラスト モードではない) の場合は、`\Assets\Images\contrast-standard` フォルダー内のリソース ファイルが読み込まれます。

## <a name="use-qualifiers-in-file-names"></a>修飾子をファイル名に使用する

フォルダーを作成して名前を付ける代わりに、修飾子を使用してリソース ファイル自体の名前を付けることもできます。 1 つの修飾子につきリソース ファイルが 1 つのみの場合は、この方法が適しています。 次に例を示します。

```console
\Assets\Images\logo.contrast-standard.png
\Assets\Images\logo.contrast-high.png
\Assets\Images\logo.contrast-black.png
\Assets\Images\logo.contrast-white.png
```

読み込まれるのは、設定に最も適した修飾子を含む名前のファイルです。 ファイル名についても、フォルダー名と同様の照合ロジックが使用されます。

## <a name="reference-a-string-or-image-resource-by-name"></a>文字列または画像リソースを名前で参照する

「[XAML マークアップから文字列リソース識別子を参照する](localize-strings-ui-manifest.md#refer-to-a-string-resource-identifier-from-xaml)」、「[コードから文字列リソース識別子を参照する](localize-strings-ui-manifest.md#refer-to-a-string-resource-identifier-from-code)」、「[XAML マークアップとコードから画像やその他のアセットを参照する](images-tailored-for-scale-theme-contrast.md#reference-an-image-or-other-asset-from-xaml-markup-and-code)」をご覧ください。

## <a name="actual-and-neutral-qualifier-matches"></a>修飾子の実際の一致と中立的な一致
修飾子の値の*すべて*にリソース ファイルを指定する必要はありません。 たとえば、ハイ コントラスト用と標準コントラスト用にビジュアル アセットを各 1 つのみ必要とする場合は、これらのアセット名を次のように付けることができます。

```console
\Assets\Images\logo.contrast-high.png
\Assets\Images\logo.png
```

最初のファイル名には、`contrast-high` 修飾子が含まれています。 ハイ コントラストが *[オン]* になっている場合、この修飾子は、あらゆるハイ コントラスト設定に対する*実際の*一致です。 言い換えると、これは近似一致であり、優先されます。 この場合のように、*実際*の一致は、修飾子に*実際*の値が含まれている場合にのみ発生します。 この場合、`high` が `contrast` に対する*実際*の値です。

`logo.png` というファイル名には、contrast 修飾子がまったく含まれていません。 修飾子がない値は、*中立的*です。 優先される一致が見つからない場合、中立値はフォールバックの一致として使用されます。 この例では、ハイ コントラストが*オフ*になっている場合、実際の一致はありません。 見つかるベスト マッチが*中立的*な一致であるため、`logo.png` というアセットが読み込まれます。

`logo.png` の名前を `logo.contrast-standard.png` に変更すると、ファイル名に実際の修飾子の値が含まれます。 ハイ コントラストがオフになっている場合、`logo.contrast-standard.png` との実際の一致があり、このアセット ファイルが読み込まれます。 このため、別々の一致が原因ですが、同じ条件下で同じファイルが読み込まれます。

必要なアセット セットが、ハイ コントラスト用に 1 つと標準コントラスト用に 1 つのみである場合は、ファイル名の代わりにフォルダー名を使用できます。 この場合、フォルダー名を省略すると、完全に中立的な一致になります。

```console
\Assets\Images\contrast-high\<logo.png, and other images to load when high contrast theme is not None>
\Assets\Images\<logo.png, and other images to load when high contrast theme is None>
```

修飾子の照合について詳しくは、「[リソース管理システム](resource-management-system.md)」を参照してください。

## <a name="multiple-qualifiers"></a>複数の修飾子

修飾子は、フォルダー名とファイル名で組み合わせることができます。 たとえば、ハイ コントラスト モードがオンであり** 表示倍率が 400 のときに、イメージ アセットをアプリに読み込むとします。 これを行う方法の 1 つは、入れ子になったフォルダーの使用です。

```console
\Assets\Images\contrast-high\scale-400\<logo.png, and other image files>
```

`logo.png` およびその他のファイルを読み込むには、設定が*両方*の修飾子と一致する必要があります。

もう 1 つのオプションは、複数の修飾子を結合して 1 つのフォルダー名にすることです。

```console
\Assets\Images\contrast-high_scale-400\<logo.png, and other image files>
```

フォルダー名として、複数の修飾子をアンダー スコアで結合します。 `<qualifier1>[_<qualifier2>...]` の形式はです。

同じ形式で、複数の修飾子を結合して 1 つのファイル名にすることもできます。

```console
\Assets\Images\logo.contrast-high_scale-400.png
```

アセット作成に使用するツールとワークフローや、読みやすさや管理のしやすさによって、すべての修飾子に単一の命名方法を選択することも、修飾子によって異なる方法を組み合わせることもできます。

## <a name="alternateform"></a>AlternateForm

特別な目的でリソースの代替フォームを提供するには、`alternateform` 修飾子を使います。 通常、日本のアプリ開発者によってふりがな文字列を提供する目的のみで使用されます。そのために、`msft-phonetic` という値が予約されています (「[ローカライズの準備をする方法](/previous-versions/windows/apps/hh967762(v=win.10))」の「並べ替えることができる日本語文字列のふりがなのサポート」をご覧ください)。

ターゲット システムとアプリのうちいずれかが、`alternateform` 修飾子と一致する値を提供する必要があります。 カスタムの `alternateform` 修飾子の値に `msft-` プレフィックスを使用しないでください。

## <a name="configuration"></a>構成

`configuration` 修飾子名が必要になる可能性は高くありません。 テストのみのリソースなど、オーサリング時環境にのみ使用されるリソースを指定するために使用できます。

`configuration` 修飾子は、`MS_CONFIGURATION_ATTRIBUTE_VALUE` 環境変数の値と最も一致するリソースを読み込むために使用します。 このため、この変数は、関連するリソースに割り当てられた文字列値 (`designer` や `test` など) に設定することができます。

## <a name="contrast"></a>この例を、

`contrast` 修飾子は、ハイ コントラスト設定と最も一致するリソースを提供するために使用します。

## <a name="custom"></a>Custom

アプリで `custom` 修飾子の値を設定すると、その値に最も一致するリソースが読み込まれます。 たとえば、アプリのライセンスに基づいてリソースを読み込む必要があるとします。 アプリは、起動するとライセンスを確認し、[SetGlobalQualifierValue](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.setglobalqualifiervalue) を呼び出すことによって、ライセンスを `custom` 修飾子の値として使用します。コード例をご覧ください。

```csharp
public void SetLicenseLevel(BrandID brand)
{
    if (brand == BrandID.Premium)
    {
        ResourceContext.SetGlobalQualifierValue("Custom", "Premium", ResourceQualifierPersistence.LocalMachine);
    }
    else if (brand == BrandID.Standard)
    {
        ResourceContext.SetGlobalQualifierValue("Custom", " Standard", ResourceQualifierPersistence.LocalMachine);
    }
    else
    {
        ResourceContext.SetGlobalQualifierValue("Custom", "Trial", ResourceQualifierPersistence.LocalMachine);
    }
}
```

このシナリオでは、修飾子 `custom-premium`、`custom-standard`、および `custom-trial` をそれぞれ含む名前をリソースに適用します。

## <a name="devicefamily"></a>DeviceFamily

`devicefamily` 修飾子名が必要になる可能性は高くありません。 他にもっと便利で強力な修飾子を使う手法があるため、この修飾子名の使用はできる限り避けてください。 このような手法については、「[アプリが実行されているプラットフォームの検出](../porting/wpsl-to-uwp-input-and-sensors.md#detecting-the-platform-your-app-is-running-on)」および「[バージョン アダプティブ コード](../debug-test-perf/version-adaptive-code.md)」を参照してください。

ただし他に方法がなければ、XAML ビュー (XAML ビューは、UI レイアウトとコントロールを含む XAML ファイル) を格納するフォルダーの名前として devicefamily という修飾子を使用することもできます。

```console
\devicefamily-desktop\<MainPage.xaml, and other markup files to load when running on a desktop computer>
\devicefamily-mobile\<MainPage.xaml, and other markup files to load when running on a phone>
```

または、次のようにファイルに命名することもできます。

```console
\MainPage.devicefamily-desktop.xaml
\MainPage.devicefamily-mobile.xaml
```

いずれの場合も、`MainPage.[<qualifier>].xaml` の各コピーで、共通の `MainPage.xaml.cs` が使用されます (プロジェクト内で名前、場所、コンテンツが変わりません)。

また、devicefamily 修飾子を使用してリソース ファイル (`.resw`) またはフォルダーに名前を付けることもできます。 たとえば、モバイル デバイス ファミリでアプリが実行されている場合、UI 要素 `<TextBlock x:Uid="DeviceFriendlyName"/>` では、`Resources.devicefamily-mobile.resw` ファイルに定義されているテキストと前景リソースが使用されます。以下はその例です。

```xml
<data name="DeviceFriendlyName.Foreground">
    <value>Red</value>
</data>
<data name="DeviceFriendlyName.Text">
    <value>Mobile device</value>
</data>
```

リソース ファイルの使用について詳しくは、[UI 文字列のローカライズ](localize-strings-ui-manifest.md)に関するページをご覧ください。

## <a name="dxfeaturelevel"></a>DXFeatureLevel

`dxfeaturelevel` 修飾子名が必要になる可能性は高くありません。 これは Direct3D ゲーム アセットで使用し、以前の特定な下位レベル ハードウェア構成に一致するように、下位レベルのリソースを読み込むために用意されたものです。 ただ、このハードウェア構成はあまり普及していないため、この修飾子は使用しないことをお勧めします。

## <a name="homeregion"></a>HomeRegion

`homeregion` 修飾子は、国または地域のユーザー設定に対応します。 ユーザーが住んでいる地域の場所を表します。 値には、有効な [BCP-47 region タグ](https://tools.ietf.org/html/bcp47)が含まれます。 つまり、**ISO 3166-1 alpha-2** の 2 文字の地域番号に、構成地域用の **ISO 3166-1 numeric** の 3 桁の地域番号のセットを加えた値となります ([国連統計部 M49 地域番号構成に関するページ](https://unstats.un.org/unsd/methods/m49/m49regin.htm)をご覧ください)。 "Selected economic and other groupings" の番号は有効ではありません。

## <a name="language"></a>Language

`language` 修飾子は、表示言語設定に対応します。 値には、有効な [BCP 47 language タグ](https://tools.ietf.org/html/bcp47)が含まれます。 言語の一覧については、[IANA 言語サブタグ レジストリに関するページ](https://www.iana.org/assignments/language-subtag-registry)をご覧ください。

アプリで複数の表示言語をサポートする必要があり、コードまたは XAML マークアップ内に文字列リテラルが含まれている場合は、その文字列をコードまたはマークアップからリソース ファイル (`.resw`) に移動します。 アプリでサポートする各言語用に、このリソース ファイルを翻訳したコピーを作成することができます。

`language` 修飾子は通常、リソース ファイル (`.resw`) が含まれているフォルダーの命名に使用します。

```console
\Strings\language-en\Resources.resw
\Strings\language-ja\Resources.resw
```

`language` 修飾子の `language-` の部分 (修飾子名) は省略することができます。 これは他の種類の修飾子には適用されません。また、適用できるのはフォルダー名の場合のみです。

```console
\Strings\en\Resources.resw
\Strings\ja\Resources.resw
```

フォルダーに名前を付ける代わりに、`language` 修飾子を使用してリソース ファイル自体の名前を付けることもできます。

```console
\Strings\Resources.language-en.resw
\Strings\Resources.language-ja.resw
```

文字列リソースを使用してアプリをローカライズ可能にする方法と、アプリ内で文字列リソースを参照する方法について詳しくは、[UI 文字列のローカライズに関するページ](localize-strings-ui-manifest.md)をご覧ください。

## <a name="layoutdirection"></a>LayoutDirection

`layoutdirection` 修飾子は、表示言語設定のレイアウト方向に対応します。 たとえば、アラビア語やヘブライ語などの右から左に記述する言語では、イメージの反転が必要になる場合があります。 UI のレイアウト パネルとイメージは、[FlowDirection](/uwp/api/Windows.UI.Xaml.FrameworkElement.FlowDirection) プロパティを設定すると、レイアウト方向が正しく反映されます (「[レイアウトやフォントの調整と RTL のサポート](../design/globalizing/adjust-layout-and-fonts--and-support-rtl.md)」をご覧ください)。 `layoutdirection` 修飾子は、単純な反転だけでは十分でないケースを想定し、特定の読み取り順序の辞書やテキスト配置にも、より一般的な方法で対応することができます。

## <a name="scale"></a>スケール

Windows では、ディスプレイの DPI (1 インチあたりのドット数) と、デバイスの視聴距離に基づいて各ディスプレイの倍率が自動的に選択されます。 「[有効ピクセルと倍率](../design/layout/screen-sizes-and-breakpoints-for-responsive-design.md#effective-pixels-and-scale-factor)」をご覧ください。 Windows で最適なサイズを選択したり、最も近いサイズを使用して拡大または縮小したりできるように、いくつかの推奨されるサイズ (少なくとも、100、200、400) で画像を作成する必要があります。 Windows で表示倍率に対して正確なサイズの画像を含む物理ファイルを識別できるように、`scale` 修飾子を使用します。 リソースのスケールは、[DisplayInformation.ResolutionScale](/uwp/api/windows.graphics.display.displayinformation.ResolutionScale) の値、または次に大きい拡大リソースに一致します。

フォルダー レベルで修飾子を設定する例を次に示します。

```console
\Assets\Images\scale-100\<logo.png, and other image files>
\Assets\Images\scale-200\<logo.png, and other image files>
\Assets\Images\scale-400\<logo.png, and other image files>
```

この例では、ファイル レベルで修飾子を設定します。

```console
\Assets\Images\logo.scale-100.png
\Assets\Images\logo.scale-200.png
\Assets\Images\logo.scale-400.png
```

`scale` と `targetsize` でリソースを修飾する方法については、「[targetsize で画像リソースを修飾する](images-tailored-for-scale-theme-contrast.md#qualify-an-image-resource-for-targetsize)」をご覧ください。

## <a name="targetsize"></a>TargetSize

`targetsize` 修飾子は主に、エクスプローラーに表示される[ファイルの種類の関連付け](/windows/desktop/shell/how-to-assign-a-custom-icon-to-a-file-type)アイコンまたは[プロトコル アイコン](/windows/desktop/search/-search-3x-wds-ph-ui-extensions)の指定に使用されます。 この修飾子の値は、正方形のイメージの辺の長さを RAW (物理) ピクセル単位で表します。 エクスプローラーの表示設定に値が一致するリソースが読み込まれます。正確に一致する対象が存在しない場合は、次に大きな値のリソースが読み込まれます。

アプリ パッケージ マニフェスト デザイナーの [ビジュアル資産] タブで、複数サイズのアプリ アイコン (`/Assets/Square44x44Logo.png`) に対応する `targetsize` 修飾子の値を表すアセットを定義できます。

`scale` と `targetsize` でリソースを修飾する方法については、「[targetsize で画像リソースを修飾する](images-tailored-for-scale-theme-contrast.md#qualify-an-image-resource-for-targetsize)」をご覧ください。

## <a name="theme"></a>テーマ

`theme` 修飾子は、既定のアプリ モード設定に最も一致するリソースか、[Application.RequestedTheme](/uwp/api/windows.ui.xaml.application.requestedtheme) を使用してアプリのオーバーライドを提供するために使用されます。


## <a name="shell-light-theme-and-unplated-resources"></a>シェルライトテーマとプレートなしリソース
*Windows 10 2019 年5月の更新プログラム*では、windows シェルの新しい "ライト" テーマが導入されました。 その結果、以前は暗い背景に表示されていた一部のアプリケーションアセットが明るい背景に表示されるようになりました。 タスクバーとウィンドウにプレートなしアセットを提供したアプリ (Alt + Tab、タスクビューなど) では、明るい背景で使用できるコントラストがあるかどうかを確認する必要があります。

### <a name="providing-light-theme-specific-assets"></a>ライトテーマ固有のアセットを提供する
シェルライトテーマ用に調整されたリソースを提供するアプリでは、新しい代替フォームリソース修飾子であるを使用できます。 `altform-lightunplated` この修飾子は、既存の altform-プレートなし修飾子を反映します。 

### <a name="downlevel-considerations"></a>ダウンレベルの考慮事項
アプリでは、修飾子で修飾子を使用しないでください `theme-light` `altform-unplated` 。 これにより、タスクバーのリソースが読み込まれる方法によって、RS5 以前のバージョンの Windows で予期しない動作が発生します。 以前のバージョンの windows では、テーマライトのバージョンが正しく使用されない場合があります。 `altform-lightunplated`この修飾子は、この問題を回避します。 

### <a name="compatibility-behavior"></a>互換性の動作
旧バージョンとの互換性を維持するために、Windows には、モノクロのアイコンを検出し、意図した背景と比較するかどうかを確認するロジックが含まれています。 アイコンがコントラストの要件を満たすことができない場合、Windows は、コントラストが白のアセットを検索します。 使用できない場合は、plated バージョンの資産を使用するように Windows が切り替えられます。



## <a name="important-apis"></a>重要な API

* [ResourceContext.QualifierValues](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.QualifierValues)
* [SetGlobalQualifierValue](/uwp/api/windows.applicationmodel.resources.core.resourcecontext.setglobalqualifiervalue)

## <a name="related-topics"></a>関連トピック

* [有効ピクセルと倍率](../design/layout/screen-sizes-and-breakpoints-for-responsive-design.md#effective-pixels-and-scale-factor)
* [リソース管理システム](resource-management-system.md)
* [ローカライズの準備をする方法](/previous-versions/windows/apps/hh967762(v=win.10))
* [アプリが実行されているプラットフォームの検出](../porting/wpsl-to-uwp-input-and-sensors.md#detecting-the-platform-your-app-is-running-on)
* [拡張機能 Sdk を使用したプログラミング](/uwp/extension-sdks/device-families-overview)
* [UI 文字列のローカライズ](localize-strings-ui-manifest.md)
* [BCP-47](https://tools.ietf.org/html/bcp47)
* [国連統計部 M49 地域番号構成](https://unstats.un.org/unsd/methods/m49/m49regin.htm)
* [IANA 言語サブタグ レジストリ](https://www.iana.org/assignments/language-subtag-registry)
* [レイアウトやフォントの調整と RTL のサポート](../design/globalizing/adjust-layout-and-fonts--and-support-rtl.md)