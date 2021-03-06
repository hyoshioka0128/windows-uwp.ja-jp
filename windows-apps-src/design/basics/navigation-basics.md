---
Description: ユニバーサル Windows プラットフォーム (UWP) アプリのナビゲーションは、ナビゲーション構造、ナビゲーション要素、システム レベルの機能から成る柔軟なモデルに基づいています。
title: UWP アプリのナビゲーションの基本
ms.assetid: B65D33BA-AAFE-434D-B6D5-1A0C49F59664
label: Navigation design basics
template: detail.hbs
op-migration-status: ready
ms.date: 07/16/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.custom: RS5
ms.openlocfilehash: 1c764eeb57ec8046a93e7fb58e156fa68daea8df
ms.sourcegitcommit: 13fe5d04bdb43c75d0fc4de18c2c3d4ae58ff982
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "64564525"
---
# <a name="navigation-design-basics-for-uwp-apps"></a>UWP アプリのナビゲーション デザインの基本

![ナビゲーションの基本のヘッダー](images/nav/navigation-basics-header.jpg)

アプリをページの集まりと考えると、*ナビゲーション*は、ページ間およびページ内を移動する動作を表します。 これはユーザー エクスペリエンスの出発点です。これによって、ユーザーは利用するコンテンツと機能を見つけます。 これは非常に重要ですが、適切な設計が難しい場合もあります。

ナビゲーションに関して行うことができる膨大な数の選択肢があります。 以下を行うことができます。

:::row:::
    :::column:::
        ![navigation example 1](images/nav/nav-1.svg)

ユーザーは、一連の順序でページを経由する必要があります。
    :::column-end:::
    :::column:::
        ![navigation example 2](images/nav/nav-2.svg)

ユーザーが任意のページに直接ジャンプできるメニューを提供します。
    :::column-end:::
    :::column:::
        ![navigation example 3](images/nav/nav-3.svg)

すべてを 1 ページに配置し、コンテンツを表示するためのフィルター処理メカニズムを提供します。
    :::column-end:::
:::row-end:::

1 つのナビゲーション デザインですべてのアプリに対応することはできませんが、アプリの適切な設計を判断するための原則やガイドラインがあります。

## <a name="principles-of-good-navigation"></a>優れたナビゲーションの原則

優れたナビゲーション デザインの基本原則から始めましょう。

- **整合性:** ユーザーの期待を満たします。
- **わかりやすくするため:** 必要があるよりしません。
- **わかりやすくするため:** 明確なパスとオプションを提供します。

### <a name="consistency"></a>一貫性

