---
description: ここでは、ほとんどの XAML ファイルのルート要素で行われる XML/XAML 名前空間 (xmlns) マッピングについて説明します。 また、カスタム型やカスタム アセンブリに対して同様のマッピングを行う方法についても説明します。
title: XAML 名前空間と名前空間マッピング
ms.assetid: A19DFF78-E692-47AE-8221-AB5EA9470E8B
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 557301873cbea09d3601b09254c5a296ceb9fc82
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89168996"
---
# <a name="xaml-namespaces-and-namespace-mapping"></a>XAML 名前空間と名前空間マッピング


このトピックでは、ほとんどの XAML ファイルのルート要素で見つかった XML/XAML 名前空間 (**xmlns**) マッピングについて説明します。 また、カスタム型やカスタム アセンブリに対して同様のマッピングを行う方法についても説明します。

## <a name="how-xaml-namespaces-relate-to-code-definition-and-type-libraries"></a>XAML 名前空間のコード定義とタイプ ライブラリとの関連

XAML は、一般用と Windows ランタイム アプリのプログラミング用の両方の用途において、オブジェクト、オブジェクトのプロパティ、階層として表されるオブジェクトとプロパティの関係を宣言するために使われます。 XAML で宣言するオブジェクトは、他のプログラミング手法やプログラミング言語で定義されるタイプ ライブラリまたはその他の表現によってサポートされます。 たとえば、次のようなライブラリがあります。

-   Windows ランタイムのオブジェクトの組み込みのセット。 オブジェクトの固定セットです。XAML からこれらのオブジェクトにアクセスする場合は、内部型マッピングとアクティブ化ロジックが使われます。
-   Microsoft またはサード パーティによって配布されるライブラリ。
-   アプリに組み込まれ、パッケージとして再配布される、サード パーティ コントロールの定義を表すライブラリ。
-   プロジェクトの一部で、ユーザー コード定義の一部または全部を保持する独自のライブラリ。

バッキング型の情報は特定の XAML 名前空間の定義に関連付けられています。 Windows ランタイムなどの XAML フレームワークでは、複数のアセンブリや複数のコード名前空間を集約して単一の XAML 名前空間にマップすることができます。 これにより、大規模なプログラミング フレームワークやテクノロジに対応する XAML ボキャブラリという概念が実現されます。 XAML ボキャブラリは、非常に広範囲に及ぶことがあります。たとえば、このリファレンスに示されている Windows ランタイム アプリのために作成された XAML は、ほとんどが 1 つの XAML ボキャブラリを構成します。 XAML ボキャブラリは拡張することもできます。XAML ボキャブラリを拡張するには、バッキング型のコード定義に型を追加します。その際には、その XAML ボキャブラリの、マップされた名前空間のソースとして既に使われているコード名前空間にその型が含まれている必要があります。

XAML プロセッサは、ランタイム オブジェクト表現を作成するときに、XAML 名前空間に関連付けられているバッキング アセンブリから型とメンバーを検索できます。 これが、XAML がオブジェクト構築の動作の定義を形式化および交換する方法として役立ち、UWP アプリの UI 定義の手法として使われる理由です。

## <a name="xaml-namespaces-in-typical-xaml-markup-usage"></a>XAML マークアップの一般的な使用法における XAML 名前空間

ほとんどの場合、XAML ファイルでは、既定の XAML 名前空間をルート要素で宣言します。 既定の XAML 名前空間は、プレフィックスで修飾することなく宣言できる要素を定義します。 たとえば、要素 `<Balloon />` を宣言した場合、XAML パーサーでは、**Balloon** という要素が既定の XAML 名前空間に存在し有効であることが想定されます。 その一方、定義済みの既定の XAML 名前空間に **Balloon** が存在しない場合は、`<party:Balloon />` のようにプレフィックスを使って要素名を修飾する必要があります。 このプレフィックスは、要素が既定の名前空間とは異なる XAML 名前空間に存在することを示します。この要素を使う前に、プレフィックス **party** に XAML 名前空間をマップする必要があります。 XAML 名前空間は、名前空間が宣言されている特定の要素に適用されるほか、XAML 構造においてこの要素に含まれるすべての要素に対しても適用されます。 したがって、ほとんどの場合は、この継承を利用するために、XAML 名前空間を XAML ファイルのルート要素で宣言します。

## <a name="the-default-and-xaml-language-xaml-namespace-declarations"></a>既定および XAML 言語の XAML 名前空間の宣言

ほとんどの XAML ファイルのルート要素内には 2 つの **xmlns** 宣言があります。 1 つ目の宣言では、XAML 名前空間を既定としてマップします。 `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`

これは、前身である複数の Microsoft テクノロジで使われていたものと同じ XAML 名前空間識別子です。このようなテクノロジでは、XAML を UI 定義のマークアップ形式としても使います。 同じ識別子の採用は意図的なものであり、既に定義済みの UI を、C++、C#、または Visual Basic を使った Windows ランタイム アプリに移行する場合に役立ちます。

