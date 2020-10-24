---
title: URI のアクティブ化の処理
description: URI (Uniform Resource Identifier) スキーム名の既定のハンドラーとしてアプリを登録する方法について説明します。
ms.assetid: 92D06F3E-C8F3-42E0-A476-7E94FD14B2BE
ms.date: 07/05/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 9a9d3c073bdfc23511728825a0defac790ae6623
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89167886"
---
# <a name="handle-uri-activation"></a>URI のアクティブ化の処理

**重要な API**

-   [**Windows.ApplicationModel.Activation.ProtocolActivatedEventArgs**](/uwp/api/Windows.ApplicationModel.Activation.ProtocolActivatedEventArgs)
-   [**Windows.UI.Xaml.Application.OnActivated**](/uwp/api/windows.ui.xaml.application.onactivated)

URI (Uniform Resource Identifier) スキーム名の既定のハンドラーとしてアプリを登録する方法について説明します。 Windows デスクトップ アプリとユニバーサル Windows プラットフォーム (UWP) アプリの両方を、URI スキーム名の既定のハンドラーとして登録できます。 アプリを URI スキーム名の既定のハンドラーとして選ぶと、アプリはその種類の URI を起動するたびにアクティブ化されます。

URI スキーム名に登録するのは、その種類の URI スキームのすべての URI 起動を処理する場合のみにすることをお勧めします。 URI スキーム名に登録する場合は、その URI スキームのためにアプリをアクティブ化した際に期待される機能をエンド ユーザーに提供する必要があります。 たとえば、mailto: URI スキーム名に登録したアプリでは、新しいメールを開いて、ユーザーが新しいメールを書くことができるようにする必要があります。 URI の関連付けについて詳しくは、「[ファイルの種類と URI のガイドラインとチェック リスト](../files/index.md)」をご覧ください。

以下の手順では、カスタムの URI スキーム名 `alsdk://` を登録する方法と、ユーザーによって `alsdk://` URI が起動されたときにアプリをアクティブ化する方法について説明します。

> [!NOTE]
> UWP アプリでは、組み込みアプリとオペレーティングシステムで使用するために、特定の Uri とファイル拡張子が予約されています。 予約されている URI またはファイル拡張子にアプリを登録しようとしても無視されます。 予約または禁止されいるため、UWP アプリを登録できない URI スキームの一覧 (アルファベット順) については、「[予約済みの URI スキーム名とファイルの種類](reserved-uri-scheme-names.md)」をご覧ください。

## <a name="step-1-specify-the-extension-point-in-the-package-manifest"></a>ステップ 1: パッケージ マニフェストに拡張点を指定する

アプリは、パッケージ マニフェストに一覧表示される URI スキーム名のアクティブ化イベントだけを受け取ります。 アプリが `alsdk` URI スキーム名を処理することを示す方法は次のとおりです。

1. **ソリューション エクスプローラー**で、package.appxmanifest をダブルクリックしてマニフェスト デザイナーを開きます。 **[宣言]** タブを選び、**[使用可能な宣言]** ドロップダウンから **[プロトコル]** を選んで **[追加]** をクリックします。

    プロトコルのマニフェスト デザイナーで指定することができる各フィールドについて、以下で簡単に説明します (詳しくは、「[**AppX パッケージ マニフェスト**](/uwp/schemas/appxpackage/uapmanifestschema/element-uap-extension)」をご覧ください)。

| フィールド | 説明 |
|-------|-------------|
| **ロゴ** | **コントロール パネル**の [[既定のプログラムを設定する]](/windows/desktop/shell/default-programs) で URI スキーム名を識別するために使われるロゴを指定します。 ロゴを指定しない場合は、アプリの小さいロゴが使われます。 |
| **表示名** | **コントロール パネル**の [[既定のプログラムを設定する]](/windows/desktop/shell/default-programs) で URI スキーム名を識別するための表示名を指定します。 |
| **名前** | URI スキームの名前を選びます。 |
|  | **注**  名前はすべて小文字である必要があります。 |
|  | **予約および禁止されているファイルの種類** 予約または禁止されいるため、UWP アプリを登録できない URI スキームの一覧 (アルファベット順) については、「[予約済みの URI スキーム名とファイルの種類](reserved-uri-scheme-names.md)」をご覧ください。 |
| **[実行可能ファイル]** | プロトコルの既定の起動実行可能ファイルを指定します。 指定しない場合、アプリの実行可能ファイルが使用されます。 文字列の長さは 1 ~ 256 文字で、末尾には ".exe" を使用する必要があります。また、、、 &gt; &lt; :、"、&#124;、?、または \* の各文字を含めることはできません。 指定した場合、**エントリ ポイント**も使用されます。 **[エントリ ポイント]** を指定しない場合、アプリで定義されているエントリ ポイントが使用されます。 |
| **エントリ ポイント** | プロトコル拡張機能を処理するタスクを指定します。 これは、通常、Windows ランタイムの型の完全な名前空間修飾名です。 指定しない場合、アプリのエントリ ポイントが使用されます。 |
| **スタートページ** | 拡張ポイントを処理する Web ページです。 |
| **リソース グループ** | リソース管理のために拡張機能のアクティブ化をグループ化するために使用できるタグ。 |
| **必要な表示** (Windows のみ) | この URI スキーム名に対して起動されたときにアプリのウィンドウに必要なスペースの量を示すには、**[必要な表示]** フィールドを指定します。 **[必要な表示]** に指定できる値は、**Default**、**UseLess**、**UseHalf**、**UseMore**、または **UseMinimum** です。<br/>**注**  Windows では、ターゲット アプリの最終的なウィンドウ サイズを決定するときに複数の異なる要素が考慮されます。たとえば、ソース アプリの設定、画面上のアプリの数、画面の向きなどです。 **[必要な表示]** を設定しても、ターゲット アプリの特定のウィンドウ動作が保証されるわけではありません。<br/>**モバイルデバイスファミリ:** モバイルデバイスファミリでは、目的のビューがサポートされていません。 |

