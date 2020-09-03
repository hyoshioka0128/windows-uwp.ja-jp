---
ms.assetid: CAC6A7C7-3348-4EC4-8327-D47EB6E0C238
title: SD カードへのアクセス
description: オプションの microSD カード上にある重要度の低いデータに保存およびアクセスできます (特に内部ストレージに制限がある低コストのモバイル デバイス)。
ms.date: 03/08/2017
ms.topic: article
keywords: Windows 10, UWP, SD カード, ストレージ
ms.localizationpriority: medium
ms.openlocfilehash: d41eb13bd153206f6140d869fa19558725bbc94b
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89163196"
---
# <a name="access-the-sd-card"></a>SD カードへのアクセス



オプションの microSD カードに重要度の低いデータを保存したり、これらのデータにアクセスしたりすることができます (特に内部ストレージに制限があり、microSD カード用のスロットがある低コストのモバイル デバイスの場合)。

ほとんどの場合、アプリで SD カード上のファイルの保存とアクセスを行うには、アプリ マニフェスト ファイルで **removableStorage** 機能を指定する必要があります。 通常、アプリから保存したりアクセスしたりするファイルの種類を処理対象として登録することも必要です。

次の方法を使って、オプションの SD カードに対してファイルの保存とアクセスを行うことができます。
- ファイル ピッカー
- [  **Windows.Storage**](/uwp/api/Windows.Storage) API

## <a name="what-you-can-and-cant-access-on-the-sd-card"></a>SD カードでアクセスできるデータとアクセスできないデータ

### <a name="what-you-can-access"></a>アクセスできるデータ

- アプリでファイルの読み取りと書き込みを実行するには、そのファイルの種類が処理対象となるように、アプリでアプリ マニフェスト ファイルに登録する必要があります。
- アプリでは、フォルダーの作成と管理も実行できます。

### <a name="what-you-cant-access"></a>アクセスできないデータ

- アプリでは、システム フォルダーとそのフォルダー内のファイルを参照したり、アクセスしたりすることはできません。
- 隠し属性でマークされたファイルを参照することはできません。 通常、隠し属性は、データを誤って削除するというリスクを減らすために使われます。
- [  **KnownFolders.DocumentsLibrary**](/uwp/api/windows.storage.knownfolders.documentslibrary) を使ってドキュメント ライブラリを参照したり、ドキュメント ライブラリにアクセスしたりすることはできません。 ただしファイル システムを走査することによって、SD カード上のドキュメント ライブラリにアクセスすることはできます。

## <a name="security-and-privacy-considerations"></a>セキュリティとプライバシーに関する考慮事項

アプリが SD カードのグローバルな場所にファイルを保存する場合、それらのファイルは暗号化されないため、通常は他のアプリからアクセスすることができます。

- SD カードがデバイスに挿入されている間、SD カード上のファイルは、同じファイルの種類を処理対象として登録している他のアプリからアクセスすることができます。
- SD カードをデバイスから取り外し、PC で開くと、ファイルはエクスプローラーに表示されるため、他のアプリからアクセスすることができます。

アプリを SD カードにインストールし、ファイルを SD カードの [**LocalFolder**](/uwp/api/windows.storage.applicationdata.localfolder) に保存する場合、それらのファイルは暗号化されるため、他のアプリからアクセスすることはできません。

## <a name="requirements-for-accessing-files-on-the-sd-card"></a>SD カード上のファイルへアクセスするための要件

SD カードのファイルにアクセスするには通常、次のことを指定する必要があります。

1.  アプリ マニフェスト ファイルで **removableStorage** 機能を指定する必要があります。
2.  また、アクセスするメディアの種類に関連付けられたファイル拡張子を処理対象として登録する必要があります。

**KnownFolders.MusicLibrary** などの既知のフォルダーを参照せずに SD カード上のメディア ファイルにアクセスしたり、メディア ライブラリ フォルダーの外部に格納されているメディア ファイルにアクセスしたりするに場合にも、上記の方法を使います。

ミュージック、写真、ビデオなどのメディア ライブラリに格納されているメディア ファイルに既知のフォルダーを使ってアクセスする場合は、関連付けられている機能 (**musicLibrary**、**picturesLibrary**、**videoLibrary**) をアプリ マニフェスト ファイルで指定するだけで十分です。 **removableStorage** 機能を指定する必要はありません。 詳しくは、「[ミュージック、画像、およびビデオ ライブラリのファイルとフォルダー](quickstart-managing-folders-in-the-music-pictures-and-videos-libraries.md)」をご覧ください。

## <a name="accessing-files-on-the-sd-card"></a>SD カード上のファイルへのアクセス

### <a name="getting-a-reference-to-the-sd-card"></a>SD カードへの参照の取得

[  **KnownFolders.RemovableDevices**](/uwp/api/windows.storage.knownfolders.removabledevices) フォルダーは、デバイスに現在接続されている一連のリムーバブル デバイスに対する論理ルートである [**StorageFolder**](/uwp/api/Windows.Storage.StorageFolder) です。 SD カードが取り付けられている場合は、**KnownFolders.RemovableDevices** フォルダーの下にある、最初の (唯一の) **StorageFolder** が SD カードを表します。