2 つ目の宣言では、XAML で定義された言語要素に個別の XAML 名前空間をマップします。通常、この名前空間は "x:" プレフィックスにマップされます。 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`

この **xmlns** の値と、マップされている "x:" プレフィックスも、前身であり XAML を使う複数の Microsoft テクノロジで使われていた定義と同じです。

これらの宣言の関係としては、XAML が言語定義であること、および Windows ランタイムが言語として XAML を使用し、型が XAML で参照される特定のボキャブラリを定義する 1 つの実装であることが挙げられます。

XAML 言語では、特定の言語要素を指定します。これらの各要素には、XAML 名前空間に対応する XAML プロセッサの実装を介してアクセスする必要があります。 XAML 言語の XAML 名前空間に通常マップする "x:" の後には、プロジェクト テンプレート、サンプル コード、および言語機能に関するドキュメントが続きます。 XAML 言語の名前空間では、C++、C#、または Visual Basic を使った基本的な Windows ランタイム アプリでも必要な、よく使われる複数の機能を定義します。 たとえば、部分クラスを介して XAML ファイルにコード ビハインドを追加するには、関連する XAML ファイルのルート要素における [x:Class 属性](x-class-attribute.md)としてそのクラスを指定する必要があります。 または、[ResourceDictionary と XAML リソースの参照](../design/controls-and-patterns/resourcedictionary-and-xaml-resource-references.md)内のキーを持つリソースとして XAML ページで定義されている要素の該当するオブジェクト要素では、[x:Key](x-key-attribute.md) 属性を設定する必要があります。

## <a name="code-namespaces-that-map-to-the-default-xaml-namespace"></a>既定の XAML 名前空間にマップされるコードの名前空間

ここでは、現在既定の XAML 名前空間にマップされているコードの名前空間の一覧を示します。

* Windows.UI
* Windows.UI.Xaml
* Windows.UI.Xaml.Automation
* Windows.UI.Xaml.Automation.Peers
* Windows.UI.Xaml.Automation.Provider
* Windows.UI.Xaml.Automation.Text
* Windows.UI.Xaml.Controls
* Windows.UI.Xaml.Controls.Primitives
* Windows.UI.Xaml.Data
* Windows.UI.Xaml.Documents
* Windows.UI.Xaml.Input
* Windows.UI.Xaml.Interop
* Windows.UI.Xaml.Markup
* Windows.UI.Xaml.Media
* Windows.UI.Xaml.Media.Animation
* Windows.UI.Xaml.Media.Imaging
* Windows.UI.Xaml.Media.Media3D
* Windows.UI.Xaml.Navigation
* Windows.UI.Xaml.Resources
* Windows.UI.Xaml.Shapes
* Windows. UI. .Xaml. スレッド
* Windows.UI.Text

<span id="other-XAML-namespaces"/>

## <a name="other-xaml-namespaces"></a>その他の XAML 名前空間

既定の名前空間と XAML 言語の XAML 名前空間である "x:" に加えて、Microsoft Visual Studio で生成されるアプリで使う初期の既定の XAML では、その他の XAML 名前空間がマップされる場合もあります。

### <a name="d-httpschemasmicrosoftcomexpressionblend2008"></a>**d: ( `http://schemas.microsoft.com/expression/blend/2008` )**

"d:" は、デザイナー サポート (特に、Microsoft Visual Studio の XAML デザイン サーフェイスにおけるデザイナー サポート) を対象とした XAML 名前空間です。 "d:" XAML 名前空間を使うと、XAML 要素でデザイナー (設計時) 属性が有効になります。 このようなデザイナー属性は、XAML の動作の設計面にのみ影響します。 アプリの実行時に同じ XAML が Windows ランタイム XAML パーサーによって読み込まれると、デザイナー属性は無視されます。 一般に、デザイナー属性はすべての XAML 要素で有効ですが、実際のところ、デザイナー属性の適用が適しているのは特定のシナリオのみです。 特に、デザイナー属性の多くは、XAML とデータ バインディングを使うコードの開発時にデータ コンテキストやデータ ソースを操作しやすくすることを目的としています。

