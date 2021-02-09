---
description: 書式付きテキスト、ハイパーリンク、イメージなどを含んだリッチ テキスト ドキュメントの入力と編集には、RichEditBox コントロールを使うことができます。 このコントロールの IsReadOnly プロパティを true に設定すると、RichEditBox を読み取り専用にできます。
title: RichEditBox
ms.assetid: 4AFC0DFA-3B89-434D-9F86-4309CCFF7839
label: Rich edit box
template: detail.hbs
ms.date: 09/24/2020
ms.topic: article
keywords: windows 10, uwp
pm-contact: miguelrb
design-contact: ksulliv
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: bb5ee48152b96c430e3b6ab8cf320b3055620865
ms.sourcegitcommit: a3bbd3dd13be5d2f8a2793717adf4276840ee17d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93035215"
---
# <a name="rich-edit-box"></a>リッチ エディット ボックス

書式付きテキスト、ハイパーリンク、イメージなどを含んだリッチ テキスト ドキュメントの入力と編集には、RichEditBox コントロールを使うことができます。 このコントロールの IsReadOnly プロパティを **true** に設定すると、RichEditBox を読み取り専用にできます。

**Windows UI ライブラリを入手する**

:::row:::
   :::column:::
      ![WinUI ロゴ](images/winui-logo-64x64.png)
   :::column-end:::
   :::column span="3":::
      Windows UI ライブラリ 2.2 以降には、丸めた角を使用するこのコントロールの新しいテンプレートが含まれます。 詳しくは、「[角の半径](../style/rounded-corner.md)」をご覧ください。 WinUI は、Windows アプリの新しいコントロールと UI 機能が含まれる NuGet パッケージです。 インストール手順などについて詳しくは、「[Windows UI Library (Windows UI ライブラリ)](/uwp/toolkits/winui/)」をご覧ください。
   :::column-end:::
   :::column:::

   :::column-end:::
:::row-end:::

> **プラットフォーム API** : [RichEditBox クラス](/uwp/api/Windows.UI.Xaml.Controls.RichEditBox)、 [Document プロパティ](/uwp/api/windows.ui.xaml.controls.richeditbox.document)、 [IsReadOnly プロパティ](/uwp/api/windows.ui.xaml.controls.richeditbox.isreadonly)、 [IsSpellCheckEnabled プロパティ](/uwp/api/windows.ui.xaml.controls.richeditbox.isspellcheckenabled)

## <a name="is-this-the-right-control"></a>これは適切なコントロールですか?

**RichEditBox** を使用して、テキスト ファイルを表示および編集します。 その他の標準的なテキスト入力ボックスを使用するように、RichEditBox を使用してアプリにユーザー入力を行わないでください。 代わりに、アプリとは別のテキスト ファイルを操作するために使用します。 通常は、RichEditBox に入力されたテキストを .rtf ファイルに保存します。
-   複数行テキスト ボックスの主な目的が読み取り専用ドキュメントの作成 (ブログのエントリ、メール メッセージのコンテンツなど) であり、ドキュメントでリッチ テキストが必要な場合は、代わりに[リッチ テキスト ブロック](./rich-text-block.md)を使います。
-   内部的に使うだけで、ユーザーに再表示しないテキストを取得する場合は、プレーンテキスト入力コントロールを使います。
-   他のすべてのシナリオでは、プレーンテキスト入力コントロールを使います。

適切なテキスト コントロールの選択の詳細については、「[テキスト コントロール](text-controls.md)」の記事をご覧ください。

## <a name="examples"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/RichEditBox">アプリを開き、RichEditBox の動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

このリッチ エディット ボックスで、リッチ テキスト ドキュメントを開きます。 書式設定とファイルのボタンは、リッチ エディット ボックスの一部ではありませんが、最小限のスタイル設定ボタンを用意し、その動作を実装する必要があります。

![開いたドキュメントが用意されたリッチ テキスト ボックス](images/rich-edit-box.png)

## <a name="create-a-rich-edit-box"></a>リッチ エディット ボックスを作成します。

既定では、RichEditBox はスペル チェックをサポートします。 スペル チェックを無効にするには、 [IsSpellCheckEnabled](/uwp/api/windows.ui.xaml.controls.richeditbox.isspellcheckenabled) プロパティを **false** に設定します。 詳しくは、「[スペル チェックのガイドライン](text-controls.md)」をご覧ください。

