---
title: 暗号化キー
description: この記事では、標準のキー派生関数を使ってキーを派生させる方法、および対称キーと非対称キーを使ってコンテンツを暗号化する方法について説明します。
ms.assetid: F35BEBDF-28C5-4F91-A94E-F7D862B6ED59
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp, セキュリティ
ms.localizationpriority: medium
ms.openlocfilehash: a781ae79b54223916c9de379dcdb4f8cb3b8e4b5
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89167256"
---
# <a name="cryptographic-keys"></a>暗号化キー




この記事では、標準のキー派生関数を使ってキーを派生させる方法、および対称キーと非対称キーを使ってコンテンツを暗号化する方法について説明します。 

## <a name="symmetric-keys"></a>対称キー


秘密鍵の暗号化とも呼ばれる対称キーの暗号化には、暗号化にも暗号化解除にも使われるキーが必要です。 [**SymmetricKeyAlgorithmProvider**](/uwp/api/Windows.Security.Cryptography.Core.SymmetricKeyAlgorithmProvider) クラスを使って対称アルゴリズムを指定し、キーを作成またはインポートできます。 [**CryptographicEngine**](/uwp/api/Windows.Security.Cryptography.Core.CryptographicEngine) クラスで静的メソッドを使って、アルゴリズムとキーでデータを暗号化および暗号化解除できます。

通常、対称キーの暗号化ではブロック暗号とブロック暗号モードを使います。 ブロック暗号は、固定サイズのブロックで動作する対称暗号化機能です。 暗号化するメッセージがブロックの長さよりも長い場合は、ブロック暗号モードを使う必要があります。 ブロック暗号モードは、ブロック暗号を使って作成された対称暗号化機能です。 このモードでは、プレーンテキストが一連の固定サイズ ブロックとして暗号化されます。 アプリでは、次のモードがサポートされます。

-   ECB (電子コードブック) モードでは、メッセージの各ブロックが個別に暗号化されます。 これは、セキュリティで保護された暗号化モードとは見なされません。
-   CBC (暗号ブロック チェーン) モードでは、前の暗号テキスト ブロックを使って現在のブロックを難読にします。 最初のブロックに使う値を決める必要があります。 この値は初期化ベクトル (IV) と呼ばれます。
-   CCM (Counter with CBC-MAC) モードは、CBC ブロック暗号モードとメッセージ認証コード (MAC) が組み合わされたものです。
-   GCM (ガロア カウンター モード) モードは、カウンター暗号化モードとガロア認証モードが組み合わされたものです。

CBC などの一部のモードでは、最初の暗号テキスト ブロックに初期化ベクトル (IV) を使う必要があります。 一般的な初期化ベクトルを次に示します。 IV は [**CryptographicEngine.Encrypt**](/uwp/api/windows.security.cryptography.core.cryptographicengine.encrypt) を呼び出すときに指定します。 多くの場合、IV は同じキーで再利用しないことが重要です。

-   "固定" では、暗号化されるすべてのメッセージで同じ IV を使います。 情報が漏れるので、この方法を使うことはお勧めできません。
-   "カウンター" ではブロックごとに IV を増分します。
-   "ランダム" では、擬似乱数の IV を作成します。 [**CryptographicBuffer.GenerateRandom**](/uwp/api/windows.security.cryptography.cryptographicbuffer.generaterandom) を使って IV を追加できます。
-   "nonce 生成" では、暗号化されるメッセージごとに固有の番号を使います。 通常、nonce は修正されたメッセージまたはトランザクションの識別子を表します。 nonce は秘密にする必要はありませんが、同じキーで再利用できません。

ほとんどのモードでは、プレーンテキストの長さをブロック サイズの正確な倍数にする必要があります。 このため、通常はプレーンテキストをパディングして適切な長さにする必要があります。

