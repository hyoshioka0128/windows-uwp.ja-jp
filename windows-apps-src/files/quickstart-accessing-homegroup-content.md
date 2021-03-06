---
ms.assetid: 12ECEA89-59D2-4BCE-B24C-5A4DD525E0C7
title: ホームグループ コンテンツへのアクセス
description: ユーザーのホームグループ フォルダーに格納されているコンテンツ (画像、音楽、ビデオなど) にアクセスします。
ms.date: 12/19/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 07d94f5b11acfe14bf55392c5cbf2c1b7bcfbeef
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369396"
---
# <a name="accessing-homegroup-content"></a>ホームグループ コンテンツへのアクセス



**重要な API**

-   [**Windows.Storage.KnownFolders クラス**](https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders)

ユーザーのホームグループ フォルダーに格納されているコンテンツ (画像、音楽、ビデオなど) にアクセスします。

## <a name="prerequisites"></a>前提条件

-   **ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングを理解します。**

    C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)」をご覧ください。 C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。

-   **アプリの capabilty 宣言**

    ホームグループ コンテンツにアクセスするには、ユーザーのコンピューターにホームグループがセットアップされ、アプリに **picturesLibrary**、**musicLibrary**、**videosLibrary** のうちの少なくとも 1 つの機能が備わっている必要があります。 アプリは、ホームグループ フォルダーにアクセスすると、アプリのマニフェストで宣言されている機能に対応するライブラリだけを参照します。 詳しくは、「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。

    > [!NOTE]
    > ホーム グループのドキュメント ライブラリ内のコンテンツは、アプリのマニフェストで宣言されている機能に関係なく、ユーザーの共有設定に関係なく、アプリに表示されません。     

-   **ファイル ピッカーを使用する方法を理解します。**

    ホームグループのファイルやフォルダーにアクセスするには、通常、ファイル ピッカーを使います。 ファイル ピッカーの使い方については、「[ピッカーでファイルやフォルダーを開く](quickstart-using-file-and-folder-pickers.md)」をご覧ください。

-   **ファイルとフォルダーのクエリを理解します。**

    ホームグループのファイルやフォルダーを列挙するには、クエリを使うことができます。 ファイルとフォルダーのクエリについて詳しくは、「[ファイルとフォルダーの列挙と照会](quickstart-listing-files-and-folders.md)」をご覧ください。

## <a name="open-the-file-picker-at-the-homegroup"></a>ホームグループでファイル ピッカーを開く

以下の手順に従って、ユーザーがホームグループのファイルとフォルダーを選ぶことができるファイル ピッカーのインスタンスを開きます。

