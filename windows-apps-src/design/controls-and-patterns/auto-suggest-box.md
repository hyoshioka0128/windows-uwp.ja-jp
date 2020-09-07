---
title: 自動提案ボックスのガイドライン
description: AutoSuggestBox を使用して、入力しながら選択できる候補リストをユーザーに表示する方法について説明します。
ms.assetid: 1F608477-F795-4F33-92FA-F200CC243B6B
dev.assetid: 54F8DB8A-120A-4D79-8B5A-9315A3764C2F
label: Auto-suggest box
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: miguelrb
design-contact: ksulliv
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 6eaa57aa5e3ae9d60a9c199c8011da95cd7147e2
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89160662"
---
# <a name="auto-suggest-box"></a>自動提案ボックス

AutoSuggestBox を使って、ユーザーが入力と同時に選べる候補リストを表示します。

![自動提案ボックス](images/controls_autosuggest_expanded01.png)

**Windows UI ライブラリを入手する**

|  |  |
| - | - |
| ![WinUI ロゴ](images/winui-logo-64x64.png) | Windows UI ライブラリ 2.2 以降には、丸めた角を使用するこのコントロールの新しいテンプレートが含まれます。 詳しくは、「[角の半径](../style/rounded-corner.md)」をご覧ください。 WinUI は、Windows アプリの新しいコントロールと UI 機能が含まれる NuGet パッケージです。 インストール手順などについて詳しくは、「[Windows UI Library (Windows UI ライブラリ)](/uwp/toolkits/winui/)」をご覧ください。 |

> **プラットフォーム API**: [AutoSuggestBox クラス](/uwp/api/Windows.UI.Xaml.Controls.AutoSuggestBox)、[TextChanged イベント](/uwp/api/windows.ui.xaml.controls.autosuggestbox.textchanged)、[SuggestionChose イベント](/uwp/api/windows.ui.xaml.controls.autosuggestbox.suggestionchosen)、[QuerySubmitted イベント](/uwp/api/windows.ui.xaml.controls.autosuggestbox.querysubmitted)

## <a name="is-this-the-right-control"></a>これは適切なコントロールですか?

候補の一覧を使ってテキストを検索できる、シンプルでカスタマイズ可能なコントロールが必要な場合は、自動提案ボックスを使います。

適切なテキスト コントロールの選択の詳細については、「[テキスト コントロール](text-controls.md)」の記事をご覧ください。

## <a name="examples"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/AutoSuggestBox">アプリを開き、AutoSuggestBox の動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

Groove ミュージック アプリの自動提案ボックス。

![Groove ミュージック アプリの自動提案ボックス](images/control-examples/auto-suggest-box-groove.png)

## <a name="anatomy"></a>構造
自動提案ボックスのエントリ ポイントは、オプションのヘッダーとオプションのヒント テキスト付きのテキスト ボックスで構成されます。

![自動提案コントロールのエントリ ポイントの例](images/controls_autosuggest_entrypoint.png)

自動提案結果の一覧には、ユーザーがテキストの入力を開始すると自動的に内容が入力されます。 結果の一覧は、テキスト入力ボックスの上または下に表示されます。 [すべてクリア] ボタンも表示されます。

![展開された自動提案コントロールの例](images/controls_autosuggest_expanded01.png)

## <a name="create-an-auto-suggest-box"></a>自動提案ボックスの作成

AutoSuggestBox を使うには、3 つのユーザー操作に応答する必要があります。

- テキストの変更 - ユーザーがテキストを入力したときに、候補リストを更新します。
- 候補の選択 - ユーザーが候補リストで候補を選んだときに、テキスト ボックスを更新します。
- クエリの送信 - ユーザーがクエリを送信したときに、クエリの結果を表示します。

### <a name="text-changed"></a>テキストの変更

テキスト ボックスの内容が更新されるたびに、[TextChanged](/uwp/api/windows.ui.xaml.controls.autosuggestbox.textchanged) イベントが発生します。 イベント引数 [Reason](/uwp/api/windows.ui.xaml.controls.autosuggestboxtextchangedeventargs.reason) プロパティを使って、変更がユーザー入力によって生じたものかどうかを調べます。 変更の理由が **UserInput** の場合、入力に基づいてデータをフィルター処理します。 次に、フィルター処理されたデータを AutoSuggestBox の [ItemsSource](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemssource) に設定し、候補リストを更新します。

候補リストでの項目の表示方法を制御するには、[DisplayMemberPath](/uwp/api/windows.ui.xaml.controls.itemscontrol.displaymemberpath) または [ItemTemplate](/uwp/api/windows.ui.xaml.controls.itemscontrol.itemtemplate) を使うことができます。

- データ項目の単一のプロパティのテキストを表示するには、DisplayMemberPath プロパティを設定し、候補リストに表示するオブジェクトのプロパティを選択します。
- リストの各項目に対してカスタマイズした外観を定義するには、ItemTemplate プロパティを使います。

### <a name="suggestion-chosen"></a>候補の選択

ユーザーがキーボードを使って候補リスト内を移動したときは、テキスト ボックス内のテキストを更新して合わせる必要があります。

[TextMemberPath](/uwp/api/windows.ui.xaml.controls.autosuggestbox.textmemberpath) プロパティを設定し、テキスト ボックスに表示するデータ オブジェクトのプロパティを選択します。 TextMemberPath を指定した場合、テキスト ボックスは自動的に更新されます。 通常は、DisplayMemberPath と TextMemberPath に同じ値を指定する必要があるため、候補リストとテキスト ボックスのテキストは同じです。

