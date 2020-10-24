---
title: カメラ バーコード スキャナーのシンボル体系
description: Windows 10 に付属するソフトウェアバーコードデコーダーでサポートされている各 symbologies のサンプルバーコードを表示します。
ms.date: 05/02/2018
ms.topic: article
keywords: Windows 10, UWP, 店舗販売時点管理, POS
ms.localizationpriority: medium
ms.openlocfilehash: a9618402a6ee76a20ff5f95418ee7280b39db4a2
ms.sourcegitcommit: 8e0e4cac79554e86dc7f035c4b32cb1f229142b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88943132"
---
# <a name="symbologies"></a>シンボル体系

このトピックでは、Windows 10 に付属しているソフトウェア バーコード デコーダーでサポートされている各シンボル体系のサンプル バーコードを示します。UPC/EAN、Code 39、Code 128、Interleaved 2 of 5、Databar Omnidirectional、Databar Stacked、QR コード、GS1DWCode などが含まれます。

Windows 10 では、標準のレンズカメラとソフトウェアデコーダーを組み合わせて、バーコードスキャナーを生成します。 この記事では、ソフトウェアデコーダーでサポートされている symbologies について説明します。 ハードウェアデコーダーが組み込まれている専用バーコードスキャナーデバイスでは、追加の symbologies がサポートされる場合があります。詳細については、バーコードスキャナーの製造元にお問い合わせください。 記載されている symbologies は、特に指定がない限り、Windows 10 ビルド17134以降のすべてのエディションでサポートされています。

[GetSupportedSymbologiesAsync](/uwp/api/windows.devices.pointofservice.barcodescanner.getsupportedsymbologiesasync)を使用して、バーコードスキャナーでサポートされている特定の symbologies を特定します。

> [!NOTE]
> Windows 10 に組み込まれているソフトウェアデコーダーは、 [*Digimarc Corporation*](https://www.digimarc.com/)によって提供されています。

## <a name="1d-symbologies"></a>1D シンボル体系

### <a name="code-39"></a>Code 39
![サンプル バーコード - Code 39](images/pos/sample-barcode-code39.png)

### <a name="code-128"></a>Code 128
![サンプル バーコード - Code 128](images/pos/sample-barcode-code128.png)

### <a name="databar-omnidirectional"></a>Databar Omnidirectional
![サンプル バーコード - Databar Omnidirectional](images/pos/sample-barcode-databar-omnidirectional.png) 
### <a name="databar-stacked"></a>Databar Stacked
![サンプル バーコード - Databar Stacked](images/pos/sample-barcode-databar-stacked.png)

### <a name="ean-8"></a>EAN-8
![サンプル バーコード - EAN-8](images/pos/sample-barcode-ean8.png)

### <a name="ean-13"></a>EAN-13
![サンプル バーコード - EAN-13](images/pos/sample-barcode-ean13.png)

### <a name="interleaved-2-of-5"></a>Interleaved 2 of 5
![サンプル バーコード - Interleaved 2 of 5](images/pos/sample-barcode-interleaved-2-of-5.png)

### <a name="upc-a"></a>UPC-A
![サンプル バーコード - UPC A](images/pos/sample-barcode-upca.png)

### <a name="upc-e"></a>UPC-E
![サンプル バーコード - UPC E](images/pos/sample-barcode-upce.png)

## <a name="2d-symbologies"></a>2D シンボル体系
### <a name="qr-code"></a>QR コード
![サンプル バーコード - QR コード](images/pos/sample-barcode-qrcode.png)

## <a name="digital-watermark"></a>電子透かし
### <a name="gs1-dwcode"></a>GS1-DWCode

カメラ バーコード スキャナー アプリケーションを使用して以下のパッケージの画像をスキャンすると、GS1DWCode の動作を確認できます。  この画像は、UPCA 856107006854 でエンコードされています。  GS1DWCode 機能の詳細については、http://www.digimarc.com を参照してください。

![サンプル バーコード - GS1DWCode](images/pos/Rice-Box-V7.jpg)

## <a name="see-also"></a>関連項目

### <a name="samples"></a>サンプル

- [バーコード スキャナーのサンプル](https://github.com/microsoft/Windows-universal-samples/tree/master/Samples/BarcodeScanner)
