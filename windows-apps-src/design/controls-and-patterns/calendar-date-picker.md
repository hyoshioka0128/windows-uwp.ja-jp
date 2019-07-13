---
Description: カレンダーの日付の選択コントロールは、カレンダーの曜日や埋まり具合などのコンテキスト情報が必要となるカレンダー ビューから単一の日付を選ぶ用途に最適なドロップダウン コントロールです。
title: カレンダーの日付の選択コントロール
ms.assetid: 9e0213e0-046a-4906-ba86-0b49be51ca99
label: Calendar date picker
template: detail.hbs
ms.date: 05/19/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: kisai
design-contact: ksulliv
dev-contact: joyate
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 4de2f1cefc47e8740bfebbe7853ae317d25ab9d0
ms.sourcegitcommit: aaa4b898da5869c064097739cf3dc74c29474691
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "66363219"
---
# <a name="calendar-date-picker"></a>カレンダーの日付の選択コントロール

 

カレンダーの日付の選択コントロールは、カレンダーの曜日や埋まり具合などのコンテキスト情報が必要となるカレンダー ビューから単一の日付を選ぶ用途に最適なドロップダウン コントロールです。 追加のコンテキストを提供したり、使用可能な日付を制限したりするように、カレンダーを変更することもできます。

> **重要な API**:[CalendarDatePicker クラス](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarDatePicker)、[Date プロパティ](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.date)、[DateChanged イベント](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.datechanged)


## <a name="is-this-the-right-control"></a>適切なコントロールの選択
**カレンダーの日付の選択コントロール**を使うと、ユーザーはコンテキストに沿ったカレンダー ビューから 1 つの日付を選ぶことができます。 予定日や出発日の選択などに使います。

ユーザーが誕生日などの既知の日付 (カレンダーのコンテキストとしては重要ではない日) を選べるようにするには、[日付の選択コントロール](date-picker.md)を使うことを検討してください。

適切なコントロールの選択について詳しくは、「[日付と時刻コントロール](date-and-time.md)」をご覧ください。

## <a name="examples"></a>例

<table>
<th align="left">XAML コントロール ギャラリー<th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p><strong style="font-weight: semi-bold">XAML コントロール ギャラリー</strong> アプリがインストールされている場合、こちらをクリックして<a href="xamlcontrolsgallery:/item/CalendarDatePicker">アプリを開き、CalendarDatePicker の動作を確認</a>してください。</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></li>
    </ul>
</td>
</tr>
</table>

日付が設定されていない場合、エントリ ポイントにはプレースホルダー テキストが表示されます。設定されている場合は、選んだ日付が表示されます。 ユーザーがエントリ ポイントを選ぶと、カレンダー ビューが展開されて、ユーザーが日付を選べるようになります。 カレンダー ビューは他の UI をオーバーレイし、他の UI を別の位置に移動させることはありません。

![カレンダーの日付の選択コントロールの例](images/calendar-date-picker-2-views.png)

## <a name="create-a-date-picker"></a>日付の選択コントロールの作成

```xaml
<CalendarDatePicker x:Name="arrivalCalendarDatePicker" Header="Arrival date"/>
```

```csharp
CalendarDatePicker arrivalCalendarDatePicker = new CalendarDatePicker();
arrivalCalendarDatePicker.Header = "Arrival date";
```

結果として、カレンダーの日付の選択コントロールは、次のように表示されます。

![カレンダーの日付の選択コントロールの例](images/calendar-date-picker-closed.png)

カレンダーの日付の選択コントロールの内部には、日付選択用の [CalendarView](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.CalendarView) があります。 CalendarDatePicker には [IsTodayHighlighted](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.istodayhighlighted) や [FirstDayOfWeek](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.firstdayofweek) のような CalendarView プロパティのサブセットが存在し、内部の CalendarView に転送されるため、このサブセットを使って内部の CalendarView を変更できます。 

ただし、複数選択を許可するために、内部の CalendarView の [SelectionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendarview.selectionmode) を変更することはできません。 ユーザーが複数の日付を選べるようにしたり、カレンダーを常に表示しておく必要がある場合、カレンダーの日付の選択コントロールではなく、カレンダー ビューを使うことを検討してください。 カレンダー表示を変更する方法について詳しくは、「[カレンダー ビュー](calendar-view.md)」をご覧ください。

### <a name="selecting-dates"></a>日付の選択

選んだ日付を取得または設定するには、[Date](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.date) プロパティを使います。 既定では、Date プロパティは **null** です。 ユーザーがカレンダー ビューで日付を選ぶと、このプロパティが更新されます。 日付をクリアするには、カレンダー ビュー内で選んだ日付をクリックして選択を解除します。 

次のようなコードで日付を設定できます。

```csharp
myCalendarDatePicker.Date = new DateTime(1977, 1, 5);
```

コードで Date を設定するときに、その値は [MinDate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.mindate) プロパティと [MaxDate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.maxdate) プロパティの制約を受けます。
- **Date** の値が **MinDate** よりも小さい場合、Date の値は **MinDate** に設定されます。
- **Date** の値が **MaxDate** よりも大きい場合、Date の値は **MaxDate** に設定されます。

Date 値が変化したときに通知を受け取るには、[DateChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.datechanged) イベントを処理します。

> [!NOTE]
> 日付値の重要な情報については、「日付と時刻コントロール」の「[DateTime と Calendar の値](date-and-time.md#datetime-and-calendar-values)」をご覧ください。

### <a name="setting-a-header-and-placeholder-text"></a>ヘッダーとプレースホルダー テキストの設定

[Header](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.header) (ラベル) と [PlaceholderText](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.placeholdertext) (透かし) をカレンダーの日付の選択コントロールに追加すると、ユーザーに用途を示すことができます。 ヘッダーの外観をカスタマイズするには、Header ではなく [HeaderTemplate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.calendardatepicker.headertemplate) プロパティを設定します。

既定のプレースホルダー テキストは、"日付を選択" です。 PlaceholderText プロパティに空の文字列を設定してこのテキストを削除するか、次のようにカスタム テキストを指定することもできます。

```xaml
<CalendarDatePicker x:Name="arrivalCalendarDatePicker" Header="Arrival date" 
                    PlaceholderText="Choose your arrival date"/>
```

## <a name="get-the-sample-code"></a>サンプル コードを入手する

- [XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。

## <a name="related-articles"></a>関連記事

- [日付と時刻コントロール](date-and-time.md)
- [カレンダー ビュー](calendar-view.md)
- [日付の選択コントロール](date-picker.md)
- [時刻の選択コントロール](time-picker.md)
