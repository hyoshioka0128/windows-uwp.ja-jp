---
ms.assetid: 1AE29512-7A7D-4179-ADAC-F02819AC2C39
title: 音楽、画像、ビデオのライブラリの管理
description: 音楽、画像、またはビデオの既存のフォルダーを対応するライブラリに追加できます。 ライブラリからフォルダーを削除したり、ライブラリ内のフォルダーの一覧を取得したり、保存した写真、音楽、ビデオにアクセスしたりすることもできます。
ms.date: 06/18/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: da3e5e74ae1e4e72b47cf80c3a5dfac4d2c6d3ef
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89156526"
---
# <a name="files-and-folders-in-the-music-pictures-and-videos-libraries"></a>ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー

音楽、画像、またはビデオの既存のフォルダーを対応するライブラリに追加できます。 ライブラリからフォルダーを削除したり、ライブラリ内のフォルダーの一覧を取得したり、保存した写真、音楽、ビデオにアクセスしたりすることもできます。

ライブラリは、フォルダーの仮想コレクションです。既定で含まれている既知のフォルダーに加えて、ユーザーがアプリや組み込みのアプリのいずれかを使ってライブラリに追加した他のフォルダーが含まれています。 たとえば、画像ライブラリには、既定で画像の既知のフォルダーが含まれています。 ユーザーは、アプリや組み込みのフォト アプリを使って、画像ライブラリに対してフォルダーの追加や削除を行うことができます。

## <a name="prerequisites"></a>前提条件


-   **ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングについての理解**

    C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](../threading-async/call-asynchronous-apis-in-csharp-or-visual-basic.md)」をご覧ください。 C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](../threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps.md)」をご覧ください。

-   **場所へのアクセス許可**

    Visual Studio のマニフェスト デザイナーで、アプリ マニフェスト ファイルを開きます。 **[機能]** ページで、アプリで管理するライブラリを選択します。

    -   **音楽ライブラリ**
    -   **画像ライブラリ**
    -   **ビデオ ライブラリ**

    詳しくは、「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。

## <a name="get-a-reference-to-a-library"></a>ライブラリへの参照を取得する

> [!NOTE]
> 必ず適切な機能を宣言してください。 詳しくは、「[アプリ機能の宣言](../packaging/app-capability-declarations.md)」をご覧ください。
 

ユーザーの音楽、画像、またはビデオ ライブラリへの参照を取得するには、[**StorageLibrary.GetLibraryAsync**](/uwp/api/windows.storage.storagelibrary.getlibraryasync) メソッドを呼び出します。 [  **KnownLibraryId**](/uwp/api/Windows.Storage.KnownLibraryId) 列挙体の対応する値を指定します。

-   [**KnownLibraryId.Music**](/uwp/api/windows.storage.knownfolders.musiclibrary)
-   [**KnownLibraryId.Pictures**](/uwp/api/windows.storage.knownfolders.pictureslibrary)
-   [**KnownLibraryId.Videos**](/uwp/api/windows.storage.knownfolders.videoslibrary)

```cs
var myPictures = await Windows.Storage.StorageLibrary.GetLibraryAsync(Windows.Storage.KnownLibraryId.Pictures);
```

## <a name="get-the-list-of-folders-in-a-library"></a>ライブラリ内のフォルダーの一覧を取得する


ライブラリ内のフォルダーの一覧を取得するには、[**StorageLibrary.Folders**](/uwp/api/windows.storage.storagelibrary.folders) プロパティの値を取得します。

```cs
using Windows.Foundation.Collections;
IObservableVector<Windows.Storage.StorageFolder> myPictureFolders = myPictures.Folders;
```

## <a name="get-the-folder-in-a-library-where-new-files-are-saved-by-default"></a>新しいファイルが既定で保存されるライブラリのフォルダーを取得する


新しいファイルが既定で保存されるライブラリのフォルダーを取得するには、[**StorageLibrary.SaveFolder**](/uwp/api/windows.storage.storagelibrary.savefolder) プロパティの値を取得します。

```cs
Windows.Storage.StorageFolder savePicturesFolder = myPictures.SaveFolder;
```

## <a name="add-an-existing-folder-to-a-library"></a>ライブラリに既存のフォルダーを追加する

ライブラリにフォルダーを追加するには、[**StorageLibrary.RequestAddFolderAsync**](/uwp/api/windows.storage.storagelibrary.requestaddfolderasync) を呼び出します。 画像ライブラリを例として考えた場合、このメソッドを呼び出すとフォルダー ピッカーが **[ピクチャにこのフォルダーを追加]** ボタンと共に表示されます。 ユーザーがフォルダーを選ぶと、フォルダーはディスク上の元の場所に残り、[**StorageLibrary.Folders**](/uwp/api/windows.storage.storagelibrary.folders) プロパティ (および組み込みのフォト アプリ) 内の項目となりますが、フォルダーはエクスプローラーでピクチャ フォルダーの子として表示されません。


