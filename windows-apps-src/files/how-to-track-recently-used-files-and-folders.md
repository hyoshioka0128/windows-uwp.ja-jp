---
ms.assetid: BF929A68-9C82-4866-BC13-A32B3A550005
title: 最近使ったファイルやフォルダーの追跡
description: ユーザーが頻繁にアクセスするファイルを追跡するには、そのファイルを最近使ったアプリの一覧 (MRU) に追加します。
ms.date: 12/19/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 97ad2485abab0bd4733699bc4ffcf29e17a22844
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66369447"
---
# <a name="track-recently-used-files-and-folders"></a>最近使ったファイルやフォルダーの追跡

**重要な API**

- [**MostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.mostrecentlyusedlist)
- [**FileOpenPicker**](https://docs.microsoft.com/uwp/schemas/appxpackage/appxmanifestschema/element-fileopenpicker)

ユーザーが頻繁にアクセスするファイルを追跡するには、そのファイルを最近使ったアプリの一覧 (MRU) に追加します。 MRU はプラットフォームが管理し、最後にアクセスした日時に基づいて項目を並べ替えたり、一覧の上限である 25 項目に達したら最も古い項目を削除したりします。 すべてのアプリにはそれぞれに専用の MRU があります。

お使いのアプリの MRU は、静的な [**StorageApplicationPermissions.MostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.mostrecentlyusedlist) プロパティから取得する [**StorageItemMostRecentlyUsedList**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageItemMostRecentlyUsedList) クラスによって表されます。 MRU の項目は [**IStorageItem**](https://docs.microsoft.com/uwp/api/Windows.Storage.IStorageItem) オブジェクトとして格納されます。つまり、[**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) オブジェクト (ファイルを表すオブジェクト) と [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) オブジェクト (フォルダーを表すオブジェクト) は、どちらも MRU に追加できます。

> [!NOTE]
> 完全なサンプルは、次を参照してください。、[ファイル ピッカー サンプル](https://go.microsoft.com/fwlink/p/?linkid=619994)と[ファイル アクセス サンプル](https://go.microsoft.com/fwlink/p/?linkid=619995)します。

## <a name="prerequisites"></a>前提条件

-   **ユニバーサル Windows プラットフォーム (UWP) アプリの非同期プログラミングを理解します。**

    C# や Visual Basic での非同期アプリの作成方法については、「[C# または Visual Basic での非同期 API の呼び出し](https://docs.microsoft.com/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic)」をご覧ください。 C++ での非同期アプリの作成方法については、「[C++ での非同期プログラミング](https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-in-cpp-universal-windows-platform-apps)」をご覧ください。

-   **場所へのアクセス許可**

    「[ファイル アクセス許可](file-access-permissions.md)」をご覧ください。

-   [ピッカーでファイルやフォルダーを開く](quickstart-using-file-and-folder-pickers.md)

    ユーザーは同じファイルを何度も選ぶ傾向にあります。

 ## <a name="add-a-picked-file-to-the-mru"></a>MRU に選んだファイルを追加する

-   ユーザーは同じファイルを繰り返し選ぶ傾向にあります。 そのため、選んだファイルはできるだけ早くアプリの MRU に追加することを検討してください。 以下にその方法を示します。

    ```cs
    Windows.Storage.StorageFile file = await picker.PickSingleFileAsync();

    var mru = Windows.Storage.AccessCache.StorageApplicationPermissions.MostRecentlyUsedList;
    string mruToken = mru.Add(file, "profile pic");
    ```

    [**StorageItemMostRecentlyUsedList.Add** ](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add)はオーバー ロードされます。 この例では [**Add(IStorageItem, String)** ](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add) を使って、メタデータをファイルに関連付けられるようにしています。 メタデータを設定すると、その項目の目的 ("プロファイル画像" など) を記録できます。 メタデータなしで MRU にファイルを追加するには、[**Add(IStorageItem)** ](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.add) を呼び出します。 MRU に項目を追加すると、項目を取得するときに使われる一意に識別するための文字列であるトークンが返されます。

> [!TIP]
> 項目を MRU から取得するにはそのトークンが必要であるため、どこかに保存しておいてください。 アプリ データの詳細については、「[アプリケーション データの管理](https://docs.microsoft.com/previous-versions/windows/apps/hh465109(v=win.10))」をご覧ください。

## <a name="use-a-token-to-retrieve-an-item-from-the-mru"></a>トークンを使って MRU から項目を取得する

取得する項目に最適な取得メソッドを使います。

-   ファイルを [**StorageFile**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFile) として取得するには [**GetFileAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getfileasync) を使います。
-   フォルダーを [**StorageFolder**](https://docs.microsoft.com/uwp/api/Windows.Storage.StorageFolder) として取得するには [**GetFolderAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getfolderasync) を使います。
-   ファイルかフォルダーを表す汎用の [**IStorageItem**](https://docs.microsoft.com/uwp/api/Windows.Storage.IStorageItem) を取得するには [**GetItemAsync**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.getitemasync) を使います。

先ほど追加したファイルを取得する方法は次のとおりです。

```cs
StorageFile retrievedFile = await mru.GetFileAsync(mruToken);
```

すべてのエントリを反復処理してトークンを取得した後に項目を取得する方法は次のとおりです。

```cs
foreach (Windows.Storage.AccessCache.AccessListEntry entry in mru.Entries)
{
    string mruToken = entry.Token;
    string mruMetadata = entry.Metadata;
    Windows.Storage.IStorageItem item = await mru.GetItemAsync(mruToken);
    // The type of item will tell you whether it's a file or a folder.
}
```

[  **AccessListEntryView**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.AccessListEntryView) を使うと MRU 内のエントリを反復処理できます。 これらのエントリは、項目のトークンとメタデータが格納された [**AccessListEntry**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.AccessListEntry) 構造体です。

## <a name="removing-items-from-the-mru-when-its-full"></a>空きのない MRU から項目を削除する

MRU の上限である 25 項目に達している場合、新しい項目を追加しようとすると、最後にアクセスしてからの経過時間が最も長い項目が自動的に削除されます。 そのため、新しい項目を追加する前に項目を削除する必要はありません。

## <a name="future-access-list"></a>後でアクセスする一覧

アプリには MRU のほか、後でアクセスする一覧もあります。 ファイルやフォルダーを選ぶことで、ユーザーはアプリがアクセスできない可能性がある項目にアクセス許可を付与します。 これらの項目を後でアクセスする一覧に追加すると、後にそれらの項目にアプリがアクセスする場合に備えてアクセス許可が保持されます。 お使いのアプリの、後でアクセスする一覧は、静的な [**StorageApplicationPermissions.FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) プロパティから取得する [**StorageItemAccessList**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageItemAccessList) クラスによって表されます。

ユーザーが項目を選ぶ際には、MRU のほか、後でアクセスする一覧にも追加することを検討してください。

-   [  **FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) は最大 1,000 項目を保持できます。 ファイル以外にもフォルダーを保持できるため、大量のフォルダーがあることにご注意ください。
-   プラットフォームによって [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) から項目が削除されることはありません。 項目の数が上限の 1,000 に到達した場合、[**Remove**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageitemmostrecentlyusedlist.remove) メソッドで空きを確保するまで項目を追加できません。
