---
description: このセクションの C# コード例を使用して、Microsoft Store 申請 API を使用したゲーム オプションおよびトレーラーの申請方法をご確認ください。
title: C# のコード例 - ゲーム オプションおよびトレーラーを含むアプリの申請
ms.date: 07/10/2017
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 申請 API, コード例, ゲーム オプション, トレーラー, 詳細な登録情報, C#
ms.localizationpriority: medium
ms.openlocfilehash: 16d51a12c6d703be3a76c1c90d5ab6a2e9442603
ms.sourcegitcommit: c3ca68e87eb06971826087af59adb33e490ce7da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89363195"
---
# <a name="c-sample-app-submission-with-game-options-and-trailers"></a>C \# サンプル: ゲームのオプションとトレーラーを使用したアプリの送信

この記事では、次のタスクで [Microsoft Store 申請 API](create-and-manage-submissions-using-windows-store-services.md) を使用する方法を示す C# コード例を提供します。

* Microsoft Store 申請 API で使用する Azure AD アクセス トークンを取得します。
* アプリの申請の作成
* [ゲーム](manage-app-submissions.md#gaming-options-object)と[トレーラー](manage-app-submissions.md#trailer-object)の高度な登録情報のオプションを含む、アプリの申請用のストア登録情報データを構成します。
* アプリの申請用のパッケージ、登録情報の画像、トレーラー ファイルが含まれた ZIP ファイルをアップロードします。
* アプリの申請をコミットします。

各例を確認して、それぞれが対応するタスクについて詳しく知ることができます。また、この記事のすべてのコード例を使って、コンソール アプリケーションをビルドすることもできます。 サンプルをビルドするには、Visual Studio で **DevCenterApiSample** という名前の C# コンソール アプリケーションを作成し、各サンプルをプロジェクトの別のコード ファイルにコピーして、プロジェクトをビルドします。

## <a name="prerequisites"></a>前提条件

これらの例には、次の要件があります。

* プロジェクトに System.Web アセンブリへの参照を追加します。
* Newtonsoft の [Newtonsoft.Json](https://www.newtonsoft.com/json) NuGet パッケージをプロジェクトにインストールします。

<span id="create-app-submission" />

## <a name="create-an-app-submission"></a>アプリの申請の作成

```CreateAndSubmitSubmissionExample``` クラスでは、```Execute``` というパブリック メソッドを定義します。このメソッドは、他のサンプル メソッドを呼び出し、Microsoft Store 申請 API を使って、ゲーム オプションとトレーラーを含むアプリの申請を作成およびコミットします。 このコードを採用するには、次の手順を実行してください。

* ```tenantId``` 変数をアプリのテナント ID に割り当てて、```clientId``` 変数と ```clientSecret``` 変数をアプリのクライアント ID とキーに割り当てます。 詳細については、「 [Azure AD アプリケーションをパートナーセンターアカウントに関連付ける方法](create-and-manage-submissions-using-windows-store-services.md#how-to-associate-an-azure-ad-application-with-your-partner-center-account)」を参照してください。
* ```applicationId``` 変数を、申請を作成するアプリの[ストア ID](in-app-purchases-and-trials.md#store-ids) に割り当てます。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/StoreServicesExamples_SubmissionAdvancedListings/cs/CreateAndSubmitSubmissionExample.cs" id="CreateAndSubmitSubmissionExample":::

<span id="token" />

## <a name="obtain-an-azure-ad-access-token"></a>Azure AD アクセス トークンの取得

```DevCenterAccessTokenClient``` クラスでは、指定された ```tenantId```、```clientId```、```clientSecret``` の値を使って、Microsoft Store 申請 API で使用する Azure AD アクセス トークンを作成するヘルパー メソッドを定義します。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/StoreServicesExamples_SubmissionAdvancedListings/cs/DevCenterAccessTokenClient.cs" id="DevCenterAccessTokenClient":::

<span id="utilities" />

## <a name="helper-methods-to-invoke-the-submission-api-and-upload-submission-files"></a>申請 API を呼び出して申請ファイルをアップロードするヘルパー メソッド

```DevCenterClient``` クラスでは、Microsoft Store 申請 API のさまざまなメソッドを呼び出して、アプリの申請用のパッケージ、登録情報の画像、トレーラー ファイルを含む ZIP ファイルをアップロードするヘルパー メソッドを定義します。

> [!div class="tabbedCodeSnippets"]
:::code language="csharp" source="~/../snippets-windows/windows-uwp/monetize/StoreServicesExamples_SubmissionAdvancedListings/cs/DevCenterClient.cs" id="DevCenterClient":::

## <a name="related-topics"></a>関連トピック

* [Microsoft Store サービスを使用した申請の作成と管理](create-and-manage-submissions-using-windows-store-services.md)
