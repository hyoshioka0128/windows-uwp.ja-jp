---
description: 移植プロセスを開始するとき、2 つの方法から選ぶことができます。
title: Windows ランタイム 8.x プロジェクトの UWP プロジェクトへの移植'
ms.assetid: 2dee149f-d81e-45e0-99a4-209a178d415a
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 5cac5e66fe6d940ec73cc0e898924b4398382466
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89174836"
---
# <a name="porting-a-windows-runtime-8x-project-to-a-uwp-project"></a>Windows ランタイム 8.x プロジェクトの UWP プロジェクトへの移植



移植プロセスを開始するとき、2 つの方法から選ぶことができます。 1 つは、既にあるプロジェクト ファイル (アプリ パッケージ マニフェストなど) のコピーを編集する方法です。この方法については、「[アプリをユニバーサル Windows プラットフォーム (UWP) へ移行する](/visualstudio/misc/migrate-apps-to-the-universal-windows-platform-uwp?view=vs-2015)」に記載されているプロジェクト ファイルの更新に関する説明をご覧ください。 もう 1 つの方法は、Visual Studio で新しい Windows 10 プロジェクトを作成し、お使いのファイルをそのプロジェクトにコピーする方法です。 このトピックの最初のセクションでは、2 番目の方法について説明しますが、トピックの他の部分では、両方の方法に適用できる追加情報について説明します。 既にあるプロジェクトと同じソリューションに新しい Windows 10 プロジェクトを保持しておき、共有プロジェクトを使ってソース コード ファイルを共有することもできます。 また、新しいプロジェクトを独自のソリューションに保持しておき、Visual Studio のリンク ファイル機能を使ってソース コード ファイルを共有することもできます。

## <a name="create-the-project-and-copy-files-to-it"></a>プロジェクトを作成し、ファイルをコピーする

次の手順では、Visual Studio で新しい Windows 10 プロジェクトを作成し、お使いのファイルをそのプロジェクトにコピーする方法について説明しています。 作成するプロジェクトの数およびコピーするファイルに関する一部の仕様は、「[ユニバーサル 8.1 アプリがある場合](w8x-to-uwp-root.md)」や、それに続くセクションで説明されている要因と決定事項によって異なります。 次の手順では、最もシンプルなケースを前提としています。