RichEditBox のコンテンツを取得するには、このコントロールの [Document](/uwp/api/windows.ui.xaml.controls.richeditbox.document) プロパティを使います。 RichTextBlock コントロールと異なり、RichEditBox のコンテンツは [Windows.UI.Text.ITextDocument](/windows/desktop/api/tom/nn-tom-itextdocument) オブジェクトです。このコンテンツは、[Windows.UI.Xaml.Documents.Block](/uwp/api/Windows.UI.Xaml.Documents.Block) オブジェクトをそのコンテンツとして使います。 ITextDocument インターフェイスは、ドキュメントの読み込みとストリームへの保存、テキスト範囲の取得、アクティブな選択内容の取得、変更の取り消しとやり直し、既定の書式設定属性の設定などに利用できます。

この例では、RichEditBox でリッチ テキスト形式 (.rtf) ファイルの編集、読み込み、保存を行う方法を示します。

```xaml
<RelativePanel Margin="20" HorizontalAlignment="Stretch">
    <RelativePanel.Resources>
        <Style TargetType="AppBarButton">
            <Setter Property="IsCompact" Value="True"/>
        </Style>
    </RelativePanel.Resources>
    <AppBarButton x:Name="openFileButton" Icon="OpenFile"
                  Click="OpenButton_Click" ToolTipService.ToolTip="Open file"/>
    <AppBarButton Icon="Save" Click="SaveButton_Click"
                  ToolTipService.ToolTip="Save file"
                  RelativePanel.RightOf="openFileButton" Margin="8,0,0,0"/>

    <AppBarButton Icon="Bold" Click="BoldButton_Click" ToolTipService.ToolTip="Bold"
                  RelativePanel.LeftOf="italicButton" Margin="0,0,8,0"/>
    <AppBarButton x:Name="italicButton" Icon="Italic" Click="ItalicButton_Click"
                  ToolTipService.ToolTip="Italic" RelativePanel.LeftOf="underlineButton" Margin="0,0,8,0"/>
    <AppBarButton x:Name="underlineButton" Icon="Underline" Click="UnderlineButton_Click"
                  ToolTipService.ToolTip="Underline" RelativePanel.AlignRightWithPanel="True"/>

    <RichEditBox x:Name="editor" Height="200" RelativePanel.Below="openFileButton"
                 RelativePanel.AlignLeftWithPanel="True" RelativePanel.AlignRightWithPanel="True"/>
</RelativePanel>
```


