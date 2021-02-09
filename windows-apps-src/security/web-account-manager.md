---
title: Web アカウント マネージャー
description: この記事では、Windows 10 Web アカウント マネージャー API を使い、AccountsSettingsPane を利用して、ユニバーサル Windows プラットフォーム (UWP) アプリを外部の ID プロバイダー (Microsoft や Facebook など) に接続する方法について説明します。
ms.date: 12/06/2017
ms.topic: article
keywords: windows 10, uwp, セキュリティ
ms.assetid: ec9293a1-237d-47b4-bcde-18112586241a
ms.localizationpriority: medium
ms.openlocfilehash: 0a67c88eb7eb70308e6dcbbd096289c0617793b1
ms.sourcegitcommit: 53c00939b20d4b0a294936df3d395adb0c13e231
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91933073"
---
# <a name="web-account-manager"></a>Web アカウント マネージャー

この記事では、 **[AccountsSettingsPane](/uwp/api/Windows.UI.ApplicationSettings.AccountsSettingsPane)** を使用して、Windows 10 Web アカウントマネージャー api を使用して、ユニバーサル WINDOWS プラットフォーム (UWP) アプリを Microsoft や Facebook などの外部 id プロバイダーに接続する方法について説明します。 ユーザーの Microsoft アカウントを使用するためにユーザーの許可を求める方法、アクセス トークンを取得する方法、アクセス トークンを使って基本的な操作 (プロファイル データの取得や OneDrive アカウントへのファイルのアップロードなど) を実行する方法を学習してください。 この手順は、ユーザーの許可を得て、Web アカウント マネージャーをサポートする ID プロバイダーにアクセスするための手順と似ています。

> [!NOTE]
> 完全なコード サンプルについては、[GitHub の WebAccountManagement サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WebAccountManagement)をご覧ください。

## <a name="get-set-up"></a>準備

まず、Visual Studio で新しい空白のアプリを作成します。 

次に、ID プロバイダーに接続するために、アプリをストアに関連付ける必要があります。 これを行うには、プロジェクトを右クリックし、[**ストア**] [アプリをストアと関連付ける] の順に選択  >  **Associate app with the store**して、ウィザードの指示に従います。 

3 番目に、シンプルな XAML ボタンと 2 つのテキスト ボックスから成る、非常に基本的な UI を作成します。

```XML
<StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
    <Button x:Name="LoginButton" Content="Log in" Click="LoginButton_Click" />
    <TextBlock x:Name="UserIdTextBlock"/>
    <TextBlock x:Name="UserNameTextBlock"/>
</StackPanel>
```

そして、コード ビハインドでイベント ハンドラーをボタンにアタッチします。

```csharp
private void LoginButton_Click(object sender, RoutedEventArgs e)
{   
}
```

最後に、次の名前空間を追加します。これにより、後で参照の問題について考える必要がなくなります。 

```csharp
using System;
using Windows.Security.Authentication.Web.Core;
using Windows.System;
using Windows.UI.ApplicationSettings;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.Data.Json;
using Windows.UI.Xaml.Navigation;
using Windows.Web.Http;
```

## <a name="show-the-accounts-settings-pane"></a>アカウント設定ウィンドウの表示

システムには、ID プロバイダーを管理するための組み込みのユーザー インターフェイスと、**AccountsSettingsPane** という名前の Web アカウントが用意されています。 これを次のように表示することができます。

```csharp
private void LoginButton_Click(object sender, RoutedEventArgs e)
{
    AccountsSettingsPane.Show(); 
}
```

アプリを実行して "ログイン" ボタンをクリックすると、空のウィンドウが表示されます。 

![アカウントが一覧表示されていない [アカウントの選択] ウィンドウのスクリーンショット。](images/tb-1.png)

システムは UI シェルのみを提供するため、このウィンドウは空になっています。開発者がこのウィンドウに ID プロバイダーをプログラムで入力します。 

