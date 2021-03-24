---
description: Windows アプリにコントロールとパターンを追加する方法についての設計ガイダンスとコーディングの手順を入手できます。 アプリで使用できる 45 種類以上の強力なコントロールを紹介します。
title: Windows のコントロールとパターン - Windows アプリの開発
keywords: UWP コントロール, ユーザー インターフェイス, アプリ コントロール, Windows コントロール
label: Controls & patterns
template: detail.hbs
ms.date: 03/23/2020
ms.topic: article
ms.assetid: ce2e611c-c419-4a14-9095-b88ac711d1b8
ms.localizationpriority: medium
ms.openlocfilehash: df9acd948ea2dc964989803a550d9ee57ea5caf6
ms.sourcegitcommit: 6661f4d564d45ba10e5253864ac01e43b743c560
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104804796"
---
# <a name="controls-for-windows-apps"></a>Windows アプリ用のコントロール

![コントロール](../images/controls-2x.png)

Windows アプリの開発では、"<i>コントロール</i>" は、コンテンツを表示したり、操作を有効にしたりする UI 要素です。 コントロールとは、ユーザー インターフェイスの構成要素です。 <i>パターン</i>とは、いくつかのコントロールを組み合わせて、新しいものを作成するためのレシピです。

単純なボタンから、グリッド ビューのような強力なデータ コントロールまで、ユーザーが使用できる 45 種類以上のコントロールが用意されています。  これらのコントロールは Fluent Design System の一部です。すべでのデバイスやあらゆる画面サイズで見栄えがよく、力強い、スケーラブルな UI を作成できます。

このセクションの記事では、Windows アプリにコントロールとパターンを追加するための設計ガイダンスとコーディングの手順を示します。

## <a name="intro"></a>はじめに

XAML と C# でコントロールを追加し、スタイルを指定するための一般的な手順とコード例を示します。

:::row:::
    :::column:::
      <p><b><a href="controls-and-events-intro.md">コントロールを追加し、イベントを処理する</a></b> <br/>
アプリにコントロールを追加するには、3 つの重要な手順があります。アプリの UI にコントロールを追加し、コントロールのプロパティを設定し、コントロールを動作させるためのコードをコントロールのイベント ハンドラーに追加します。</p>
    :::column-end:::
    :::column:::
      <p><b><a href="xaml-styles.md">コントロールのスタイル指定</a></b> <br/>
XAML フレームワークを使って、さまざまな方法でアプリの外観をカスタマイズできます。 スタイルを使うと、コントロールのプロパティに値を設定し、その設定を再利用することで、複数のコントロールの外観を統一できます。</p>
    :::column-end:::
:::row-end:::

## <a name="get-the-windows-ui-library"></a>Windows UI ライブラリを入手する

:::row:::
   :::column:::
      ![WinUI ロゴ](images/winui-logo-64x64.png)
   :::column-end:::
   :::column span="3":::
      一部のコントロールは、Windows UI ライブラリ (WinUI) (新しいコントロールと UI 機能を含む NuGet パッケージ) でのみ入手可能です。 これを入手する場合は、[Windows UI ライブラリの概要とインストール手順](/uwp/toolkits/winui/)に関するページを参照してください。<br/>WinUI 2.2 から、多くのコントロールで既定のスタイルが更新され、角の丸めを使用するようになりました。 詳しくは、「[角の半径](../style/rounded-corner.md)」をご覧ください。
   :::column-end:::
   :::column:::

   :::column-end:::
:::row-end:::

## <a name="alphabetical-index"></a>アルファベット順インデックス

特定のコントロールとパターンに関する詳細情報を説明します。 

:::row:::
    :::column:::

