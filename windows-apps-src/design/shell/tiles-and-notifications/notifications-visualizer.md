---
Description: Notifications Visualizer は、Microsoft Store の新しい Windows アプリで、開発者が Windows 10 のアダプティブ ライブ タイルをデザインする際に役立ちます。
title: Notifications Visualizer
ms.assetid: FCBB7BB1-2C79-484B-8FFC-26FE1934EC1C
template: detail.hbs
ms.date: 09/24/2020
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: b50dc41a52d478afc9ed2fc9cf94d94dedb18ef4
ms.sourcegitcommit: eda7bbe9caa9d61126e11f0f1a98b12183df794d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2020
ms.locfileid: "91219925"
---
# <a name="notifications-visualizer"></a>Notifications Visualizer

 


通知ビジュアライザーは、開発者が Windows 10 のアダプティブライブタイルと対話型トースト通知をデザインするのに役立つ、 [ストア](https://www.microsoft.com/store/apps/notifications-visualizer/9nblggh5xsl1) の新しい Windows アプリです。


## <a name="overview"></a>概要

Notifications Visualizer では、Visual Studio の XAML エディター/デザイン ビューと同様、XML ペイロードを編集すると、タイルとトースト通知の視覚的なプレビューが即座に表示されます。 このアプリではエラーのチェックも行われます。これにより、有効なタイルまたはトースト通知のペイロードを作成できます。

次のアプリのスクリーンショットは、XML ペイロードと、各サイズのタイルが選んだデバイス上でどのように表示されるかを示しています。

![コードとタイルが示されている Notifications Visualizer アプリのエディター](images/notif-visualizer-001.png)

 

Notifications Visualizer を使うと、アプリ自体を編集、展開しなくても、アダプティブ タイルとトーストのペイロードを作成してテストすることができます。 適切な表示のペイロードが完成したら、そのペイロードをアプリに統合できます。 詳しくは、「[ローカル タイル通知の送信](sending-a-local-tile-notification.md)」および 「[ローカル トースト通知の送信](send-local-toast.md)」をご覧ください。

**メモ**   通知ビジュアライザーの Windows の [スタート] メニューとトースト通知のシミュレーションは、常に完全に正確ではありません。また、一部の高度なペイロードプロパティはサポートされていません。 タイルやトーストを適切にデザインしたら、意図したとおりに表示されることを確認するために、タイルをスタート メニューにピン留めしたり、トーストを表示したりしてテストします。

 

## <a name="features"></a>機能

Notifications Visualizer にはさまざまなサンプル ペイロードが付属しており、アダプティブ ライブ タイルや対話型トーストの機能を実際に確認して、作成を開始する際の参考にすることができます。 さまざまなテキスト オプション、グループ/サブグループ、背景画像を試すことができます。また、さまざまなデバイスや画面にタイルがどのように対応するかを確認することもできます。 サンプルに変更を加えたら、今後利用するために、更新したペイロードをファイルに保存できます。

エディターでは、リアルタイムにエラーと警告が示されます。 たとえば、アプリのペイロードが 5 KB (プラットフォームの上限) より大きい場合、上限を超えていることを示す警告が Notifications Visualizer によって表示されます。 Notifications Visualizer では誤った属性名や値に関する警告も示され、視覚的な問題をデバッグする際に役立ちます。

表示名、色、ロゴ、ShowName、バッジの値などのタイルのプロパティを制御することができます。 これらのオプションを使うと、タイルのプロパティとタイル通知のペイロードがどのように影響するのか、およびこれらのオプションによって生成される結果をすぐに理解できます。

次のアプリのスクリーンショットは、タイル エディターを示しています。

![タイルが示されている Notifications Visualizer のエディター](images/notif-visualizer-004.png)

 

## <a name="related-topics"></a>関連トピック

* [ストアでの Notifications Visualizer の入手](https://www.microsoft.com/store/apps/notifications-visualizer/9nblggh5xsl1)
* [アダプティブ タイルの作成](create-adaptive-tiles.md)
* [対話型トースト](adaptive-interactive-toasts.md)