```cs
Windows.Storage.StorageFolder newFolder = await myPictures.RequestAddFolderAsync();
```

## <a name="remove-a-folder-from-a-library"></a>フォルダーをライブラリから削除する

フォルダーをライブラリから削除するには、[**StorageLibrary.RequestRemoveFolderAsync**](/uwp/api/windows.storage.storagelibrary.requestremovefolderasync) メソッドを呼び出して、削除するフォルダーを指定します。 [  **StorageLibrary.Folders**](/uwp/api/windows.storage.storagelibrary.folders) と [**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) コントロール (または同様のコントロール) を使って、ユーザーが削除するフォルダーを選べるようにすることができます。

[  **StorageLibrary.RequestRemoveFolderAsync**](/uwp/api/windows.storage.storagelibrary.requestremovefolderasync) を呼び出すと、フォルダーが "ピクチャに表示されなくなるが、削除されない" ことを示す確認ダイアログがユーザーに表示されます。 これは、フォルダーがディスク上の元の場所に残るが、[**StorageLibrary.Folders**](/uwp/api/windows.storage.storagelibrary.folders) プロパティから削除され、組み込みのフォト アプリには含まれなくなることを意味します。

次の例では、ユーザーが削除するフォルダーを **lvPictureFolders** という名前の [**ListView**](/uwp/api/Windows.UI.Xaml.Controls.ListView) コントロールから選んだことを前提としています。


```cs
bool result = await myPictures.RequestRemoveFolderAsync(folder);
```

## <a name="get-notified-of-changes-to-the-list-of-folders-in-a-library"></a>ライブラリ内のフォルダーの一覧に対する変更の通知を受け取る


ライブラリ内のフォルダーの一覧に対する変更について通知を受け取るには、ライブラリの [**StorageLibrary.DefinitionChanged**](/uwp/api/windows.storage.storagelibrary.definitionchanged) イベントにハンドラーを登録します。


```cs
myPictures.DefinitionChanged += MyPictures_DefinitionChanged;

void HandleDefinitionChanged(Windows.Storage.StorageLibrary sender, object args)
{
    // ...
}
```

## <a name="media-library-folders"></a>メディア ライブラリ フォルダー


デバイスには、ユーザーやアプリがメディア ファイルを格納するための定義済みの場所が 5 つ用意されています。 組み込みのアプリでは、ユーザーが作成したメディアとダウンロードしたメディアをこれらの場所に格納できます。

次の場所が定義されています。

-   **ピクチャ** フォルダー。 画像が格納されます。

    -   **カメラ ロール** フォルダー。 組み込みのカメラからの写真やビデオが格納されます。

    -   **保存済みの写真**フォルダー。 ユーザーが他のアプリから保存した画像が格納されます。

-   **ミュージック** フォルダー。 楽曲、ポッドキャスト、オーディオ ブックが格納されます。

-   **ビデオ** フォルダー。 ビデオが格納されます。

ユーザーやアプリは、メディア ライブラリ フォルダーだけではなく、SD カード上にメディア ファイルを保存することもできます。 SD カード上のメディア ファイルを確実に検索するには、SD カードのコンテンツをスキャンするか、ファイル ピッカーを使ってファイルを検索するようにユーザーに対して要求します。 詳しくは、「[SD カードへのアクセス](access-the-sd-card.md)」をご覧ください。

## <a name="querying-the-media-libraries"></a>メディア ライブラリへの照会

ファイルのコレクションを取得するには、ライブラリと必要なファイルの種類を指定します。

```cs
using Windows.Storage;
using Windows.Storage.Search;

private async void getSongs()
{
    QueryOptions queryOption = new QueryOptions
        (CommonFileQuery.OrderByTitle, new string[] { ".mp3", ".mp4", ".wma" });

    queryOption.FolderDepth = FolderDepth.Deep;

    Queue<IStorageFolder> folders = new Queue<IStorageFolder>();

    var files = await KnownFolders.MusicLibrary.CreateFileQueryWithOptions
      (queryOption).GetFilesAsync();

    foreach (var file in files)
    {
        // do something with the music files
    }
}
```

### <a name="query-results-include-both-internal-and-removable-storage"></a>内部ストレージとリムーバブル ストレージの両方が含まれるクエリ結果

