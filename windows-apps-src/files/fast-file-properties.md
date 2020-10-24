---
title: UWP でファイルのプロパティにすばやくアクセスする
description: UWP アプリで使用するために、ライブラリからファイルとそのプロパティの一覧を効率的に収集します。
ms.date: 02/06/2019
ms.topic: article
keywords: Windows 10, UWP, ファイル, プロパティ
ms.localizationpriority: medium
ms.openlocfilehash: 75d835a5f7de6fd26e6a05a80b5f47a8fe0c0e1b
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173226"
---
# <a name="fast-access-to-file-properties-in-uwp"></a>UWP でファイルのプロパティにすばやくアクセスする 

ライブラリからファイルとそのプロパティの一覧をすばやく収集し、アプリでそれらのプロパティを使用する方法について説明します。  

前提条件 
- **ユニバーサル Windows プラットフォーム (UWP) アプリ向けの非同期プログラミング**     C# または Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](../threading-async/call-asynchronous-apis-in-csharp-or-visual-basic.md)」をご覧ください。 C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](../threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps.md)」をご覧ください。 
- **ライブラリへのアクセス許可**   これらの例のコードでは **picturesLibrary** 機能が必要ですが、ご利用のファイルの場所によっては別の機能が必要な場合や、機能をまったく必要としない場合もあります。 詳しくは、「[ファイル アクセス許可](./file-access-permissions.md)」をご覧ください。 
- **シンプルなファイルの列挙**    この例では、[QueryOptions](/uwp/api/Windows.Storage.Search.QueryOptions) を使用して、高度な列挙プロパティをいくつか設定します。 小さいディレクトリを対象としてファイルの簡単な一覧を取得する方法について詳しくは、「[ファイルとフォルダーの列挙と照会](./quickstart-listing-files-and-folders.md)」をご覧ください。 

## <a name="usage"></a>使用方法  
多くのアプリでは、ファイルのグループのプロパティを一覧表示する必要がありますが、常にファイルと直接やり取りする必要はありません。 たとえば、音楽アプリは一度に 1 つのファイルを再生します (開きます) が、アプリで曲のキューを表示したり、ユーザーが再生可能なファイルを選択したりする場合には、フォルダー内にあるすべてのファイルのプロパティが必要になります。 

このページで紹介する例は、すべてのファイルのメタデータを変更するアプリや、プロパティを読み取ることができない場合に、生成されるすべての StorageFiles とやり取りするアプリには使用しないでください。 詳しくは、「[ファイルとフォルダーの列挙と照会](./quickstart-listing-files-and-folders.md)」をご覧ください。 

## <a name="enumerate-all-the-pictures-in-a-location"></a>ある場所に保存されているすべての画像を列挙する 
この例では、以下を行います。
-  [QueryOptions](/uwp/api/Windows.Storage.Search.QueryOptions) オブジェクトを作成して、アプリではできるだけ早くファイルを列挙する必要があることを指定します。
-  StorageFile オブジェクトをアプリにページングすることにより、ファイル プロパティをフェッチします。 ファイルをページングすることで、アプリによるメモリの使用量を削減し、認識可能な応答性を向上させることができます。

### <a name="creating-the-query"></a>クエリの作成 
クエリを作成するには、QueryOptions オブジェクトを使用して、アプリでは特定の種類の画像ファイルだけを列挙する必要があることを指定し、Windows 情報保護 (System.Security.EncryptionOwners) によって保護されているファイルを除外します。 

[QueryOptions.SetPropertyPrefetch](/uwp/api/windows.storage.search.queryoptions.setpropertyprefetch) を使用して、アプリがアクセサリするプロパティを設定することが重要です。 アプリがプリフェッチされていないプロパティにアクセスすると、重大なパフォーマンス ペナルティが発生します。

[IndexerOption.OnlyUseIndexerAndOptimzeForIndexedProperties](/uwp/api/Windows.Storage.Search.IndexerOption) を設定して、結果をできるだけ早く返すこと、および [SetPropertyPrefetch](/uwp/api/windows.storage.search.queryoptions.setpropertyprefetch) で指定したプロパティのみを含めることをシステムに通知します。 

### <a name="paging-in-the-results"></a>ページングして結果を生成する 
画像ライブラリには数十万または数百万のファイルが保存されている場合があり、[GetFilesAsync](/uwp/api/windows.storage.search.storagefilequeryresult.getfilesasync) を呼び出すことによって、コンピューターに過剰な負荷がかかる可能性があります。これは、画像ごとに StorageFile が作成されるためです。 これを解決するには、一度に一定数の StorageFiles を作成し、それらを処理して UI を作成してから、メモリを解放します。 