-   **d:DesignHeight 属性と d:DesignWidth 属性:** この 2 つの属性は、Visual Studio または別の XAML デザイナー サーフェイスが作成する XAML ファイルのルートに適用されることがあります。 この 2 つの属性は、たとえば、アプリ プロジェクトに新しく [**UserControl**](/uwp/api/Windows.UI.Xaml.Controls.UserControl) を追加した場合に、作成される XAML の **UserControl** ルートに設定されます。 この属性はいずれも、XAML コンテンツの構成を設計しやすくするものであり、XAML コンテンツがコントロール インスタンスや、それより大きな UI ページの一部に使われた場合に生じるレイアウト面の制約がある程度予測できるようになります。

   **メモ**   Microsoft Silverlight から XAML を移行する場合、UI ページ全体を表すルート要素にこれらの属性が含まれている可能性があります。 この場合、この属性の削除が必要になります。 シミュレーターなどの XAML デザイナーの方が、拡大縮小やビュー状態の処理に優れた機能が備わっており、**d:DesignHeight** と **d:DesignWidth** を使った固定サイズのページ レイアウトよりも、ページのレイアウトを設計するうえで便利であると考えられます。

-   **d:DataContext 属性:** ページ ルートまたはコントロールでこの属性を設定すると、そうでない場合にはオブジェクトに含まれる明示的または継承された [**DataContext**](/uwp/api/windows.ui.xaml.frameworkelement.datacontext) を上書きします。
-   **d:DesignSource 属性:** 設計時の [**CollectionViewSource**](/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) のデータ ソースを指定して、[**Source**](/uwp/api/windows.ui.xaml.data.collectionviewsource.source) を上書きします。
-   **d:DesignInstance マークアップ拡張と d:DesignData マークアップ拡張:** この 2 つのマークアップ拡張は、**d:DataContext** または **d:DesignSource** の設計時のデータ リソースを提供するために使われます。 設計時のデータ リソースの使い方は、ここで説明した内容がすべてではありません。 詳しくは、「[デザイン時属性](/previous-versions/windows/silverlight/dotnet-windows-silverlight/ff602277(v=vs.95))」をご覧ください。 使用例については、「[デザイン サーフェイス上のサンプル データとプロトタイプを作るためのサンプル データ](../data-binding/displaying-data-in-the-designer.md)」をご覧ください。

### <a name="mc-httpschemasopenxmlformatsorgmarkup-compatibility2006"></a>**mc: ( `http://schemas.openxmlformats.org/markup-compatibility/2006` )**

" mc:" は、XAML を読み取るためのマークアップ互換モードを示し、このモードをサポートします。 通常、"d:" プレフィックスは属性 **mc:Ignorable** に関連付けられます。 この手法により、ランタイムの XAML パーサーで "d:" のデザイナー属性を無視することができます。

### <a name="local-and-common"></a>**local:** と **common:**

"local:" は、テンプレート化された UWP アプリ プロジェクトの XAML ページ内でマップされることが多いプレフィックスです。 これは app.xaml を含むすべての XAML ファイルで [x:Class 属性](x-class-attribute.md)とコードを含めるために作成される同じ名前空間を参照するためにマップされています。 XAML で使うカスタム クラスをこの同じ名前空間で定義する限り、**local:** プレフィックスを使って XAML でカスタム型を参照することができます。 テンプレート化された UWP アプリ プロジェクトに由来する関連のプレフィックスは **common:** です。 このプレフィックスは、コンバーターやコマンドのようなユーティリティ クラスを含む入れ子になった "Common" 名前空間を参照します。その定義は**ソリューション エクスプローラー** ビューの Common フォルダーで確認できます。

### <a name="vsm"></a>**vsm:**

使用しないでください。 "vsm:" は、他の Microsoft テクノロジからインポートされる従来の XAML テンプレートで使う場合のあるプレフィックスです。 従来の名前空間の作成に関する問題には、この名前空間を使って対応していました。 Windows ランタイムに使う XAML で "vsm:" の XAML 名前空間の定義を削除したうえで、[**VisualState**](/uwp/api/Windows.UI.Xaml.VisualState)、[**VisualStateGroup**](/uwp/api/Windows.UI.Xaml.VisualStateGroup)、関連オブジェクトのプレフィックスの使用法を変更して、代わりに既定の XAML 名前空間を使う必要があります。 XAML の移行について詳しくは、「[Silverlight または WPF XAML/コードの Windows ランタイム アプリへの移行](/previous-versions/windows/apps/br229571(v=win.10))」をご覧ください。

## <a name="mapping-custom-types-to-xaml-namespaces-and-prefixes"></a>XAML 名前空間およびプレフィックスへのカスタム型のマッピング

