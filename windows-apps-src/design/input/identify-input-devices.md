---
Description: Windows アプリデバイスに接続されている入力デバイスを特定し、それらの機能と属性を特定します。
title: 入力デバイスの識別
ms.assetid: B2E93FBF-C508-44D9-BA46-ECFDAA8746F4
label: Identify input devices
template: detail.hbs
keywords: デバイス, デジタイザー, 入力, 操作
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: afd0a855ce35ecb37eb55ac8788ec51c063e8da7
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173436"
---
# <a name="identify-input-devices"></a>入力デバイスの識別


Windows アプリデバイスに接続されている入力デバイスを特定し、それらの機能と属性を特定します。

> **重要な API**: [**Windows.Devices.Input**](/uwp/api/Windows.Devices.Input)、[**Windows.UI.Input**](/uwp/api/Windows.UI.Core)、[**Windows.UI.Xaml.Input**](/uwp/api/Windows.UI.Input)

## <a name="retrieve-mouse-properties"></a>マウスのプロパティの取得


接続されているマウスによって公開されているプロパティを取得するには、[**Windows.Devices.Input**](/uwp/api/Windows.Devices.Input) 名前空間の [**MouseCapabilities**](/uwp/api/Windows.Devices.Input.MouseCapabilities) クラスを使います。 新しい **MouseCapabilities** オブジェクトを作成し、目的のプロパティを取得するだけです。

**メモ**   ここで説明するプロパティによって返される値は、検出されたすべてのマウスに基づいています。1つ以上のマウスが特定の機能をサポートし、数値プロパティが任意の1つのマウスによって公開される最大値を返す場合、ブール型プロパティは0以外の値を返します。

 

次のコードでは、一連の [**TextBlock**](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) 要素を使って、個別のマウスのプロパティと値を表示しています。

```CSharp
private void GetMouseProperties()
{
    MouseCapabilities mouseCapabilities = new Windows.Devices.Input.MouseCapabilities();
    MousePresent.Text = mouseCapabilities.MousePresent != 0 ? "Yes" : "No";
    VertWheel.Text = mouseCapabilities.VerticalWheelPresent != 0 ? "Yes" : "No";
    HorzWheel.Text = mouseCapabilities.HorizontalWheelPresent != 0 ? "Yes" : "No";
    SwappedButtons.Text = mouseCapabilities.SwapButtons != 0 ? "Yes" : "No";
    NumButtons.Text = mouseCapabilities.NumberOfButtons.ToString();
}
```

## <a name="retrieve-keyboard-properties"></a>キーボードのプロパティの取得


キーボードが接続されているかどうかを取得するには、[**Windows.Devices.Input**](/uwp/api/Windows.Devices.Input) 名前空間の [**KeyboardCapabilities**](/uwp/api/Windows.Devices.Input.KeyboardCapabilities) クラスを使います。 新しい **KeyboardCapabilities** オブジェクトを作成し、[**KeyboardPresent**](/uwp/api/windows.devices.input.keyboardcapabilities.keyboardpresent) プロパティを取得するだけです。

次のコードでは、[**TextBlock**](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) 要素を使って、キーボードのプロパティと値を表示しています。

```CSharp
private void GetKeyboardProperties()
{
    KeyboardCapabilities keyboardCapabilities = new Windows.Devices.Input.KeyboardCapabilities();
    KeyboardPresent.Text = keyboardCapabilities.KeyboardPresent != 0 ? "Yes" : "No";
}
```

## <a name="retrieve-touch-properties"></a>タッチのプロパティの取得


タッチ デジタイザーが接続されているかどうかを取得するには、[**Windows.Devices.Input**](/uwp/api/Windows.Devices.Input) 名前空間の [**TouchCapabilities**](/uwp/api/Windows.Devices.Input.TouchCapabilities) クラスを使います。 新しい **TouchCapabilities** オブジェクトを作成し、目的のプロパティを取得するだけです。

**メモ**   ここで説明するプロパティによって返される値は、検出されたすべてのタッチデジタイザーに基づきます。少なくとも1つのデジタイザーが特定の機能をサポートし、数値プロパティが1つのデジタイザーによって公開された最大値を返す場合、ブール型プロパティは0以外の値を返します。

 

次のコードでは、一連の [**TextBlock**](/uwp/api/Windows.UI.Xaml.Controls.TextBlock) 要素を使って、タッチのプロパティと値を表示しています。

```CSharp
private void GetTouchProperties()
{
    TouchCapabilities touchCapabilities = new Windows.Devices.Input.TouchCapabilities();
    TouchPresent.Text = touchCapabilities.TouchPresent != 0 ? "Yes" : "No";
    Contacts.Text = touchCapabilities.Contacts.ToString();
}
```

## <a name="retrieve-pointer-properties"></a>ポインターのプロパティの取得


