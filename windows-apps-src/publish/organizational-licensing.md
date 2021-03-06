---
Description: アプリの申請の [組織のライセンス] セクションでは、ビジネス向け Microsoft ストアと教育機関向け Microsoft ストアでアプリでボリューム購入を提供するかどうかと、その提供方法を指定できます。
title: 組織のライセンス オプション
ms.assetid: 1EB139B0-67E7-4F66-AAEF-491B1E52E96F
ms.date: 10/31/2018
ms.topic: article
keywords: windows 10, uwp, ビジネス向け Store, 教育機関向け Store, 組織, ボリューム ライセンス, 企業, 教育機関 Store, ビジネス Store, ボリューム購入, 一括
localizationpriority: high
ms.openlocfilehash: b7f0ecc1eb7faec39eaad925ccd6c9d501d39749
ms.sourcegitcommit: fca0132794ec187e90b2ebdad862f22d9f6c0db8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63788401"
---
# <a name="organizational-licensing-options"></a>組織のライセンス オプション


アプリの申請の [[価格と使用可能状況]](set-app-pricing-and-availability.md#organizational-licensing) ページの **[組織のライセンス]** セクションでは、ビジネス向け Microsoft ストアと教育機関向け Microsoft ストアでアプリのボリューム購入を提供するかどうかと、その提供方法を指定できます。

これらの設定を使用して、アプリに使用可能にすることを許可する選択できますを取得し、ユーザーは、Windows 10 の間での組織に規模を拡大する機会を提供する複数のライセンスを展開した組織 (企業や教育機関)デバイスの種類、Pc、タブレット、携帯電話などです。

企業に直接公開する[基幹業務 (LOB) アプリ](distribute-lob-apps-to-enterprises.md)に対して組織のライセンスを許可する必要もあります。

> [!NOTE]
> 各アプリの選択はそれぞれ独立して構成します。 アプリの基本設定は、新しい申請を作成することでいつでも変更できます。また、変更は申請が[認定プロセス](the-app-certification-process.md)を完了した後に有効になります。

> [!IMPORTANT]
> [Microsoft Store 申請 API](../monetize/create-and-manage-submissions-using-windows-store-services.md) を使う申請は、ビジネス向け Microsoft Store と教育機関向け Microsoft Store では利用可能になりません。 アプリで使用できるようにのボリューム購入組織では、作成し、パートナー センターでのあなたの投稿を送信する必要があります。


## <a name="allowing-your-app-to-be-offered-to-organizations"></a>組織へのアプリの提供の許可

既定では、**[ストアで管理される (オンライン) ボリューム ライセンスと配布に基づいて組織がこのアプリを購入できるようにする]** チェック ボックスはオンになっています。 これは、組織がボリューム取得できるアプリのカタログにアプリを含め、ストアのオンライン ライセンス システムでアプリのライセンスが管理されるようにすることを意味します。

> [!NOTE]
> すべての組織がアプリを利用できるようになるわけではありません。

組織がアプリをボリューム取得できるようにしない場合は、このチェック ボックスをオフにします。 この変更はアプリが認定プロセスを完了した後にのみ有効になることに注意してください。 組織が以前にアプリのライセンスを取得していた場合、これらのライセンスは有効であり、アプリを既に持っているユーザーは使い続けることができます。

> [!TIP]
> 基幹業務 (LOB) アプリを特定の組織に対してのみ公開するには、企業の関連付けを設定して、組織がアプリをプライベート ストアに直接追加できるようにします。 詳しくは、「[LOB アプリの企業への配布](distribute-lob-apps-to-enterprises.md)」をご覧ください。


## <a name="allowing-disconnected-offline-licensing"></a>未接続状態 (オフライン) のライセンスの許可

オフラインのライセンスに対応したアプリを多くの組織が必要としています。 たとえば、一部の組織では、インターネットに接続することがまったくないか、ほとんどないデバイスにアプリを展開する必要があります。 このようなユーザーがアプリを利用できるようにする場合は、**[組織に対して、組織で管理される (オフライン) ライセンスと配布を許可する]** というチェック ボックスをオンにします。

既定では、このチェック ボックスは**オフ**です。 検証済みの組織が組織で管理する (オフライン) ライセンスを使用してインストールできるように、Microsoft ストアからアプリを提供する場合は、このチェック ボックスをオンにする必要があります。 この方法で有料アプリをエンド ユーザーにインストールするためには、組織は追加の検証を受ける必要があります。

オフラインのライセンスでは、組織はボリューム ベースでアプリを取得し、各デバイスがストアのライセンス システムに問い合わせる必要なくアプリをインストールすることができます。 組織はライセンスと共にアプリのパッケージをダウンロードすることができ、このライセンスでは特定のライセンスが使用されているときにストアに通知することなく、(独自の管理ツールを使用するか、OS イメージにアプリを事前に読み込むことによって) アプリをデバイスにインストールすることができます。 このシナリオを有効にすることで展開の柔軟性が大幅に増し、ユーザーにとってのアプリの魅力が大きく高まる場合があります。

> [!IMPORTANT]
> .xap パッケージでは、オフラインのライセンスはサポートされていません。

 
## <a name="paid-app-support"></a>有料アプリのサポート

現在、特定の市場の開発者アカウントでは、有料アプリをビジネス向け Microsoft ストアでボリューム取得用に提供することができます。 

> [!NOTE]
> 一部の市場では、ビジネス向け Microsoft Store や教育機関向け Microsoft Store に表示されるアプリの価格が、Microsoft Store の同じ価格帯で小売顧客に表示される価格と異なる場合があります。 組織による購入の収益の支払いは、コンシューマーによるアプリの購入の場合と同様に機能します。 詳しくは、「[支払いの受け取り](getting-paid-apps.md)」と「[アプリ開発者契約](https://docs.microsoft.com/legal/windows/agreements/app-developer-agreement)」をご覧ください。 ビジネス向け Microsoft ストアと教育機関向け Microsoft ストアを利用できる市場の一覧については、「[ビジネス向け Microsoft ストアと教育機関向け Microsoft ストアの概要](https://technet.microsoft.com/itpro/windows/manage/windows-store-for-business-overview#supported-markets)」をご覧ください。

お住まいの国または地域が以下の一覧にない場合は、現在、有料アプリをビジネス向け Microsoft ストアと教育機関向け Microsoft ストアで提供することはできません。 この場合、有料アプリ用に選択した組織のライセンスの設定は後で適用されることがあります。Microsoft ストアでは、他の開発者アカウント市場からの申請に対するサポートを将来追加することがあるためです。

現時点では、ビジネス向け Microsoft ストアと教育機関向け Microsoft ストアで組織の顧客に有料アプリを配付できるのは、以下の国または地域の開発者です。

- オーストリア
- ベルギー
- ブルガリア
- カナダ
- クロアチア
- キプロス
- チェコ共和国
- デンマーク
- エストニア
- フィンランド
- フランス
- ドイツ
- ギリシャ
- ハンガリー
- アイルランド
- マン島
- イタリア
- ラトビア
- リヒテンシュタイン
- リトアニア
- ルクセンブルク
- マルタ
- モナコ
- オランダ
- ノルウェー
- ポーランド
- ポルトガル
- ルーマニア
- スロバキア
- スロベニア
- スペイン
- スウェーデン
- スイス
- イギリス
- 米国
