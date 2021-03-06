---
title: Windows ランタイム コンポーネントに配列を渡す
description: Windows ユニバーサル プラットフォーム (UWP) では、パラメーターは入力または出力のどちらかに使用され、両方に使用されることはありません。 つまり、メソッドに渡される配列の内容および配列自体は、入力か出力のどちらかに使用されます。
ms.assetid: 8DE695AC-CEF2-438C-8F94-FB783EE18EB9
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: aedf33b6fab55aeb217a3b41a22b55f1cc5c9c5f
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372504"
---
# <a name="passing-arrays-to-a-windows-runtime-component"></a>Windows ランタイム コンポーネントに配列を渡す




Windows ユニバーサル プラットフォーム (UWP) では、パラメーターは入力または出力のどちらかに使用され、両方に使用されることはありません。 つまり、メソッドに渡される配列の内容および配列自体は、入力か出力のどちらかに使用されます。 配列の内容が入力に使用される場合、メソッドは配列から読み取りを行いますが、書き込みはしません。 配列の内容が出力に使用される場合、メソッドは配列に書き込みを行いますが、読み取りはしません。 .NET framework の配列は参照型であり、配列の参照が値 (Visual Basic では **ByVal**) で渡されるときも配列の内容は変更可能であるため、これは配列パラメーターにとって問題となります。 [Windows ランタイム メタデータのエクスポート ツール (Winmdexp.exe)](https://docs.microsoft.com/dotnet/framework/tools/winmdexp-exe-windows-runtime-metadata-export-tool) では、コンテキストから判別できない場合、パラメーターに ReadOnlyArrayAttribute 属性または WriteOnlyArrayAttribute 属性を適用して、配列の用途を指定する必要があります。 配列の使用方法は、次のように決定されます。

-   戻り値、または出力パラメーター (Visual Basic では、[OutAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.outattribute?redirectedfrom=MSDN) 属性の **ByRef** パラメーター) の場合、配列は常に出力に使用されます。 ReadOnlyArrayAttribute 属性は適用しないでください。 出力パラメーターで WriteOnlyArrayAttribute 属性を適用することはできますが、冗長になります。

    > **注意**  Visual Basic コンパイラが出力のみの規則を強制しません。 出力パラメーターからの読み取りは行わないでください。**Nothing** が含まれている可能性があります。 常に新しい配列を割り当ててください。
 
-   **ref** 修飾子 (Visual Basic では **ByRef**) を持つパラメーターは使用できません。 Winmdexp.exe によりエラーが生成されます。
-   値で渡されるパラメーターの場合、[ReadOnlyArrayAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime.readonlyarrayattribute?redirectedfrom=MSDN) 属性または [WriteOnlyArrayAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime.writeonlyarrayattribute?redirectedfrom=MSDN) 属性を適用して、配列の内容が入力と出力のどちらで使用されるのかを指定する必要があります。 両方の属性を指定すると、エラーになります。

メソッドで、入力の配列を受け取り、配列の内容を変更して、呼び出し元に配列を返す必要がある場合、入力には読み取り専用のパラメーター、出力には書き込み専用のパラメーター (または戻り値) を使用します。 次のコードは、このパターンを実装する 1 つの方法を示します。

> [!div class="tabbedCodeSnippets"]
> ```csharp
> public int[] ChangeArray([ReadOnlyArray()] int[] input)
> {
>     int[] output = input.Clone();
>     // Manipulate the copy.
>     //   ...
>     return output;
> }
> ```
> ```vb
> Public Function ChangeArray(<ReadOnlyArray> input() As Integer) As Integer()
>     Dim output() As Integer = input.Clone()
>     ' Manipulate the copy.
>     '   ...
>     Return output
> End Function
> ```

すぐに入力の配列をコピーして、利用することをお勧めします。 コピーして利用することにより、コンポーネントを .NET Framework のコードで呼び出すかどうかに関係なく、メソッドが同じように動作します。

## <a name="using-components-from-managed-and-unmanaged-code"></a>マネージ コードおよびアンマネージ コードからコンポーネントを使用する


ReadOnlyArrayAttribute 属性または WriteOnlyArrayAttribute 属性を持つパラメーターは、呼び出し元がネイティブ コードで記述されているか、マネージ コードで記述されているかによって、動作が異なります。 呼び出し元が、ネイティブ コード (JavaScript、または Visual C++ コンポーネント拡張機能) の場合、配列の内容は次のように処理されます。

-   ReadOnlyArrayAttribute:呼び出しがアプリケーション バイナリ インターフェイス (ABI) の境界を超えたときに、配列がコピーされます。 要素は必要に応じて変換されます。 このため、入力専用の配列に、メソッドで誤って変更が加えられた場合でも、呼び出し元では認識されません。
-   WriteOnlyArrayAttribute:呼び出されたメソッドには、元の配列の内容に関する想定をことはできません。 たとえば、メソッドが受け取る配列は、初期化されていなかったり既定値を含む可能性があります。 メソッドは、配列内のすべての要素に値を設定することが求められます。

呼び出し元がマネージ コードの場合、元の配列は .NET framework のメソッド呼び出しの中にあるため、呼び出されたメソッドでも使用可能です。 配列の内容は .NET Framework のコードで変更可能なため、メソッドが配列に加えた変更は、呼び出し元からも認識されます。 これは、Windows ランタイム コンポーネント用に作成された単体テストに影響するため、注意してください。 テストがマネージ コードで作成された場合、配列の内容はテスト中に変更可能になります。

## <a name="related-topics"></a>関連トピック

* [ReadOnlyArrayAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime.readonlyarrayattribute?redirectedfrom=MSDN)
* [WriteOnlyArrayAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime.writeonlyarrayattribute?redirectedfrom=MSDN)
* [C# および Visual Basic での Windows ランタイム コンポーネントの作成](creating-windows-runtime-components-in-csharp-and-visual-basic.md)