ブロック暗号は固定サイズのデータ ブロックを暗号化する一方、ストリーム暗号はプレーンテキスト ビットと擬似乱数ビット ストリーム (キー ストリームと呼ばれる) を組み合わせて暗号テキストを生成する対称暗号化機能を表します。 出力フィードバック モード (OTF) やカウンター モード (CTR) などの一部のブロック暗号モードでは、ブロック暗号がストリーム暗号に効率よく変換されます。 ただし、RC4 などの実際のストリーム暗号は通常、ブロック暗号モードよりも高速で動作します。

次の例に、[**SymmetricKeyAlgorithmProvider**](/uwp/api/Windows.Security.Cryptography.Core.SymmetricKeyAlgorithmProvider) クラスを使って対称キーを作成し、それを使ってデータを暗号化および暗号化解除する方法を示します。

## <a name="asymmetric-keys"></a>非対称キー


非対称キーの暗号化 (公開キーの暗号化とも呼ばれます) は、公開キーと秘密キーを使って暗号化および暗号化解除します。 これらのキーは異なるものですが、数学的に関連性があります。 通常、秘密キーは秘密として保持され、データの暗号化解除に使われます。一方、公開キーは関係者に配布され、データの暗号化に使われます。 非対称キーの暗号化は、データ署名にも役立ちます。

非対称暗号化方式は対称暗号化方式よりかなり遅いため、大量のデータを直接暗号化する場合にはあまり使われません。 非対称暗号化が一般に使われるのは、次のような方法でキーを暗号化する場合です。

-   アリスはボブに、暗号化されたメッセージだけを送るように要求します。
-   アリスは秘密キー/公開キーのペアを作り、秘密キーを秘密に保有し、公開キーを公開します。
-   ボブにはアリスに送りたいメッセージがあります。
-   ボブは対称キーを作ります。
-   ボブは、新しい対称キーを使って、アリスへのメッセージを暗号化します。
-   ボブは、アリスの公開キーを使って、対称キーを暗号化します。
-   ボブは、暗号化したメッセージと暗号化した対称キーを、(エンベロープにして) アリスに送ります。
-   アリスは、(秘密キー/公開キー ペアの) 自分の秘密キーを使って、ボブの対称キーを暗号化解除します。
-   アリスは、ボブの対称キーを使って、メッセージを暗号化解除します。

[**AsymmetricKeyAlgorithmProvider**](/uwp/api/Windows.Security.Cryptography.Core.AsymmetricKeyAlgorithmProvider) オブジェクトを使うと、非対称アルゴリズムまたは署名アルゴリズムの指定、短期的なキー ペアの作成またはインポート、キー ペアの公開キー部分のインポートが可能になります。

## <a name="deriving-keys"></a>キーの派生


多くの場合、共有シークレットから追加キーを派生する必要があります。 [**KeyDerivationAlgorithmProvider**](/uwp/api/Windows.Security.Cryptography.Core.KeyDerivationAlgorithmProvider) クラスおよび [**KeyDerivationParameters**](/uwp/api/Windows.Security.Cryptography.Core.KeyDerivationParameters) クラスの次の専用メソッドのいずれかを使って、キーを派生できます。

| Object                                                                            | 説明                                                                                                                                |
|-----------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| [**BuildForPbkdf2**](/uwp/api/windows.security.cryptography.core.keyderivationparameters.buildforpbkdf2)    | パスワードベースのキー派生関数 2 (PBKDF2) で使う KeyDerivationParameters オブジェクトを作成します。                                 |
| [**BuildForSP800108**](/uwp/api/windows.security.cryptography.core.keyderivationparameters.buildforsp800108)  | カウンター モードのハッシュベース メッセージ認証コード (HMAC) キー派生関数で使う KeyDerivationParameters オブジェクトを作成します。 |
| [**BuildForSP80056a**](/uwp/api/windows.security.cryptography.core.keyderivationparameters.buildforsp80056a)  | SP800-56A キー派生関数で使う KeyDerivationParameters オブジェクトを作成します。                                                 |

 