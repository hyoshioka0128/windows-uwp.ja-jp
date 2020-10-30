---
description: カスタムテンプレートおよびパターンと共に Windows.globalization.datetimeformatting API を使用して、目的の形式で日付と時刻を表示します。
title: パターンを使った日付と時刻の書式設定
ms.assetid: 012028B3-9DA2-4E72-8C0E-3E06BEC3B3FE
label: Use patterns to format dates and times
template: detail.hbs
ms.date: 11/09/2017
ms.topic: article
keywords: Windows 10, UWP, グローバリゼーション, ローカライズの可否, ローカライズ
ms.localizationpriority: medium
ms.openlocfilehash: dbabbcaccd88b187a03c83909bcb38d5f64b30bb
ms.sourcegitcommit: a3bbd3dd13be5d2f8a2793717adf4276840ee17d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93034315"
---
# <a name="use-templates-and-patterns-to-format-dates-and-times"></a>テンプレートとパターンを使った日付と時刻の書式設定

[**Windows.Globalization.DateTimeFormatting**](/uwp/api/windows.globalization.datetimeformatting?branch=live) 名前空間のクラスでカスタムのテンプレートとパターンを使うと、日付と時刻を好みの形式で表示できます。

## <a name="introduction"></a>はじめに

[**DateTimeFormatter**](/uwp/api/windows.globalization.datetimeformatting?branch=live) クラスでは、世界中の言語と地域に対応するように、日付と時刻をさまざまな方法で適切に書式設定できます。 年、月、日などについて標準形式を使うことができます。 または、"longdate" または "month day" のような **DateTimeFormatter** コンストラクターの *formatTemplate* 引数に書式テンプレートを渡すことができます。

ただし、表示する [**DateTime**](/uwp/api/windows.foundation.datetime?branch=live) オブジェクトの構成要素の順序や形式をより細かく制御する場合は、コンストラクターの *formatTemplate* 引数に書式パターンを渡すことができます。 書式パターンでは、特別な構文を使用します。これにより、 **DateTime** オブジェクトの個々のコンポーネントを &mdash; 月の名前のみ、または年の値のみを使用して、 &mdash; 選択した任意のカスタム書式で表示することができます。 さらに、パターンをローカライズして、他の言語や地域に対応させることができます。

**注**  ここで説明しているのは、単なる書式パターンの概要です。 書式テンプレートと書式パターンの詳細については、 [**DateTimeFormatter**](/uwp/api/windows.globalization.datetimeformatting?branch=live) クラスの「解説」セクションを参照してください。

## <a name="the-difference-between-format-templates-and-format-patterns"></a>書式テンプレートと書式パターンの違い

書式テンプレートは、カルチャに依存しない形式の文字列です。 そのため、書式テンプレートを使用して **DateTimeFormatter** を作成する場合、フォーマッタでは現在の言語の正しい順序で書式コンポーネントを表示します。 逆に、書式パターンはカルチャ固有です。 書式パターンを使用して **DateTimeFormatter** 作成している場合、フォーマッタでは与えられたとおりにパターンを使用します。 その結果、パターンは、すべてのカルチャに対して有効であるとは限りません。

例を使用してこの違いを説明しましょう。 単純な書式テンプレート (パターンではない) を **DateTimeFormatter** コンストラクターに渡します。 これは、書式テンプレート "month day" です。

```csharp
var dateFormatter = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("month day");
```

これにより、現在のコンテキストの言語や地域の値に基づいてフォーマッタが作成されます。 書式テンプレート内のコンポーネントの順序は問題になりません。フォーマッタでは、現在の言語の正しい順序でそれらを表示します。 たとえば、英語 (米国) の場合は "January 1"、フランス語 (フランス) の場合は "1 janvier"、日本語の場合は "1 月 1 日" と表示されます。

その一方で、書式パターンはカルチャ固有です。 書式テンプレートの形式パターンにアクセスしてみましょう。

```csharp
IReadOnlyList<string> monthDayPatterns = dateFormatter.Patterns;
```

これにより、実行時の言語と地域に応じて異なる結果が返されます。 さまざまな地域で、順序の違いや文字とスペースの追加の有無など、それぞれ異なるコンポーネントが使われる場合があります。

```syntax
En-US: "{month.full} {day.integer}"
Fr-FR: "{day.integer} {month.full}"
Ja-JP: "{month.integer}月{day.integer}日"
```

上の例では、カルチャに依存しない書式設定文字列を入力し、カルチャ固有の書式設定文字列を再度取得しました (これは、`dateFormatter.Patterns` を呼び出したときに有効であった言語と地域の関数でした)。 要するに、カルチャ固有の書式パターンから **DateTimeFormatter** を作成する場合、特定の言語または地域でのみ有効になります。

```csharp
var dateFormatter = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("{month.full} {day.integer}");
```

