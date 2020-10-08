---
description: 連絡先カードを使用して、ユーザーが名前、電話番号、住所などの連絡先情報を表示および編集できるようにする方法について説明します。
title: 連絡先カード
ms.date: 09/24/2020
ms.topic: article
keywords: windows 10, uwp
pm-contact: kele
design-contact: tbd
dev-contact: tbd
doc-status: not-published
ms.localizationpriority: medium
ms.openlocfilehash: d31c1a22260b8d98e767fba6b6d6e0db20fdbbb8
ms.sourcegitcommit: 4f032d7bb11ea98783db937feed0fa2b6f9950ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91829601"
---
# <a name="contact-card"></a>連絡先カード

連絡先カードには、[Contact](/uwp/api/Windows.ApplicationModel.Contacts.Contact) (個人や企業を表すために Windows によって使用されるメカニズム) で使用されている名前、電話番号、住所などの連絡先情報が表示されます。  連絡先カードを使用して、ユーザーは連絡先情報を編集することもできます。 コンパクトな連絡先カードを表示するか、追加の情報を含む完全な連絡先カードを表示することができます。

> **重要な API**:[ShowContactCard メソッド](/uwp/api/windows.applicationmodel.contacts.contactmanager.showcontactcard)、[ShowFullContactCard メソッド](/uwp/api/windows.applicationmodel.contacts.contactmanager.showfullcontactcard)、[IsShowContactCardSupported メソッド](/uwp/api/windows.applicationmodel.contacts.contactmanager.IsShowContactCardSupported)、[Contact クラス](/uwp/api/Windows.ApplicationModel.Contacts.Contact)  

連絡先カードを表示する方法は 2 つあります。  
* 簡易非表示に対応したポップアップに表示される標準的な連絡先カード -- ユーザーが連作先カードの外部をクリックすると、連絡先カードは消えます。 
* 多くのスペースを使用し、簡易非表示に対応していない完全な連絡先カード -- 閉じるにはユーザーが **[閉じる]** をクリックする必要があります。 


<figure>
    <img src="images/contact-card/contact-card-standard.png" alt="Screenshot showing a standard contact card.">
    <figcaption>標準の連絡先カード</figcaption>
</figure>

<figure>
    <img src="images/contact-card/contact-card-full.png" alt="Screenshot showing a full contact card.">
    <figcaption>完全な連絡先カード</figcaption>
</figure>


## <a name="is-this-the-right-control"></a>これは適切なコントロールですか?

連絡先の連絡先情報を表示する場合は、連絡先カードを使用します。 連絡先の名前と画像のみを表示する場合は、[ユーザー画像コントロール](person-picture.md) を使用します。 


<!-- TODO: Add examples back when the contact card has been added. -->

<!-- ## Examples

<table>
<th align="left">XAML Controls Gallery<th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p>If you have the <strong style="font-weight: semi-bold">XAML Controls Gallery</strong> app installed, click here to <a href="xamlcontrolsgallery:/item/Button">open the app and see the Button in action</a>.</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></li>
    </ul>
</td>
</tr>
</table> -->

## <a name="show-a-standard-contact-card"></a>標準の連絡先カードの表示

1. 通常、ユーザーが何らかのボタンや場合によって [ユーザー画像コントロール](person-picture.md) をクリックしたときに、連絡先カードが表示されます。 要素は非表示にされません。 非表示にされないようにするには、要素の位置情報やサイズについて記述した [Rect](/uwp/api/windows.foundation.rect) を作成する必要があります。 

    これを実行するユーティリティ関数を作成しましょう。このユーティリティ関数は後で使用します。
    ```csharp
    // Gets the rectangle of the element 
    public static Rect GetElementRectHelper(FrameworkElement element) 
    { 
        // Passing "null" means set to root element. 
        GeneralTransform elementTransform = element.TransformToVisual(null); 
        Rect rect = elementTransform.TransformBounds(new Rect(0, 0, element.ActualWidth, element.ActualHeight)); 
        return rect; 
    } 

    ```