```csharp
private async void OpenButton_Click(object sender, RoutedEventArgs e)
{
    // Open a text file.
    Windows.Storage.Pickers.FileOpenPicker open =
        new Windows.Storage.Pickers.FileOpenPicker();
    open.SuggestedStartLocation =
        Windows.Storage.Pickers.PickerLocationId.DocumentsLibrary;
    open.FileTypeFilter.Add(".rtf");

    Windows.Storage.StorageFile file = await open.PickSingleFileAsync();

    if (file != null)
    {
        try
        {
            Windows.Storage.Streams.IRandomAccessStream randAccStream =
        await file.OpenAsync(Windows.Storage.FileAccessMode.Read);

            // Load the file into the Document property of the RichEditBox.
            editor.Document.LoadFromStream(Windows.UI.Text.TextSetOptions.FormatRtf, randAccStream);
        }
        catch (Exception)
        {
            ContentDialog errorDialog = new ContentDialog()
            {
                Title = "File open error",
                Content = "Sorry, I couldn't open the file.",
                PrimaryButtonText = "Ok"
            };

            await errorDialog.ShowAsync();
        }
    }
}

private async void SaveButton_Click(object sender, RoutedEventArgs e)
{
    Windows.Storage.Pickers.FileSavePicker savePicker = new Windows.Storage.Pickers.FileSavePicker();
    savePicker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.DocumentsLibrary;

    // Dropdown of file types the user can save the file as
    savePicker.FileTypeChoices.Add("Rich Text", new List<string>() { ".rtf" });

    // Default file name if the user does not type one in or select a file to replace
    savePicker.SuggestedFileName = "New Document";

    Windows.Storage.StorageFile file = await savePicker.PickSaveFileAsync();
    if (file != null)
    {
        // Prevent updates to the remote version of the file until we
        // finish making changes and call CompleteUpdatesAsync.
        Windows.Storage.CachedFileManager.DeferUpdates(file);
        // write to file
        Windows.Storage.Streams.IRandomAccessStream randAccStream =
            await file.OpenAsync(Windows.Storage.FileAccessMode.ReadWrite);

        editor.Document.SaveToStream(Windows.UI.Text.TextGetOptions.FormatRtf, randAccStream);

        // Let Windows know that we're finished changing the file so the
        // other app can update the remote version of the file.
        Windows.Storage.Provider.FileUpdateStatus status = await Windows.Storage.CachedFileManager.CompleteUpdatesAsync(file);
        if (status != Windows.Storage.Provider.FileUpdateStatus.Complete)
        {
            Windows.UI.Popups.MessageDialog errorBox =
                new Windows.UI.Popups.MessageDialog("File " + file.Name + " couldn't be saved.");
            await errorBox.ShowAsync();
        }
    }
}

private void BoldButton_Click(object sender, RoutedEventArgs e)
{
    Windows.UI.Text.ITextSelection selectedText = editor.Document.Selection;
    if (selectedText != null)
    {
        Windows.UI.Text.ITextCharacterFormat charFormatting = selectedText.CharacterFormat;
        charFormatting.Bold = Windows.UI.Text.FormatEffect.Toggle;
        selectedText.CharacterFormat = charFormatting;
    }
}

private void ItalicButton_Click(object sender, RoutedEventArgs e)
{
    Windows.UI.Text.ITextSelection selectedText = editor.Document.Selection;
    if (selectedText != null)
    {
        Windows.UI.Text.ITextCharacterFormat charFormatting = selectedText.CharacterFormat;
        charFormatting.Italic = Windows.UI.Text.FormatEffect.Toggle;
        selectedText.CharacterFormat = charFormatting;
    }
}

private void UnderlineButton_Click(object sender, RoutedEventArgs e)
{
    Windows.UI.Text.ITextSelection selectedText = editor.Document.Selection;
    if (selectedText != null)
    {
        Windows.UI.Text.ITextCharacterFormat charFormatting = selectedText.CharacterFormat;
        if (charFormatting.Underline == Windows.UI.Text.UnderlineType.None)
        {
            charFormatting.Underline = Windows.UI.Text.UnderlineType.Single;
        }
        else {
            charFormatting.Underline = Windows.UI.Text.UnderlineType.None;
        }
        selectedText.CharacterFormat = charFormatting;
    }
}
```

## <a name="choose-the-right-keyboard-for-your-text-control"></a>テキスト コントロールに適切なキーボードの選択

ユーザーがタッチ キーボード、つまりソフト入力パネル (SIP) でデータを入力できるように、ユーザーが入力すると予想されるデータの種類に合わせてテキスト コントロールの入力値の種類を設定できます。 通常、既定のキーボード レイアウトは、リッチ テキスト ドキュメントを扱う場合に適しています。

入力値の種類の使い方について詳しくは、「[入力値の種類を使ったタッチ キーボードの変更](../input/use-input-scope-to-change-the-touch-keyboard.md)」をご覧ください。

## <a name="dos-and-donts"></a>推奨と非推奨

- リッチ テキスト ボックスを作成する場合は、スタイル設定ボタンを用意し、その動作を実装します。
- アプリのスタイルに合ったフォントを使用します。
- テキスト コントロールの高さは、典型的な入力が十分に入るように設定します。
- ユーザーの入力中にテキスト入力コントロールの高さが増加するようにはしません。
- ユーザーが 1 行しか必要としていない場合は、複数行テキスト ボックスを使用しません。
- プレーンテキスト コントロールで十分な場合に、リッチ テキスト コントロールを使用しません。

## <a name="get-the-sample-code"></a>サンプル コードを入手する

- [XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。

## <a name="related-articles"></a>関連記事

- [テキスト コントロール](text-controls.md)
- [スペル チェックのガイドライン](text-controls.md)
- [検索の追加](search.md)
- [テキスト入力のガイドライン](text-controls.md)
- [TextBox クラス](/uwp/api/Windows.UI.Xaml.Controls.TextBox)
- [Windows.UI.Xaml.Controls PasswordBox クラス](/uwp/api/Windows.UI.Xaml.Controls.PasswordBox)