上のフォーマッタは、角かっこ内の個々のコンポーネントのカルチャ固有の値を返し {} ます。 ただし、書式パターンのコンポーネントの順序は不変です。 要求どおりのものが得られても、それがカルチャに適している場合と適していない場合があります。 このフォーマッタは英語 (米国) で有効ですが、フランス語 (フランス) または日本語では有効ではありません。

``` syntax
En-US: January 1
Fr-FR: janvier 1 (inappropriate for France; non-standard order)
Ja-JP: 1月1 (inappropriate for Japan; the day symbol 日 is missing)
```

さらに、今日正しいパターンが、将来正しくなくなる可能性があります。 国や地域で暦体系が変更されると、それに伴い書式テンプレートが変わる場合があります。 Windows では、書式テンプレートに基づき、このような変更に合わせてフォーマッタの出力を更新します。 そのため、これらの 1 つ以上の条件下でのみパターン構文を使用する必要があります。

-   書式設定の特定の出力に依存していない。
-   カルチャ固有の標準に従うための書式設定を必要としない。
-   すべてのカルチャにわたってパターンが不変であることを特に意図している。
-   実際の書式パターンの文字列自体をローカライズすることを意図している。

書式テンプレートと書式パターンの違いを、以下に簡単にまとめます。

**"month day" などの書式テンプレート**

-   月や日などの値を任意の順序で含む [DateTime](/uwp/api/windows.foundation.datetime?branch=live) 形式の抽象化された表現です。
-   Windows でサポートされているすべての言語と地域にわたって有効な標準の形式を必ず返します。
-   特定の言語と地域のカルチャに適するように書式設定された文字列を必ず提供します。
-   コンポーネントのすべての組み合わせが有効であるとは限りません。 たとえば、"dayofweek day" は正しくありません。

**"{month.full} {day.integer}" などの書式パターン**

-   月の完全な名前の後にスペースが挿入され、その後に日付の整数が続く、特定の順序、または指定した特定の書式パターンの明示的に指定された文字列です。
-   任意の言語と地域のペアについて有効な標準の形式に対応しない場合があります。
-   カルチャに適するとは限りません。
-   任意の順序のコンポーネントのあらゆる組み合わせを指定できます。

## <a name="examples"></a>例

現在の月と日を特定の形式で現在時刻と一緒に表示するとします。 たとえば、米国英語のユーザーに次のように表示する必要があるとします。

``` syntax
June 25 | 1:38 PM
```

日付の部分は "month day" 書式テンプレートに対応し、時刻の部分は "hour minute" 書式テンプレートに対応します。 そのため、関連する日付と時刻の書式テンプレートのフォーマッタを構築してから、ローカライズ可能な書式指定文字列を使用して、出力を連結することができます。

```csharp
var dateToFormat = System.DateTime.Now;
var resourceLoader = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView();

var dateFormatter = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("month day");
var timeFormatter = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("hour minute");

var date = dateFormatter.Format(dateToFormat);
var time = timeFormatter.Format(dateToFormat);

string output = string.Format(resourceLoader.GetString("CustomDateTimeFormatString"), date, time);
```

`CustomDateTimeFormatString` リソースファイル (resw) 内のローカライズ可能なリソースを参照するリソース識別子です。 既定の言語 (米国) の場合、この値は "|" に設定され、"" {0} {1} が日付であること {0} と "" が時刻であることを示すコメントと共に設定され {1} ます。 このようにして、翻訳者は必要に応じて書式項目を調整できます。 たとえば、時刻を日付より前に配置する方が一部の言語や地域では自然であると思われる場合は、項目の順序を変更できます。 また、"|" を別の区切り文字に置き換えることもできます。

また、この例を実装する別の方法として、2 つのフォーマッタを照会して書式パターンを検索し、それらの書式パターンを連結して、結果として生成される書式パターンから 3 つ目のフォーマッタを構築することができます。

```csharp
var resourceLoader = Windows.ApplicationModel.Resources.ResourceLoader.GetForCurrentView();

var dateFormatter = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("month day");
var timeFormatter = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter("hour minute");

string dateFormatterPattern = dateFormatter.Patterns[0];
string timeFormatterPattern = timeFormatter.Patterns[0];

string pattern = string.Format(resourceLoader.GetString("CustomDateTimeFormatString"), dateFormatterPattern, timeFormatterPattern);

var patternFormatter = new Windows.Globalization.DateTimeFormatting.DateTimeFormatter(pattern);

string output = patternFormatter.Format(System.DateTime.Now);
```

## <a name="important-apis"></a>重要な API

* [Windows.Globalization.DateTimeFormatting](/uwp/api/windows.globalization.datetimeformatting?branch=live)
* [DateTimeFormatter](/uwp/api/windows.globalization.datetimeformatting?branch=live)
* [DateTime](/uwp/api/windows.foundation.datetime?branch=live)

## <a name="related-topics"></a>関連トピック

* [日付と時刻の書式設定のサンプル](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Windows%208%20app%20samples/%5BC%23%5D-Windows%208%20app%20samples/C%23/Windows%208%20app%20samples/Date%20and%20time%20formatting%20sample%20(Windows%208))