> [!TIP]
> 必要に応じて、 **[Show](/uwp/api/windows.ui.applicationsettings.accountssettingspane.show#Windows_UI_ApplicationSettings_AccountsSettingsPane_Show)** ではなく**[ShowAddAccountAsync](/uwp/api/windows.ui.applicationsettings.accountssettingspane.showaddaccountasync)** を使用して、操作の状態を照会する**[iasyncaction](/uwp/api/Windows.Foundation.IAsyncAction)** を返します。 

## <a name="register-for-accountcommandsrequested"></a>AccountCommandsRequested への登録

ウィンドウにコマンドを追加するには、まず AccountCommandsRequested イベント ハンドラーに登録します。 これにより、ユーザーがペインを表示するように求められたとき (たとえば、XAML ボタンをクリックしたとき) に、ビルドロジックを実行するようシステムに指示します。 

コードビハインドで、OnNavigatedTo イベントと OnNavigatedFrom イベントを上書きし、次のコードを追加します。 

```csharp
protected override void OnNavigatedTo(NavigationEventArgs e)
{
    AccountsSettingsPane.GetForCurrentView().AccountCommandsRequested += BuildPaneAsync; 
}
```

```csharp
protected override void OnNavigatedFrom(NavigationEventArgs e)
{
    AccountsSettingsPane.GetForCurrentView().AccountCommandsRequested -= BuildPaneAsync; 
}
```

ユーザーは頻繁にはアカウントを操作しないため、この方法でイベント ハンドラーを登録および登録解除することは、メモリ リークを防ぐために役立ちます。 この方法では、カスタマイズしたウィンドウは (ユーザーが "設定" ページや "ログイン" ページにいるなどの理由で) ユーザーが使う可能性が高いときにのみメモリ内にあります。 

## <a name="build-the-account-settings-pane"></a>アカウント設定ウィンドウを構築します。

**AccountsSettingsPane** が表示されるたびに、BuildPaneAsync メソッドが呼び出されます。 ここに、ウィンドウに表示されるコマンドをカスタマイズするコードを記述します。 

まず、遅延を取得します。 これにより、構築が完了するまで **AccountsSettingsPane** の表示を遅延するようシステムに指示を出すことができます。

```csharp
private async void BuildPaneAsync(AccountsSettingsPane s,
    AccountsSettingsPaneCommandsRequestedEventArgs e)
{
    var deferral = e.GetDeferral();
        
    deferral.Complete(); 
}
```

次に、WebAuthenticationCoreManager.FindAccountProviderAsync メソッドを使ってプロバイダーを取得します。 プロバイダーの URL はプロバイダーによって異なり、プロバイダーのドキュメントに記載されています。 Microsoft アカウントと Azure Active Directory の場合、"https \: //login.microsoft.com" になります。 

```csharp
private async void BuildPaneAsync(AccountsSettingsPane s,
    AccountsSettingsPaneCommandsRequestedEventArgs e)
{
    var deferral = e.GetDeferral();
        
    var msaProvider = await WebAuthenticationCoreManager.FindAccountProviderAsync(
        "https://login.microsoft.com", "consumers"); 
        
    deferral.Complete(); 
}
```

文字列 "consumers" をオプションの *authority* パラメーターに渡すことにも注意してください。 これは、Microsoft は "消費者 (consumers)" 向けの Microsoft アカウント (MSA) と、"組織 (organizations)" 向けの Azure Active Directory (AAD) という、2 種類の認証を提供しているためです。 "consumers" 権限は、MSA オプションを必要としていることを示します。 企業向けのアプリを開発している場合は、代わりに文字列 "organizations" を使います。

最後に、次のように新しい**[Webaccountprovidercommand](/uwp/api/windows.ui.applicationsettings.webaccountprovidercommand)** を作成して、プロバイダーを**AccountsSettingsPane**に追加します。 

```csharp
private async void BuildPaneAsync(AccountsSettingsPane s,
    AccountsSettingsPaneCommandsRequestedEventArgs e)
{
    var deferral = e.GetDeferral();

    var msaProvider = await WebAuthenticationCoreManager.FindAccountProviderAsync(
        "https://login.microsoft.com", "consumers");

    var command = new WebAccountProviderCommand(msaProvider, GetMsaTokenAsync);  

    e.WebAccountProviderCommands.Add(command);

    deferral.Complete(); 
}
```

新しい **WebAccountProviderCommand** に渡した GetMsaToken メソッドはまだ存在していないため (次の手順で構築します)、現時点では、このメソッドを空のメソッドとして自由に追加できます。

上記のコードを実行すると、ウィンドウは次のようになります。 

![アカウントが一覧表示されている [アカウントの選択] ウィンドウのスクリーンショット。](images/tb-2.png)

### <a name="request-a-token"></a>トークンの要求

Microsoft アカウントのオプションが **AccountsSettingsPane** に 表示されたら、ユーザーがこのオプションを選択したときに、どのような動作を行うかを処理する必要があります。 ユーザーが自分の Microsoft アカウントを使ってログインしたときに GetMsaToken メソッドが発生するように登録しているため、ここでトークンを取得します。 

トークンを取得するには、次のような RequestTokenAsync メソッドを使います。 

```csharp
private async void GetMsaTokenAsync(WebAccountProviderCommand command)
{
    WebTokenRequest request = new WebTokenRequest(command.WebAccountProvider, "wl.basic");
    WebTokenRequestResult result = await WebAuthenticationCoreManager.RequestTokenAsync(request);
}
```

この例では、文字列 "wl" を _スコープ_ パラメーターに渡します。 スコープは、特定のユーザーの提供サービスから要求する情報の種類を表します。 スコープには、名前やメール アドレスなど、ユーザーの基本情報のみへのアクセス権を与えるものや、ユーザーの写真やメールの受信トレイなど、機密情報へのアクセス権を与えるものもあります。 一般的に、アプリではその機能を実行するために必要な最も制限の多いスコープが使われます。 サービス プロバイダーからは、サービス プロバイダーのサービスで使うトークンを取得する場合に必要となるスコープについて示したドキュメントが提供されます。 

* Microsoft 365 スコープと Outlook.com スコープについては、「 [Outlook REST API を使用する (バージョン 2.0)](/previous-versions/office/office-365-api/api/version-2.0/use-outlook-rest-api)」を参照してください。 
* OneDrive のスコープについては、「[OneDrive の認証とサインイン](https://dev.onedrive.com/auth/msa_oauth.htm#authentication-scopes)」をご覧ください。 

> [!TIP]
> 必要に応じて、アプリでログインヒント (既定の電子メールアドレスをユーザーフィールドに設定するため) またはサインインエクスペリエンスに関連するその他の特殊なプロパティを使用する場合は、 **[Webtokenrequest. AppProperties](/uwp/api/windows.security.authentication.web.core.webtokenrequest.appproperties#Windows_Security_Authentication_Web_Core_WebTokenRequest_AppProperties)** プロパティに一覧表示します。 これにより、システムは web アカウントをキャッシュするときにプロパティを無視するため、キャッシュ内のアカウントの不一致を防ぐことができます。

企業向けのアプリを開発している場合は、Azure Active Directory (AAD) インスタンスに接続し、通常の MSA サービスではなく Microsoft Graph API を使用します。 このシナリオでは、次のコードを代わりに使います。 

```csharp
private async void GetAadTokenAsync(WebAccountProviderCommand command)
{
    string clientId = "your_guid_here"; // Obtain your clientId from the Azure Portal
    WebTokenRequest request = new WebTokenRequest(provider, "User.Read", clientId);
    request.Properties.Add("resource", "https://graph.microsoft.com");
    WebTokenRequestResult result = await WebAuthenticationCoreManager.RequestTokenAsync(request);
}
```

この記事の残りの部分では、引き続き MSA シナリオについて説明しますが、AAD 用のコードもよく似ています。 GitHub の完全なサンプルを含め、AAD/Graph について詳しくは、[Microsoft Graph のドキュメント](https://developer.microsoft.com/graph)をご覧ください。

## <a name="use-the-token"></a>トークンを使用する

RequestTokenAsync メソッドは、要求の結果を含む WebTokenRequestResult オブジェクトを返します。 要求が成功した場合には、トークンが含まれます。  

```csharp
private async void GetMsaTokenAsync(WebAccountProviderCommand command)
{
    WebTokenRequest request = new WebTokenRequest(command.WebAccountProvider, "wl.basic");
    WebTokenRequestResult result = await WebAuthenticationCoreManager.RequestTokenAsync(request);
    
    if (result.ResponseStatus == WebTokenRequestStatus.Success)
    {
        string token = result.ResponseData[0].Token; 
    }
}
```

> [!NOTE]
> トークンを要求したときにエラーが発生した場合、最初の手順で説明したように、アプリを Microsoft Store に関連付けたかどうかを確認してください。 この手順を省略すると、アプリでトークンを取得することはできません。 

トークンを取得したら、プロバイダーの API を呼び出すためにトークンを使うことができます。 次のコードでは、[ユーザー情報のための Microsoft Live API](/office/) を呼び出してユーザーに関する基本情報を取得し、UI に表示します。 ただし、ほとんどの場合、取得したトークンは保存してから、別のメソッドで使用することをお勧めします。

```csharp
private async void GetMsaTokenAsync(WebAccountProviderCommand command)
{
    WebTokenRequest request = new WebTokenRequest(command.WebAccountProvider, "wl.basic");
    WebTokenRequestResult result = await WebAuthenticationCoreManager.RequestTokenAsync(request);
    
    if (result.ResponseStatus == WebTokenRequestStatus.Success)
    {
        string token = result.ResponseData[0].Token; 
        
        var restApi = new Uri(@"https://apis.live.net/v5.0/me?access_token=" + token);

        using (var client = new HttpClient())
        {
            var infoResult = await client.GetAsync(restApi);
            string content = await infoResult.Content.ReadAsStringAsync();

            var jsonObject = JsonObject.Parse(content);
            string id = jsonObject["id"].GetString();
            string name = jsonObject["name"].GetString();

            UserIdTextBlock.Text = "Id: " + id; 
            UserNameTextBlock.Text = "Name: " + name;
        }
    }
}
```

さまざまな REST API の呼び出し方法は、プロバイダーによって異なります。トークンの使い方に関する情報については、プロバイダーの API ドキュメントをご覧ください。 

## <a name="store-the-account-for-future-use"></a>将来の使用に備えてアカウントを保存する

トークンはユーザーに関する情報を直ちに取得する場合に便利ですが、通常はさまざまな有効期限を持ちます。たとえば、MSA トークンは数時間のみ有効です。 ただし、トークンの有効期限が切れるたびに **AccountsSettingsPane** を再表示する必要はありません。 ユーザーが一度アプリを承認すると、将来使うためにユーザーのアカウント情報を保存できます。 

これを行うには、 **[WebAccount](/uwp/api/windows.security.credentials.webaccount)** クラスを使用します。 **WebAccount** は、トークンの要求で使ったメソッドと同じメソッドによって返されます。

```csharp
private async void GetMsaTokenAsync(WebAccountProviderCommand command)
{
    WebTokenRequest request = new WebTokenRequest(command.WebAccountProvider, "wl.basic");
    WebTokenRequestResult result = await WebAuthenticationCoreManager.RequestTokenAsync(request);
    
    if (result.ResponseStatus == WebTokenRequestStatus.Success)
    {
        WebAccount account = result.ResponseData[0].WebAccount; 
    }
}
```

**WebAccount** インスタンスを取得すると、これを簡単に保存することができます。 次の例では、LocalSettings を使います。 LocalSettings やユーザー データを保存するための他のメソッドの使用方法について詳しくは、「[Store and retrieve app settings and data](../design/app-settings/store-and-retrieve-app-data.md)」(アプリの設定とデータを保存して取得する) をご覧ください。

```csharp
private async void StoreWebAccount(WebAccount account)
{
    ApplicationData.Current.LocalSettings.Values["CurrentUserProviderId"] = account.WebAccountProvider.Id;
    ApplicationData.Current.LocalSettings.Values["CurrentUserId"] = account.Id; 
}
```

その後で、次のような非同期メソッドを使い、保存された **WebAccount** を利用して、トークンの取得をバックグラウンドで実行することができます。

```csharp
private async Task<string> GetTokenSilentlyAsync()
{
    string providerId = ApplicationData.Current.LocalSettings.Values["CurrentUserProviderId"]?.ToString();
    string accountId = ApplicationData.Current.LocalSettings.Values["CurrentUserId"]?.ToString();

    if (null == providerId || null == accountId)
    {
        return null; 
    }

    WebAccountProvider provider = await WebAuthenticationCoreManager.FindAccountProviderAsync(providerId);
    WebAccount account = await WebAuthenticationCoreManager.FindAccountAsync(provider, accountId);

    WebTokenRequest request = new WebTokenRequest(provider, "wl.basic");

    WebTokenRequestResult result = await WebAuthenticationCoreManager.GetTokenSilentlyAsync(request, account);
    if (result.ResponseStatus == WebTokenRequestStatus.UserInteractionRequired)
    {
        // Unable to get a token silently - you'll need to show the UI
        return null; 
    }
    else if (result.ResponseStatus == WebTokenRequestStatus.Success)
    {
        // Success
        return result.ResponseData[0].Token;
    }
    else
    {
        // Other error 
        return null; 
    }
}
```

上記のメソッドは、**AccountsSettingsPane** を構築するコードの直前に配置します。 トークンをバックグラウンドで取得する場合は、ウィンドウを表示する必要はありません。 

```csharp
private void LoginButton_Click(object sender, RoutedEventArgs e)
{
    string silentToken = await GetMsaTokenSilentlyAsync();

    if (silentToken != null)
    {
        // the token was obtained. store a reference to it or do something with it here.
    }
    else
    {
        // the token could not be obtained silently. Show the AccountsSettingsPane
        AccountsSettingsPane.Show();
    }
}
```

通知なしでのトークンの取得は非常に単純なため、(トークンの有効期限がいつ切れても大丈夫なように) セッション間でのトークンの更新には、既存のトークンをキャッシュするのではなく、このプロセスを使います。

> [!NOTE]
> 上記の例は、基本的な成功と失敗のケースのみを扱っています。 アプリは特殊なシナリオ (ユーザーによってアプリのアクセス許可が無効にされた場合や、Windows からユーザーのアカウントが削除された場合など) も考慮し、適切に処理する必要があります。  

## <a name="remove-a-stored-account"></a>保存されたアカウントの削除

Web アカウントを保持するとき、場合によっては、ユーザーが自分のアカウントとアプリの関連付けを解除できるようにする必要があります。 こうすることで、アプリを効果的に "ログアウト" できます。アカウント情報は、起動時に自動的に読み込まれなくなります。 これを行うには、まず保存されたアカウントとプロバイダーの情報を記憶域から削除します。 次に、**[SignOutAsync](/uwp/api/windows.security.credentials.webaccount.SignOutAsync)** を呼び出してキャッシュをクリアし、アプリが保持している可能性がある既存のトークンをすべて無効にします。 

```csharp
private async Task SignOutAccountAsync(WebAccount account)
{
    ApplicationData.Current.LocalSettings.Values.Remove("CurrentUserProviderId");
    ApplicationData.Current.LocalSettings.Values.Remove("CurrentUserId"); 
    account.SignOutAsync(); 
}
```

## <a name="add-providers-that-dont-support-webaccountmanager"></a>WebAccountManager をサポートしていないプロバイダーの追加

サービスからの認証をアプリに統合するが、そのサービスが WebAccountManager (Google + または Twitter) をサポートしていない場合でも、そのプロバイダーを手動で **AccountsSettingsPane**に追加することができます。 これを行うには、新しい WebAccountProvider オブジェクトを作成し、独自の名前と .png アイコンを指定してから、WebAccountProviderCommands リストに追加します。 いくつかのスタブ コードを次に示します。 

 ```csharp
private async void BuildPaneAsync(AccountsSettingsPane s, AccountsSettingsPaneCommandsRequestedEventArgs e)
{
    // other code here 

    var twitterProvider = new WebAccountProvider("twitter", "Twitter", new Uri(@"ms-appx:///Assets/twitter-auth-icon.png")); 
    var twitterCmd = new WebAccountProviderCommand(twitterProvider, GetTwitterTokenAsync);
    e.WebAccountProviderCommands.Add(twitterCmd);   
    
    // other code here
}

private async void GetTwitterTokenAsync(WebAccountProviderCommand command)
{
    // Manually handle Twitter login here
}

```

> [!NOTE] 
> この例では、アイコンを **AccountsSettingsPane** に追加し、指定されたメソッド (この場合は GetTwitterTokenAsync) をアイコンのクリック時に実行するだけです。 実際の認証を処理するコードを提供する必要があります。 詳細については、「 [Web 認証ブローカー](web-authentication-broker.md)」を参照してください。これは、REST サービスを使用して認証するためのヘルパーメソッドを提供します。 

## <a name="add-a-custom-header"></a>カスタム ヘッダーの追加

次のように、HeaderText プロパティを使ってアカウント設定ウィンドウをカスタマイズできます。 

```csharp
private async void BuildPaneAsync(AccountsSettingsPane s, AccountsSettingsPaneCommandsRequestedEventArgs e)
{
    // other code here 
    
    args.HeaderText = "MyAwesomeApp works best if you're signed in.";   
    
    // other code here
}
```

![アカウントが一覧表示されていない [アカウントの選択] ウィンドウのスクリーンショットと、サインインしている場合は、優れたアプリが最適であるというメッセージが表示されます。](images/tb-3.png)

ヘッダー テキストを長くしすぎないでください。短く簡潔なテキストにします。 ログイン プロセスが複雑で、詳しい情報を表示する必要がある場合には、カスタム リンクを使ってユーザーを別のページにリンクします。 

## <a name="add-custom-links"></a>カスタム リンクの追加

サポートされている WebAccountProviders の下にリンクとして表示されるカスタム コマンドを AccountsSettingsPane に追加することができます。 カスタム コマンドは、プライバシー ポリシーの表示や問題が発生したユーザーのためのサポート ページの起動などの、ユーザー アカウントに関連する単純なタスクに適しています。 

次に例を示します。 

```csharp
private async void BuildPaneAsync(AccountsSettingsPane s, AccountsSettingsPaneCommandsRequestedEventArgs e)
{
    // other code here 
    
    var settingsCmd = new SettingsCommand(
        "settings_privacy", 
        "Privacy policy", 
        async (x) => await Launcher.LaunchUriAsync(new Uri(@"https://privacy.microsoft.com/en-US/"))); 

    e.Commands.Add(settingsCmd); 
    
    // other code here
}
```

![アカウントが一覧表示されていない [アカウントの選択] ウィンドウのスクリーンショットと、プライバシーポリシーへのリンク。](images/tb-4.png)

理論上は、あらゆることのために設定コマンドを使うことができます。 ただし、上記のような、直観的なアカウント関連のシナリオにのみ使うことをお勧めします。 

## <a name="see-also"></a>関連項目

[Windows.Security.Authentication.Web.Core 名前空間](/uwp/api/windows.security.authentication.web.core)

[Windows.Security.Credentials 名前空間](/uwp/api/windows.security.credentials)

[AccountsSettingsPane クラス](/uwp/api/windows.ui.applicationsettings.accountssettingspane)

[Web 認証ブローカー](web-authentication-broker.md)

[Web アカウント管理のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/WebAccountManagement)

[ランチ スケジューラ アプリ](https://github.com/Microsoft/Windows-appsample-lunch-scheduler)