---
title: 喪失デバイス
description: Direct3D デバイスは、稼働状態または喪失状態に設定できます。
ms.assetid: 1639CC02-8000-4208-AA95-91C1F0A3B08D
keywords:
- 喪失デバイス
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: d7f2c06564e0477fcec67418cae739e2fae123d7
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89158856"
---
# <a name="lost-devices"></a>喪失デバイス


Direct3D デバイスは、稼働状態または喪失状態に設定できます。 *稼働*状態は、デバイスが実行され、期待どおりにすべてのレンダリングが表示される、デバイスの通常の状態です。 全画面表示のアプリケーションでキーボード フォーカスが失われるなどのイベントによって、レンダリングが不可能になると、デバイスは*喪失*状態に移行します。 喪失状態には、すべてのレンダリング操作のサイレント エラーという特徴があります。つまり、レンダリング操作に失敗しても、レンダリング メソッドが成功コードを返すことがあります。

仕様上、デバイスが喪失になる可能性があるあらゆるシナリオ セットが定められているわけではありません。 一般的な例には、ユーザーが Alt + Tab を押した場合やシステム ダイアログが初期化された場合など、フォーカスの喪失が含まれます。 電源管理インベントや、別のアプリケーションが全画面操作を引き受けた場合などのためにデバイスが喪失することもあります。 加えて、デバイスのリセットによるエラーによってもデバイスが喪失状態になります。

[**IUnknown**](/windows/desktop/api/unknwn/nn-unknwn-iunknown) から派生したすべてのメソッドは、デバイスが喪失した後も動作することが保証されています。 デバイスの喪失後、各機能には一般に次の 3 つのオプションがあります。

-   "デバイス喪失" エラーによって失敗する - これは、何らかの操作が正常でないことをアプリケーションが識別できるように、そのデバイスが喪失したことをアプリケーションが認識する必要があることを意味します。
-   自動的に失敗し、S \_ OK またはその他のリターンコードが返されます。関数がサイレントに失敗した場合、アプリケーションは通常、"成功" と "サイレントエラー" の結果を区別できません。
-   リターン コードを返す。

## <a name="span-idresponding_to_a_lost_devicespanspan-idresponding_to_a_lost_devicespanspan-idresponding_to_a_lost_devicespanresponding-to-a-lost-device"></a><span id="Responding_to_a_Lost_Device"></span><span id="responding_to_a_lost_device"></span><span id="RESPONDING_TO_A_LOST_DEVICE"></span>紛失したデバイスへの応答


喪失デバイスは、リセット後にリソース (ビデオ メモリ リソースなど) を再作成する必要があります。 デバイスが喪失した場合、アプリケーションは動作状態に復元できるかどうかを確認するようデバイスに問い合わせます。 復元でない場合、アプリケーションはデバイスが復元可能になるまで待機します。

デバイスが復元可能な場合、アプリケーションはすべてのビデオ メモリ リソースとスワップ チェーンを破棄することによってデバイスを準備します。 リセットは、デバイスが喪失したときに効果がある唯一の手順であり、アプリケーションがデバイスを喪失状態から動作状態に変えることができる唯一の方法です。 アプリケーションが割り当てられたすべてのリソース (レンダー ターゲットや深度ステンシル サーフェスなど) を解放しなければ、リセットに失敗します。

ほとんどの場合、Direct3D を高頻度で呼び出すと、デバイスが喪失したかどうかに関する情報が返されません。 アプリケーションは、レンダリング メソッドの呼び出しを続けますが、喪失デバイスの通知は受け取りません。 内部では、デバイスが動作状態にリセットされるまでこれらの操作は破棄されます。

## <a name="span-idlocking_operationsspanspan-idlocking_operationsspanspan-idlocking_operationsspanlocking-operations"></a><span id="Locking_Operations"></span><span id="locking_operations"></span><span id="LOCKING_OPERATIONS"></span>ロック操作


内部では、デバイスが喪失した後にロック操作を成功させるための処理を Direct3D は十分に行いません。 ただし、ロック操作中にビデオ メモリ リソースのデータが正確であることは保証されません。 エラー コードが返されないことは保証されます。 このため、ロック操作中にデバイスが喪失することを気にせずにアプリケーションを記述できます。

## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanresources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>参考


リソースは、ビデオ メモリを消費する可能性があります。 喪失デバイスはアダプターが所有するビデオ メモリから切断されるため、デバイス喪失したときにビデオ メモリの割り当てを保証することはできません。 このため、すべてのリソース作成メソッドが成功するように実装されていますが、実際にはダミー システム メモリのみ割り当てられます。 デバイスをサイズ変更する前にビデオ メモリ リソースを破棄する必要があるため、ビデオ メモリの過剰割り当ての問題は発生しません。 これらのダミー サーフェスにより、そのデバイスが喪失したことをアプリケーションが検出するまでロック操作とコピー操作が正常に機能しているように見えます。

デバイスを喪失状態から動作状態にリセットするには、すべてのビデオ メモリを解放する必要があります。 他の状態データは、動作状態への遷移時に自動的に破棄されます。

デバイス喪失に対応するため、単一のコード パスでアプリケーションを開発することをお勧めします。 このコード パスは、起動時にデバイスを初期化するコード パスとまったく同じとは言わないまでもほぼ同様です。

## <a name="span-idretrieved_dataspanspan-idretrieved_dataspanspan-idretrieved_dataspanretrieved-data"></a><span id="Retrieved_Data"></span><span id="retrieved_data"></span><span id="RETRIEVED_DATA"></span>取得されたデータ


Direct3D を使うと、アプリケーションはテクスチャを検証し、ハードウェアによる単一パス レンダリングとは異なる方法で状態をレンダリングできます。

さらに、Direct3D を使うと、アプリケーションは生成されたイメージや以前に書き込まれたイメージをビデオ メモリ リソースから不揮発性システム メモリ リソースにコピーできます。 そのような転送のソース イメージはいつでも失われる可能性があるため、Direct3D ではデバイスが喪失するとそのコピー操作を失敗させることができます。

デバイスが喪失すると、プライマリ サーフェスがないためコピー操作が失敗する可能性があります。 デバイスが喪失するとバック バッファーを作成できないため、スワップ チェーンの作成も失敗する可能性があります。

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>関連トピック


[デバイス](devices.md)

 

 