1.  Microsoft Visual Studio 2015 を起動し、"新しいアプリケーション (Windows ユニバーサル)" プロジェクトを新規作成します。 詳細については、「 [テンプレートを使用した Windows ランタイム 8. x アプリのクイックスタート (C#、C++、Visual Basic)](/previous-versions/windows/apps/hh768232(v=win.10))」を参照してください。 新しいプロジェクトによって、すべてのデバイス ファミリで実行される 1 つのアプリ パッケージ (appx ファイル) が構築されます。
2.  ユニバーサル 8.1 アプリ プロジェクトで、再利用するすべてのソース コード ファイルとビジュアル アセット ファイルを確認します。 エクスプローラーを使って、データ モデル、ビュー モデル、ビジュアル アセット、リソース ディクショナリ、フォルダー構造、および再利用するその他すべての要素を、新しいプロジェクトにコピーします。 必要に応じて、ディスクにサブフォルダーをコピーするか、作成します。
3.  新しいプロジェクトに、ビュー (たとえば MainPage.xaml、MainPage.xaml.cs など) もコピーします。 ここでも、必要に応じて新しいサブフォルダーを作成し、プロジェクトから既にあるビューを削除します。 ただし、Visual Studio が生成したビューを上書きまたは削除する前に、後で参照するときに役立つ場合があるため、コピーを保存しておきます。 ユニバーサル 8.1 アプリを移植する最初のフェーズでは、1 つのデバイス ファミリでアプリが適切に表示され機能することを重視します。 その後で、すべてのフォーム ファクターに対してビューを適切に対応させることに重点を置きます。必要に応じて、特定のデバイス ファミリを最大限に活用できるように、アダプティブ コードを追加します。
4.  **ソリューション エクスプローラー**で、 **[すべてのファイルを表示]** がオンであることを確認します。 コピーしたファイルを選択して右クリックし、**[プロジェクトに含める]** をクリックします。 これによって、含まれるフォルダーが自動的に取り込まれます。 後で必要に応じて、**[すべてのファイルを表示]** をオフに切り替えることができます。 代替ワークフローとして、**[既存項目の追加]** コマンドを使って Visual Studio **ソリューション エクスプローラー**で必要なすべてのサブフォルダーを作成することもできます。 ビジュアル アセットで、**[ビルド アクション]** が **[コンテンツ]** に設定されており、**[出力ディレクトリにコピー]** が **[コピーしない]** に設定されていることを確認します。
5.  この段階では、ビルド エラーが発生する可能性があります。 ただし、どのような変更が必要であるかを理解している場合は、Visual Studio の **[検索と置換]** コマンドを使って、ソース コードに対して一括変更を実行できます。また Visual Studio の命令型コード エディターで、コンテキスト メニューの **[解決]** コマンドと **[using の整理]** コマンドを使って、よりターゲットを絞った変更を実行することもできます。

## <a name="maximizing-markup-and-code-reuse"></a>マークアップとコードを最大限に再利用する

若干のリファクタリングを行い、アダプティブ コード (後で説明します) を追加することで、すべてのデバイス ファミリで動作するマークアップとコードを最大限に活用することができます。 詳しい説明を次に示します。

-   すべてのデバイス ファミリに共通するファイルについては、特に考慮する必要はありません。 これらのファイルは、実行対象となるすべてのデバイス ファミリで、アプリが使うファイルです。 これには、XAML マークアップ ファイル、命令型ソース コード ファイル、アセット ファイルが含まれます。
-   実行されているデバイス ファミリをアプリで検出し、そのデバイス ファミリ専用に設計されたビューに移動させることができます。 詳しくは、「[アプリが実行されているプラットフォームの検出](w8x-to-uwp-input-and-sensors.md)」をご覧ください。
-   プラットフォームを検出するための代替方法がない場合に役立つと考えられる同様の手法として、マークアップ ファイルや **ResourceDictionary** ファイル (またはこのファイルが保存されているフォルダー) に対して特殊な名前を設定する方法があります。この特殊な名前によって、アプリが特定のデバイス ファミリで実行される場合にのみ、これらのファイルが実行時に自動的に読み込まれるようになります。 この手法については、「[Bookstore1](w8x-to-uwp-case-study-bookstore1.md)」のケース スタディをご覧ください。
-   Windows 10 のみをサポートする必要がある場合は、ユニバーサル 8.1 アプリのソース コードに含まれている多数の条件付きコンパイル ディレクティブを削除できます。 このトピックの「 [条件付きコンパイルとアダプティブコード](#conditional-compilation-and-adaptive-code) 」を参照してください。
-   一部のデバイス ファミリでのみ利用できる機能 (プリンター、スキャナー、またはカメラのボタンなど) を使うには、アダプティブ コードを記述します。 このトピックの「 [条件付きコンパイルとアダプティブコード](#conditional-compilation-and-adaptive-code) 」の3番目の例を参照してください。
-   Windows 8.1、Windows Phone 8.1、および Windows 10 をサポートする必要がある場合は、3 つのプロジェクトを同じソリューション内に保持し、共有プロジェクトを使ってコードを共有することができます。 または、プロジェクト間でソース コード ファイルを共有することができます。 Visual Studio でこのような処理を行うには、**ソリューション エクスプローラー**でプロジェクトを右クリックして **[既存項目の追加]** を選択し、共有するファイルを選択して **[リンクとして追加]** をクリックします。 リンクしたプロジェクトを確認できるファイル システム上の共通のフォルダーにソース コード ファイルを格納します。 また、ソース コントロールに追加することを忘れないでください。
-   ソースコードレベルではなく、バイナリレベルで再利用するには、「 [C# および Visual Basic での Windows ランタイムコンポーネントの作成](/previous-versions/windows/apps/br230301(v=vs.140))」を参照してください。 また、Windows 8.1、Windows Phone 8.1、Windows 10 (.NET Core) の各アプリ用の .NET Framework で利用できる .NET API のサブセットやフル バージョンの .NET Framework をサポートするポータブル クラス ライブラリがあります。 ポータブル クラス ライブラリ アセンブリは、これらのプラットフォームすべてとバイナリ レベルで互換性があります。 Visual Studio を使って、ポータブル クラス ライブラリをターゲットとするプロジェクトを作成します。 「[汎用性のあるクラス ライブラリを使用したプラットフォーム間の開発](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)」をご覧ください。

## <a name="extension-sdks"></a>拡張 SDK

ユニバーサル 8.1 アプリによって呼び出されている Windows ランタイム API のほとんどは、ユニバーサル デバイス ファミリと呼ばれる API のセットに実装されています。 ただし、一部の API は拡張 SDK に実装されており、Visual Studio で認識されるのは、アプリのターゲット デバイス ファミリによって実装された API、または参照している拡張 SDK によって実装された API のみです。

検出できなかった名前空間、型、メンバーについてのコンパイル エラーが発生した場合は、上記のことが原因となる可能性があります。 API リファレンス ドキュメントで API のトピックを表示し、要件に関するセクションに移動します。このセクションでは、どのようなデバイス ファミリが API を実装するかが示されています。 ターゲット デバイス ファミリが示されていない場合は、プロジェクトで API を利用できるようにするために、そのデバイス ファミリ用の拡張 SDK に対する参照が必要になります。

[ **プロジェクト**] [ &gt; **参照の追加**] [ &gt; **Windows ユニバーサル** &gt; **拡張** ] の順にクリックし、適切な拡張 SDK を選択します。 たとえば、呼び出す API がモバイル デバイス ファミリでのみ利用可能であり、それらの API がバージョン 10.0.x.y で導入されている場合は、**[Windows Mobile Extensions for the UWP]** を選びます。

これにより、次の参照がプロジェクト ファイルに追加されます。

```XML
<ItemGroup>
    <SDKReference Include="WindowsMobile, Version=10.0.x.y">
        <Name>Windows Mobile Extensions for the UWP</Name>
    </SDKReference>
</ItemGroup>
```

名前とバージョン番号は、SDK がインストールされている場所にあるフォルダーと一致します。 たとえば、上記の情報は次のフォルダー名と一致します。

`\Program Files (x86)\Windows Kits\10\Extension SDKs\WindowsMobile\10.0.x.y`

API を実装するデバイス ファミリがアプリのターゲットではない場合は、[**ApiInformation**](/uwp/api/Windows.Foundation.Metadata.ApiInformation) クラスを使って、API を呼び出す前に API の有無をテストする必要があります (これはアダプティブ コードと呼ばれます)。 このテストの条件は、アプリの実行時に必ず評価されますが、API が存在するデバイスに対してのみ true と評価され、呼び出しが可能になります。 ユニバーサル API が存在するかどうかを最初に確認した後では、拡張 SDK とアダプティブ コードのみを使います。 次のセクションで、例をいくつか示します。

「[アプリ パッケージ マニフェスト](#app-package-manifest)」もご覧ください。

## <a name="conditional-compilation-and-adaptive-code"></a>条件付きコンパイルとアダプティブ コード

コード ファイルが Windows 8.1 と Windows Phone 8.1 の両方で動作するように、条件付きコンパイル (C# プリプロセッサ ディレクティブによる条件付きコンパイル) を使っている場合は、Windows 10 に対して実行される集約作業を考慮して、その条件付きコンパイルを確認できます。 この集約作業では、Windows 10 アプリで、いくつかの条件を完全に削除できることを意味します。 削除されない条件は、次に説明するように実行時チェックに変更します。

**メモ**   1つのコードファイルで Windows 8.1、Windows Phone 8.1、Windows 10 をサポートする場合は、この操作を行うこともできます。 プロジェクトのプロパティページで Windows 10 プロジェクトを確認すると、プロジェクトで WINDOWS \_ UAP が条件付きコンパイルシンボルとして定義されていることがわかります。 そのため、これを WINDOWS \_ アプリと windows PHONE アプリと組み合わせて使用でき \_ \_ ます。 次の例では、ユニバーサル 8.1 アプリから条件付きコンパイルを削除し、Windows 10 アプリ用の同等のコードで置き換えるシンプルなケースを紹介します。

最初の例では、**PickSingleFileAsync** API (Windows 8.1 にのみ適用) と **PickSingleFileAndContinue** API (Windows Phone 8.1 にのみ適用) の使用パターンを示しています。

```csharp
#if WINDOWS_APP
    // Use Windows.Storage.Pickers.FileOpenPicker.PickSingleFileAsync
#else
    // Use Windows.Storage.Pickers.FileOpenPicker.PickSingleFileAndContinue
#endif // WINDOWS_APP
```

Windows 10 では、[**PickSingleFileAsync**](/uwp/api/windows.storage.pickers.fileopenpicker.picksinglefileasync) API に集約され、次のようにコードが簡略化されます。

```csharp
    // Use Windows.Storage.Pickers.FileOpenPicker.PickSingleFileAsync
```

次の例では、ハードウェアの "戻る" ボタンを処理しますが、Windows Phone のみが対象となります。

```csharp
#if WINDOWS_PHONE_APP
        Windows.Phone.UI.Input.HardwareButtons.BackPressed += this.HardwareButtons_BackPressed;
#endif // WINDOWS_PHONE_APP

...

#if WINDOWS_PHONE_APP
    void HardwareButtons_BackPressed(object sender, Windows.Phone.UI.Input.BackPressedEventArgs e)
    {
        // Handle the event.
    }
#endif // WINDOWS_PHONE_APP
```

Windows 10 では、"戻る" ボタンのイベントはユニバーサルな概念です。 ハードウェアまたはソフトウェアに実装されているすべての "戻る" ボタンでは [**BackRequested**](/uwp/api/windows.ui.core.systemnavigationmanager.backrequested) イベントが発生するため、このイベントを処理します。

```csharp
    Windows.UI.Core.SystemNavigationManager.GetForCurrentView().BackRequested +=
        this.ViewModelLocator_BackRequested;

...

private void ViewModelLocator_BackRequested(object sender, Windows.UI.Core.BackRequestedEventArgs e)
{
    // Handle the event.
}
```

最後の例は、前の例に類似しています。 ここでは、ハードウェアの "カメラ" ボタンを処理しますが、この場合も Windows Phone アプリ パッケージにコンパイルされるコードのみが対象となります。

```csharp
#if WINDOWS_PHONE_APP
    Windows.Phone.UI.Input.HardwareButtons.CameraPressed += this.HardwareButtons_CameraPressed;
#endif // WINDOWS_PHONE_APP

...

#if WINDOWS_PHONE_APP
void HardwareButtons_CameraPressed(object sender, Windows.Phone.UI.Input.CameraEventArgs e)
{
    // Handle the event.
}
#endif // WINDOWS_PHONE_APP
```

Windows 10 では、ハードウェアの "カメラ" ボタンはモバイル デバイス ファミリに固有の概念です。 1 つのアプリ パッケージがすべてのデバイスで実行されるため、アダプティブ コードと呼ばれる手法を使って、コンパイル時の条件を実行時の条件に変更します。 そのためには、[**ApiInformation**](/uwp/api/Windows.Foundation.Metadata.ApiInformation) クラスを使って、実行時に [**HardwareButtons**](/uwp/api/Windows.Phone.UI.Input.HardwareButtons) クラスの有無を照会します。 **HardwareButtons** は、モバイル拡張 SDK で定義されているため、その SDK への参照をプロジェクトに追加して、このコードをコンパイルする必要があります。 ただし、ハンドラーはモバイル拡張 SDK で定義されている型を実装するデバイスでのみ実行されることに注意してください。このようなデバイスは、モバイル デバイス ファミリに該当します。 このコードは事実上ユニバーサル 8.1 コードと同等のコードとなるため、このコードでは存在する機能のみを使うように注意してください。これは、別の方法で実施することもできます。

```csharp
    // Note: Cache the value instead of querying it more than once.
    bool isHardwareButtonsAPIPresent = Windows.Foundation.Metadata.ApiInformation.IsTypePresent
        ("Windows.Phone.UI.Input.HardwareButtons");

    if (isHardwareButtonsAPIPresent)
    {
        Windows.Phone.UI.Input.HardwareButtons.CameraPressed +=
            this.HardwareButtons_CameraPressed;
    }

    ...

private void HardwareButtons_CameraPressed(object sender, Windows.Phone.UI.Input.CameraEventArgs e)
{
    // Handle the event.
}
```

「[アプリが実行されているプラットフォームの検出](w8x-to-uwp-input-and-sensors.md)」もご覧ください。

## <a name="app-package-manifest"></a>アプリ パッケージ マニフェスト

「 [Windows 10 の変更点](/uwp/schemas/appxpackage/uapmanifestschema/what-s-changed-in-windows-10) 」トピックには、Windows 10 のパッケージ マニフェスト スキーマ リファレンスに対する変更点 (追加、削除、変更された要素など) が記載されています。 このスキーマのすべての要素、属性、タイプに関するリファレンス情報については、「[要素の階層](/uwp/schemas/appxpackage/uapmanifestschema/root-elements)」をご覧ください。 Windows Phone ストア アプリを移植する場合、または Windows Phone ストアのアプリに対する更新となるアプリを作成する場合は、**pm:PhoneIdentity** 要素が、以前のアプリのアプリ マニフェストの値と一致していることを確認してください (ストアからアプリに割り当てられたものと同じ GUID を使用してください)。 これにより、アプリのユーザーが Windows 10 にアップグレードした場合に、新しいアプリが確実に更新プログラムとして配布され、アプリの重複を避けることができます。 詳しくは、[**pm:PhoneIdentity**](/uwp/schemas/appxpackage/uapmanifestschema/element-pm-phoneidentity) のリファレンス トピックをご覧ください。

プロジェクトの設定 (すべての拡張 SDK の参照を含む) により、アプリが呼び出すことができる API サーフェス領域が決定されます。 ただし、ユーザーがアプリをストアからインストールできる実際のデバイスのセットを決定するのは、アプリ パッケージ マニフェストです。 詳細については、「 [**TargetDeviceFamily**](/uwp/schemas/appxpackage/uapmanifestschema/element-targetdevicefamily)」の例を参照してください。

さまざまな宣言、機能、および一部の機能で必要となる他の設定を指定するように、アプリ パッケージ マニフェストを編集できます。 Visual Studio アプリ パッケージ マニフェスト エディターを使って、編集できます。 **ソリューション エクスプローラー**が表示されていない場合は、**[表示]** メニューから選択します。 **Package.appxmanifest** をダブルクリックします。 マニフェスト エディター ウィンドウが開きます。 変更する適切なタブを選び、保存します。

次のトピックは「[トラブルシューティング](w8x-to-uwp-troubleshooting.md)」です。

## <a name="related-topics"></a>関連トピック

* [ユニバーサル Windows プラットフォーム用アプリの開発](/visualstudio/cross-platform/develop-apps-for-the-universal-windows-platform-uwp?view=vs-2015)
* [テンプレート (C#、C++、Visual Basic) を使用して Windows ランタイム 8. x アプリをすぐに使い始めます](/previous-versions/windows/apps/hh768232(v=win.10))
* [Windows ランタイムコンポーネントの作成](/previous-versions/windows/apps/hh441572(v=vs.140))
* [汎用性のあるクラス ライブラリを使用したプラットフォーム間の開発](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library)