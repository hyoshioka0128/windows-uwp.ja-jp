---
title: Windows 10 ユニバーサル Windows プラットフォーム (UWP) アプリの自動起動
description: 開発者はプロトコルのアクティブ化および起動アクティブ化を使って、自動テスト用に UWP アプリや UWP ゲームを自動で起動できます。
ms.topic: article
ms.localizationpriority: medium
ms.date: 02/08/2017
ms.openlocfilehash: 661576ede9a940f7f8aa71715900306d2c2b28a9
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89154876"
---
# <a name="automate-launching-windows-10-uwp-apps"></a>Windows 10 UWP アプリの自動起動

## <a name="introduction"></a>はじめに

開発者はいくつかの方法でユニバーサル Windows プラットフォーム (UWP) アプリの自動起動を実現できます。 ここでは、プロトコルのアクティブ化と起動アクティブ化を使ってアプリを起動する方法を説明します。

*プロトコルのアクティブ化*では、アプリ自体を特定のプロトコルのハンドラーとして登録できます。 

*起動アクティブ化*では、アプリのタイルなど、通常の方法でアプリを起動します。

これらのアクティブ化はどちらも、コマンド ラインまたはランチャー アプリケーションを使って実行できます。 いずれの方法でアクティブ化を行う場合も、アプリが実行中のときは、アクティブ化によってアプリがフォアグラウンドになり (再アクティブ化され)、新しいアクティブ化引数が提供されます。 そのため、アクティブ化コマンドを使ってアプリに新しいメッセージを柔軟に提供できます。 アクティブ化メソッドで更新後の新しいアプリが実行されるようにするには、プロジェクトをコンパイルして展開する必要があることに注意してください。 

## <a name="protocol-activation"></a>プロトコルのアクティブ化

アプリに対してプロトコルのアクティブ化を設定するには、次の手順に従います。 

1. Visual Studio で **Package.appxmanifest** ファイルを開きます。
2. **[宣言]** タブをクリックします。
3. **[使用可能な宣言]** ボックスの一覧で **[プロトコル]** を選び、**[追加]** をクリックします。
4. **[プロパティ]** の **[名前]** フィールドに、アプリの起動に使うプロトコルの一意の名前を入力します。 

    ![プロトコルのアクティブ化](images/automate-uwp-apps-1.png)

5. ファイルを保存し、プロジェクトを展開します。 
6. プロジェクトの展開が完了したら、プロトコルのアクティブ化を設定します。 
7. **[コントロール パネル]、[すべてのコントロール パネル項目]、[既定のプログラム]** の順にクリックし、**[ファイルの種類またはプロトコルのプログラムへの関連付け]** を選択します。 **[プロトコル]** セクションまでスクロールし、プロトコルが一覧に表示されていることを確認します。 

プロトコルのアクティブ化を設定したら、2 つの方法 (コマンド ラインまたはランチャー アプリケーション) のどちらかを使用して、プロトコルを使ってアプリをアクティブ化できます。 

### <a name="command-line"></a>コマンド ライン

コマンド ラインでプロトコルのアクティブ化を使ってアプリを起動するには、start コマンドを使います。このコマンドで、先ほど設定したプロトコル名を指定し、コロン (“:”) に続けて任意のパラメーターを指定します。 パラメーターには任意の文字列を指定できますが、Uniform Resource Identifier (URI) の機能を利用できるように、URI の標準の形式に従うことをお勧めします。 

  ```
  scheme://username:password@host:port/path.extension?query#fragment
  ```

この形式の URI 文字列は、Uri オブジェクトのメソッドで解析できます。 詳しくは、[MSDN の Uri クラスのトピック](/uwp/api/windows.foundation.uri)をご覧ください。 

例 :

  ```
  >start bingnews:
  >start myapplication:protocol-parameter
  >start myapplication://single-player/level3?godmode=1&ammo=200
  ```

コマンド ラインによるプロトコルのアクティブ化では、生の URI で指定できる Unicode 文字は 2038 文字までに制限されます。 

### <a name="launcher-application"></a>ランチャー アプリケーション

WinRT API をサポートするアプリケーションを起動用に別途作成します。 プロトコルのアクティブ化を使ってアプリを起動するランチャー プログラムの C++ コードの例を次に示します。**PackageURI** は、アプリケーションの URI を示す任意の引数です (例: `myapplication:`、`myapplication:protocol activation arguments`)。

```
bool ProtocolLaunchURI(Platform::String^ URI)
{
       IAsyncOperation<bool>^ protocolLaunchAsyncOp;
       try
       {
              protocolLaunchAsyncOp = Windows::System::Launcher::LaunchUriAsync(ref new 
Uri(URI));
       }
       catch (Platform::Exception^ e)
       {
              Platform::String^ dbgStr = "ProtocolLaunchURI Exception Thrown: " 
+ e->ToString() + "\n";
              OutputDebugString(dbgStr->Data());
              return false;
       }

       concurrency::create_task(protocolLaunchAsyncOp).wait();

       if (protocolLaunchAsyncOp->Status == AsyncStatus::Completed)
       {
              bool LaunchResult = protocolLaunchAsyncOp->GetResults();
              Platform::String^ dbgStr = "ProtocolLaunchURI " + URI 
+ " completed. Launch result " + LaunchResult + "\n";
              OutputDebugString(dbgStr->Data());
              return LaunchResult;
       }
       else
       {
              Platform::String^ dbgStr = "ProtocolLaunchURI " + URI + " failed. Status:" 
+ protocolLaunchAsyncOp->Status.ToString() + " ErrorCode:" 
+ protocolLaunchAsyncOp->ErrorCode.ToString() + "\n";
              OutputDebugString(dbgStr->Data());
              return false;
       }
}
```
ランチャー アプリケーションでプロトコルのアクティブ化を行う場合も、引数の制限はコマンド ラインの場合と同じです。 どちらを使う場合も、生の URI で指定できる Unicode 文字は 2038 文字までです。 