2. **[ロゴ]** に `images\Icon.png` と入力します。
3. **[表示名]** に `SDK Sample URI Scheme` と入力します。
4. `alsdk`**名前**として「」と入力します。
5. Ctrl + S キーを押して、変更を package.appxmanifest に保存します。

    これにより、次のような [**Extension**](/uwp/schemas/appxpackage/appxmanifestschema/element-1-extension) 要素がパッケージ マニフェストに追加されます。 **windows.protocol** カテゴリは、アプリが `alsdk` URI スキーム名を処理することを示しています。

```xml
    <Applications>
        <Application Id= ... >
            <Extensions>
                <uap:Extension Category="windows.protocol">
                  <uap:Protocol Name="alsdk">
                    <uap:Logo>images\icon.png</uap:Logo>
                    <uap:DisplayName>SDK Sample URI Scheme</uap:DisplayName>
                  </uap:Protocol>
                </uap:Extension>
          </Extensions>
          ...
        </Application>
   <Applications>
```

## <a name="step-2-add-the-proper-icons"></a>ステップ 2: 適切なアイコンを追加する

URI スキーム名の既定となるアプリは、そのアイコンがシステムのさまざまな場所に表示されます。アイコンは、[既定のプログラム] コントロール パネルなどに表示されます。 このため、プロジェクトに 44 x 44 アイコンを含めます。 アプリのタイルのロゴの外観を調和させ、アイコンを透明にするのではなく、アプリの背景色を使います。 パディングせずにロゴを端まで拡張します。 アイコンは、白い背景でテストします。 アイコンの詳細については [、「アプリアイコンとロゴ](../design/style/app-icons-and-logos.md) 」を参照してください。

## <a name="step-3-handle-the-activated-event"></a>ステップ 3: アクティブ化イベントを処理する

[**OnActivated**](/uwp/api/windows.ui.xaml.application.onactivated) イベント ハンドラーは、すべてのファイル アクティブ化イベントを受け取ります。 **Kind** プロパティは、アクティブ化イベントの種類を示しています。 次の例では、[**Protocol**](/uwp/api/Windows.ApplicationModel.Activation.ActivationKind) アクティブ化イベントを処理するように設定されています。

```csharp
public partial class App
{
   protected override void OnActivated(IActivatedEventArgs args)
  {
      if (args.Kind == ActivationKind.Protocol)
      {
         ProtocolActivatedEventArgs eventArgs = args as ProtocolActivatedEventArgs;
         // TODO: Handle URI activation
         // The received URI is eventArgs.Uri.AbsoluteUri
      }
   }
}
```

```vb
Protected Overrides Sub OnActivated(ByVal args As Windows.ApplicationModel.Activation.IActivatedEventArgs)
   If args.Kind = ActivationKind.Protocol Then
      ProtocolActivatedEventArgs eventArgs = args As ProtocolActivatedEventArgs
      
      ' TODO: Handle URI activation
      ' The received URI is eventArgs.Uri.AbsoluteUri
 End If
End Sub
```

```cppwinrt
void App::OnActivated(Windows::ApplicationModel::Activation::IActivatedEventArgs const& args)
{
    if (args.Kind() == Windows::ApplicationModel::Activation::ActivationKind::Protocol)
    {
        auto protocolActivatedEventArgs{ args.as<Windows::ApplicationModel::Activation::ProtocolActivatedEventArgs>() };
        // TODO: Handle URI activation  
        auto receivedURI{ protocolActivatedEventArgs.Uri().RawUri() };
    }
}
```