- アニメーション化された視覚的プレーヤー ([Lottie](/windows/communitytoolkit/animations/lottie) をご覧ください) :::image type="icon" source="images/winui-logo-16x16.png":::
- [自動提案ボックス](auto-suggest-box.md)
- [ボタン](buttons.md)
- [カレンダーの日付の選択コントロール](calendar-date-picker.md)
- [カレンダー ビュー](calendar-view.md)
- [チェック ボックス](checkbox.md)
- [カラー ピッカー](color-picker.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [コンボ ボックス](combo-box.md)
- [コマンド バー](app-bars.md)
- [コマンド バーのポップアップ](command-bar-flyout.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [連絡先カード](contact-card.md)
- [コンテンツ ダイアログ](dialogs-and-flyouts/dialogs.md)
- [コンテンツ リンク](content-links.md)
- [コンテキスト メニュー](menus.md)
- [日付の選択コントロール](date-picker.md)
- [ダイアログとポップアップ](dialogs-and-flyouts/index.md)
- [ドロップ ダウン ボタン](buttons.md#create-a-drop-down-button) :::image type="icon" source="images/winui-logo-16x16.png":::
- [FlipView](flipview.md)
- [Flyout](dialogs-and-flyouts/flyouts.md)
- [フォーム](forms.md) (パターン)
- [グリッド ビュー](listview-and-gridview.md)
- [ハイパーリンク](hyperlinks.md)
- [ハイパーリンク ボタン](hyperlinks.md#create-a-hyperlinkbutton)
- [画像とイメージ ブラシ](images-imagebrushes.md)
- [インク コントロール](inking-controls.md)
- [リスト/詳細](list-details.md) (パターン)
- [リスト ビュー](listview-and-gridview.md)
- [マップ コントロール](../../maps-and-location/display-maps.md)
- [メディア再生](media-playback.md)
- [メニュー バー](menus.md#create-a-menu-bar) :::image type="icon" source="images/winui-logo-16x16.png":::
- [メニュー ポップアップ](menus.md)
- [ナビゲーション ビュー](navigationview.md) :::image type="icon" source="images/winui-logo-16x16.png":::

    :::column-end:::
    :::column:::

- [数値ボックス](number-box.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [視差ビュー](..\motion\parallax.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [パスワード ボックス](password-box.md)
- [ユーザー画像](person-picture.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [ピボット](pivot.md)
- [進行状況バー](progress-controls.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [進行状況リング](progress-controls.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [ラジオ ボタン](radio-button.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [評価コントロール](rating.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [繰り返しボタン](buttons.md#create-a-repeat-button)
- [リッチ エディット ボックス](rich-edit-box.md)
- [リッチ テキスト ブロック](rich-text-block.md)
- [スクロール ビューアー](scroll-controls.md)
- [検索](search.md) (パターン)
- [セマンティック ズーム](semantic-zoom.md)
- [図形](shapes.md)
- [スライダー](slider.md)
- [分割ボタン](buttons.md#create-a-split-button) :::image type="icon" source="images/winui-logo-16x16.png":::
- [分割ビュー](split-view.md)
- [スワイプ コントロール](swipe.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [タブ ビュー](tab-view.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [教育のヒント](dialogs-and-flyouts/teaching-tip.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [テキスト ブロック](text-block.md)
- [テキスト ボックス](text-box.md)
- [時刻の選択コントロール](time-picker.md)
- [トグル スイッチ](toggles.md)
- [トグル ボタン](buttons.md)
- [分割トグル ボタン](buttons.md#create-a-toggle-split-button)
- [ヒント](tooltips.md)
- [ツリー ビュー](tree-view.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [2 つのペインからなるビュー](two-pane-view.md) :::image type="icon" source="images/winui-logo-16x16.png":::
- [Web ビュー](web-view.md)

    :::column-end:::
:::row-end:::




## <a name="xaml-controls-gallery"></a>XAML コントロール ギャラリー

Microsoft Store から _XAML コントロール ギャラリー_ アプリを入手し、これらのコントロールおよび Fluent Design System の動作を確認します。 このアプリは、この Web サイトの対話型コンパニオンです。 このアプリがインストールされている場合、個々のコントロール ページのリンクを使用して、アプリを起動し、コントロールの動作を確認することができます。

<a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a>

<a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a>

<img src="images/xaml-controls-gallery.png" alt="XAML Controls Gallery screen" />

## <a name="additional-controls"></a>その他のコントロール

Windows 開発用の追加のコントロールは、<a href="https://www.telerik.com/">Telerik</a>、<a href="https://www.syncfusion.com/uwp-ui-controls">SyncFusion</a>、<a href="https://www.devexpress.com/Products/NET/Controls/Win10Apps/">DevExpress</a>、<a href="https://www.infragistics.com/products/universal-windows-platform">Infragistics</a>、<a href="https://www.componentone.com/Studio/Platform/UWP">ComponentOne</a>、<a href="https://www.actiprosoftware.com/products/controls/universal">ActiPro</a> などの企業から入手できます。 これらのコントロールは、カスタム コントロールおよびサービスによって標準システム コントロールを補うことにより、エンタープライズおよび .NET 開発者に追加のサポートを提供します。