XAML 名前空間をマップすると、XAML を使用して独自のカスタム型にアクセスできるようになります。 つまり、カスタム型を定義するコード表現にコード名前空間が存在する場合にコード名前空間をマップし、使用法に対応したプレフィックス付きの XAML 名前空間をそのコード名前空間に割り当てます。 XAML 用のカスタム型は Microsoft .NET 言語 (C# または Microsoft Visual Basic) または C++ で定義できます。 マッピングを行う場合は **xmlns** プレフィックスが定義されます。 たとえば、`xmlns:myTypes` では、すべての使用法に対し、プレフィックスとしてトークン `myTypes:` を付けてアクセスする新しい XAML 名前空間を定義します。

**xmlns** 定義には、値およびプレフィックスの命名が含まれます。 この値は引用符で囲まれた文字列であり、後ろに等号が続きます。 XML では通常、XML 名前空間を Uniform Resource Identifier (URI) に関連付けるため、一意性および識別に関する規則が存在します。 また、これは既定の XAML 名前空間と XAML 言語の XAML 名前空間、および Windows ランタイム XAML で使用される (使用頻度の少ない) 一部の XAML 名前空間にも当てはまります。 ただし、カスタム型をマップする XAML 名前空間の場合は、URI を指定する代わりに、プレフィックスの定義の先頭にトークン "using:" を使用します。 "using:" トークンに続けて、コード名前空間の名前を指定します。

たとえば、"CustomClasses" 名前空間を参照できるようにする "custom1" プレフィックスをマップし、その名前空間またはアセンブリのクラスを XAML でオブジェクト要素として使用するには、XAML ページのルート要素に次のマッピングを含める必要があります。 `xmlns:custom1="using:CustomClasses"`

同じページのスコープの部分クラスをマップする必要はありません。 たとえば、ページの XAML UI 定義からのイベントを処理するために定義したイベント ハンドラーを参照するプレフィックスは不要です。 また、C++、C#、または Visual Basic を使った Windows ランタイム アプリ向けに Visual Studio によって生成されたプロジェクトの XAML 開始ページの多くは、既に "local:" プレフィックスをマップしています。このプレフィックスは、プロジェクト固有の既定の名前空間と部分クラス定義で使われる名前空間を参照します。

### <a name="clr-language-rules"></a>CLR 言語規則

.NET 言語 (C# または Microsoft Visual Basic) でバッキング コードを記述する場合は、名前空間の名前の一部にドット (".") を使用する規則を使って、コード名前空間の概念的な階層を作成できます。 名前空間の定義にドットを含める場合は、"using:" トークンの後ろに指定する値の一部としてそのドットを使う必要があります。

コード ビハインド ファイルまたはコード定義ファイルが C++ ファイルである場合、XAML 構文に違いを出さないために、共通言語ランタイム (CLR) の言語形式に従う特定の構文があります。 "using:" トークンに続く値を指定する場合、C++ で入れ子になった名前空間を宣言すると、以降の入れ子になった名前空間の文字列間の区切り文字も "::" ではなく "." である必要があります。

XAML で使うコードを定義するときに入れ子になった型を使わないでください (クラス内で列挙型を入れ子にするなど)。 入れ子になった型は評価できません。 ドットが名前空間名の一部なのか、それとも入れ子になった型名の一部なのかを区別する方法は XAML パーサーにはありません。

## <a name="custom-types-and-assemblies"></a>カスタム型およびカスタム アセンブリ

マッピングでは、その XAML 名前空間のバッキング型を定義するアセンブリの名前は指定されません。 アセンブリを使うことができるロジックはアプリ定義のレベルで制御され、アプリの展開とセキュリティの基本原則に含まれます。 XAML のコード定義ソースとして含めるすべてのアセンブリを、依存アセンブリとしてプロジェクト設定で宣言します。 詳しくは、「[C# と Visual Basic での Windows ランタイム コンポーネントの作成](/previous-versions/windows/apps/hh441572(v=vs.140))」をご覧ください。

主要なアプリのアプリケーション定義やページ定義のカスタム型を参照する場合は、それらの型を使うのにさらに依存アセンブリを構成する必要はありませんが、それらの型を含むコード名前空間をマップする必要はあります。 通常は、プレフィックス "local" を特定の XAML ページの既定のコード名前空間にマップします。 この方法は、XAML プロジェクトのプロジェクト開始テンプレートでよく使われています。

## <a name="attached-properties"></a>添付プロパティ

添付プロパティを参照する場合、添付プロパティ名の所有者型の部分は、既定の XAML 名前空間に存在するか、またはプレフィックスが付けられている必要があります。 要素とは別に属性にプレフィックスを付けることはまれですが、これは、特にカスタム添付プロパティの場合に、必要となることのあるケースの 1 つです。 詳しくは、「[カスタム添付プロパティ](custom-attached-properties.md)」をご覧ください。

## <a name="related-topics"></a>関連トピック

* [XAML の概要](xaml-overview.md)
* [XAML 構文のガイド](xaml-syntax-guide.md)
* [C# および Visual Basic での Windows ランタイムコンポーネントの作成](/previous-versions/windows/apps/hh441572(v=vs.140))
* [Windows ランタイム アプリ用の C#、VB、C++ プロジェクト テンプレート](/previous-versions/windows/apps/hh768232(v=win.10))
* [Silverlight または WPF XAML/コードの Windows ランタイム アプリへの移行](/previous-versions/windows/apps/br229571(v=win.10))
 