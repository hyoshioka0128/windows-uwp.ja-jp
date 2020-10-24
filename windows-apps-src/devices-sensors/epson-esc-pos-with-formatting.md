---
ms.assetid: 70667353-152B-4B18-92C1-0178298052D4
title: 書式設定における Epson ESC/POS
description: POS プリンターで、ESC/POS コマンド言語を使用して、太字、倍角文字など、テキストの書式を設定する方法について説明します。
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 9fa9a0746e65fe3cbb42ce140a62a3129023d011
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89165456"
---
# <a name="epson-escpos-with-formatting"></a>書式設定における Epson ESC/POS


**重要な API**

-   [**PointofService プリンター**](/uwp/api/Windows.Devices.PointOfService)
-   [**Windows.Devices.PointOfService**](/uwp/api/Windows.Devices.PointOfService)

POS プリンターで、ESC/POS コマンド言語を使用して、太字、倍角文字など、テキストの書式を設定する方法について説明します。

## <a name="escpos-usage"></a>ESC/POS の使い方

Windows Point of Service (POS) では、Epson の TM シリーズのプリンターなど、さまざまなプリンターを使用できます。サポートされているプリンターの完全な一覧は、[PointofService プリンター](/uwp/api/Windows.Devices.PointOfService)のページをご覧ください。 Windows では、ESC/POS プリンター制御言語を使用した印刷をサポートしています。この制御言語により、お使いのプリンターと通信するときに、効率的で実用的なコマンドを使用できます。

ESC/POS は、Epson が開発したコマンド システムで、広範囲の POS プリンター システムで使用されています。どのプリンターにも適用可能にすることで、コマンド セットの非互換性を回避することを目的としています。 現在のほとんどのプリンターでは、ESC/POS がサポートされています。

すべてのコマンドは、ESC 文字 (ASCII 27、16 進の 1B) または GS (ASCII 29、16 進の 1D) で始まり、その後にコマンドを指定する別の文字が続きます。 通常のテキストは単純にプリンターに送信され、改行で区切られます。

[**Windows PointOfService API**](/uwp/api/Windows.Devices.PointOfService) では、その機能の大半を **Print()** または **PrintLine()** メソッドを通して提供します。 ただし、特定の書式を設定する、または特定のコマンドを送信するには、ESC/POS コマンドを使用して文字列として作成し、プリンターに送信する必要があります。

## <a name="example-using-bold-and-double-size-characters"></a>文字および倍角文字を使用する例

次の例は、ESC/POS コマンドを使用して、太字および倍角文字で印刷する方法を示しています。 各コマンドが文字列として作成され、印刷ジョブの呼び出しに挿入されていることに注意してください。

```csharp
// … prior plumbing code removed for brevity
// this code assumed you've already created a receipt print job (printJob)
// and also that you've already checked the PosPrinter Capabilities to
// verify that the printer supports Bold and DoubleHighDoubleWide print modes

const string ESC = "\u001B";
const string GS = "\u001D";
const string InitializePrinter = ESC + "@";
const string BoldOn = ESC + "E" + "\u0001";
const string BoldOff = ESC + "E" + "\0";
const string DoubleOn = GS + "!" + "\u0011";  // 2x sized text (double-high + double-wide)
const string DoubleOff = GS + "!" + "\0";

printJob.Print(InitializePrinter);
printJob.PrintLine("Here is some normal text.");
printJob.PrintLine(BoldOn + "Here is some bold text." + BoldOff);
printJob.PrintLine(DoubleOn + "Here is some large text." + DoubleOff);

printJob.ExecuteAsync();
```

利用可能なコマンドなど、ESC/POS について詳しくは、[Epson ESC/POS に関する FAQ](https://content.epson.de/fileadmin/content/files/RSD/downloads/escpos.pdf) をご覧ください。 [**Windows.Devices.PointOfService**](/uwp/api/Windows.Devices.PointOfService) と利用可能な機能について詳しくは、MSDN の「[PointofService プリンター](/uwp/api/Windows.Devices.PointOfService)」をご覧ください。