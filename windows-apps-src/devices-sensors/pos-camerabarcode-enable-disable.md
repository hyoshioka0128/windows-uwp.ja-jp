---
title: カメラ バーコード スキャナーの構成
description: カメラ バーコード スキャナーの有効化と無効化
ms.date: 4/8/2019
ms.topic: article
keywords: Windows 10, UWP, 店舗販売時点管理, POS
ms.localizationpriority: medium
ms.openlocfilehash: 7db48b610d5bdf256d6a44d4786b8642d984c0b0
ms.sourcegitcommit: 6f32604876ed480e8238c86101366a8d106c7d4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2019
ms.locfileid: "67321536"
---
# <a name="enable-or-disable-the-software-decoder-that-ships-with-windows"></a>Windows に付属するソフトウェア デコーダーを有効または無効にします。

Windows 10 バージョン 1803 では、ソフトウェア デコーダーがインストールされ、既定で有効になっています。  カメラ バーコード スキャナーを使用しない場合、Windows.Devices.PointOfService.BarcodeScanner API で動作するサード パーティ製のデコーダーを入手した場合、およびそのどちらも使用しない場合は、ソフトウェア デコーダーを無効にすることができます。

## <a name="enable-or-disable-using-the-system-registry"></a>システム レジストリを使用して有効または無効にする

システム レジストリを使用して、Windows に付属するソフトウェア デコーダーを有効または無効にするには、*HKLM\Software\Microsoft\PointOfService\BarcodeScanner* の下にレジストリ キー *InboxDecoder* を追加し、*Enable* の値を以下に示すように設定します。

| 値の名前  | 値の種類 | Value | 状況 |
| ----------- | --------- | -------|--------|
| Enable      | DWORD     | 1 (既定)<br/>0 |  Windows に付属するソフトウェア デコーダーを有効にします。 <br/> Windows に付属するソフトウェア デコーダーを無効にします。 |

Windows に付属するソフトウェア デコーダーを**無効にする**ために使用できるレジストリ ファイルの例を次に示します。

```text
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PointOfService\BarcodeScanner\InboxDecoder]
"Enable"=dword:0000000
```  

次のレジストリ ファイルの例を使用すると、Windows に付属するソフトウェア デコーダーを**有効にする**ことができます。

```text
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PointOfService\BarcodeScanner\InboxDecoder]
"Enable"=dword:0000001
```  

> [!Warning]
> 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。  さらに安全を考慮して、レジストリのバックアップをとってから変更を行ってください。  バックアップがあれば、問題が生じた場合でもレジストリを復元できます。  バックアップおよび復元方法の詳細を参照するには、以下の Microsoft サポート技術情報番号をクリックしてください。 <br/><br/> [322756](https://support.microsoft.com/help/322756/how-to-back-up-and-restore-the-registry-in-windows) Windows でレジストリをバックアップおよび復元する方法

> [!NOTE]
> Windows 10 に付属するソフトウェア デコーダーは、[**Digimarc Corporation**](https://www.digimarc.com/) から無料で提供されています。
