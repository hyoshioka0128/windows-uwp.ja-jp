---
Description: ユニバーサル Windows プラットフォーム (UWP) アプリがアクセシビリティ対応であると Microsoft Store で宣言するための要件について説明します。
ms.assetid: 59FA3B87-75A6-4B30-BA7C-A0E769D68050
title: ストア内のアクセシビリティ
label: Accessibility in the Store
template: detail.hbs
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 8f00bb9449d9e48518d16e08fa6b6665eecd2f85
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66359742"
---
# <a name="accessibility-in-the-store"></a>ストア内のアクセシビリティ  



ユニバーサル Windows プラットフォーム (UWP) アプリがアクセシビリティ対応であると Microsoft Store で宣言するための要件について説明します。

Microsoft Store で認定を受けるためにアプリを提出している間に、アプリがアクセシビリティ対応であることを宣言することができます。 アクセシビリティ対応アプリであることを宣言すると、視覚に障碍があるユーザーのように、アクセシビリティ対応アプリに興味を持っているユーザーが簡単にそのアプリを見つけられるようになります。 ユーザーは、Microsoft Store での検索時に**アクセシビリティ対応**のフィルターを使うことで、アクセシビリティ対応アプリを見つけます。 また、アクセシビリティ対応アプリであることを宣言すると、アプリの説明に**アクセシビリティ対応**のタグが追加されます。

アプリがアクセシビリティ対応であることを宣言して、次のうちの 1 つ以上を使う主なシナリオでユーザーが必要とする [基本的なアクセシビリティ情報](basic-accessibility-information.md) が用意されていることを示します。

* キーボード。
* ハイ コントラスト テーマ。
* 可変 DPI (1 インチあたりのドット数) の設定。
* Windows アクセシビリティ機能 (ナレーター、拡大鏡、スクリーン キーボードなど) のような一般的な支援技術。

アプリをアクセシビリティ対応としてビルドし、テストした場合は、アプリをアクセシビリティ対応として宣言する必要があります。 これは、次のことが完了していることを意味します。

* 名前、役割、値などの UI 要素に関するすべてのアクセシビリティ情報を設定している。
* キーボードの完全なアクセシビリティを実装している。ユーザーは次のことができる。
    * キーボードのみを使ってアプリの主なシナリオを達成する。
    * Tab キーを使って論理的な順序で UI 要素を切り替える。
    * 方向キーを使ってコントロール内の UI 要素間を移動する。
    * キーボード ショートカットを使ってアプリの主な機能を利用する。
    * キーボードがないデバイスで、タブと矢印を同等に扱うためにナレーターのタッチ ジェスチャを使う。
* アプリの UI が視覚上のアクセシビリティに対応している。最低でも 4.5:1 のテキスト コントラスト比がある、情報を伝えるときに色だけに依存していない、など。
* [  **Inspect**](https://docs.microsoft.com/windows/desktop/WinAuto/inspect-objects)、[**UIAVerify**](https://docs.microsoft.com/windows/desktop/WinAuto/ui-automation-verify) などのアクセシビリティ テスト ツールを使ってアクセシビリティの実装が検証されていて、このようなツールで報告される優先度 1 のエラーをすべて解決している。
* ナレーター、拡大鏡、スクリーン キーボード、ハイ コントラスト テーマ、調整された DPI 設定を使って、エンド ツー エンドでアプリの主なシナリオを検証している。

これらの手順と、その実行に役立つリソースへのリンクを確認する場合は、「[アクセシビリティのチェック リスト](accessibility-checklist.md)」をご覧ください。

<span id="related_topics"/>

## <a name="related-topics"></a>関連トピック    
* [ユーザー補助](accessibility.md) 