次のようなコードを使って、SD カードが存在するかどうかを判断し、SD カードへの参照を [**StorageFolder**](/uwp/api/Windows.Storage.StorageFolder) として取得します。

```csharp
using Windows.Storage;

// Get the logical root folder for all external storage devices.
StorageFolder externalDevices = Windows.Storage.KnownFolders.RemovableDevices;

// Get the first child folder, which represents the SD card.
StorageFolder sdCard = (await externalDevices.GetFoldersAsync()).FirstOrDefault();

if (sdCard != null)
{
    // An SD card is present and the sdCard variable now contains a reference to it.
}
else
{
    // No SD card is present.
}
```

> [!NOTE]
> SD カード リーダーが内蔵のリーダー (ノート PC や PC のスロットなど) である場合、KnownFolders.RemovableDevices によってアクセスできない場合があります。

### <a name="querying-the-contents-of-the-sd-card"></a>SD カードのコンテンツの照会

SD カードには、既知のフォルダーとして認識されないさまざまなフォルダーやファイルを含めることができますが、[**KnownFolders**](/uwp/api/Windows.Storage.KnownFolders) の場所の情報を使って照会することはできません。 ファイルを検索するには、アプリでファイル システムを再帰的に走査して、SD カードのコンテンツを列挙する必要があります。 SD カードのコンテンツを効率的に取得するには、[**GetFilesAsync (CommonFileQuery.DefaultQuery)** ](/uwp/api/windows.storage.storagefolder.getfilesasync) と [**GetFoldersAsync (CommonFolderQuery.DefaultQuery)** ](/uwp/api/windows.storage.storagefolder.getfoldersasync) を使います。

SD カードを走査するにはバックグラウンド スレッドを使うことをお勧めします。 SD カードには、かなりのギガバイト数のデータを格納できる場合があります。

また、アプリでは、ユーザーに対してフォルダー ピッカーを使って特定のフォルダーを選ぶように要求することもできます。

[  **KnownFolders.RemovableDevices**](/uwp/api/windows.storage.knownfolders.removabledevices) から取得したパスを使って SD カード上のファイル システムにアクセスした場合のメソッドの動作を次に示します。

-   [  **GetFilesAsync**](/uwp/api/windows.storage.storagefolder.getfilesasync) メソッドは、処理対象として登録したファイル拡張子と、指定したメディア ライブラリ機能に関連付けられているファイル拡張子との和集合を返します。
-   アクセスしようとするファイルの拡張子を処理対象として登録しなかった場合、[**GetFileFromPathAsync**](/uwp/api/windows.storage.storagefile.getfilefrompathasync) メソッドは失敗します。

## <a name="identifying-the-individual-sd-card"></a>個々の SD カードの識別

SD カードが最初にマウントされると、オペレーティング システムによって、そのカードの一意の識別子が生成されます。 この ID は、カードのルートにある WPSystem フォルダー内のファイルに格納されます。 アプリはこの ID を使って、カードを認識できるかどうかを判断することができます。 カードがアプリによって認識されると、アプリでは、既に完了している特定の操作を後で実行できる場合があります。 ただし、アプリが前回カードにアクセスした以降、カードのコンテンツが変更されている可能性があります。

たとえば、電子ブックにインデックスを付けるアプリについて考えてみましょう。 アプリが以前に SD カード全体を走査して電子ブックのファイルを探し、電子ブックのインデックスを作成した場合、カードをもう一度挿入し、アプリがカードを認識すると、直ちにインデックスの一覧を表示できます。 これとは別に、新しい電子ブックを検索する優先度の低いバックグラウンド スレッドを開始することもできます。 また、削除された電子ブックへアクセスしようとしたとき、以前に存在していた電子ブックが見つからなかった場合のエラーを処理することもできます。

この ID を含むプロパティの名前は、**WindowsPhone.ExternalStorageId** です。

```csharp
using Windows.Storage;

// Get the logical root folder for all external storage devices.
StorageFolder externalDevices = Windows.Storage.KnownFolders.RemovableDevices;

// Get the first child folder, which represents the SD card.
StorageFolder sdCard = (await externalDevices.GetFoldersAsync()).FirstOrDefault();

if (sdCard != null)
{
    var allProperties = sdCard.Properties;
    IEnumerable<string> propertiesToRetrieve = new List<string> { "WindowsPhone.ExternalStorageId" };

    var storageIdProperties = await allProperties.RetrievePropertiesAsync(propertiesToRetrieve);

    string cardId = (string)storageIdProperties["WindowsPhone.ExternalStorageId"];

    if (...) // If cardID matches the cached ID of a recognized card.
    {
        // Card is recognized. Index contents opportunistically.
    }
    else
    {
        // Card is not recognized. Index contents immediately.
    }
}
```

 

 