単純ではないプロパティを表示する必要がある場合、[SuggestionChosen](/uwp/api/windows.ui.xaml.controls.autosuggestbox.suggestionchosen) イベントを処理し、選択した項目に基づいてカスタム テキストをテキスト ボックスに入力します。

### <a name="query-submitted"></a>クエリの送信

[QuerySubmitted](/uwp/api/windows.ui.xaml.controls.autosuggestbox.querysubmitted) イベントを処理し、アプリに適したクエリ操作を実行して、ユーザーに結果を表示します。

ユーザーがクエリ文字列をコミットすると、QuerySubmitted イベントが発生します。 ユーザーは次のいずれかの方法でクエリをコミットできます。
- テキスト ボックスにフォーカスがあるときに、Enter キーを押すか、クエリ アイコンをクリックします。 イベント引数の [ChosenSuggestion](/uwp/api/windows.ui.xaml.controls.autosuggestboxquerysubmittedeventargs.chosensuggestion) プロパティは **null** です。
- 候補リストにフォーカスがあるときに、Enter キーを押すか、項目をクリックまたはタップします。 イベント引数の ChosenSuggestion プロパティには、一覧から選択された項目が含まれています。

いずれの場合も、イベント引数の [QueryText](/uwp/api/windows.ui.xaml.controls.autosuggestboxquerysubmittedeventargs.querytext) プロパティにはテキスト ボックスのテキストが含まれています。

必須のイベント ハンドラーを使った簡単な AutoSuggestBox を次に示します。

```xaml
<AutoSuggestBox PlaceholderText="Search" QueryIcon="Find" Width="200"
                TextChanged="AutoSuggestBox_TextChanged"
                QuerySubmitted="AutoSuggestBox_QuerySubmitted"
                SuggestionChosen="AutoSuggestBox_SuggestionChosen"/>
```

```csharp
private void AutoSuggestBox_TextChanged(AutoSuggestBox sender, AutoSuggestBoxTextChangedEventArgs args)
{
    // Only get results when it was a user typing,
    // otherwise assume the value got filled in by TextMemberPath
    // or the handler for SuggestionChosen.
    if (args.Reason == AutoSuggestionBoxTextChangeReason.UserInput)
    {
        //Set the ItemsSource to be your filtered dataset
        //sender.ItemsSource = dataset;
    }
}


private void AutoSuggestBox_SuggestionChosen(AutoSuggestBox sender, AutoSuggestBoxSuggestionChosenEventArgs args)
{
    // Set sender.Text. You can use args.SelectedItem to build your text string.
}


private void AutoSuggestBox_QuerySubmitted(AutoSuggestBox sender, AutoSuggestBoxQuerySubmittedEventArgs args)
{
    if (args.ChosenSuggestion != null)
    {
        // User selected an item from the suggestion list, take an action on it here.
    }
    else
    {
        // Use args.QueryText to determine what to do.
    }
}
```

## <a name="use-autosuggestbox-for-search"></a>検索に AutoSuggestBox を使う

AutoSuggestBox を使って、ユーザーが入力と同時に選べる候補リストを表示します。

既定では、テキスト入力ボックスにはクエリ ボタンが表示されません。 [QueryIcon](/uwp/api/windows.ui.xaml.controls.autosuggestbox.queryicon) プロパティを設定し、テキスト ボックスの右側に指定したアイコンが表示されるボタンを追加することができます。 たとえば、AutoSuggestBox を一般的な検索ボックスと同様の外観にするには、次のような "検索" アイコンを追加します。

```xaml
<AutoSuggestBox QueryIcon="Find"/>
```

ここでは、AutoSuggestBox に "検索" アイコンが付いています。

![自動提案コントロールのエントリ ポイントの例](images/controls_autosuggest_entrypoint.png)

## <a name="dos-and-donts"></a>推奨と非推奨

-   自動提案ボックスを使って検索を実行したときに、入力したテキストに対応する検索結果が存在しなかった場合は、"検索結果が見つかりませんでした" という 1 行を表示します。これにより、ユーザーは検索要求が実行されたことがわかります。

    ![検索結果のない自動提案ボックスの例](images/controls_autosuggest_noresults.png)

<!--
<div class="microsoft-internal-note">
**Globalization and localization checklist**

<table>
<tr>
<th>Vertical spacing</th><td>Use non-Latin characters for vertical spacing to ensure non-Latin scripts will display properly, including numbers.</td>
</tr>
<tr>
<th>Scrolling</th><td>When auto suggest text is selected, user should be able to scroll to end of string.</td>
</tr>
</table>
</div>
-->

## <a name="get-the-sample-code"></a>サンプル コードの入手

- [XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。
- [AutoSuggestBox サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlAutoSuggestBox)

## <a name="related-articles"></a>関連記事

- [テキスト コントロール](text-controls.md)
- [スペル チェック](text-controls.md)
- [検索](search.md)
- [TextBox クラス](/uwp/api/Windows.UI.Xaml.Controls.TextBox)
- [Windows.UI.Xaml.Controls PasswordBox クラス](/uwp/api/Windows.UI.Xaml.Controls.PasswordBox)
- [String.Length プロパティ](/dotnet/api/system.string.length)