```cpp
void App::OnActivated(Windows::ApplicationModel::Activation::IActivatedEventArgs^ args)
{
   if (args->Kind == Windows::ApplicationModel::Activation::ActivationKind::Protocol)
   {
      Windows::ApplicationModel::Activation::ProtocolActivatedEventArgs^ eventArgs =
          dynamic_cast<Windows::ApplicationModel::Activation::ProtocolActivatedEventArgs^>(args);
      
      // TODO: Handle URI activation  
      // The received URI is eventArgs->Uri->RawUri
   }
}
```

> [!NOTE]
> プロトコルコントラクトによって起動された場合は、[戻る] ボタンをクリックすると、アプリを起動した画面に戻り、アプリの以前のコンテンツではなくなります。

次のコードでは、プログラムで URI からアプリを起動しています。

```csharp
   // Launch the URI
   var uri = new Uri("alsdk:");
   var success = await Windows.System.Launcher.LaunchUriAsync(uri)
```

URI からアプリを起動する方法について詳しくは、「[URI に応じた既定のアプリの起動](launch-default-app.md)」をご覧ください。

アプリでは、新しいページを開くアクティブ化イベントごとに新しい XAML [**フレーム**](/uwp/api/Windows.UI.Xaml.Controls.Frame) を作成することをお勧めします。 こうすると、新しい XAML **フレーム**のナビゲーション バックスタックに、中断されたときに現在のウィンドウに表示されていた以前のコンテンツが含まれなくなります。 起動コントラクトとファイル コントラクトで単一 XAML **フレーム**を使うことにしたアプリは、新しいページに移動する前に**フレーム**のナビゲーション ジャーナルにあるページをクリアする必要があります。

プロトコルのアクティブ化によって起動されるときは、アプリの先頭ページに戻ることができる UI を含めることを検討してください。

## <a name="remarks"></a>注釈

URI スキーム名は、悪意のあるものも含め、あらゆるアプリや Web サイトから使われる可能性があります。 そのため、その URI で受け取るデータは、信頼できないソースからのデータである可能性があります。 URI で受け取るパラメーターに基づいて永続的な操作を実行しないことをお勧めします。 たとえば、アプリを起動するとユーザーのアカウント ページが表示されるようにするために URI パラメーターを使うことはかまいませんが、ユーザーのアカウントを直接変更するためにプロトコル パラメーターを使うことは行わないことをお勧めします。

> [!NOTE]
> アプリの新しい URI スキーム名を作成する場合は、 [RFC 4395](https://tools.ietf.org/html/rfc4395)のガイダンスに従ってください。 これにより確実に名前が URI スキームの標準に準拠するようになります。

> [!NOTE]
> プロトコルコントラクトによって起動された場合は、[戻る] ボタンをクリックすると、アプリを起動した画面に戻り、アプリの以前のコンテンツではなくなります。

新しい URI ターゲットを開くアクティブ化イベントごとに、アプリで新しい XAML [**フレーム**](/uwp/api/Windows.UI.Xaml.Controls.Frame)を作成することをお勧めします。 こうすると、新しい XAML **フレーム**のナビゲーション バックスタックに、中断されたときに現在のウィンドウに表示されていた以前のコンテンツが含まれなくなります。

アプリが、起動コントラクトとプロトコル コントラクトに単一 XAML [**フレーム**](/uwp/api/Windows.UI.Xaml.Controls.Frame)を使うようにした場合は、新しいページに移動する前に**フレーム**のナビゲーション ジャーナルにあるページをクリアする必要があります。 プロトコル コントラクトによって起動されるときは、アプリの先頭に戻ることができる UI をアプリに含めることを検討してください。

## <a name="related-topics"></a>関連トピック

### <a name="complete-sample-app"></a>完全なサンプルアプリ

- [Association Launching サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AssociationLaunching)

### <a name="concepts"></a>概念

- [既定のプログラム](/windows/desktop/shell/default-programs)
- [ファイルの種類と URI の関連付けのモデル](/windows/desktop/w8cookbook/file-type-and-protocol-associations-model)

### <a name="tasks"></a>タスク

- [URI に応じた既定のアプリの起動](launch-default-app.md)
- [ファイルのアクティブ化の処理](handle-file-activation.md)

### <a name="guidelines"></a>ガイドライン

- [ファイルの種類と URI のガイドライン](../files/index.md)

### <a name="reference"></a>参照先

- [AppX パッケージ マニフェスト](/uwp/schemas/appxpackage/uapmanifestschema/element-uap-extension)
- [Windows.ApplicationModel.Activation.ProtocolActivatedEventArgs](/uwp/api/Windows.ApplicationModel.Activation.ProtocolActivatedEventArgs)
- [Windows.UI.Xaml.Application.OnActivated](/uwp/api/windows.ui.xaml.application.onactivated)