## <a name="launch-activation"></a>起動アクティブ化

起動アクティブ化を使ってアプリを起動することもできます。 セットアップは必要ありませんが、UWP アプリのアプリケーション ユーザー モデル ID (AUMID) が必要になります。 AUMID は、パッケージ ファミリ名とアプリケーション ID を感嘆符で区切った形式で表されます。 

パッケージ ファミリ名を取得するには、次の手順に従うと最も簡単です。

1. **Package.appxmanifest** ファイルを開きます。
2. **[パッケージ化]** タブで、**[パッケージ名]** を入力します。

    ![起動アクティブ化](images/automate-uwp-apps-2.png)

3. **[パッケージ ファミリ名]** が表示されない場合は、PowerShell を開いて `>get-appxpackage MyPackageName` を実行し、**PackageFamilyName** を探します。

アプリケーション ID は、**Package.appxmanifest** ファイル (XML ビューで開く) の `<Applications>` 要素で確認できます。

### <a name="command-line"></a>コマンド ライン

UWP アプリの起動アクティブ化を実行するためのツールは Windows 10 SDK に付属しています。 このツールはコマンド ラインから実行することができ、起動するアプリの AUMID を引数として指定できます。

```
C:\Program Files (x86)\Windows Kits\10\App Certification Kit\microsoft.windows.softwarelogo.appxlauncher.exe <AUMID>
```

たとえば、次のようになります。

```
"C:\Program Files (x86)\Windows Kits\10\App Certification Kit\microsoft.windows.softwarelogo.appxlauncher.exe" MyPackageName_ph1m9x8skttmg!AppId
```

この方法では、コマンド ライン引数はサポートされません。 

### <a name="launcher-application"></a>ランチャー アプリケーション

COM の使用をサポートするアプリケーションを起動用に別途作成できます。 起動アクティブ化を使ってアプリを起動するランチャー プログラムの C++ コードの例を次に示します。 このコードでは、**ApplicationActivationManager** を作成して **ActivateApplication** を呼び出し、先ほど確認した AUMID と任意の引数を渡すことができます。 その他のパラメーターについて詳しくは、[MSDN の IApplicationActivationManager::ActivateApplication メソッドのトピック](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-iapplicationactivationmanager-activateapplication)をご覧ください。

```
#include <ShObjIdl.h>
#include <atlbase.h>

HRESULT LaunchApp(LPCWSTR AUMID)
{
     HRESULT hr = CoInitializeEx(nullptr, COINIT_APARTMENTTHREADED);
     if (FAILED(hr))
     {
            wprintf(L"LaunchApp %s: Failed to init COM. hr = 0x%08lx \n", AUMID, hr);
     }
     {
            CComPtr<IApplicationActivationManager> AppActivationMgr = nullptr;
            if (SUCCEEDED(hr))
            {
                   hr = CoCreateInstance(CLSID_ApplicationActivationManager, nullptr,  
CLSCTX_LOCAL_SERVER, IID_PPV_ARGS(&AppActivationMgr));
                   if (FAILED(hr))
                   {
                         wprintf(L"LaunchApp %s: Failed to create Application Activation 
Manager. hr = 0x%08lx \n", AUMID, hr);
                   }
            }
            if (SUCCEEDED(hr))
            {
                   DWORD pid = 0;
                   hr = AppActivationMgr->ActivateApplication(AUMID, nullptr, AO_NONE, 
&pid);
                   if (FAILED(hr))
                   {
                         wprintf(L"LaunchApp %s: Failed to Activate App. hr = 0x%08lx 
\n", AUMID, hr);
                   }
            }
     }
     CoUninitialize();
     return hr;
}
```

この方法では、コマンド ラインを使った先ほどの起動方法とは異なり、引数を渡すことができることに注意してください。

## <a name="accepting-arguments"></a>引数を受け取る

UWP アプリのアクティブ化で渡される引数を受け取るには、アプリにコードを追加する必要があります。 プロトコルのアクティブ化または起動アクティブ化が実行されたかどうかを判断するのには、**OnActivated** イベントをオーバーライドして引数の型を確認し、生の文字列または Uri オブジェクトの事前解析値を取得します。 

次の例は、生の文字列を取得する方法を示しています。

```
void OnActivated(IActivatedEventArgs^ args)
{
        // Check for launch activation
        if (args->Kind == ActivationKind::Launch)
        {
            auto launchArgs = static_cast<LaunchActivatedEventArgs^>(args); 
            Platform::String^ argval = launchArgs->Arguments;
            // Manipulate arguments …
        }

        // Check for protocol activation
        if (args->Kind == ActivationKind::Protocol)
        {
            auto protocolArgs = static_cast< ProtocolActivatedEventArgs^>(args);
            Platform::String^ argval = protocolArgs->Uri->ToString();
            // Manipulate arguments …
        }
}
```

## <a name="summary"></a>まとめ
以上のように、UWP アプリはさまざまな方法で起動することができます。 要件や用途に応じて、適切な方法を利用してください。 

## <a name="see-also"></a>関連項目
- [Xbox One の UWP](index.md)