1.  **作成し、ファイル ピッカーをカスタマイズします。**

    [  **FileOpenPicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) を使ってファイル ピッカーを作成し、ピッカーの [**SuggestedStartLocation**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.suggestedstartlocation) を [**PickerLocationId.HomeGroup**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.PickerLocationId) に設定します。 または、ユーザーとアプリに関連するその他のプロパティを設定します。 ファイル ピッカーのカスタマイズ方法を判断するためのガイドラインについては、「[ファイル ピッカーのガイドラインとチェック リスト](https://docs.microsoft.com/windows/uwp/files/quickstart-using-file-and-folder-pickers)」をご覧ください。

    次の例では、ホームグループで開かれ、すべての種類のファイルを含み、ファイルをサムネイル画像として表示するファイル ピッカーを作成しています。
    ```cs
    Windows.Storage.Pickers.FileOpenPicker picker = new Windows.Storage.Pickers.FileOpenPicker();
    picker.ViewMode = Windows.Storage.Pickers.PickerViewMode.Thumbnail;
    picker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.HomeGroup;
    picker.FileTypeFilter.Clear();
    picker.FileTypeFilter.Add("*");
    ```

2.  **ファイル ピッカーを表示し、選択されたファイルを処理します。**

    ファイル ピッカーを作成してカスタマイズしたら、ユーザーが 1 つのファイルを選べるように [**FileOpenPicker.PickSingleFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync) を呼び出すか、複数のファイルを選べるように [**FileOpenPicker.PickMultipleFilesAsync**](https://docs.microsoft.com/uwp/api/windows.storage.pickers.fileopenpicker.pickmultiplefilesasync) を呼び出します。

    次の例では、ファイル ピッカーを表示して、ユーザーが 1 つのファイルを選べるようにしています。
    ```cs
    Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();

    if (file != null)
    {
        // Do something with the file.
    }
    else
    {
        // No file returned. Handle the error.
    }   
    ```

## <a name="search-the-homegroup-for-files"></a>ホームグループでファイルを検索する

このセクションでは、ユーザーが指定したクエリ語句に一致するホームグループ項目を見つける方法を示します。

1.  **ユーザーから、クエリ用語を取得します。**

    ここでは、ユーザーが `searchQueryTextBox` という名前の [**TextBox**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBox) コントロールに入力したクエリ語句を取得します。
    ```cs
    string queryTerm = this.searchQueryTextBox.Text;    
    ```

2.  **検索フィルター クエリ オプションを設定します。**

    クエリ オプションは、検索結果をどのように並べ替えるかを決めます。検索フィルターは、どの項目が検索結果に含まれるかを決めます。

    次の例は、検索結果をまず関連性で、次に更新日で並べ替えるクエリ オプションを設定します。 検索フィルターは、ユーザーが前の手順で入力したクエリ語句です。
    ```cs
    Windows.Storage.Search.QueryOptions queryOptions =
            new Windows.Storage.Search.QueryOptions
                (Windows.Storage.Search.CommonFileQuery.OrderBySearchRank, null);
    queryOptions.UserSearchFilter = queryTerm.Text;
    Windows.Storage.Search.StorageFileQueryResult queryResults =
            Windows.Storage.KnownFolders.HomeGroup.CreateFileQueryWithOptions(queryOptions);    
    ```

3.  **クエリを実行し、結果を処理します。**

    次の例は、ホームグループで検索クエリを実行し、一致するファイルの名前を文字列の一覧として保存します。
    ```cs
    System.Collections.Generic.IReadOnlyList<Windows.Storage.StorageFile> files =
        await queryResults.GetFilesAsync();

    if (files.Count > 0)
    {
        outputString += (files.Count == 1) ? "One file found\n" : files.Count.ToString() + " files found\n";
        foreach (Windows.Storage.StorageFile file in files)
        {
            outputString += file.Name + "\n";
        }
    }    
    ```


## <a name="search-the-homegroup-for-a-particular-users-shared-files"></a>ホームグループで特定のユーザーの共有ファイルを検索する

このセクションでは、特定のユーザーによって共有されているホームグループ ファイルを見つける方法を示します。

1.  **ホーム グループのユーザーのコレクションを取得します。**

    ホームグループの第 1 レベルのフォルダーは、それぞれが個々のホームグループ ユーザーを表しています。 そのため、ホームグループ ユーザーのコレクションを取得するには、[**GetFoldersAsync**](https://docs.microsoft.com/uwp/api/windows.storage.storagefolder.getfoldersasync) を呼び出し、第 1 レベルのホームグループ フォルダーを取得します。
    ```cs
    System.Collections.Generic.IReadOnlyList<Windows.Storage.StorageFolder> hgFolders =
        await Windows.Storage.KnownFolders.HomeGroup.GetFoldersAsync();    
    ```

2.  **ターゲット ユーザーのフォルダーを見つけて、そのユーザーのフォルダーにスコープ設定ファイルのクエリを作成します。**

    次の例は、取得したフォルダーを反復処理して、目的のユーザーのフォルダーを見つけます。 次に、クエリ オプションを設定して、フォルダー内のすべてのファイルを検索し、まずは関連性で、次に更新日で並べ替えます。 この例では、見つかったファイルの数とファイルの名前を報告する文字列を作成します。
    ```cs
    bool userFound = false;
    foreach (Windows.Storage.StorageFolder folder in hgFolders)
    {
        if (folder.DisplayName == targetUserName)
        {
            // Found the target user's folder, now find all files in the folder.
            userFound = true;
            Windows.Storage.Search.QueryOptions queryOptions =
                new Windows.Storage.Search.QueryOptions
                    (Windows.Storage.Search.CommonFileQuery.OrderBySearchRank, null);
            queryOptions.UserSearchFilter = "*";
            Windows.Storage.Search.StorageFileQueryResult queryResults =
                folder.CreateFileQueryWithOptions(queryOptions);
            System.Collections.Generic.IReadOnlyList<Windows.Storage.StorageFile> files =
                await queryResults.GetFilesAsync();

            if (files.Count > 0)
            {
                string outputString = "Searched for files belonging to " + targetUserName + "'\n";
                outputString += (files.Count == 1) ? "One file found\n" : files.Count.ToString() + " files found\n";
                foreach (Windows.Storage.StorageFile file in files)
                {
                    outputString += file.Name + "\n";
                }
            }
        }
    }    
    ```

## <a name="stream-video-from-the-homegroup"></a>ホームグループからビデオをストリーミングする

ホームグループからビデオ コンテンツをストリーミングするには、次の手順を実行します。

1.  **アプリ内に MediaElement を含めます。**

    [  **MediaElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement) は、アプリのオーディオ コンテンツとビデオ コンテンツを再生します。 オーディオとビデオの再生について詳しくは、「[カスタム トランスポート コントロールを作成する](https://docs.microsoft.com/windows/uwp/controls-and-patterns/custom-transport-controls)」と「[オーディオ、ビデオ、およびカメラ](https://docs.microsoft.com/windows/uwp/audio-video-camera/index)」をご覧ください。
    ```HTML
    <Grid x:Name="Output" HorizontalAlignment="Left" VerticalAlignment="Top" Grid.Row="1">
        <MediaElement x:Name="VideoBox" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0" Width="400" Height="300"/>
    </Grid>    
    ```

2.  **ホーム グループにファイル ピッカーを開き、アプリでサポートされる形式でビデオ ファイルを含むフィルターを適用します。**

    次の例では、ファイル オープン ピッカーに .mp4 ファイルと .wmv ファイルが含まれます。
    ```cs
    Windows.Storage.Pickers.FileOpenPicker picker = new Windows.Storage.Pickers.FileOpenPicker();
    picker.ViewMode = Windows.Storage.Pickers.PickerViewMode.Thumbnail;
    picker.SuggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.HomeGroup;
    picker.FileTypeFilter.Clear();
    picker.FileTypeFilter.Add(".mp4");
    picker.FileTypeFilter.Add(".wmv");
    Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();   
    ```

3.  **読み取りアクセス権をユーザーのファイルの選択を開いてのソースとしてファイル ストリームを設定して、** [ **MediaElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaElement)、し、ファイルを再生します。
    ```cs
    if (file != null)
    {
        var stream = await file.OpenAsync(Windows.Storage.FileAccessMode.Read);
        VideoBox.SetSource(stream, file.ContentType);
        VideoBox.Stop();
        VideoBox.Play();
    }
    else
    {
        // No file selected. Handle the error here.
    }    
    ```