ユーザーは、既定でオプションの SD カードにファイルを格納するように選ぶことができます。 また、アプリでは、ファイルが SD カードに格納されないようにすることができます。 その結果、メディア ライブラリがデバイスの内部ストレージと SD カードの両方に存在する可能性があります。

この状況を処理するために追加のコードを記述する必要はありません。 既知のフォルダーを照会する [**Windows.Storage**](/uwp/api/Windows.Storage) 名前空間のメソッドが、両方の場所からのクエリ結果を透過的に結合します。 結合された結果を取得するために、アプリ マニフェスト ファイルで **removableStorage** 機能を指定する必要もありません。

次の図に示すデバイスのストレージの状態について考えてみましょう。

![電話と SD カード上にある画像](images/phone-media-locations.png)

`await KnownFolders.PicturesLibrary.GetFilesAsync()`を呼び出して、画像ライブラリのコンテンツを照会すると、その結果には internalPic.jpg と SDPic.jpg の両方が含まれます。


## <a name="working-with-photos"></a>写真の操作

すべての画像について低解像度の画像と高解像度の画像の両方を保存するカメラ機能を備えたデバイスでは、深いクエリからは低解像度の画像のみが返されます。

[カメラ ロール] フォルダーと [保存済みの写真] フォルダーでは、深いクエリがサポートされていません。

**撮影に使ったアプリで写真を開く**

ユーザーが撮影に使ったアプリで後から再び写真を表示できるようにするには、写真のメタデータと一緒に **CreatorAppId** を保存します。次のコード例を参考にしてください。 この例では、**testPhoto** は [**StorageFile**](/uwp/api/Windows.Storage.StorageFile) です。

```cs
IDictionary<string, object> propertiesToSave = new Dictionary<string, object>();

propertiesToSave.Add("System.CreatorOpenWithUIOptions", 1);
propertiesToSave.Add("System.CreatorAppId", appId);

testPhoto.Properties.SavePropertiesAsync(propertiesToSave).AsyncWait();   
```

## <a name="using-stream-methods-to-add-a-file-to-a-media-library"></a>ストリーム メソッドを使ってメディア ライブラリにファイルを追加する

**KnownFolders.PictureLibrary** など、既知のフォルダーを使ってメディア ライブラリにアクセスし、ストリーム メソッドを使ってそのメディア ライブラリにファイルを追加するときは、コードで開いているすべてのストリームを閉じる必要があります。 そのようにしなかった場合、ファイルへのハンドルを保持しているストリームが少なくとも 1 つは存在することとなり、ストリーム メソッドは、メディア ライブラリに正しくファイルを追加できません。

たとえば、以下のコードを実行したときに、メディア ライブラリにファイルが追加されません。 `using (var destinationStream = (await destinationFile.OpenAsync(FileAccessMode.ReadWrite)).GetOutputStreamAt(0))` のコード行において、**OpenAsync** メソッドと **GetOutputStreamAt** メソッドの両方がストリームを開いています。 しかし、**using** ステートメントの結果として破棄されるのは、**GetOutputStreamAt** メソッドによって開かれたストリームだけです。 もう一方のストリームは開いたままであり、そのことがファイルの保存を妨げます。

```cs
StorageFolder testFolder = await StorageFolder.GetFolderFromPathAsync(@"C:\test");
StorageFile sourceFile = await testFolder.GetFileAsync("TestImage.jpg");
StorageFile destinationFile = await KnownFolders.CameraRoll.CreateFileAsync("MyTestImage.jpg");
using (var sourceStream = (await sourceFile.OpenReadAsync()).GetInputStreamAt(0))
{
    using (var destinationStream = (await destinationFile.OpenAsync(FileAccessMode.ReadWrite)).GetOutputStreamAt(0))
    {
        await RandomAccessStream.CopyAndCloseAsync(sourceStream, destinationStream);
    }
}
```

ストリーム メソッドを正しく使ってメディア ライブラリにファイルを追加するには、以下の例のように、コード中で開いているストリームをすべて閉じてください。

```cs
StorageFolder testFolder = await StorageFolder.GetFolderFromPathAsync(@"C:\test");
StorageFile sourceFile = await testFolder.GetFileAsync("TestImage.jpg");
StorageFile destinationFile = await KnownFolders.CameraRoll.CreateFileAsync("MyTestImage.jpg");

using (var sourceStream = await sourceFile.OpenReadAsync())
{
    using (var sourceInputStream = sourceStream.GetInputStreamAt(0))
    {
        using (var destinationStream = await destinationFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            using (var destinationOutputStream = destinationStream.GetOutputStreamAt(0))
            {
                await RandomAccessStream.CopyAndCloseAsync(sourceInputStream, destinationStream);
            }
        }
    }
}
```