ナビゲーションは、ユーザーの期待に沿ったものである必要があります。 使用して[標準コントロール](#use-the-right-controls)ユーザーは、アイコン、場所の標準の規則をよく理解し、次をスタイル設定は行うことナビゲーション予測可能で直感的なユーザー。

![ページ コンポーネントのイメージ](images/nav/page-components.svg)

> ユーザーは特定の UI 要素が標準の位置にあることを期待します。

### <a name="simplicity"></a>シンプルさ

ナビゲーション項目が少ないほど、ユーザーの意思決定がシンプルになります。 重要な移動先に簡単にアクセスできるようにして、重要度の低い項目を非表示にすることで、ユーザーは目的の場所にすばやく移動できるようになります。

:::row:::
    :::column:::
        ![do example](images/nav/do.svg)

        ![navview good](images/nav/navview-good.svg)

使い慣れたナビゲーション メニューで、ナビゲーション項目を表示します。
    :::column-end:::
    :::column:::
        ![don't example](images/nav/dont.svg)

        ![navview bad](images/nav/navview-bad.svg)

多くのナビゲーション オプションを持つユーザーの重荷となってください。
    :::column-end:::
:::row-end:::

### <a name="clarity"></a>明確さ

明確なパスを示すと、ユーザーは論理的なナビゲーションを行うことができます。 ナビゲーション オプションをわかりやすくし、ページ間の関係を明確にすることで、ユーザーが自分の位置を見失うことを防止できます。

![実行例](images/nav/clarity-image.svg)

> 移動先にはわかりやすいラベルが付けられているため、ユーザーは自分の位置を知ることができます。

## <a name="general-recommendations"></a>一般的な推奨事項

一貫性、シンプルさ、明確さという設計原則を念頭に置いて、一般的な推奨事項を作成しましょう。

1. ユーザーのことを考えてください。 アプリ使用時のユーザーの一般的な移動パスを追跡し、ページごとに、ユーザーがそのページを表示している理由と、次にどこに移動しようとしているかを考えてください。

2. 詳細のナビゲーション階層を回避します。 3 レベルを超えるナビゲーションでは、ユーザーは迷ってしまい、深い階層から抜け出せなくなる可能性があります。

3. 「ホッピング」を避けます。 ホッピングとは、関連するコンテンツに移動するために、ユーザーが上のレベルに移動して、それから下のレベルに移動する必要があるナビゲーションを意味します。

## <a name="use-the-right-structure"></a>適切な構造を使う

ナビゲーションの一般的な原則について説明しました。次に、アプリの構造について考えます。 2 種類の一般的な構造があります。フラット構造と階層構造です。

:::row:::
    :::column:::
        ![Pages arranged in a flat structure](images/nav/flat-lateral-structure.svg)
    :::column-end:::
    :::column span="2":::
        ### Flat/lateral

フラット構造/水平構造では、ページは横方向に存在します。 どのような順序でもページ間を移動できます。

次のような場合に、フラット構造の使用を推奨します。

- ページをどのような順序でも表示できる場合。
- 各ページはそれぞれ異なるページであり、明確な親/子関係がない場合。
- グループには、8 未満のページがあります。 <br>
(ページ数が 8 ページ以上の場合、ページが一意であるかどうかを判断したり、グループ内の現在の位置を把握したりするのが難しくなる場合があります。 このことがアプリでは問題にはならないと考えられる場合は、ページをピアとして作成します。 このことが問題となる可能性がある場合は、階層構造を使って、ページを 2 つ以上の小さなグループに分割することを検討してください。)

    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        ![Pages arranged in a hierarchy](images/nav/hierarchical-structure.svg)
    :::column-end:::
    :::column span="2":::
        ### Hierarchical

階層構造では、ページはツリー状の構造に配置されています。 それぞれの子ページの親は 1 つですが、親ページは 1 つ以上の子ページを持つことができます。 子ページにアクセスするには、親ページを経由します。

階層構造体は、多数のページにわたる複雑なコンテンツを配置する場合に適してします。 欠点は、ナビゲーションのオーバーヘッドが発生することです。階層が深くなると、ページからページへの移動するために、多くのクリックが必要となります。

階層をお勧めときに構造体します。
        
- 特定の順序でページを移動する必要がある場合。
- ページ間に明白な親子関係がある場合。
- グループ内のページ数が 7 ページを超える場合。
        
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        ![an app with a hybrid structure](images/nav/combining-structures.svg)
    :::column-end:::
    :::column span="2":::
        ### Combining structures

1 つの構造または; その他に選択しません。適切に設計の多くのアプリでは、両方を使用します。 アプリでは、トップレベルのページにはフラット構造を使って、任意の順序で参照できるようにし、複雑な関係のあるページには階層構造を使うことができます。

ナビゲーション構造に複数のレベルがある場合は、現在のサブツリー内のピアにのみリンクするピア ツー ピアのナビゲーション要素を使うことをお勧めします。 2 つのレベルを持つナビゲーション構造を示しています、隣接する図を考慮してください。

- レベル 1 では、ピア ツー ピアのナビゲーション要素によって、ページ A、B、C、および D へのアクセスが提供されます。
- レベル 2 では、A2 ページのピア ツー ピアのナビゲーション要素は、他の A2 ページにのみリンクしています。 これらのナビゲーション要素は、C サブツリー内にあるレベル 2 のページにはリンクしていません。
    :::column-end:::
:::row-end:::

## <a name="use-the-right-controls"></a>適切なコントロールを使用する

ページの構造を決定したら、ユーザーがページ間をどのように移動するかを決定する必要があります。 UWP にはさまざまなナビゲーション コントロールが用意されていて、アプリで一貫性があり信頼性が高いナビゲーション エクスペリエンスを提供するために役立ちます。

:::row:::
    :::column:::
        ![Frame image](images/nav/thumbnail-frame.svg)
    :::column-end:::
    :::column span="2":::
        [**Frame**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Frame)

少数の例外を除き、複数のページがあるアプリではフレームを使用します。 通常、アプリにはフレームと、ナビゲーション ビュー コントロールなどの主要なナビゲーション要素を含むメイン ページがあります。 ユーザーがページを選択すると、フレームがページを読み込んで表示します。
:::row-end:::

:::row:::
    :::column:::
        ![tabs and pivot image](images/nav/thumbnail-tabs-pivot.svg)
    :::column-end:::
    :::column span="2":::
        [**Top navigation and tabs**](../controls-and-patterns/navigationview.md)

同じレベルにあるページへのリンクの横方向の一覧を表示します。 [NavigationView](../controls-and-patterns/navigationview.md)コントロールは、上部のナビゲーションを実装し、パターンのタブします。
        
上部のナビゲーションを使用する場合。

- 画面上のすべてのナビゲーション オプションを表示するには。
- アプリのコンテンツを追加する領域を必要とします。
- アイコンは、ナビゲーションのカテゴリを明確に記述できません。
        
ときにタブを使用します。

- ナビゲーション履歴とページの状態を保存するには。
- 頻繁にタブを切り替えるユーザーを必要とします。

:::row-end:::

:::row:::
    :::column:::
         ![tabs and pivot image](images/nav/thumbnail-tabs-pivot.svg)
    :::column-end:::
        :::column span="2":::
    [**Pivot**](../controls-and-patterns/pivot.md)
    
ような[ナビゲーション ビュー](../controls-and-patterns/navigationview.md)タッチと若干異なるナビゲーションの動作の追加をサポートしています。
    
ピボットを使用する場合。
- 項目間のタッチ スワイプを許可するアプリで使用します。
- カルーセル infintely のナビゲーション オプションをします。
- カテゴリ間のナビゲーション動作を広範囲に制御する必要はありません。

:::row-end:::

:::row:::
    :::column:::
        ![navview image](images/nav/thumbnail-navview.svg)
    :::column-end:::
    :::column span="2":::
        [**Left navigation**](../controls-and-patterns/navigationview.md)

トップレベルのページへのリンクの縦方向の一覧を表示します。 次の場合に使用します。
        
- ページがトップレベルに存在する場合。
- 多くのナビゲーション項目 (5 以上の場合) があります。
- ユーザーが頻繁にページ間を切り替えることを前提としていない場合。

:::row-end:::
        
:::row:::
    :::column:::
        ![Master details image](images/nav/thumbnail-master-detail.svg)
    :::column-end:::
    :::column span="2":::
        [**Master/details**](../controls-and-patterns/master-details.md)

項目の一覧 (マスター ビュー) を表示します。 項目を選ぶと、対応するページが詳細セクションに表示されます。 次の場合に使用します。
        
- ユーザーが頻繁に子項目間を切り替えることを前提としている場合。
- ユーザーが個々の項目や項目のグループに対して高いレベルの操作 (削除や並べ替えなど) を実行できるようにする場合、およびユーザーが各項目の詳細情報の表示や更新を実行できるようにする場合。

マスター/詳細は、メールの受信トレイ、連絡先リスト、データ入力に適しています。
:::row-end:::

:::row:::
    :::column:::
        ![Hyperlinks and buttons image](images/nav/thumbnail-hyperlinks-buttons.svg)
    :::column-end:::
    :::column span="2":::
        [**Hyperlinks**](../controls-and-patterns/hyperlinks.md)

埋め込まれたナビゲーション要素は、ページのコンテンツに表示されます。 他のナビゲーション要素はページの全体で一貫性がありますが、それとは異なり、コンテンツに埋め込まれたナビゲーション要素はそれぞれのページに固有のナビゲーション要素です。
:::row-end:::

## <a name="next-add-navigation-code-to-your-app"></a>次に：アプリへのナビゲーションのコードを追加します。

次の記事「[基本的なナビゲーションを実装する](navigate-between-two-pages.md)」では、アプリで 2 つのページ間で基本的なナビゲーションを行うための、Frame コントロールを使用するために必要なコードを示します。
