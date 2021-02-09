---
description: ユーザー画像を利用できる場合はユーザーのアバター画像を表示します。利用できない場合は、ユーザーの頭文字か汎用アイコンを表示します。
title: ユーザー画像コントロール
template: detail.hbs
label: Parallax View
ms.date: 09/24/2020
ms.topic: article
keywords: windows 10, uwp
pm-contact: trestar
design-contact: kimsea
dev-contact: kefodero
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: ee8d78b38c05483f127571b15e1f4ebfb267c331
ms.sourcegitcommit: 4f032d7bb11ea98783db937feed0fa2b6f9950ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91829432"
---
# <a name="person-picture-control"></a>ユーザー画像コントロール

ユーザー画像コントロールは、ユーザー画像を利用できる場合はユーザーのアバター画像を表示します。利用できない場合は、ユーザーの頭文字か汎用アイコンを表示します。 このコントロールを使うと、ユーザーの連絡先情報を管理するオブジェクトである [Contact オブジェクト](/uwp/api/Windows.ApplicationModel.Contacts.Contact)を表示できます。また、表示名やプロフィール画像などの連絡先情報は手動で提供することもできます。

![ユーザー画像コントロールのスクリーンショット。](images/person-picture/person-picture_hero.png)

 > ユーザーの名前を表示する 2 つの[テキスト ブロック](text-block.md)要素が付属している 2 つのユーザー画像コントロール。

**Windows UI ライブラリを入手する**

:::row:::
   :::column:::
      ![WinUI ロゴ](images/winui-logo-64x64.png)
   :::column-end:::
   :::column span="3":::
      **PersonPicture** コントロールは、Windows アプリのための新しいコントロールと UI 機能を含む NuGet パッケージである Windows UI ライブラリの一部として含まれています。 インストール手順などについて詳しくは、「[Windows UI Library (Windows UI ライブラリ)](/uwp/toolkits/winui/)」をご覧ください。
   :::column-end:::
   :::column:::

   :::column-end:::
:::row-end:::

> **プラットフォーム API**: [PersonPicture クラス](/uwp/api/windows.ui.xaml.controls.personpicture)、[Contact クラス](/uwp/api/Windows.ApplicationModel.Contacts.Contact)、[ContactManager クラス](/uwp/api/Windows.ApplicationModel.Contacts.ContactManager)

## <a name="is-this-the-right-control"></a>これは適切なコントロールですか?

ユーザーと連絡先情報を表示するときはユーザー画像を使います。 このコントロールの使用例をいくつか紹介します。

* 現在のユーザーを表示する
* アドレス帳の連絡先を表示する
* メッセージの送信者を表示する
* ソーシャル メディアの連絡先を表示する

この図では、連絡先リストのユーザー画像コントロールを示しています。![連絡先リストのユーザー画像コントロールを示すスクリーンショット。](images/person-picture/person-picture-control.png)

## <a name="examples"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-app-icon-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/PersonPicture">アプリを開き、PersonPicture の動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

## <a name="how-to-use-the-person-picture-control"></a>ユーザー画像コントロールの使用方法

ユーザー画像を作成するには、PersonPicture クラスを使用します。 この例では、PersonPicture コントロールを作成し、ユーザーの表示名、プロフィール画像、および頭文字を手動で提供します。

```xaml
<Page
    x:Class="App2.ExamplePage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:App2"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <PersonPicture
            DisplayName="Betsy Sherman"
            ProfilePicture="Assets\BetsyShermanProfile.png"
            Initials="BS" />
    </StackPanel>
</Page>
```

## <a name="using-the-person-picture-control-to-display-a-contact-object"></a>ユーザー画像コントロールを使用して、Contact オブジェクトを表示する

ユーザー選択コントロールを使用して、[Contact](/uwp/api/Windows.ApplicationModel.Contacts.Contact) オブジェクトを表示できます。

```xaml
<Page
    x:Class="SampleApp.PersonPictureContactExample"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:SampleApp"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

        <PersonPicture
            Contact="{x:Bind CurrentContact, Mode=OneWay}" />

        <Button Click="LoadContactButton_Click">Load contact</Button>
    </StackPanel>
</Page>
```

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Runtime.InteropServices.WindowsRuntime;
using Windows.Foundation;
using Windows.Foundation.Collections;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Primitives;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Navigation;
using Windows.ApplicationModel.Contacts;

namespace SampleApp
{
    public sealed partial class PersonPictureContactExample : Page, System.ComponentModel.INotifyPropertyChanged
    {
        public PersonPictureContactExample()
        {
            this.InitializeComponent();
        }

        private Windows.ApplicationModel.Contacts.Contact _currentContact;
        public Windows.ApplicationModel.Contacts.Contact CurrentContact
        {
            get => _currentContact;
            set
            {
                _currentContact = value;
                PropertyChanged?.Invoke(this,
                    new System.ComponentModel.PropertyChangedEventArgs(nameof(CurrentContact)));
            }

        }
        public event System.ComponentModel.PropertyChangedEventHandler PropertyChanged;

        public static async System.Threading.Tasks.Task<Windows.ApplicationModel.Contacts.Contact> CreateContact()
        {

            var contact = new Windows.ApplicationModel.Contacts.Contact();
            contact.FirstName = "Betsy";
            contact.LastName = "Sherman";

            // Get the app folder where the images are stored.
            var appInstalledFolder =
                Windows.ApplicationModel.Package.Current.InstalledLocation;
            var assets = await appInstalledFolder.GetFolderAsync("Assets");
            var imageFile = await assets.GetFileAsync("betsy.png");
            contact.SourceDisplayPicture = imageFile;

            return contact;
        }

        private async void LoadContactButton_Click(object sender, RoutedEventArgs e)
        {
            CurrentContact = await CreateContact();
        }
    }
}
```

> [!NOTE]
> コードを簡潔にするために、この例では新しい Contact オブジェクトを作成しています。 実際のアプリでは、ユーザーに連絡先を選択してもらうか、[ContactManager](/uwp/api/Windows.ApplicationModel.Contacts.ContactManager) を使用して連絡先リストを照会します。 連絡先の取得と管理については、[連絡先とカレンダーの記事](../../contacts-and-calendar/index.md)をご覧ください。

## <a name="determining-which-info-to-display"></a>表示する情報の決定

[Contact](/uwp/api/Windows.ApplicationModel.Contacts.Contact) オブジェクトを指定すると、ユーザー画像コントロールによってそのオブジェクトが評価され、表示できる情報が判断されます。

画像を利用できる場合、コントロールでは次の優先順位で最初に見つかった画像が表示されます。

1. LargeDisplayPicture
1. SmallDisplayPicture
1. サムネイル

選択される画像は、PreferSmallImage プロパティを true に設定することで変更できます。このように設定すると、SmallDisplayPicture の優先順位が LargeDisplayPicture よりも高くなります。

画像がない場合、コントロールは連絡先の名前か頭文字を表示します。名前のデータがない場合、コントロールはメール アドレスや電話番号などの連絡先データ表示します。

## <a name="get-the-sample-code"></a>サンプル コードを入手する

- [XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。

## <a name="related-articles"></a>関連記事

* [連絡先とカレンダー](../../contacts-and-calendar/index.md)
* [連絡先カードのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ContactCards)