検出されたデバイスがポインター入力 (タッチ、タッチパッド、マウス、ペン) をサポートしているかどうかを取得するには、[**Windows.Devices.Input**](/uwp/api/Windows.Devices.Input) 名前空間の [**PointerDevice**](/uwp/api/Windows.Devices.Input.PointerDevice) クラスを使います。 新しい **PointerDevice** オブジェクトを作成し、目的のプロパティを取得するだけです。

**メモ**   ここで説明するプロパティによって返される値は、検出されたすべてのポインターデバイスに基づいています。1つ以上のデバイスが特定の機能をサポートし、数値プロパティが1つのポインターデバイスによって公開される最大値を返す場合、ブール型プロパティは0以外の値を返します。

次のコードでは、テーブルを使って、各ポインター デバイスのプロパティと値を表示しています。

```CSharp
private void GetPointerDevices()
{
    IReadOnlyList<PointerDevice> pointerDevices = Windows.Devices.Input.PointerDevice.GetPointerDevices();
    int gridRow = 0;
    int gridColumn = 0;

    for (int i = 0; i < pointerDevices.Count; i++)
    {
        // Pointer device type.
        TextBlock textBlock1 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock1);
        textBlock1.Text = (i + 1).ToString() + " Pointer Device Type:";
        Grid.SetRow(textBlock1, gridRow);
        Grid.SetColumn(textBlock1, gridColumn);

        TextBlock textBlock2 = new TextBlock();
        textBlock2.Text = pointerDevices[i].PointerDeviceType.ToString();
        Grid_PointerProps.Children.Add(textBlock2);
        Grid.SetRow(textBlock2, gridRow++);
        Grid.SetColumn(textBlock2, gridColumn + 1);

        // Is external?
        TextBlock textBlock3 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock3);
        textBlock3.Text = (i + 1).ToString() + " Is External?";
        Grid.SetRow(textBlock3, gridRow);
        Grid.SetColumn(textBlock3, gridColumn);

        TextBlock textBlock4 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock4);
        textBlock4.Text = pointerDevices[i].IsIntegrated.ToString();
        Grid.SetRow(textBlock4, gridRow++);
        Grid.SetColumn(textBlock4, gridColumn + 1);

        // Maximum contacts.
        TextBlock textBlock5 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock5);
        textBlock5.Text = (i + 1).ToString() + " Max Contacts:";
        Grid.SetRow(textBlock5, gridRow);
        Grid.SetColumn(textBlock5, gridColumn);

        TextBlock textBlock6 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock6);
        textBlock6.Text = pointerDevices[i].MaxContacts.ToString();
        Grid.SetRow(textBlock6, gridRow++);
        Grid.SetColumn(textBlock6, gridColumn + 1);

        // Physical device rectangle.
        TextBlock textBlock7 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock7);
        textBlock7.Text = (i + 1).ToString() + " Physical Device Rect:";
        Grid.SetRow(textBlock7, gridRow);
        Grid.SetColumn(textBlock7, gridColumn);

        TextBlock textBlock8 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock8);
        textBlock8.Text = pointerDevices[i].PhysicalDeviceRect.X.ToString() + "," +
            pointerDevices[i].PhysicalDeviceRect.Y.ToString() + "," +
            pointerDevices[i].PhysicalDeviceRect.Width.ToString() + "," +
            pointerDevices[i].PhysicalDeviceRect.Height.ToString();
        Grid.SetRow(textBlock8, gridRow++);
        Grid.SetColumn(textBlock8, gridColumn + 1);

        // Screen rectangle.
        TextBlock textBlock9 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock9);
        textBlock9.Text = (i + 1).ToString() + " Screen Rect:";
        Grid.SetRow(textBlock9, gridRow);
        Grid.SetColumn(textBlock9, gridColumn);

        TextBlock textBlock10 = new TextBlock();
        Grid_PointerProps.Children.Add(textBlock10);
        textBlock10.Text = pointerDevices[i].ScreenRect.X.ToString() + "," +
            pointerDevices[i].ScreenRect.Y.ToString() + "," +
            pointerDevices[i].ScreenRect.Width.ToString() + "," +
            pointerDevices[i].ScreenRect.Height.ToString();
        Grid.SetRow(textBlock10, gridRow++);
        Grid.SetColumn(textBlock10, gridColumn + 1);

        gridColumn += 2;
        gridRow = 0;
    }
```

## <a name="related-articles"></a>関連記事

### <a name="samples"></a>サンプル

- [基本的な入力のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/BasicInput)
- [待機時間が短い入力のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/LowLatencyInput)
- [ユーザー操作モードのサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/UserInteractionMode)

### <a name="archive-samples"></a>サンプルのアーカイブ

- [入力: デバイス機能のサンプルに関するページ](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Windows%208%20app%20samples/%5BC%23%5D-Windows%208%20app%20samples/C%23/Windows%208%20app%20samples/Input%20Device%20capabilities%20sample%20(Windows%208))