2. [ContactManager.IsShowContactCardSupported](/uwp/api/windows.applicationmodel.contacts.contactmanager.IsShowContactCardSupported) メソッドを呼び出して連絡先カードを表示できるかどうかを確認します。 サポートされていない場合は、エラー メッセージが表示されます。 (この例では、クリック イベントに応じて連絡先カードが表示されることを前提としています)
    ```csharp
    // Contact and Contact Managers are existing classes 
    private void OnUserClickShowContactCard(object sender, RoutedEventArgs e) 
    { 
        if (ContactManager.IsShowContactCardSupported()) 
        { 

    ```

3. 手順 1 で作成したユーティリティ関数を使用して、イベントを発生させたコントロールの境界を取得します (連絡先カードで非表示にされません)。

    ```csharp
            Rect selectionRect = GetElementRect((FrameworkElement)sender); 
    ```

4. 表示する [Contact](//docs.microsoft.com/uwp/api/Windows.ApplicationModel.Contacts.Contact) オブジェクトを取得します。 この例では、単に連絡先を作成しますが、コードでは実際の連絡先を取得する必要があります。 

    ```csharp
                // Retrieve the contact to display
                var contact = new Contact(); 
                var email = new ContactEmail(); 
                email.Address = "jsmith@contoso.com"; 
                contact.Emails.Add(email); 
    ```
5. 連絡先カードを表示するには [ShowContactCard](/uwp/api/windows.applicationmodel.contacts.contactmanager.showcontactcard) メソッドを呼び出します。 

    ```csharp
            ContactManager.ShowFullContactCard(
                contact, selectionRect, Placement.Default); 
        } 
    } 
    ```

コード例の全体を次に示します。

```csharp
// Gets the rectangle of the element 
public static Rect GetElementRect(FrameworkElement element) 
{ 
    // Passing "null" means set to root element. 
    GeneralTransform elementTransform = element.TransformToVisual(null); 
    Rect rect = elementTransform.TransformBounds(new Rect(0, 0, element.ActualWidth, element.ActualHeight)); 
    return rect; 
} 
 
// Display a contact in response to an event
private void OnUserClickShowContactCard(object sender, RoutedEventArgs e) 
{ 
    if (ContactManager.IsShowContactCardSupported()) 
    { 
        Rect selectionRect = GetElementRect((FrameworkElement)sender);

        // Retrieve the contact to display
        var contact = new Contact(); 
        var email = new ContactEmail(); 
        email.Address = "jsmith@contoso.com"; 
        contact.Emails.Add(email); 
    
        ContactManager.ShowContactCard(
            contact, selectionRect, Placement.Default); 
    } 
} 

```

## <a name="show-a-full-contact-card"></a>完全な連絡先カードの表示

完全な連絡先カードを表示するには、[ShowContactCard](/uwp/api/windows.applicationmodel.contacts.contactmanager.showcontactcard) メソッドではなく [ShowFullContactCard](/uwp/api/windows.applicationmodel.contacts.contactmanager.showfullcontactcard) メソッドを呼び出します。

```csharp
private void onUserClickShowContactCard() 
{ 
   
    Contact contact = new Contact(); 
    ContactEmail email = new ContactEmail(); 
    email.Address = "jsmith@hotmail.com"; 
    contact.Emails.Add(email); 
 
 
    // Setting up contact options.     
    FullContactCardOptions fullContactCardOptions = new FullContactCardOptions(); 
 
    // Display full contact card on mouse click.   
    // Launch the People’s App with full contact card  
    fullContactCardOptions.DesiredRemainingView = ViewSizePreference.UseLess; 
     
 
    // Shows the full contact card by launching the People App. 
    ContactManager.ShowFullContactCard(contact, fullContactCardOptions); 
} 

```

## <a name="retrieving-real-contacts"></a>"実際の” 連絡先の取得

この記事の例では、単純な連絡先を作成します。 実際のアプリでは、おそらく既存の連絡先を取得します。 手順については、[連絡先とカレンダーの記事](../../contacts-and-calendar/index.md)をご覧ください。




## <a name="related-articles"></a>関連記事
- [連絡先とカレンダー](../../contacts-and-calendar/index.md)
- [連絡先カードのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/ContactCards)
- [ユーザー画像コントロール](/windows/uwp/controls-and-patterns/person-picture/)
