---
ms.assetid: cf0d2709-21a1-4d56-9341-d4897e405f5d
description: アプリで AdControl エラーをキャッチする方法について説明します。
title: XAML/C# ウォークスルーでのエラー処理
ms.date: 05/11/2018
ms.topic: article
keywords: Windows 10, UWP, 広告, 宣伝, エラー処理, XAML, C#
ms.localizationpriority: medium
ms.openlocfilehash: c0b8389d2319a670dd314417726b24e98378cd49
ms.sourcegitcommit: 6a7dd4da2fc31ced7d1cdc6f7cf79c2e55dc5833
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "58334470"
---
# <a name="error-handling-in-xamlc-walkthrough"></a>XAML/C# ウォークスルーでのエラー処理

このチュートリアルでは、アプリで広告関連のエラーをキャッチする方法について説明します。 このチュートリアルでは、[AdControl](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol) を使用してバナー広告を表示していますが、その中の一般的な概念はスポット広告やネイティブ広告にも適用されます。

これらの例は、**AdControl** を含む XAML/C# アプリがあることを前提としています。 アプリに **AdControl** を追加する方法を示す具体的な手順については、「[XAML および .NET の AdControl](adcontrol-in-xaml-and--net.md)」をご覧ください。 

1.  MainPage.xaml ファイルで、**AdControl** の定義を見つけます。 コードは次のようになります。
    ``` xml
    <UI:AdControl
      ApplicationId="3f83fe91-d6be-434d-a0ae-7351c5a997f1"
      AdUnitId="test"
      HorizontalAlignment="Left"
      Height="250"
      Margin="10,10,0,0"
      VerticalAlignment="Top"
      Width="300" />
    ```

2.   **Width** プロパティの後、終了タグの前で、エラー イベント ハンドラーの名前を [ErrorOccurred](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.erroroccurred) イベントに割り当てます。 このウォークスルーでは、エラー イベント ハンドラーの名前は **OnAdError** です。
    ``` xml
    <UI:AdControl
      ApplicationId="3f83fe91-d6be-434d-a0ae-7351c5a997f1"
      AdUnitId="test"
      HorizontalAlignment="Left"
      Height="250"
      Margin="10,10,0,0"
      VerticalAlignment="Top"
      Width="300"
      ErrorOccurred="OnAdError"/>
    ```

3.  実行時にエラーを生成するために、2 つ目の **AdControl** を異なるアプリケーション ID を使って作成します。 アプリ内のすべての **AdControl** オブジェクトは同じアプリケーション ID を使う必要があるため、追加の **AdControl** を異なるアプリケーション ID を使って作成するとエラーがスローされます。

    MainPage.xaml で、最初の **AdControl** の直後に 2 つ目の **AdControl** を定義し、[ApplicationId](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol.applicationid) プロパティをゼロ (“0”) に設定します。
    ``` xml
    <UI:AdControl
        ApplicationId="0"
        AdUnitId="test"
        HorizontalAlignment="Left"
        Height="250"
        Margin="10,265,0,0"
        VerticalAlignment="Top"
        Width="300"
        ErrorOccurred="OnAdError" />
    ```

4.  MainPage.xaml.cs で、次の **OnAdError** イベント ハンドラーを **MainPage** クラスに追加します。 このイベント ハンドラーは、Visual Studio の **[出力]** ウィンドウに情報を書き込みます。
    ``` csharp
    private void OnAdError(object sender, AdErrorEventArgs e)
    {
        System.Diagnostics.Debug.WriteLine("AdControl error (" + ((AdControl)sender).Name +
            "): " + e.ErrorMessage + " ErrorCode: " + e.ErrorCode.ToString());
    }
    ```

4.  プロジェクトをビルドして実行します。 アプリの実行後に、次のようなメッセージが Visual Studio の **[出力]** ウィンドウに表示されます。
    ```json
    AdControl error (): MicrosoftAdvertising.Shared.AdException: all ad requests must use the same application ID within a single application (0, d25517cb-12d4-4699-8bdc-52040c712cab) ErrorCode: ClientConfiguration
    ```

## <a name="related-topics"></a>関連トピック

* [GitHub の広告サンプル](https://aka.ms/githubads)
