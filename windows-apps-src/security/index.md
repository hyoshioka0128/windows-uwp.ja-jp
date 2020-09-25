---
title: セキュリティ
description: このセクションには、Windows 10 のユニバーサル Windows プラットフォーム (UWP) アプリをセキュリティで保護されたアプリとしてビルドする方法に関する記事が含まれています。
ms.assetid: 41E2EEFB-E8A9-4592-814C-72B703CD952C
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp, セキュリティ
ms.localizationpriority: medium
ms.openlocfilehash: 9a565c9bdec6932d0e8ca376f677c309991773d6
ms.sourcegitcommit: eda7bbe9caa9d61126e11f0f1a98b12183df794d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91219725"
---
# <a name="security"></a>セキュリティ



このセクションには、Windows 10 のユニバーサル Windows プラットフォーム (UWP) アプリをセキュリティで保護されたアプリとしてビルドする方法に関する記事が含まれています。

## <a name="introduction"></a>はじめに 

Windows または UWP での開発が初めての場合は、最初に「[安全な Windows アプリの開発について](intro-to-secure-windows-app-development.md)」をご覧ください。 この初級レベルの記事では、アプリのセキュリティに関する考慮事項の概要と Windows 10 で使用できるさまざまな機能について説明しています。

## <a name="authentication-and-user-identity"></a>認証とユーザー ID

[認証とユーザー ID に関するセクション](authentication-and-user-identity.md)には、ユーザーのログインや身元確認に関連するシナリオのためのチュートリアルが記載されています。 アプリでは、[Web 認証ブローカー](web-authentication-broker.md)を使う簡単なシングル サインオン (SSO) から、高度なセキュリティで保護された 2 要素認証に至るまで、いくつかの方法でユーザー認証を行うことができます。

<table>
<tr><th>トピック</th><th>説明</th></tr>
<tr><td><a href="credential-locker.md">資格情報保管ボックス</a></td><td>この記事では、アプリで資格情報保管ボックスを使ってユーザーの資格情報を安全に保管し取得する方法、およびユーザーの Microsoft アカウントを使ってデバイス間でこれらの資格情報をローミングする方法について説明します。</td></tr>

<tr><td><a href="fingerprint-biometrics.md">指紋生体認証</a> </td><td>この記事では、アプリに指紋生体認証を追加する方法について説明します。 特定の操作に対してユーザーの同意を得る必要がある場合は、指紋認証の要求を含めると、アプリのセキュリティを高めることができます。 たとえば、アプリ内購入を承認する前や制限されたリソースにアクセスする前に指紋認証を要求できます。 指紋認証は、<a href="/uwp/api/Windows.Security.Credentials.UI">Windows.Security.Credentials.UI</a> 名前空間の <a href="/uwp/api/Windows.Security.Credentials.UI.UserConsentVerifier">UserConsentVerifier</a> クラスを使って管理されます。</td></tr>
<tr><td><a href="microsoft-passport.md">Microsoft Passport と Windows Hello</a></td><td>この記事では、新しい Windows 10 の Microsoft Passport テクノロジについて説明します。また、開発者がこのテクノロジを実装してアプリやバックエンド サービスを保護する方法についても説明します。 従来の資格情報の脅威を軽減するこれらのテクノロジの特定の機能に着目し、Windows 10 ロールアウトに含まれるこれらのテクノロジの設計と展開の方法について説明します。 </td></tr>
<tr><td><a href="microsoft-passport-login.md">Microsoft Passport ログイン アプリの作成</a></td><td>従来のユーザー名とパスワードの認証システムの代わりに Microsoft Passport を使う Windows 10 UWP (ユニバーサル Windows プラットフォーム) アプリの作成方法に関する詳しいチュートリアルのパート 1 です。</td></tr>
<tr><td><a href="microsoft-passport-login-auth-service.md">Microsoft Passport ログイン サービスの作成</a></td><td>Windows 10 UWP (ユニバーサル Windows プラットフォーム) アプリで従来のユーザー名とパスワードの認証システムの代わりに Microsoft Passport を使う方法に関する詳しいチュートリアルのパート 2 です。</td></tr>
<tr><td><a href="smart-cards.md">スマート カード</a></td><td>このトピックでは、アプリでスマート カードを使ってユーザーをセキュリティで保護されたネットワーク サービスに接続する方法のほか、物理スマート カード リーダーにアクセスする方法、仮想スマート カードの作成方法、スマート カードとの通信方法、ユーザーの認証方法、ユーザーの PIN のリセット方法、スマート カードの取り外しや切断の方法などについて説明します。</td></tr>
<tr><td><a href="share-certificates.md">アプリ間での証明書の共有</a></td><td>ユーザー ID とパスワードの組み合わせよりも安全な認証を必要とする UWP アプリでは、証明書を認証に使うことができます。 証明書認証は、ユーザーの認証時に高レベルの信頼性を提供します。 場合によっては、複数のアプリから複数のサービスのグループに対してユーザーを認証することがあります。 この記事では、1 つの証明書を使って複数のアプリを認証する方法と、セキュリティで保護された Web サービスにアクセスするための証明書をユーザーがインポートできる便利なコードを記述する方法について説明します。</td></tr>
<tr><td><a href="companion-device-unlock.md">コンパニオン (IoT) デバイスを使った Windows のロック解除</a></td><td>コンパニオン デバイスは、ユーザー認証のエクスペリエンスを強化するために、Windows 10 のデスクトップと組み合わせて使用できるデバイスです。 コンパニオン デバイス フレームワークを使用すると、Windows Hello を利用できない場合 (たとえば、Windows 10 デスクトップに顔認証用のカメラや指紋リーダー デバイスがない場合) でも、コンパニオン デバイスによって Microsoft Passport のための優れたエクスペリエンスを提供できます。</td></tr>
<tr><td><a href="web-account-manager.md">Web アカウント マネージャー</a></td><td>この記事では、Windows 10 Web アカウント マネージャー API を使って、AccountsSettingsPane を表示し、ユニバーサル Windows プラットフォーム (UWP) アプリを外部の ID プロバイダー (Microsoft や Facebook など) に接続する方法について説明します。 ユーザーの Microsoft アカウントを使用するためにユーザーの許可を求める方法、アクセス トークンを取得する方法、アクセス トークンを使って基本的な操作 (プロファイル データの取得や OneDrive へのファイルのアップロードなど) を実行する方法を学習してください。 </td></tr>
<tr><td><a href="web-authentication-broker.md">Web 認証ブローカー</a></td><td>この記事では、OpenID や OAuth などの認証プロトコルを使うオンライン ID プロバイダー (Facebook、Twitter、Flickr、Instagram など) にアプリを接続する方法について説明します。 <a href="/uwp/api/windows.security.authentication.web.webauthenticationbroker.authenticateasync">AuthenticateAsync</a> メソッドは、要求をオンライン ID プロバイダーに送信し、アプリがアクセスできるプロバイダー リソースを表すアクセス トークンを返します。</td></tr>
</table>