この例では、[StorageFileQueryResult.GetFilesAsync(UInt32 StartIndex, UInt32 maxNumberOfItems)](/uwp/api/windows.storage.search.storagefilequeryresult.getfilesasync) を使用して、一度に 100 個のファイルのみをフェッチして、こうした問題に対処しています。 この処理の次にアプリでファイルが処理され、その後で OS がメモリーを解放できるようにしています。 この方法では、アプリの最大メモリが制限され、システムは応答性を維持します。 もちろん、実施するシナリオで返されるファイルの数は調整する必要がありますが、すべてのユーザーに対して応答性の高いエクスペリエンスを確保するために、一度にフェッチするファイルの数は 500 未満にすることをお勧めします。


**例**  
```csharp
StorageFolder folderToEnumerate = KnownFolders.PicturesLibrary; 
// Check if the folder is indexed before doing anything. 
IndexedState folderIndexedState = await folderToEnumerate.GetIndexedStateAsync(); 
if (folderIndexedState == IndexedState.NotIndexed || folderIndexedState == IndexedState.Unknown) 
{ 
    // Only possible in indexed directories.  
    return; 
} 
 
QueryOptions picturesQuery = new QueryOptions() 
{ 
    FolderDepth = FolderDepth.Deep, 
    // Filter out all files that have WIP enabled
    ApplicationSearchFilter = "System.Security.EncryptionOwners:[]", 
    IndexerOption = IndexerOption.OnlyUseIndexerAndOptimizeForIndexedProperties 
}; 

picturesQuery.FileTypeFilter.Add(".jpg"); 
string[] otherProperties = new string[] 
{ 
    SystemProperties.GPS.LatitudeDecimal, 
    SystemProperties.GPS.LongitudeDecimal 
}; 
 
picturesQuery.SetPropertyPrefetch(PropertyPrefetchOptions.BasicProperties | PropertyPrefetchOptions.ImageProperties, 
                                    otherProperties); 
SortEntry sortOrder = new SortEntry() 
{ 
    AscendingOrder = true, 
    PropertyName = "System.FileName" // FileName property is used as an example. Any property can be used here.  
}; 
picturesQuery.SortOrder.Add(sortOrder); 
 
// Create the query and get the results 
uint index = 0; 
const uint stepSize = 100; 
if (!folderToEnumerate.AreQueryOptionsSupported(picturesQuery)) 
{ 
    log("Querying for a sort order is not supported in this location"); 
    picturesQuery.SortOrder.Clear(); 
} 
StorageFileQueryResult queryResult = folderToEnumerate.CreateFileQueryWithOptions(picturesQuery); 
IReadOnlyList<StorageFile> images = await queryResult.GetFilesAsync(index, stepSize); 
while (images.Count != 0 || index < 10000) 
{ 
    foreach (StorageFile file in images) 
    { 
        // With the OnlyUseIndexerAndOptimizeForIndexedProperties set, this won't  
        // be async. It will run synchronously. 
        var imageProps = await file.Properties.GetImagePropertiesAsync(); 
 
        // Build the UI 
        log(String.Format("{0} at {1}, {2}", 
                    file.Path, 
                    imageProps.Latitude, 
                    imageProps.Longitude)); 
    } 
    index += stepSize; 
    images = await queryResult.GetFilesAsync(index, stepSize); 
} 
```

### <a name="results"></a>結果 
結果として生成される StorageFile ファイルには要求したプロパティのみが含まれますが、他の IndexerOptions と比較して、10 倍速く結果が返されます。 アプリでは、クエリにまだ含まれていないプロパティへのアクセスを要求できますが、ファイルを開き、それらのプロパティを取得するとパフォーマンス ペナルティが発生します。  

## <a name="adding-folders-to-libraries"></a>フォルダーをライブラリに追加する 
アプリでは、[StorageLibrary.RequestAddFolderAsync](/uwp/api/Windows.Storage.StorageLibrary.RequestAddFolderAsync) を使用して、ファイルの場所をインデックスに追加するよう、ユーザーに対して要求することができます。 場所が追加されると、自動的にインデックスが作成されます。アプリはこの方法を使用してファイルを列挙することができます。
 
## <a name="see-also"></a>関連項目
[QueryOptions API リファレンス](/uwp/api/windows.storage.search.queryoptions)  
[ファイルとフォルダーの列挙と照会](./quickstart-listing-files-and-folders.md)  
[ファイル アクセス許可](./file-access-permissions.md)  
 
 