## <a name="cryptography"></a>暗号化 

暗号化についてのセクションでは、より複雑な暗号化に関するトピックが説明されています。 

| トピック                                                                         | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [証明書の概要](certificates.md)                                      | この記事では、アプリでの証明書の利用について説明します。 デジタル証明書は、公開キーを個人、コンピューター、組織にバインドするために、公開キーの暗号化で使われます。 バインドされた識別情報は、あるエンティティを別のエンティティに対して認証する際に最も頻繁に使われます。 たとえば、証明書は、Web サーバーをユーザーに対して、また、ユーザーを Web サーバーに対して認証するためによく使われます。 証明書要求を作成し、発行された証明書をインストールまたはインポートすることができます。 また、証明書階層で証明書を登録することもできます。 |
| [暗号化キー](cryptographic-keys.md)                                   | この記事では、標準のキー派生関数を使ってキーを派生させる方法、および対称キーと非対称キーを使ってコンテンツを暗号化する方法について説明します。                                                                                                                                                                                                                                                                                                                                                                         |
| [データ保護](data-protection.md)                                         | この記事では、[Windows.Security.Cryptography.DataProtection](/uwp/api/Windows.Security.Cryptography.DataProtection) 名前空間の [DataProtectionProvider](/uwp/api/Windows.Security.Cryptography.DataProtection.DataProtectionProvider) クラスを使って、UWP アプリでデジタル データの暗号化と暗号化解除を行う方法について説明します。                                                                                                                                                                                                              |
| [MAC、ハッシュ、および署名](macs-hashes-and-signatures.md)               | この記事では、メッセージ認証コード (MAC)、ハッシュ、署名をアプリで使って、メッセージの改ざんを検出する方法について説明します。                                                                                                                                                                                                                                                                                                                                                                                |
| [暗号化に関する輸出制限の順守](export-restrictions-on-cryptography.md) | アプリでの暗号化が、登録されない可能性がある方法で使われていないかどうかを判断する場合に、この情報を利用してください。                                                                                                                                                                                                                                                                                                                                                                                                     |
| [一般的な暗号化タスク](common-cryptography-tasks.md)                     | これらの記事では、乱数の生成、バッファーの比較、文字列とバイナリ データの間の変換、バイト配列間のコピー、データのエンコードとデコードなど、一般的な暗号化タスクのコード例が示されています。                                                                                                                                                                                                                                                                                    |