---
title: Windows 10 ゲーム開発ガイド
description: ユニバーサル Windows プラットフォーム (UWP) ゲーム開発のためのリソースや情報を網羅したガイドです。
ms.assetid: 6061F498-96A8-44EF-9711-68AE5A1218C9
ms.date: 04/16/2018
ms.topic: article
keywords: Windows 10, UWP, ゲーム、ゲーム開発
ms.localizationpriority: medium
ms.openlocfilehash: 53e977e07337c11036916c2087a00e9ec7a95118
ms.sourcegitcommit: 51d884c3646ba3595c016e95bbfedb7ecd668a88
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821125"
---
# <a name="windows-10-game-development-guide"></a>Windows 10 ゲーム開発ガイド


Windows 10 ゲーム開発ガイドへようこそ。

このガイドでは、ユニバーサル Windows プラットフォーム (UWP) ゲームの開発に必要なリソースと情報を網羅したコレクションを提供します。 このガイドの英語 (米国) 版は [PDF](https://download.microsoft.com/download/9/C/9/9C9D344F-611F-412E-BB01-259E5C76B17F/Windev_Game_Dev_Guide_Oct_2017.pdf) 形式で利用できます。

## <a name="introduction-to-game-development-for-the-universal-windows-platform-uwp"></a>ユニバーサル Windows プラットフォーム (UWP) 用ゲーム開発の概要


Windows 10 ゲームを作成すると、スマートフォンから PC、Xbox One にいたる数百万人のプレイヤーにゲームを提供するチャンスを得られます。 Windows の Xbox、Xbox Live、クロス デバイス マルチプレイヤー、すばらしいゲーム コミュニティ、ユニバーサル Windows プラットフォーム (UWP) や DirectX 12 などの強力な新機能により、Windows 10 ゲームは、あらゆる世代やジャンルのプレイヤーを楽しませるでしょう。 新しいユニバーサル Windows プラットフォーム (UWP) は、スマートフォン、PC、Xbox One 用の共通 API と、各デバイスのエクスペリエンスに合わせてゲームをカスタマイズするツールやオプションによって、Windows 10 デバイスでのゲームの互換性を実現します。

このガイドでは、ゲームの開発に役立つさまざまなリソースや情報を網羅して提供します。 必要なときに情報を検索する場所がわかるように、各セクションはゲームの開発の各段階に従って編成されています。

Windows または Xbox で初めてゲームを開発する場合は、最初に[ファースト ステップ](getting-started.md) ガイドをご覧ください。 「[ゲーム開発に関するリソース](#game-development-resources)」セクションでも、ゲームの作成時に役立つドキュメント、プログラム、その他のリソースの大まかな概要を示します。 概要ではなく、実際の UWP コードを見て作業を始める場合は、「[ゲームのサンプル](#game-samples)」をご覧ください。

このガイドは、Windows 10 ゲーム開発に関する新しいリソースや資料が利用可能になると更新されます。

## <a name="game-development-resources"></a>ゲーム開発に関するリソース

ドキュメントから、開発者向けのプログラム、フォーラム、ブログ、サンプルまで、ゲーム開発に役立つ多くのリソースが用意されています。 ここでは、Windows 10 ゲームの開発を始めるにあたって役立つリソースをまとめています。

> [!Note]
> 一部の機能は、さまざまなプログラムで管理されています。 このガイドでは幅広いリソースを取り上げているため、参加しているプログラムや特定の開発の役割によっては、一部のリソースにアクセスできない場合があります。 developer.xboxlive.com、forums.xboxlive.com、xdi.xboxlive.com、Game Developer Network (GDN) に解決されるリンクなどです。 Microsoft との提携について詳しくは、「[開発者プログラム](#developer-programs)」をご覧ください。


### <a name="game-development-documentation"></a>ゲーム開発に関するドキュメント

このガイド全体を通して、タスク、テクノロジ、ゲームの開発の段階ごとに整理された、関連ドキュメントへのディープ リンクを示しています。 利用可能なドキュメントのさまざまなビューを提供するために、Windows 10 ゲーム開発用の主要なドキュメント ポータルを次に示します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Windows デベロッパー センターのメイン ポータル</td>
        <td><a href="https://developer.microsoft.com/windows">Windows デベロッパー センター</a></td>
    </tr>
    <tr>
        <td>Windows アプリの開発</td>
        <td><a href="https://developer.microsoft.com/windows/apps/develop">Windows アプリを開発します。</a></td>
    </tr>
    <tr>
        <td>ユニバーサル Windows プラットフォーム アプリの開発</td>
        <td><a href="https://developer.microsoft.com/windows/apps">Windows 10 アプリに関するハウツー ガイド</a></td>
    </tr>
    <tr>
        <td>UWP ゲームに関する使い方ガイド</td>
        <td><a href="index.md">ゲームと DirectX</a> </td>
    </tr>
    <tr>
        <td>DirectX のリファレンスと概要</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/directx">DirectX のグラフィックスとゲーミング</a></td>
    </tr>
    <tr>
        <td>ゲームのための Azure</td>
        <td><a href="https://azure.microsoft.com/solutions/gaming/">ビルドし、Azure を使用してゲームをスケール</a></td>
    </tr>
    <tr>
        <td>PlayFab</td>
        <td><a href="https://api.playfab.com/">ライブ ゲーム向けの完全なバックエンド ソリューション</a></td>
    </tr>
    <tr>
        <td>Xbox One の UWP</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/xbox-apps/index">Xbox One での UWP アプリのビルド</a></td>
    </tr>
    <tr>
        <td>HoloLens の UWP</td>
        <td><a href="https://developer.microsoft.com/windows/mixed-reality/development_overview">HoloLens で UWP アプリのビルド</a></td>
    </tr>
    <tr>
        <td>Xbox Live に関するドキュメント</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/">開発者ガイドの Xbox Live</a></td>
    </tr>
    <tr>
        <td>Xbox One 開発に関するドキュメント (XGD)</td>
        <td><a href="https://developer.microsoft.com/games/xbox/partner/development-home">Xbox One の開発</a></td>
    </tr>
    <tr>
        <td>Xbox One 開発に関するホワイト ペーパー (XGD)</td>
        <td><a href="https://developer.microsoft.com/games/xbox/partner/development-education-whitepapers">ホワイト ペーパー</a></td>
    </tr>
    <tr>
        <td>Mixer の対話機能のドキュメント</td>
        <td><a href="https://dev.mixer.com/reference/interactive/index.html">ゲームにインタラクティビティを追加します。</a></td>
    </tr>        
</table>

### <a name="partner-center"></a>パートナー センター

[パートナー センターでは、開発者アカウントを登録する](https://developer.microsoft.com/store/register)は Windows ゲームを公開における最初の手順です。 開発者アカウントでは、ゲームの名前を予約することや、すべての Windows デバイスに対応する無料ゲームと有料ゲームを Microsoft Store に提出することができます。 開発者アカウントを使って、ゲームとゲーム内製品を管理したり、詳細な分析を取得したり、世界中のプレイヤーに優れたエクスペリエンスを提供するサービスを実現することができます。 

さらにマイクロソフトでは、Windows ゲームの開発と公開に役立ついくつかの開発者向けプログラムを提供しています。 いずれかがパートナー センター アカウントに登録する前に適切な場合が表示されることをお勧めします。 詳しくは、「[開発者プログラム](#developer-programs)」をご覧ください。


### <a name="developer-programs"></a>開発者プログラム

Microsoft では、Windows ゲームの開発と公開に役立ついくつかの開発者向けプログラムを提供しています。 Xbox One のゲームを開発し、Xbox Live の機能をゲームに統合する場合には、開発者プログラムへの参加を検討してください。 Microsoft Store でのゲームを公開するにも必要で、開発者アカウントを作成する[パートナー センター](https://partner.microsoft.com/dashboard)します。

#### <a name="xbox-live-creators-program"></a>Xbox Live クリエーターズ プログラム

Xbox Live クリエーターズ プログラムでは、だれでも Xbox Live を自分のタイトルに統合して、Xbox One や Windows 10 に公開することができます。 認定プロセスが簡素化され、標準的な [Microsoft Store ポリシー](https://docs.microsoft.com/legal/windows/agreements/store-policies)以外に概念の承認はありません。

専用の開発キットがなくても、製品版ハードウェアのみを使用して、クリエーターズ プログラムでゲームを展開、設計、公開することができます。 作業を始めるには、Xbox One で[開発者モードのアクティブ化用アプリ](https://docs.microsoft.com/windows/uwp/xbox-apps/devkit-activation)をダウンロードします。

Xbox Live の他の機能にアクセスしたり、マーケティングと開発に関する専用のサポートを受けたり、Xbox One ストアのメイン ページで取り上げられたりすることを希望する場合は、[ID@Xbox](https://www.xbox.com/Developers/id) プログラムへの登録を申し込んでください。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Xbox Live クリエーターズ プログラム</td>
        <td><a href="https://developer.microsoft.com/games/xbox/xboxlive/creator">Xbox Live Creators Program の詳細を見る</a></td>
    </tr>
</table>

#### <a name="idxbox"></a>ID@Xbox

ID@Xbox プログラムを利用すると、認定されたゲーム開発者は Windows や Xbox One 向けに自分でゲームを公開することができます。 Xbox One 向けの開発を行ったり、ゲーマースコア、達成度、ランキングなどの Xbox Live 機能を自分の Windows 10 ゲームでも実現したいと検討されているなら、ID@Xbox にサインアップしてください。 ID@Xbox 開発者になると、創造性を発揮し、成功の可能性を最大限に引き出すためのツールやサポートを利用できます。 適用することをお勧めします。ID@Xboxパートナー センターでの開発者アカウントに登録する前にします。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ID@Xbox開発者プログラム</td>
        <td><a href="https://go.microsoft.com/fwlink/p/?LinkID=526271">Xbox One の独立した開発者プログラム</a></td>
    </tr>
    <tr>
        <td>ID@Xbox コンシューマー向けサイト</td>
        <td><a href="https://www.idatxbox.com/">ID@Xbox</a></td>
    </tr>
</table>

#### <a name="xbox-tools-and-middleware"></a>Xbox のツールとミドルウェア

Xbox のツールおよびミドルウェア プログラムは、ゲームのツールやミドルウェア専門の開発者に Xbox 開発キットのライセンスを付与します。 プログラムに受け入れられた開発者は、Xbox XDK テクノロジを共有し、ライセンスを持つ他の Xbox 開発者に配布することができます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ツールおよびミドルウェア プログラムについて問い合わせる</td>
        <td><xboxtlsm@microsoft.com></td>
    </tr>
</table>


### <a name="game-samples"></a>ゲームのサンプル

Windows 10 ゲームとアプリのサンプルが数多く用意されており、Windows 10 のゲーム機能を理解して、ゲーム開発をすぐに始めることができます。 サンプルは次々と開発され、定期的に公開されるため、ときどきサンプル ポータルをチェックして、新機能を確認することを忘れないでください。 GitHub のリポジトリを[監視](https://help.github.com/en/articles/watching-and-unwatching-repositories)して、変更や追加についての通知を受け取ることもできます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ユニバーサル Windows プラットフォーム アプリのサンプル</td>
        <td><a href="https://github.com/Microsoft/Windows-universal-samples">Windows-universal-samples</a></td>
    </tr>
    <tr>
        <td>Direct3D 12 グラフィックスのサンプル</td>
        <td><a href="https://github.com/Microsoft/DirectX-Graphics-Samples">DirectX のサンプル グラフィック</a></td>
    </tr>
    <tr>
        <td>Direct3D 11 グラフィックスのサンプル</td>
        <td><a href="https://github.com/walbourn/directx-sdk-samples">directx-sdk-samples</a></td>
    </tr>
    <tr>
        <td>Direct3D 11 主観視点のゲームのサンプル</td>
        <td><a href="tutorial--create-your-first-uwp-directx-game.md">DirectX によるシンプルな UWP ゲームの作成</a></td>
    </tr>
    <tr>
        <td>Direct2D カスタム画像効果のサンプル</td>
        <td><a href="https://go.microsoft.com/fwlink/p/?LinkId=620531">D2DCustomEffects</a></td>
    </tr>
    <tr>
        <td>Direct2D グラデーション メッシュのサンプル</td>
        <td><a href="https://go.microsoft.com/fwlink/p/?LinkId=620532">D2DGradientMesh</a></td>
    </tr>
    <tr>
        <td>Direct2D 写真調整のサンプル</td>
        <td><a href="https://go.microsoft.com/fwlink/p/?LinkId=620533">D2DPhotoAdjustment</a></td>
    </tr>
    <tr>
        <td>Xbox Advanced Technology Group のパブリック サンプル</td>
        <td><a href="https://github.com/Microsoft/Xbox-ATG-Samples">Xbox 用 ATG サンプル</a></td>
    </tr>
    <tr>
        <td>Xbox Live のサンプル</td>
        <td><a href="https://github.com/Microsoft/xbox-live-samples">xbox-live-samples</a></td>
    </tr>
    <tr>
        <td>Xbox One ゲームのサンプル (XGD)</td>
        <td><a href="https://developer.microsoft.com/games/xbox/partner/development-education-samples">サンプル</a></td>
    </tr>
    <tr>
        <td>Windows ゲームのサンプル (MSDN コード ギャラリー)</td>
        <td><a href="https://code.msdn.microsoft.com/windowsapps/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=game&f%5B1%5D.Type=Contributors&f%5B1%5D.Value=Microsoft&f%5B1%5D.Text=Microsoft">Microsoft Store ゲームのサンプル</a></td>
    </tr>
    <tr>
        <td>JavaScript 2D ゲームのサンプル</td>
        <td><a href="../get-started/get-started-tutorial-game-js2d.md">JavaScript での UWP ゲームを作成します。</a></td>
    </tr>
    <tr>
        <td>JavaScript 3D ゲームのサンプル</td>
        <td><a href="../get-started/get-started-tutorial-game-js3d.md">Three.js を使用して 3D JavaScript ゲームを作成します。</a></td>
    </tr>
    <tr>
        <td>MonoGame 2D UWP ゲームのサンプル</td>
        <td><a href="../get-started/get-started-tutorial-game-mg2d.md">MonoGame 2D での UWP ゲームを作成します。</a></td>
    </tr>      
</table>


### <a name="developer-forums"></a>開発者フォーラム

開発者フォーラムは、ゲームの開発に関する質疑応答を行ったり、ゲーム開発コミュニティで交流を深めたりするのに適した場所です。 フォーラムは、他の開発者が過去に直面し、解決した困難な問題に対する既存の回答を見つけることができる、優れたリソースでもあります。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>発行のアプリやゲームの開発者向けフォーラム</td>
        <td><a href="https://social.msdn.microsoft.com/Forums/en-us/home?category=windowsapps">パブリッシングおよびアプリでの広告</a></td>
    </tr>
    <tr>
        <td>UWP アプリ開発者フォーラム</td>
        <td><a href="https://social.msdn.microsoft.com/Forums/en-us/home?forum=wpdevelop">開発のユニバーサル Windows プラットフォーム アプリ</a></td>
    </tr>
    <tr>
        <td>デスクトップ アプリケーション開発者フォーラム</td>
        <td><a href="https://social.msdn.microsoft.com/Forums/en-us/home?category=windowsdesktopdev">Windows デスクトップ アプリケーションのフォーラム</a></td>
    </tr>
    <tr>
        <td>DirectX Microsoft Store ゲーム (アーカイブ済みのフォーラムの投稿)</td>
        <td><a href="https://social.msdn.microsoft.com/Forums/vstudio/home?forum=wingameswithdirectx">DirectX (アーカイブ済み) を使用した Microsoft Store ゲームの構築</a></td>
    </tr>
    <tr>
        <td>Windows 10 対象パートナー開発者フォーラム</td>
        <td><a href="https://aka.ms/win10devforums">XBOX デベロッパー フォーラム:Windows 10</a></td>
    </tr>
    <tr>
        <td>DirectX フォーラム</td>
        <td><a href="https://forums.directxtech.com/index.php">DirectX 12 のフォーラム</a></td>
    </tr>
    <tr>
        <td>Azure プラットフォーム フォーラム</td>
        <td><a href="https://social.msdn.microsoft.com/Forums/en-us/home?category=windowsazureplatform">Azure フォーラム</a></td>
    </tr>
    <tr>
        <td>Xbox Live フォーラム</td>
        <td><a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=xboxlivedev">Xbox Live 開発フォーラム</a></td>
    </tr>
    <tr>
        <td>PlayFab フォーラム</td>
        <td><a href="https://community.playfab.com/index.html">PlayFab フォーラム</a></td>
    </tr>
</table>


### <a name="developer-blogs"></a>開発者ブログ

開発者ブログは、ゲーム開発に関する最新情報を手に入れることができる、もう 1 つの有用なリソースです。 新機能、実装の詳細、ベスト プラクティス、アーキテクチャの背景などに関する投稿を見つけることができます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Windows 用アプリ開発ブログ</td>
        <td><a href="https://blogs.windows.com/buildingapps/">Windows のアプリの構築</a></td>
    </tr>
    <tr>
        <td>Windows 10 (ブログの投稿)</td>
        <td><a href="https://blogs.windows.com/blog/tag/windows-10/">Windows 10 での投稿</a></td>
    </tr>
    <tr>
        <td>Visual Studio エンジニアリング チームのブログ</td>
        <td><a href="https://devblogs.microsoft.com/visualstudio/">Visual Studio ブログ</a></td>
    </tr>
    <tr>
        <td>Visual Studio 開発者ツールに関するブログ</td>
        <td><a href="https://devblogs.microsoft.com/visualstudio/">開発者ツールのブログ</a></td>
    </tr>
    <tr>
        <td>Somasegar の開発者ツールに関するブログ</td>
        <td><a href="https://devblogs.microsoft.com/somasegar/">Somasegar のブログ</a></td>
    </tr>
    <tr>
        <td>DirectX 開発者ブログ</td>
        <td><a href="https://devblogs.microsoft.com/directx/">DirectX の開発者向けブログ</a></td>
    </tr>
    <tr>
        <td>DirectX 12 の概要 (ブログの投稿)</td>
        <td><a href="https://devblogs.microsoft.com/directx/directx-12/">DirectX 12</a></td>
    </tr>
    <tr>
        <td>Visual C++ ツール チームのブログ</td>
        <td><a href="https://devblogs.microsoft.com/cppblog/">Visual C チーム ブログ</a></td>
    </tr>
    <tr>
        <td>PIX チームのブログ</td>
        <td><a href="https://devblogs.microsoft.com/pix/">パフォーマンスのチューニングと、Windows と Xbox でゲームを DirectX 12 のデバッグ</a></td>
    </tr>
    <tr>
        <td>ユニバーサル Windows アプリの展開チームのブログ</td>
        <td><a href="https://blogs.msdn.microsoft.com/appinstaller/">ビルドおよび配置の UWP アプリ チームのブログ</a></td>
    </tr>
</table>
 

## <a name="concept-and-planning"></a>概念と計画


概念と計画の段階では、ゲームの全体像とそれを実現するために使用するテクノロジやツールを決定します。

### <a name="overview-of-game-development-technologies"></a>ゲーム開発テクノロジの概要

UWP のゲームの開発を開始するとき、グラフィックス、入力、オーディオ、ネットワーク、ユーティリティ、ライブラリについて、利用可能なオプションは複数あります。

ゲームで使うすべてのテクノロジが既に決定している場合は問題ありません。 まだ決まっていない場合、[UWP アプリのゲーム テクノロジ](game-development-platform-guide.md) ガイドに利用可能な多くのテクノロジの概要がまとめられています。このガイドに目を通して、さまざまなオプションとそれらを組み合わせる方法を理解しておくことを強くお勧めします。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>UWP のゲーム テクノロジの概要</td>
        <td><a href="game-development-platform-guide.md">UWP アプリ用のゲーム テクノロジ</a></td>
    </tr>
</table>
 

次の 3 つの GDC 2015 のビデオは、Windows 10 のゲーム開発と Windows 10 のゲーム エクスペリエンスの概要を示しています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Windows 10 のゲーム開発の概要 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Developing-Games-for-Windows-10">Windows 10 向けゲームの開発</a></td>
    </tr>
    <tr>
        <td>Windows 10 のゲーム エクスペリエンス (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Gaming-Consumer-Experience-on-Windows-10">Windows 10 でのコンシューマー エクスペリエンスをゲーム</a></td>
    </tr>
    <tr>
        <td>Microsoft エコシステム全体でのゲーム (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/The-Future-of-Gaming-Across-the-Microsoft-Ecosystem">Microsoft のエコシステム全体でのゲームの未来</a></td>
    </tr>
</table>

### <a name="game-planning"></a>ゲームの計画

これらは、いくつかの高レベルの概念と、ゲームを計画するときに考慮する計画のトピックです。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ゲームをアクセシビリティ対応にする</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/gaming/accessibility-for-games">ゲームのユーザー補助機能</a></td>
    </tr>
    <tr>
        <td>クラウドを使用したゲームの作成</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/gaming/cloud-for-games">クラウド ゲーム</a></td>
    </tr>
    <tr>
        <td>ゲームの収益化</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/gaming/monetization-for-games">ゲームの収益化</a></td>
    </tr>
</table>



### <a name="choosing-your-graphics-technology-and-programming-language"></a>グラフィックス テクノロジとプログラミング言語の選択

Windows 10 ゲームでは、複数のプログラミング言語やグラフィックス テクノロジを使うことができます。 どれを選ぶかは、開発しているゲームの種類、開発スタジオの経験や好み、ゲームの具体的な機能要件によって決まります。 C#、C++、JavaScript のどれを使うか、 DirectX、XAML、HTML5 のどれを使うか、

#### <a name="directx"></a>DirectX

Microsoft DirectX を使うと、最高のパフォーマンスの 2D および 3D グラフィックスとマルチメディアを生み出すことができます。

DirectX 12 は、以前のバージョンよりも高速かつ効率的になっています。 Direct3D 12 は、より豊かなシーン、より多くのオブジェクト、より複雑な効果を実現し、Windows 10 PC や Xbox One の最新の GPU ハードウェアを十分に活用できます。

Direct3D 11 の使い慣れたグラフィックス パイプラインを使う場合でも、Direct3D 11.3 に追加された新しいレンダリングおよび最適化機能を活かすことができます。 さらに、Win32 をルーツとする実証済みのデスクトップ Windows API の開発者は、Windows 10 でもそのオプションを選ぶことができます。

DirectX のさまざまな機能と緊密なプラットフォーム統合により、要求の多いほとんどのゲームに必要とされる性能とパフォーマンスを実現できます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>UWP 用の DirectX 開発</td>
        <td><a href="directx-programming.md">DirectX プログラミング</a></td>
    </tr>
    <tr>
        <td>チュートリアル:UWP の DirectX ゲームを作成する方法</td>
        <td><a href="tutorial--create-your-first-uwp-directx-game.md">DirectX によるシンプルな UWP ゲームの作成</a></td>
    </tr>
    <tr>
        <td>DirectX の概要とリファレンス</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/directx">DirectX のグラフィックスとゲーミング</a></td>
    </tr>
    <tr>
        <td>Direct3D 12 プログラミング ガイドとリファレンス</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/direct3d-12-graphics">Direct3D 12 グラフィックス</a></td>
    </tr>
    <tr>
        <td>グラフィックスおよび DirectX 12 開発に関するビデオ (YouTube チャンネル)</td>
        <td><a href="https://www.youtube.com/channel/UCiaX2B8XiXR70jaN7NK-FpA">Microsoft DirectX 12 とグラフィックスの教育</a></td>
    </tr>
</table>
 

#### <a name="xaml"></a>XAML

XAML は、アニメーション、ストーリーボード、データ バインディング、拡張性の高いベクター ベース グラフィックス、動的なサイズ変更、シーン グラフなどの便利な機能を備える、使いやすい宣言型 UI 言語です。 また、XAML はゲーム UI、メニュー、スプライト、2D グラフィックスに最適です。 UI レイアウトを簡単にするため、XAML には、Expression Blend や Microsoft Visual Studio などの設計および開発ツールとの互換性があります。 XAML はよく C# と同時に使用されますが、希望する言語が C++ の場合や、ゲームが多くの CPU を必要とする場合は、C++ も適しています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>XAML プラットフォームの概要</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/xaml-platform/index">XAML プラットフォーム</a></td>
    </tr>
    <tr>
        <td>XAML UI とコントロール</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/design/basics/">コントロール、レイアウト、およびテキスト</a></td>
    </tr>
</table>
 

#### <a name="html-5"></a>HTML 5

ハイパーテキスト マークアップ言語 (HTML) は、Web ページ、アプリ、リッチ クライアントに使用される一般的な UI マークアップ言語です。 Windows ゲームでは、HTML の使い慣れた機能、ユニバーサル Windows プラットフォーム、AppCache、Web ワーカー、キャンバス、ドラッグ アンド ドロップ、非同期プログラミング、SVG などの最新の Web 機能のサポートを備えた、全機能装備のプレゼンテーション層として HTML5 を使うことができます。 HTML レンダリングの内部では、DirectX ハードウェア アクセラレータの機能が活用されるため、追加のコードを記述しなくても DirectX のパフォーマンスの恩恵を受けることができます。 Web 開発に熟練している場合、Web ゲームを移植する場合、または他の選択肢よりアプローチしやすい言語およびグラフィックス層を使う場合は、HTML5 が最適です。 HTML5 は JavaScript と同時に使用されますが、C# や C++/CX で作成されたコンポーネントを呼び出すこともできます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>HTML5 とドキュメント オブジェクト モデルに関する情報</td>
        <td><a href="https://developer.mozilla.org/en-US/docs/Web">HTML と DOM のリファレンス</a></td>
    </tr>
    <tr>
        <td>HTML5 W3C 勧告</td>
        <td><a href="https://go.microsoft.com/fwlink/p/?linkid=221374">HTML5</a></td>
    </tr>
</table>
 

#### <a name="combining-presentation-technologies"></a>プレゼンテーション テクノロジの組み合わせ

Microsoft DirectX Graphic Infrastructure (DXGI) には、複数のグラフィックス テクノロジにおける相互運用性と互換性が備わっています。 高パフォーマンスのグラフィックスを実現するため、メニューや他のシンプルな UI には XAML を使い、複雑な 2D および 3D シーンのレンダリングには DirectX を使うことで、XAML と DirectX を組み合わせることができます。 DXGI には、Direct2D、Direct3D、DirectWrite、DirectCompute、Microsoft メディア ファンデーション間の互換性も備わっています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>DirectX Graphics Infrastructure のプログラミング ガイドとリファレンス</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3ddxgi/dx-graphics-dxgi">DXGI</a></td>
    </tr>
    <tr>
        <td>DirectX と XAML の組み合わせ</td>
        <td><a href="directx-and-xaml-interop.md">DirectX および XAML の相互運用機能</a></td>
    </tr>
</table>
 

#### <a name="c"></a>C++

C++/CX はオーバーヘッドの低い高パフォーマンスな言語であり、速度、互換性、プラットフォーム アクセスがうまく組み合わせられています。 C++/CX により、DirectX や Xbox Live など、Windows 10 のすばらしいゲーム機能すべてが使いやすくなります。 既にある C++ コードとライブラリを再利用することもできます。 C++/CX を使うと、ガベージ コレクションのオーバーヘッドを生じさせない高速なネイティブ コードが作成されるため、ゲームのパフォーマンスが向上し、電力消費が低くなり、結果としてバッテリ寿命が延びます。 C++/CX を DirectX または XAML と同時に使うか、両方の組み合わせを使って、ゲームを作成することができます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>C++/CX のリファレンスと概要</td>
        <td><a href="https://docs.microsoft.com/cpp/cppcx/visual-c-language-reference-c-cx">VisualC++言語リファレンス (C++/CX)</a></td>
    </tr>
    <tr>
        <td>Visual C++ のプログラミング ガイドとリファレンス</td>
        <td><a href="https://docs.microsoft.com/cpp/visual-cpp-in-visual-studio">VisualC++で Visual Studio 2019</a></td>
    </tr>
</table>
 

#### <a name="c"></a>C#

C# ("シー シャープ" と発音) は、タイプ セーフかつオブジェクト指向のシンプルで強力な最新の革新的言語です。 C# を使うと、C スタイル言語の親しみやすさと表現力を維持しながら短期間で開発できます。 C# は使いやすい言語ですが、ポリモーフィズム、デリゲート、ラムダ、クロージャ、反復子メソッド、共変性、統合言語クエリ (LINQ) 式など、多くの高度な言語機能が備わっています。 XAML をターゲットとする場合、ゲームの開発をすぐに始めたい場合、C# を既に使ったことがある場合、C# が最適です。 C# は主に XAML と同時に使われるめ、DirectX を使う場合は、代わりに C++ を選ぶか、ゲームの一部を DirectX とやり取りする C++ コンポーネントとして記述します。 または、C# と C++ 用の即時モード Direct2D グラフィックス ライブラリである [Win2D](https://github.com/Microsoft/Win2D) を使うことを検討します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>C# のプログラミング ガイドとリファレンス</td>
        <td><a href="https://docs.microsoft.com/dotnet/articles/csharp/csharp">C# 言語のリファレンス</a></td>
    </tr>
</table>
 

#### <a name="javascript"></a>JavaScript

JavaScript は、最新の Web アプリケーションやリッチ クライアント アプリケーションに広く使用されている動的なスクリプト言語です。

Windows JavaScript アプリは、ユニバーサル Windows プラットフォームの強力な機能に簡単かつ直感的な方法でアクセスできます (オブジェクト指向 JavaScript クラスのメソッドとプロパティとして)。 JavaScript は、Web 開発環境を使っていた場合、JavaScript に既に慣れている場合、HTML5、CSS、WinJS、または JavaScript ライブラリを使用する場合のゲーム開発に最適です。 DirectX や XAML をターゲットとする場合は、代わりに C# または C++/CX を選択してください。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>JavaScript と Windows ランタイムのリファレンス</td>
        <td><a href="https://docs.microsoft.com/scripting/javascript/javascript-language-reference">JavaScript リファレンス</a></td>
    </tr>
</table>


#### <a name="use-windows-runtime-components-to-combine-languages"></a>Windows ランタイム コンポーネントを使って言語を組み合わせる

ユニバーサル Windows プラットフォームでは、異なる言語で記述されたコンポーネントを簡単に組み合わせることができます。 C++、C#、Visual Basic で Windows ランタイム コンポーネントを作成した後、JavaScript、C#、C++、Visual Basic から呼び出すことができます。 これは、好みの言語でゲームの一部をプログラミングする場合に最適な方法です。 コンポーネントにより、特定の言語でのみ使用可能な外部ライブラリや、既に記述しているレガシ コードを使うこともできるようになります。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Windows ランタイム コンポーネントを作成する方法</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/winrt-components/creating-windows-runtime-components-in-cpp">Windows ランタイム コンポーネントの作成</a></td>
    </tr>
</table>


### <a name="which-version-of-directx-should-your-game-use"></a>ゲームで使う Microsoft DirectX のバージョン

ゲームを DirectX を選択する場合は、使用するバージョンを決定する必要があります。マイクロソフトの Direct3D 12 またはマイクロソフトの Direct3D 11。

DirectX 12 は、以前のバージョンよりも高速かつ効率的になっています。 Direct3D 12 は、より豊かなシーン、より多くのオブジェクト、より複雑な効果を実現し、Windows 10 PC や Xbox One の最新の GPU ハードウェアを十分に活用できます。 Direct3D 12 は非常に低いレベルで動作するため、専門的なグラフィックス開発チームや経験豊富な DirectX 11 開発チームは、グラフィックスの最適化を十分に活かすために必要となるすべてのコントロールを利用することができます。

Direct3D 11.3 は低レベル グラフィック API です。よく利用される Direct3D プログラミング モデルが使われており、GPU レンダリングに関連する多くの複雑な処理を扱うことができます。 また、Windows 10 と Xbox One でもサポートされています。 Direct3D 11 で作成されたエンジンを既にお持ちで、Direct3D 12 への切り替えの準備がまだ整っていない場合は、Direct3D 11 on 12 を使うことによって、ある程度のパフォーマンスの向上を実現することができます。 バージョン 11.3 以降には、Direct3D 12 でも利用可能な新しいレンダリングと最適化の機能が含まれています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Direct3D を選択する 12 または Direct3D 11</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/what-is-directx-12-">Direct3d12 は何ですか。</a></td>
    </tr>
    <tr>
        <td>Direct3D の概要については 11</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d11/atoc-dx-graphics-direct3d-11">Direct3D 11 のグラフィック</a></td>
    </tr>
    <tr>
        <td>Direct3D 11 on 12 の概要</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/direct3d-11-on-12">Direct3D 11 on 12</a></td>
    </tr>
</table>


### <a name="bridges-game-engines-and-middleware"></a>ブリッジ、ゲーム エンジン、ミドルウェア

ゲームのニーズに応じて、ブリッジ、ゲーム エンジン、ミドルウェアを使うことにより、開発やテストに費やす時間やリソースを節約できます。 ここでは、ブリッジ、ゲーム エンジン、ミドルウェアの概要とリソースを示します。

#### <a name="universal-windows-platform-bridges"></a>ユニバーサル Windows プラットフォーム ブリッジ

ユニバーサル Windows プラットフォーム ブリッジは、既にあるアプリやゲームを UWP に移植するためのテクノロジです。 ブリッジは、すぐに UWP のゲーム開発の始めるときに最適な方法です。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>UWP ブリッジ</td>
        <td><a href="https://developer.microsoft.com/windows/bridges">Windows に、コードを移動できます。</a></td>
    </tr>
    <tr>
        <td>Windows Bridge for iOS</td>
        <td><a href="https://developer.microsoft.com/windows/bridges/ios">Windows、iOS アプリを表示します。</a></td>
    </tr>
    <tr>
        <td>デスクトップ アプリケーション用 Windows ブリッジ (.NET および Win32)</td>
        <td><a href="https://developer.microsoft.com/windows/bridges/desktop">デスクトップ アプリケーション UWP アプリへの変換します。</a></td>
    </tr>
</table>

#### <a name="playfab"></a>PlayFab

Microsoft ファミリの一部となった PlayFab は、ライブ ゲームの完全なバックエンド プラットフォームであり、独立系のスタジオが開発を開始するための強力な手段です。 ゲーム サービス、リアルタイム分析、LiveOps によって、コストを削減しながら、収益性、エンゲージメント、リテンションを向上させます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>PlayFab</td>
        <td><a href="https://playfab.com/">ツールとサービスの概要</a></td>
    </tr>
    <tr>
        <td>作業の開始</td>
        <td><a href="https://api.playfab.com/docs/general-getting-started">一般的な作業の開始ガイド</a></td>
    </tr>
    <tr>
        <td>ビデオ チュートリアル シリーズ</td>
        <td><a href="https://www.youtube.com/watch?v=fGNpiqVi5xU&list=PLHCfyL7JpoPbLpA_oh_T5PKrfzPgCpPT5">PlayFab のコア システムについてのデモ ビデオ シリーズ</a></td>
    </tr>
    <tr>
        <td>レシピ</td>
        <td><a href="https://api.playfab.com/docs/tutorials/recipes-index">人気のあるゲームのしくみと設計パターンのサンプル</a></td>
    </tr>
    <tr>
        <td>プラットフォーム</td>
        <td><a href="https://api.playfab.com/platforms">さまざまなプラットフォームとゲーム エンジンの特定のドキュメント</a></td>
    </tr>
    <tr>
        <td>GitHub リポジトリ</td>
        <td><a href="https://github.com/PlayFab">Android、iOS、Windows、Unity、Unreal などのさまざまなプラットフォームのスクリプトと Sdk を取得します。</a></td>
    </tr>
    <tr>
        <td>API ドキュメント</td>
        <td><a href="https://api.playfab.com/documentation/">残りの部分のような Web Api を使用して直接 PlayFab サービスへのアクセスします。</a></td>
    </tr>
    <tr>
        <td>フォーラム</td>
        <td><a href="https://community.playfab.com/index.html">PlayFab フォーラム</a></td>
    </tr>
</table>
 

#### <a name="unity"></a>Unity

Unity は、美しく魅力的な 2D、3D、VR、AR ゲームやアプリを作成するためのプラットフォームを提供します。 クリエイティブな構想をすばやく実現することができ、事実上、あらゆるメディアやデバイスにコンテンツを提供できます。

Unity 5.4 以降では、Unity は Direct3D 12 の開発をサポートします。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Unity ゲーム エンジン</td>
        <td><a href="https://unity.com/">Unity のゲーム エンジン</a></td>
    </tr>
    <tr>
        <td>Unity を入手する</td>
        <td><a href="https://store.unity.com/">Unity を入手する</a></td>
    </tr>
    <tr>
        <td>Windows 向けの Unity に関するドキュメント</td>
        <td><a href="https://docs.unity3d.com/Manual/Windows.html">Unity マニュアル/Windows</a></td>
    </tr>
    <tr>
        <td>PlayFab を使用して LiveOps を追加する</td>
        <td><a href="https://api.playfab.com/docs/getting-started/unity-getting-started">取得する-PlayFab API 呼び出しを始めること、Unity からゲーム</a></td>
    </tr>
    <tr>
        <td>Mixer の対話機能を使用して、ゲームに対話機能を追加する方法</td>
        <td><a href="https://github.com/mixer/interactive-unity-plugin/wiki/Getting-started">ファースト ステップ ガイド</a></td>
    </tr>
    <tr>
        <td>Unity 向け Mixer SDK</td>
        <td><a href="https://www.assetstore.unity3d.com/en/#!/content/88585">Mixer Unity プラグイン</a></td>
    </tr>
    <tr>
        <td>Unity 向け Mixer SDK のリファレンス ドキュメント</td>
        <td><a href="https://dev.mixer.com/reference/interactive/csharp/index.html">Mixer Unity プラグインの API リファレンス</a></td>
    </tr>
    <tr>
        <td>Unity ゲームを Microsoft Store に公開する</td>
        <td><a href="https://unity3d.com/partners/microsoft/porting-guides">移植のガイド</a></td>
    </tr>
    <tr>
        <td>.NET API に関連するアセンブリ参照が見つからない場合のトラブルシューティング</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/gaming/missing-dot-net-apis-in-unity-and-uwp">Unity と UWP での .NET Api がないです。</a></td>
    </tr>
    <tr>
        <td>ユニバーサル Windows プラットフォーム アプリとして Unity ゲームを公開する (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Blogs/One-Dev-Minute/How-to-publish-your-Unity-game-as-a-UWP-app">あなたの Unity ゲームを UWP アプリとして発行する方法</a></td>
    </tr>
    <tr>
        <td>Unity を使って Windows 向けゲームとアプリを作成する (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Blogs/One-Dev-Minute/Making-games-and-apps-with-Unity">Windows のゲームや Unity を使用したアプリの作成</a></td>
    </tr>
    <tr>
        <td>Visual Studio を使った Unity ゲームの開発 (ビデオ シリーズ)</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkId=722359">Visual Studio 2015 での Unity の使用</a></td>
    </tr>
</table>
 

#### <a name="havok"></a>Havok

Havok のモジュール化された一連のツールとテクノロジによって、ゲーム クリエーターは新しいレベルの対話式操作と没入感を提供できます。 Havok により、非常にリアルな物理的効果、対話型のシミュレーション、魅力的な映像を実現できます。 Version 2015.1 以上では、x86、64 ビット、ARM 上の Visual Studio 2015 で UWP を正式にサポートします。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Havok の Web サイト</td>
        <td><a href="https://www.havok.com/">Havok</a></td>
    </tr>
    <tr>
        <td>Havok ツール スイート</td>
        <td><a href="https://www.havok.com/products/">Havok 製品概要</a></td>
    </tr>
    <tr>
        <td>Havok サポート フォーラム</td>
        <td><a href="https://www.havok.com/">Havok</a></td>
    </tr>
</table>
 

#### <a name="monogame"></a>MonoGame

MonoGame は、オープン ソース、クロスプラット フォームのゲーム開発フレームワークで、当初は Microsoft の XNA Framework 4.0 に基づいていました。 現在、Monogame は、Windows、Windows Phone、Xbox と共に、Linux、macOS、iOS、Android、その他のいくつかのプラットフォームをサポートしています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>MonoGame</td>
        <td><a href="https://www.monogame.net">MonoGame の web サイト</a></td>
    </tr>
    <tr>
        <td>MonoGame のドキュメント</td>
        <td><a href="https://www.monogame.net/documentation/">MonoGame ドキュメント (最新)</a></td>
    </tr>
    <tr>
        <td>Monogame のダウンロード</td>
        <td>MonoGame の Web サイトから<a href="https://www.monogame.net/downloads/">リリース、開発ビルド、ソース コードをダウンロード</a>するか、<a href="https://www.nuget.org/profiles/MonoGame">NuGet から最新のリリースを入手</a>します。
    </tr>
    <tr>
        <td>MonoGame 2D UWP ゲームのサンプル</td>
        <td><a href="../get-started/get-started-tutorial-game-mg2d.md">MonoGame 2D での UWP ゲームを作成します。</a></td>
    </tr>    
</table>


#### <a name="cocos2d"></a>Cocos2d

Cocos2d-x は、オープン ソース、クロス プラットフォームのゲーム開発エンジンおよびツール スイートで、UWP ゲームの構築をサポートしています。 バージョン 3 以降、3D 機能も追加されています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Cocos2d-x</td>
        <td><a href="https://www.cocos2d-x.org/">Cocos2d-x とは何ですか。</a></td>
    </tr>
    <tr>
        <td>Cocos2d-x プログラマ ガイド</td>
        <td><a href="https://www.cocos2d-x.org/programmersguide/">Cocos2d-x プログラマ ガイド</a></td>
    </tr>
    <tr>
        <td>Windows 10 での Cocos2d-x (ブログの投稿)</td>
        <td><a href="https://blogs.windows.com/buildingapps/2015/06/15/running-cocos2d-x-on-windows-10/">Windows 10 で実行中の cocos2d-x</a></td>
    </tr>
    <tr>
        <td>PlayFab を使用して LiveOps を追加する</td>
        <td><a href="https://api.playfab.com/docs/getting-started/cocos2d-x-getting-started-guide">取得する-PlayFab API 呼び出しを始めること、Cocos2d からゲーム</a></td>
    </tr>
</table>


#### <a name="unreal-engine"></a>Unreal Engine

Unreal Engine 4 は、あらゆる種類のゲームや開発者に適したゲーム開発ツールがすべて揃ったスイートです。 最も要求の厳しいコンソールおよび PC ゲームにおいて、Unreal Engine は世界中のゲーム開発者により使用されています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Unreal Engine の概要</td>
        <td><a href="https://www.unrealengine.com/what-is-unreal-engine-4">Unreal Engine 4</a></td>
    </tr>
    <tr>
        <td>PlayFab を使用して LiveOps を追加する - C++</td>
        <td><a href="https://api.playfab.com/docs/getting-started/unreal-cpp-getting-started">取得する-PlayFab API 呼び出しを始めること、Unreal のゲーム</a></td>
    </tr>
    <tr>
        <td>PlayFab を使用して LiveOps を追加する - Blueprints</td>
        <td><a href="https://api.playfab.com/docs/getting-started/unreal-blueprints-getting-started">取得する-PlayFab API 呼び出しを始めること、Unreal のゲーム</a></td>
    </tr>
</table>

#### <a name="babylonjs"></a>BabylonJS

BabylonJS は、HTML5、WebGL、WebVR、Web オーディオで 3D ゲームを構築するための完全な JavaScript フレームワークです。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>BabylonJS</td>
        <td><a href="https://www.babylonjs.com/">BabylonJS</a></td>
    </tr>
    <tr>
        <td>HTML5 と BabylonJS を使用した WebGL 3D (ビデオ シリーズ)</td>
        <td><a href="https://channel9.msdn.com/Series/Introduction-to-WebGL-3D-with-HTML5-and-Babylonjs/01">WebGL 3D と BabylonJS 学習</a></td>
    </tr>
    <tr>
        <td>BabylonJS を使用してクロスプラットフォーム WebGL ゲームを構築する</td>
        <td><a href="https://www.smashingmagazine.com/2016/07/babylon-js-building-sponza-a-cross-platform-webgl-game/">BabylonJS を使用して、クロス プラットフォーム ゲームを開発するには</a></td>
    </tr>    
</table>

### <a name="porting-your-game"></a>ゲームの移植

既にゲームがある場合は、ゲームを短期間で UWP に移植するのに役立つ多くのリソースやガイドがあります。 移植作業をすぐに開始する場合は、[ユニバーサル Windows プラットフォーム ブリッジ](#universal-windows-platform-bridges)を使うことも検討してください。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Windows 8 アプリをユニバーサル Windows プラットフォーム アプリに移植する (ビデオ)</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/porting/w8x-to-uwp-root">Windows ランタイム 8.x から UWP への移行</a></td>
    </tr>
    <tr>
        <td>Windows 8 アプリをユニバーサル Windows プラットフォーム アプリに移植する (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Series/A-Developers-Guide-to-Windows-10/21">8.1 の移植を Windows 10 アプリ</a></td>
    </tr>
    <tr>
        <td>iOS アプリをユニバーサル Windows プラットフォーム アプリに移植する</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/porting/ios-to-uwp-root">iOS から UWP への移行</a></td>
    </tr>
    <tr>
        <td>Silverlight アプリをユニバーサル Windows プラットフォーム アプリに移植する</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/porting/wpsl-to-uwp-root">Windows Phone Silverlight から UWP への移行</a></td>
    </tr>
    <tr>
        <td>XAML または Silverlight からユニバーサル Windows プラットフォーム アプリに移植する (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/Build/2015/3-741">XAML または Silverlight から Windows 10 にアプリを移植します。</a></td>
    </tr>
    <tr>
        <td>Xbox ゲームをユニバーサル Windows プラットフォーム アプリに移植する</td>
        <td><a href="https://developer.xboxlive.com/en-us/platform/development/education/Documents/Porting%20from%20Xbox%20One%20to%20Windows%2010.aspx">Windows 10 UWP Xbox One から移植</a></td>
    </tr>
    <tr>
        <td>DirectX 9 から DirectX 11 に移植する</td>
        <td><a href="porting-your-directx-9-game-to-windows-store.md">DirectX 9 からユニバーサル Windows プラットフォーム (UWP) への移植</a></td>
    </tr>
    <tr>
        <td>Direct3D 11 から Direct3D 12 に移植する</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/porting-from-direct3d-11-to-direct3d-12">Direct3D から移植 Direct3D を 11 12</a></td>
    </tr>
    <tr>
        <td>OpenGL ES から Direct3D 11 に移植する</td>
        <td><a href="port-from-opengl-es-2-0-to-directx-11-1.md">OpenGL ES 2.0 から Direct3D への移植 11</a></td>
    </tr>
    <tr>
        <td>ANGLE を使って OpenGL ES から Direct3D 11 に移行する</td>
        <td><a href="https://go.microsoft.com/fwlink/p/?linkid=618387">角度</a></td>
    </tr>
    <tr>
        <td>UWP で従来の Windows API に相当する要素</td>
        <td><a href="https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps">Windows ユニバーサル Windows Api の代替プラットフォーム (UWP) アプリ</a></td>
    </tr>
</table>


## <a name="prototype-and-design"></a>プロトタイプとデザイン


作成するゲームの種類と、ゲームの構築に使うツールとグラフィックス テクノロジが決まったら、すぐにデザインとプロトタイプを開始できます。 ゲームのコアはユニバーサル Windows プラットフォーム アプリであるため、そこから作業を開始します。

### <a name="introduction-to-the-universal-windows-platform-uwp"></a>ユニバーサル Windows プラットフォーム (UWP) の概要

Windows 10 ではユニバーサル Windows プラットフォーム (UWP) が導入され、Windows 10 デバイス間で共通の API プラットフォームが提供されます。 UWP は、Windows ランタイム モデルを発展させて拡張したもので、まとまりのある統一されたコアとなっています。 UWP を対象とするゲームでは、すべてのデバイスに共通する WinRT API を呼び出すことができます。 UWP により保証された API 層が提供されるため、あらゆる Windows 10 デバイスにインストールできる 1 つのアプリ パッケージを作成することもできます。 また、必要に応じて、ゲームが実行されるデバイスに固有の API (Win32 や .NET の従来の Windows API など) を、ゲームで呼び出すこともできます。

次に示すガイドは、ユニバーサル Windows プラットフォーム アプリについて詳しく説明している優れたガイドであり、このプラットフォームを理解するために一読することをお勧めします。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ユニバーサル Windows プラットフォーム アプリの概要</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/get-started/whats-a-uwp">新機能、ユニバーサル Windows プラットフォーム アプリですか?</a></td>
    </tr>
    <tr>
        <td>UWP の概要</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide">UWP アプリ ガイド</a></td>
    </tr>
</table>
 

### <a name="getting-started-with-uwp-development"></a>UWP 開発の概要

ユニバーサル Windows プラットフォーム アプリを開発するための準備は非常に簡単です。 以下のガイドでは、プロセスの詳しい手順を説明しています。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>UWP 開発の概要</td>
        <td><a href="https://developer.microsoft.com/windows/apps/getstarted">Windows アプリの概要</a></td>
    </tr>
    <tr>
        <td>UWP 開発の準備</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/get-started/get-set-up">準備</a></td>
    </tr>
</table>

UWP プログラミングについて "文字どおりの初心者" である場合や、ゲームで XAML の使用を検討している場合 (「[グラフィックス テクノロジとプログラミング言語の選択](#choosing-your-graphics-technology-and-programming-language)」を参照) は、最初に[文字どおりの初心者のための Windows 10 の開発](https://channel9.msdn.com/Series/Windows-10-development-for-absolute-beginners)に関するビデオ シリーズをご覧になることをお勧めします。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>XAML を使った Windows 10 の開発の初心者向けガイド (ビデオ シリーズ)</td>
        <td><a href="https://channel9.msdn.com/Series/Windows-10-development-for-absolute-beginners">超初心者向けの Windows 10 の開発</a></td>
    </tr>
    <tr>
        <td>XAML を使う Windows 10 の初心者向けシリーズの発表 (ブログの投稿)</td>
        <td><a href="https://blogs.windows.com/buildingapps/2015/09/30/windows-10-development-for-absolute-beginners/">超初心者向けの Windows 10 の開発</a></td>
    </tr>
</table>

### <a name="uwp-development-concepts"></a>UWP 開発の概念

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ユニバーサル Windows プラットフォーム アプリの開発の概要</td>
        <td><a href="https://developer.microsoft.com/windows/apps/develop">Windows アプリを開発します。</a></td>
    </tr>
    <tr>
        <td>UWP のネットワーク プログラミングの概要</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/networking/index">ネットワークと Web サービス</a></td>
    </tr>
    <tr>
        <td>ゲームでの Windows.Web.HTTP と Windows.Networking.Sockets の使用</td>
        <td><a href="work-with-networking-in-your-directx-game.md">ゲーム用のネットワーク</a></td>
    </tr>
    <tr>
        <td>UWP での非同期プログラミングの概念</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/threading-async/asynchronous-programming-universal-windows-platform-apps">非同期プログラミング</a></td>
    </tr>
</table>

### <a name="windows-desktop-apisto-uwp"></a>UWP への Windows デスクトップ Api

Windows デスクトップ ゲームを UWP に移行する際に役立つリンクの一部を以下に示します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>既存の C++ コードを使った UWP ゲーム開発</td>
        <td><a href="https://docs.microsoft.com/cpp/porting/how-to-use-existing-cpp-code-in-a-universal-windows-platform-app">方法:UWP アプリで既存の C++ コードを使用します。</a></td>
    </tr>
    <tr>
        <td>Win32 API と COM API 用の UWP API</td>
        <td><a href="https://docs.microsoft.com/uwp/win32-and-com/win32-and-com-for-uwp-apps">Win32 および COM Api の UWP アプリ</a></td>
    </tr>
    <tr>
        <td>UWP でサポートされない CRT 関数</td>
        <td><a href="https://docs.microsoft.com/cpp/cppcx/crt-functions-not-supported-in-universal-windows-platform-apps">ユニバーサル Windows プラットフォーム アプリでサポートされていない CRT 関数</a></td>
    </tr>
    <tr>
        <td>Windows API の代替</td>
        <td><a href="https://docs.microsoft.com/uwp/win32-and-com/alternatives-to-windows-apis-uwp">Windows ユニバーサル Windows Api の代替プラットフォーム (UWP) アプリ</a></td>
    </tr>
</table>
 

### <a name="process-lifetime-management"></a>プロセス ライフタイム管理

プロセス ライフタイム管理、つまりアプリのライフ サイクルは、ユニバーサル Windows プラットフォーム アプリが取り得るさまざまなアクティブ化状態を表します。 ゲームは、アクティブ化、中断、再開、または終了することができ、さまざまな方法でこれらの状態を移行できます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>アプリのライフ サイクルの移行の処理</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/launch-resume/app-lifecycle">アプリのライフサイクル</a></td>
    </tr>
    <tr>
        <td>Microsoft Visual Studio を使ったアプリの移行のトリガー</td>
        <td><a href="https://docs.microsoft.com/visualstudio/debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio?view=vs-2015">トリガーする方法を中断、再開、およびバック グラウンド イベントを Visual Studio で UWP アプリ</a></td>
    </tr>
</table>
 

### <a name="designing-game-ux"></a>ゲーム UX の設計

優れたゲームはすばらしいデザインから始まります。

ゲームは、共通のユーザー インターフェイス要素とデザイン原則をアプリと共有していますが、ユーザー エクスペリエンスの外観、機能、設計目標が独特であることがよくあります。 テストされた UX をゲームで使用すべきなのはいつか、斬新で革新的な UX を使用すべきなのはいつか、という両方の側面に、よく考えられたデザインを当てはめるときにゲームは成功します。 ゲームに選択したプレゼンテーション テクノロジ (DirectX、XAML、HTML5、または 3 つの組み合わせ) は、実装の細部に影響を与える可能性がありますが、適用するデザイン原則はその選択とはほとんど関係がありません。

UX デザインとは別に、レベルのデザイン、ペース配分、世界のデザインなどのゲームプレイのデザインには独自の様式があり、開発者や開発チームによって決定されるため、この開発ガイドに記載していません。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>UWP の設計の基本とガイドライン</td>
        <td><a href="https://developer.microsoft.com/en-us/windows/apps/design">UWP アプリの設計</a></td>
    </tr>
    <tr>
        <td>アプリのライフサイクルの状態の設計</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/launch-resume/index">UX ガイドラインに起動、中断、および再開</a></td>
    </tr>
    <tr>
        <td>Xbox One とテレビ画面向けの UWP アプリの設計</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/design/devices/designing-for-tv">Xbox およびテレビ向け設計</a></td>
    </tr>
    <tr>
        <td>複数のデバイスのフォーム ファクターをターゲットに設定する (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Designing-Games-for-a-Windows-Core-World">Windows Core 世界中のゲームの設計</a></td>
    </tr>   
</table>
 

#### <a name="color-guideline-and-palette"></a>色のガイドラインとパレット

ゲームで一貫した色のガイドラインに従うと、美しさやナビゲーションの操作性が向上し、メニューや HUD の機能がプレーヤーに伝わりやすくなります。 警告、ダメージ、XP、成績などのゲーム要素の色が一貫していると、UI がわかりやすくなるため、ラベルによって説明する必要性が減ります。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>色のガイド</td>
        <td><a href="https://assets.windowsphone.com/499cd2be-64ed-4b05-a4f5-cd0c9ad3f6a3/101_BestPractices_Color_InvariantCulture_Default.zip">ベスト プラクティス:色</a></td>
    </tr>
</table>
 

#### <a name="typography"></a>タイポグラフィ

文字体裁を適切に使うと、UI のレイアウト、ナビゲーション、読みやすさ、雰囲気、ブランド、プレイヤーの熱中度など、多くの側面が向上します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>文字体裁のガイド</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkId=535007">ベスト プラクティス:文字体裁</a></td>
    </tr>
</table>
 

#### <a name="ui-map"></a>UI マップ

UI マップとは、ゲーム ナビゲーションのレイアウトとフローチャートで表されるメニューのことです。 UI マップを使うと、すべての関係者が、ゲームのインターフェイスとナビゲーション パスを理解しやすくなり、開発サイクルの初期段階で潜在的な障害や行き詰まりが明らかになります。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>UI マップ ガイド</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkId=535008">ベスト プラクティス:UI マップ</a></td>
    </tr>
</table>

### <a name="game-audio"></a>ゲーム オーディオ

XAudio2、XAPO、Windows Sonic を使ってオーディオをゲームで実装するためのガイドとリファレンス XAudio2 は、パフォーマンスの高いオーディオ エンジンを開発するための、信号処理とミキシングの基盤を提供する低水準のオーディオ API です。 XAPO API を使用すると、XAudio2 を使用するクロスプラットフォーム オーディオ処理オブジェクト (XAPO) を、Windows と Xbox の両方で作成できます。 Windows Sonic オーディオのサポートにより、ゲームやストリーミング メディア アプリケーションに、Dolby Atmos for Home Theater、Dolby Atmos for Headphones、Windows HRTF のサポートを追加できます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>XAudio2 API</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/xaudio2/xaudio2-apis-portal">プログラミング ガイドと XAudio2 の API リファレンス</a></td>
    </tr>
    <tr>
        <td>クロスプラット フォーム オーディオ処理オブジェクトを作成する</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/xaudio2/xapo-overview">XAPO の概要</a></td>
    </tr>
    <tr>
        <td>オーディオの概念の概要</td>
        <td><a href="working-with-audio-in-your-directx-game.md">ゲームにオーディオ</a></td>
    </tr>
    <tr>
        <td>Windows Sonic の概要</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/CoreAudio/spatial-sound">立体音響</a></td>
    </tr>
    <tr>
        <td>Windows Sonic の立体音響のサンプル</td>
        <td><a href="https://github.com/Microsoft/Xbox-ATG-Samples/tree/master/UWPSamples/Audio">高度なテクノロジのグループの Xbox オーディオ サンプル</a></td>
    </tr>
    <tr>
        <td>Windows Sonic をゲーム (ビデオ) に統合する方法</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2017/GDC2017-002">Xbox、Windows の空間のオーディオ機能を発表</a></td>
    </tr>
</table>

### <a name="directx-development"></a>DirectX 開発

DirectX ゲーム開発用のガイドと参照情報を紹介します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>UWP 用の DirectX 開発</td>
        <td><a href="directx-programming.md">DirectX プログラミング</a></td>
    </tr>
    <tr>
        <td>チュートリアル:UWP の DirectX ゲームを作成する方法</td>
        <td><a href="tutorial--create-your-first-uwp-directx-game.md">DirectX によるシンプルな UWP ゲームの作成</a></td>
    </tr>
    <tr>
        <td>UWP アプリ モデルによる DirectX の操作</td>
        <td><a href="about-the-uwp-user-interface-and-directx.md">アプリケーション オブジェクトと DirectX</a></td>
    </tr>
    <tr>
        <td>グラフィックスおよび DirectX 12 開発に関するビデオ (YouTube チャンネル)</td>
        <td><a href="https://www.youtube.com/channel/UCiaX2B8XiXR70jaN7NK-FpA">Microsoft DirectX 12 とグラフィックスの教育</a></td>
    </tr>
    <tr>
        <td>DirectX の概要とリファレンス</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/directx">DirectX のグラフィックスとゲーミング</a></td>
    </tr>
    <tr>
        <td>Direct3D 12 プログラミング ガイドとリファレンス</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/direct3d-12-graphics">Direct3D 12 グラフィックス</a></td>
    </tr>
    <tr>
        <td>DirectX 12 の基本事項 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Better-Power-Better-Performance-Your-Game-on-DirectX12">優れた電源、パフォーマンスが向上します。DirectX 12 のゲーム</a></td>
    </tr>
</table>

#### <a name="learning-direct3d-12"></a>Direct3D 12 について

Direct3D 12 での変更点、および Direct3D 12 を使ってプログラミングを開始する方法について説明します。 

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>プログラミング環境のセットアップ</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/directx-12-programming-environment-set-up">Direct3d12 プログラミング環境のセットアップ</a></td>
    </tr>
    <tr>
        <td>基本的なコンポーネントを作成する方法</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/creating-a-basic-direct3d-12-component">Direct3D 12 の基本的なコンポーネントの作成</a></td>
    </tr>
    <tr>
        <td>Direct3D 12 での変更点</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/important-changes-from-directx-11-to-directx-12">Direct3d11 から direct3d12 への移行、重要な変更</a></td>
    </tr>
    <tr>
        <td>Direct3D 11 から Direct3D 12 に移植する方法</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/porting-from-direct3d-11-to-direct3d-12">Direct3D から移植 Direct3D を 11 12</a></td>
    </tr>
    <tr>
        <td>リソース バインディングの概念 (対象となる記述子、記述子テーブル、記述子ヒープ、およびルート署名) </td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/resource-binding">Direct3D 12 でのリソース バインディング</a></td>
    </tr>
    <tr>
        <td>メモリ管理</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/memory-management">Direct3D 12 でのメモリ管理</a></td>
    </tr>
</table>
 

#### <a name="directx-tool-kit-and-libraries"></a>DirectX ツール キットとライブラリ

DirectX ツール キット、DirectX テクスチャ処理ライブラリ、DirectXMesh ジオメトリ処理ライブラリ、UVAtlas ライブラリ、DirectXMath ライブラリは、DirectX 開発用のテクスチャ、メッシュ、スプライト、その他のユーティリティ機能とヘルパー クラスを提供します。 これらのライブラリは、開発にかかる時間と労力を減らすのに役立ちます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>DirectX 11 用 DirectX ツール キットを入手する</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkId=248929">DirectXTK</a></td>
    </tr>
    <tr>
        <td>DirectX 12 用 DirectX ツール キットを入手する</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkID=615561">DirectXTK 12</a></td>
    </tr>
    <tr>
        <td>DirectX テクスチャ処理ライブラリを入手する</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkId=248926">DirectXTex</a></td>
    </tr>
    <tr>
        <td>DirectXMesh ジオメトリ処理ライブラリを入手する</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkID=324981">DirectXMesh</a></td>
    </tr>
    <tr>
        <td>isochart テクスチャ アトラスを作成してパッケージ化するための UVAtlas を入手する</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkID=512686">UVAtlas</a></td>
    </tr>
    <tr>
        <td>DirectXMath のライブラリを入手する</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkID=615560">DirectXMath</a></td>
    </tr>
    <tr>
        <td>Direct3d12 サポート DirectXTK (ブログの投稿)</td>
        <td><a href="https://github.com/Microsoft/DirectXTK/issues/2">DirectX 12 のサポート</a></td>
    </tr>
</table>

#### <a name="directx-resources-from-partners"></a>パートナーからの DirectX リソース

これらは、外部のパートナーによって作成された補足の DirectX ドキュメントです。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Nvidia:DX12」とすべきでないこと (ブログの投稿) </td>
        <td><a href="https://developer.nvidia.com/dx12-dos-and-donts-updated">Nvidia の Gpu での DirectX 12</a></td>
    </tr>
    <tr>
        <td>Intel:DirectX 12 を使用した効率的なレンダリング</td>
        <td><a href="https://software.intel.com/sites/default/files/managed/4a/38/Efficient-Rendering-with-DirectX-12-on-Intel-Graphics.pdf">Intel グラフィックスのレンダリングに DirectX 12</a></td>
    </tr>
    <tr>
        <td>Intel:DirectX 12 で複数のアダプターのサポート</td>
        <td><a href="https://software.intel.com/articles/multi-adapter-support-in-directx-12">DirectX 12 を使用して明示的なマルチ アダプター アプリケーションを実装する方法</a></td>
    </tr>
    <tr>
        <td>Intel:DirectX 12 のチュートリアル</td>
        <td><a href="https://software.intel.com/articles/tutorial-migrating-your-apps-to-directx-12-part-1">Intel、Suzhou あふれると Microsoft によって共同作業のホワイト ペーパー</a></td>
    </tr>
</table>


## <a name="production"></a>Production


制作スタジオの準備が整ったら、チーム全体に作業を分散して制作サイクルに移行します。 プロトタイプの調整、リファクタリング、拡張によって、ゲームの完成品に仕上げていきます。

### <a name="notifications-and-live-tiles"></a>通知とライブ タイル

タイルとは、[スタート] メニュー上でゲームを表すものです。 タイルや通知によって、ゲームをプレイしていない場合でも、プレイヤーに興味を持たせることができます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>タイルとバッジの開発</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-badges-notifications">タイル、バッジ、通知</a></td>
    </tr>
    <tr>
        <td>ライブ タイルと通知を示すサンプル</td>
        <td><a href="https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Notifications">通知のサンプル</a></td>
    </tr>
    <tr>
        <td>アダプティブ タイル テンプレート (ブログの投稿)</td>
        <td><a href="https://blogs.msdn.microsoft.com/tiles_and_toasts/2015/06/30/adaptive-tile-templates-schema-and-documentation/">適応型タイル テンプレートのスキーマとドキュメント</a></td>
    </tr>
    <tr>
        <td>タイルとバッジの設計</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-creating-tiles">タイルとバッジのガイドライン</a></td>
    </tr>
    <tr>
        <td>ライブ タイル テンプレートを対話形式で開発するための Windows 10 アプリ</td>
        <td><a href="https://www.microsoft.com/store/apps/9nblggh5xsl1">Notifications Visualizer</a></td>
    </tr>
    <tr>
        <td>Visual Studio 用の UWP Tile Generator 拡張機能</td>
        <td><a href="https://marketplace.visualstudio.com/items?itemName=shenchauhan.UWPTileGenerator">1 つのイメージを使用して必要なすべてのタイルを作成するためのツール</a></td>
    </tr>
    <tr>
        <td>Visual Studio 用の UWP Tile Generator 拡張機能 (ブログの投稿)</td>
        <td><a href="https://blogs.windows.com/buildingapps/2016/02/15/uwp-tile-generator-extension-for-visual-studio/">UWP タイル ジェネレーター ツールの使用に関するヒント</a></td>
    </tr>
</table>
 

### <a name="enable-in-app-product-add-on-purchases"></a>アプリ内製品 (アドオン) の購入を有効にします。

アドオン (アプリ内製品) は、プレイヤーがゲームを購入できる補助項目です。 アドオンには、ゲーム レベル、アイテム、またはプレーヤーがお勧めするその他すべてを指定できます。 適切に使用すると、アドオンは、ゲーム エクスペリエンスを向上させながら収益を提供できます。 パートナー センターでのゲームのアドオンの発行を定義し、ゲームのコードでのアプリ内購入を有効にします。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>持続性のあるアドオン</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/monetize/enable-in-app-product-purchases">アプリ内製品購入を有効にする</a></td>
    </tr>
    <tr>
        <td>使用できるアドオン</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/monetize/enable-consumable-in-app-product-purchases">コンシューマブルなアプリ内製品購入を有効にする</a></td>
    </tr>
    <tr>
        <td>アドオンの詳細と送信</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/iap-submissions">アドオンの申請</a></td>
    </tr>
    <tr>
        <td>アドオンの売上と人口統計、ゲームを監視します。</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/iap-acquisitions-report">アドオン取得レポート</a></td>
    </tr>
</table>
 

### <a name="debugging-performance-optimization-and-monitoring"></a>デバッグとパフォーマンスの最適化と監視

パフォーマンスを最適化するには、Windows 10 のゲーム モードを活用し、ハードウェアの機能を最大限に活用して、ゲーマーに可能な限りのゲーム エクスペリエンスを提供します。

Windows Performance Toolkit (WPT) は、Windows オペレーティング システムやアプリケーションの詳しいパフォーマンス プロファイルを生成するための一連のパフォーマンス監視ツールです。 これは、メモリ使用量を監視し、ゲームのパフォーマンスを向上させるために特に便利です。 Windows Performance Toolkit は、Windows 10 SDK と Windows ADK に含まれています。 このツールキットは、2 つの独立したツールで構成されます。Windows Performance Recorder (WPR) と Windows パフォーマンス アナライザー (WPA)。 [Windows Sysinternals](https://technet.microsoft.com/sysinternals/default) に含まれる ProcDump は、コマンドライン ユーティリティであり、CPU 使用量の急上昇を監視し、ゲームのクラッシュ時にダンプ ファイルを生成します。 

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>コードのパフォーマンス テストを行う</td>
        <td><a href="https://azure.microsoft.com/services/devops/test-plans/">クラウド ベースのロード テスト</a></td>
    </tr>
    <tr>
        <td>ゲーム デバイス情報を使用して Xbox 本体のタイプを取得する</td>
        <td><a href="https://docs.microsoft.com/previous-versions/windows/desktop/gamingdvcinfo/gaming-device-information-portal">ゲームのデバイス情報</a></td>
    </tr>
    <tr>
        <td>ゲーム モードの API の使用によるハードウェア リソースへの排他的または優先的なアクセスを使ったパフォーマンスの向上</td>
        <td><a href="https://docs.microsoft.com/previous-versions/windows/desktop/gamemode/game-mode-portal">ゲーム モード</a></td>
    </tr>
    <tr>
        <td>Windows 10 SDK から Windows Performance Toolkit (WPT) を入手する</td>
        <td><a href="https://developer.microsoft.com/windows/downloads/windows-10-sdk">Windows 10 SDK</a></td>
    </tr>
    <tr>
        <td>Windows ADK から Windows Performance Toolkit (WPT) を入手する</td>
        <td><a href="https://msdn.microsoft.com/windows/hardware/dn913721.aspx">Windows ADK</a></td>
    </tr>
    <tr>
        <td>Windows Performance Analyzer を使って応答しない UI のトラブルシューティングを行う (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-156-Critical-Path-Analysis-with-Windows-Performance-Analyzer">WPA では、クリティカル パス分析</a></td>
    </tr>
    <tr>
        <td>Windows Performance Recorder を使ってメモリ使用量とメモリ リークを診断する (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-154-Memory-Footprint-and-Leaks">メモリ使用量やリーク</a></td>
    </tr>
    <tr>
        <td>ProcDump を取得する</td>
        <td><a href="https://technet.microsoft.com/sysinternals/dd996900">ProcDump</a></td>
    </tr>
    <tr>
        <td>ProcDump の使い方 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-131-Windows-10-SDK">ダンプ ファイルを作成する ProcDump を構成します。</a></td>
    </tr>
</table>

### <a name="advanced-directx-techniques-and-concepts"></a>高度な DirectX の手法と概念

DirectX の開発には微妙で複雑な部分があります。 運用環境で、DirectX エンジンの詳細を掘り下げる必要がある場合や、難しいパフォーマンスの問題をデバッグする場合は、このセクションで紹介するリソースや情報が役立ちます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Windows の PIX</td>
        <td><a href="https://devblogs.microsoft.com/pix/introducing-pix-on-windows-beta/">パフォーマンスのチューニングと、Windows での DirectX 12 のデバッグ ツール</a></td>
    </tr>
    <tr>
        <td>D3D12 開発のデバッグと検証のツール (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2017/GDC2017-003">D3D12 のパフォーマンス チューニングと PIX と GPU の検証を使用したデバッグ</a></td>
    </tr>
    <tr>
        <td>グラフィックスとパフォーマンスの最適化 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Advanced-DirectX12-Graphics-and-Performance">高度な DirectX 12 のグラフィックスとパフォーマンス</a></td>
    </tr>
    <tr>
        <td>DirectX グラフィックスのデバッグ (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Solve-the-Tough-Graphics-Problems-with-your-Game-Using-DirectX-Tools">DirectX ツールを使用して、ゲームに大変なグラフィックスの問題を解決します。</a></td>
    </tr>
    <tr>
        <td>DirectX 12 をデバッグするための Visual Studio 2015 のツール (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Series/ConnectOn-Demand/212">Visual Studio 2015 での Windows 10 用の DirectX ツール</a></td>
    </tr>
    <tr>
        <td>Direct3D 12 プログラミング ガイド</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/direct3d12/direct3d-12-graphics">Direct3D 12 プログラミング ガイド</a></td>
    </tr>
    <tr>
        <td>DirectX と XAML の組み合わせ</td>
        <td><a href="directx-and-xaml-interop.md">DirectX および XAML の相互運用機能</a></td>
    </tr>
</table>

### <a name="high-dynamic-range-hdr-content-development"></a>ハイ ダイナミック レンジ (HDR) コンテンツの開発

HDR のフル カラー機能を使用するゲーム コンテンツを構築します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>HDR の概要と色の概念 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/Build/2017/P4061">HDR および DirectX での高度なカラーを照明</a></td>
    </tr>
    <tr>
        <td>HDR コンテンツをレンダリングする方法と、現在のディスプレイが HDR コンテンツをサポートするかどうかを検出する方法について説明します。</td>
        <td><a href="https://github.com/Microsoft/DirectX-Graphics-Samples/tree/master/Samples/UWP/D3D12HDR">HDR サンプル</a></td>
    </tr>
    <tr>
        <td>DirectX を使用して高度な色を作成および構成する</td>
        <td><a href="https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/D2DAdvancedColorImages">Direct2D 高度なカラー イメージのレンダリングの例</a></td>
    </tr>   
</table>


### <a name="globalization-and-localization"></a>グローバリゼーションとローカライズ

Windows プラットフォーム用の多言語対応ゲームを開発し、Microsoft の有力製品に組み込まれている地域と言語の機能について説明します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>世界市場向けのゲームの準備</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/globalizing/globalizing-portal">グローバル ユーザー向けに開発する場合のガイドライン</a></td>
    </tr>
    <tr>
        <td>言語、文化、およびテクノロジの橋渡し</td>
        <td><a href="https://www.microsoft.com/Language/Default.aspx">言語の規則および Microsoft の一般的な用語のオンライン リソース</a></td>
    </tr>
</table>

## <a name="submitting-and-publishing-your-game"></a>ゲームの申請と公開

次のガイドと情報は、公開と申請のプロセスをできるだけスムーズに進めるために役立ちます。

### <a name="publishing"></a>置換

使用して[パートナー センター](https://partner.microsoft.com/dashboard)発行して、ゲームのパッケージを管理します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>パートナー センターのアプリの発行</td>
        <td><a href="https://developer.microsoft.com/store/publish-apps">Windows アプリを公開する</a></td>
    </tr>
    <tr>
        <td>パートナー センターの詳細 (GDN) の発行</td>
        <td><a href="https://developer.xboxlive.com/en-us/windows/documentation/Pages/home.aspx">パートナー センターの公開に関するガイドの詳細</a></td>
    </tr>
    <tr>
        <td>Azure Active Directory (AAD) を使用して、パートナー センター アカウントにユーザーを追加するには</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/manage-account-users">アカウントのユーザーを管理します。</a></td>
    </tr>   
    <tr>
        <td>ゲームの評価 (ブログの投稿)</td>
        <td><a href="https://blogs.windows.com/buildingapps/2016/01/06/now-available-single-age-rating-system-to-simplify-app-submissions/">1 つのワークフローを IARC システムを使用して、年齢区分を割り当てる</a></td>
    </tr>
</table>

#### <a name="packaging-and-uploading"></a>パッケージ化とアップロード

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ストリーミング インストールとオプション パッケージを使用する方法 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/Build/2017/B8093">Nextgen UWP アプリの配布:拡張可能なストリームできる、コンポーネント化されたアプリの構築</a></td>
    </tr>
    <tr>
        <td>コンテンツの分割とグループ化によるストリーミング インストールの実現</td>
        <td><a href="../packaging/streaming-install.md">UWP アプリのストリーミング インストール</a></td>
    </tr>
    <tr>
        <td>DLC ゲーム コンテンツのようなオプション パッケージを作成する</td>
        <td><a href="../packaging/optional-packages.md">オプション パッケージと関連セットの作成</a></td>
    </tr>
    <tr>
        <td>UWP ゲームのパッケージ化</td>
        <td><a href="../packaging/index.md">アプリのパッケージ化</a></td>
    </tr>
    <tr>
        <td>UWP DirectX ゲームのパッケージ化</td>
        <td><a href="package-your-windows-store-directx-game.md">UWP の DirectX ゲームをパッケージ化します。</a></td>
    </tr>
    <tr>
        <td>サード パーティ開発者としてのゲームのパッケージ化 (ブログ投稿)</td>
        <td><a href="https://blogs.windows.com/buildingapps/2015/12/15/building-an-app-for-a-3rd-party-how-to-package-their-store-app/">発行元のストア アカウントのアクセス権を持たない uploadable パッケージを作成します。</a></td>
    </tr>
    <tr>
        <td>MakeAppx を使用したアプリ パッケージとアプリ パッケージ バンドルの作成</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/packaging/create-app-package-with-makeappx-tool">App packager ツール MakeAppx.exe を使用してパッケージを作成します。</a></td>
    </tr>
    <tr>
        <td>SignTool を使用したファイルへのデジタル署名</td>
        <td><a href="https://docs.microsoft.com/windows/desktop/SecCrypto/signtool">ファイルに署名し、SignTool を使用してファイルの署名を確認します。</a></td>
    </tr>    
    <tr>
        <td>ゲームのアップロードとバージョン管理</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/upload-app-packages">アプリ パッケージをアップロードします。</a></td>
    </tr>
</table>


### <a name="policies-and-certification"></a>ポリシーと認定

認定に関する問題によってゲームのリリースを延期しないでください。 ここでは、ポリシーと注意が必要な一般的な認定の問題を示します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Microsoft Store アプリ開発者契約</td>
        <td><a href="https://docs.microsoft.com/legal/windows/agreements/app-developer-agreement">アプリ開発者契約</a></td>
    </tr>
    <tr>
        <td>Microsoft Store でアプリを公開するためのポリシー</td>
        <td><a href="https://docs.microsoft.com/legal/windows/agreements/store-policies">Microsoft Store ポリシー</a></td>
    </tr>
    <tr>
        <td>一般的なアプリの認定の問題を回避する方法</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/avoid-common-certification-failures">一般的な認定エラーを回避します。</a></td>
    </tr>
</table>
 

### <a name="store-manifest-storemanifestxml"></a>ストア マニフェスト (StoreManifest.xml)

ストア マニフェスト (StoreManifest.xml) は、必要に応じてアプリ パッケージに含めることのできる構成ファイルです。 ストア マニフェストには、AppxManifest.xml ファイルに含まれていないその他の機能が用意されています。 たとえば、ターゲット デバイスが指定された DirectX の最小機能レベルまたは指定された最小システム メモリの条件を満たしていない場合に、ストア マニフェストを使ってゲームのインストールをブロックできます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ストア マニフェストのスキーマ</td>
        <td><a href="https://docs.microsoft.com/uwp/schemas/storemanifest/storemanifestschema2015/schema-root">StoreManifest スキーマ (Windows 10)</a></td>
    </tr>
</table>
 

## <a name="game-lifecycle-management"></a>ゲームのライフサイクル管理


開発が終了し、ゲームを出荷しても、"ゲーム オーバー" というわけではありません。 バージョン 1 の開発は終了ですが、市場でのゲームの旅は始まったばかりです。 使用状況やエラー レポートの監視、ユーザーからのフィードバックへの対応、ゲームの更新プログラムの公開という作業が必要になります。

### <a name="partner-center-analytics-and-promotion"></a>パートナー センターの分析とプロモーション

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>パートナー センターの分析</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/analytics">アプリのパフォーマンスを分析します。</a></td>
    </tr>
    <tr>
        <td>ゲーム内で Xbox の機能を使用してユーザーを引き付ける方法について説明します。</td>
        <td><a href="../publish/xbox-analytics-report.md">Xbox の分析レポート</a></td>
    </tr>
    <tr>
        <td>顧客のレビューへの返信</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/respond-to-customer-reviews">顧客のレビューに返信する</a></td>
    </tr>
    <tr>
        <td>ゲームの販売を促進する方法</td>
        <td><a href="https://developer.microsoft.com/store/promote-your-apps">アプリの販売促進</a></td>
    </tr>
</table>
 

### <a name="visual-studio-application-insights"></a>Visual Studio Application Insights

Visual Studio Application Insights は、公開されたゲームのパフォーマンス、利用統計情報、および使用状況の分析を提供します。 Application Insights は、リリース後のゲームの問題の検出と解決、使用状況の継続的な監視と向上、プレイヤーがゲームを操作する方法の把握に役立ちます。 Application Insights は、アプリに SDK を追加することで機能し、[Azure ポータル](https://portal.azure.com/)に利用統計情報を送信します。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>アプリケーションのパフォーマンスと使用状況の分析</td>
        <td><a href="https://azure.microsoft.com/documentation/articles/app-insights-get-started/">Visual Studio Application Insights</a></td>
    </tr>
    <tr>
        <td>Windows アプリでの Application Insights の有効化</td>
        <td><a href="https://azure.microsoft.com/documentation/articles/app-insights-windows-get-started/">Windows Phone とストア アプリ用の application Insights</a></td>
    </tr>
</table>


### <a name="third-party-solutions-for-analytics-and-promotion"></a>分析とプロモーションのためのサード パーティ ソリューション

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>GameAnalytics を使用してプレイヤーの動作を理解する</td>
        <td><a href="https://gameanalytics.com/">GameAnalytics</a></td>
    </tr>
    <tr>
        <td>UWP ゲームを Google Analytics に接続する</td>
        <td><a href="https://github.com/dotnet/windows-sdk-for-google-analytics">Google アナリティクスの Windows SDK を取得します。</a></td>
    </tr>
    <tr>
        <td>Google Analytics で Windows SDK を利用する方法 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/Windows/Windows-Developer-Day-Creators-Update/Getting-started-with-the-Windows-SDK-for-Google-Analytics">Google Analytics 用 Windows SDK の概要</a></td>
    </tr>    
    <tr>
        <td>Facebook のアプリ インストール広告を使って Facebook ユーザー向けにゲームのプロモーションを行う</td>
        <td><a href="https://github.com/Microsoft/winsdkfb">Facebook の Windows SDK を取得します。</a></td>
    </tr>
    <tr>
        <td>Facebook のアプリ インストール広告の使用方法 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/Windows/Windows-Developer-Day-Creators-Update/Getting-started-with-Facebook-App-Install-Ads">Facebook for Windows SDK の概要</a></td>
    </tr>
    <tr>
        <td>Vungle を使用してゲームにビデオ広告を追加する</td>
        <td><a href="https://publisher.vungle.com/sdk/">Vungle の Windows SDK を取得します。</a></td>
    </tr>
</table>
 

### <a name="creating-and-managing-content-updates"></a>コンテンツの更新プログラムの作成と管理

公開されたゲームを更新するには、大きいバージョン番号を持つ新しいアプリ パッケージを申請します。 このパッケージの申請と認定が終了すると、自動的にユーザーに更新プログラムとして公開されます。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ゲームの更新とバージョン管理</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/package-version-numbering">パッケージのバージョン番号</a></td>
    </tr>
    <tr>
        <td>ゲームのパッケージ管理のガイダンス</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/publish/package-version-numbering">アプリ パッケージの管理のためのガイダンス</a></td>
    </tr>
</table>


## <a name="adding-xbox-live-to-your-game"></a>ゲームへの Xbox Live の追加

Xbox Live は、世界中の何百万ものゲーマーを結びつける最高のゲーミング ネットワークです。 開発者は、Xbox Live プレゼンス、ランキング、クラウド保存、ゲーム ハブ、クラブ、パーティー チャット、ゲーム DVR など、ゲームの対象ユーザーを組織的に拡大できる Xbox Live の機能にアクセスできます。

> [!Note]
> Xbox Live 対応のタイトルを開発する場合、いくつかのオプションを利用できます。 さまざまなプログラムについて詳しくは、「[開発者プログラムの概要](https://docs.microsoft.com/gaming/xbox-live/developer-program-overview)」をご覧ください。

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>Xbox Live の概要</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/index.md">開発者ガイドの Xbox Live</a></td>
    </tr>
    <tr>
        <td>プログラムによって利用できる機能を理解する</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/developer-program-overview.md#feature-table">開発者向けプログラムの概要:機能テーブル</a></td>
    </tr>
    <tr>
        <td>Xbox Live ゲーム開発に役立つリソースへのリンク</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/xbox-live-resources.md">Xbox Live のリソース</a></td>
    </tr>
    <tr>
        <td>Xbox Live サービスから情報を取得する方法</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/introduction-to-xbox-live-apis.md">Xbox Live Api の概要</a></td>
    </tr>
</table>


### <a name="for-developers-in-the-xbox-live-creators-program"></a>Xbox Live クリエーターズ プログラム開発者向け

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>概要</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-creators/get-started-with-xbox-live-creators.md">Xbox Live クリエーターズ プログラムを概要します。</a></td>
    </tr>
    <tr>
        <td>ゲームへの Xbox Live の追加</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-creators/creators-step-by-step-guide.md">Xbox Live クリエーターズ プログラムを統合するステップ バイ ステップ ガイドします。</a></td>
    </tr>
    <tr>
        <td>Unity を使用して作成された UWP ゲームに Xbox Live を追加する</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-creators/develop-creators-title-with-unity.md">Unity ゲーム エンジンで、Xbox Live クリエーターズ プログラムのタイトルを開発を開始します。</a></td>
    </tr>
    <tr>
        <td>開発サンドボックスをセットアップする</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-creators/xbox-live-sandboxes-creators.md">Xbox Live のサンド ボックスの概要</a></td>
    </tr>
    <tr>
        <td>テスト用のアカウントを設定する</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-creators/authorize-xbox-live-accounts.md">テスト環境で Xbox Live アカウントを承認します。</a></td>
    </tr>
    <tr>
        <td>Xbox Live クリエーターズ プログラム向けサンプル</td>
        <td><a href="https://github.com/Microsoft/xbox-live-samples/tree/master/Samples/CreatorsSDK">クリエーターズ プログラムの開発者向けサンプル コード</a></td>
    </tr>
    <tr>
        <td>クロスプラット フォームの Xbox Live エクスペリエンスを UWP ゲームに統合する方法 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2017/GDC2017-005">Xbox Live クリエーターズ プログラム</a></td>
    </tr>  
</table>

### <a name="for-managed-partners-and-developers-in-the-idxbox-program"></a>対象パートナーおよび ID@Xbox プログラムの開発者向け

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>概要</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-partner/get-started-with-xbox-live-partner.md">管理対象のパートナーや、ID 開発者として Xbox Live の概要します。</a></td>
    </tr>
    <tr>
        <td>ゲームへの Xbox Live の追加</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-partner/partners-step-by-step-guide.md">管理対象のパートナーと ID のメンバーの Xbox Live を統合するステップ バイ ステップ ガイドします。</a></td>
    </tr>
    <tr>
        <td>Unity を使用して作成された UWP ゲームに Xbox Live を追加する</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-partner/partner-unity-uwp-il2cpp.md">Xbox Live にサポートを追加 Unity for UWP il2cpp バック エンド スクリプト バックエンドでの ID と管理対象のパートナー</a></td>
    </tr>
    <tr>
        <td>開発サンドボックスをセットアップする</td>
        <td><a href="https://docs.microsoft.com/gaming/xbox-live/get-started-with-partner/advanced-xbox-live-sandboxes.md">高度な Xbox Live のサンド ボックス</a></td>
    </tr>
    <tr>
        <td>Xbox Live を使うためのゲームの要件 (GDN)</td>
        <td><a href="https://go.microsoft.com/fwlink/?LinkId=533217">Windows 10 の Xbox の Xbox 要件が Live します。</a></td>
    </tr>
    <tr>
        <td>サンプル</td>
        <td><a href="https://github.com/Microsoft/xbox-live-samples/tree/master/Samples/ID%40XboxSDK">コード サンプルID@Xbox開発者</a></td>
    </tr>  
    <tr>
        <td>Xbox Live のゲーム開発の概要 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Developing-with-Xbox-Live-for-Windows-10">Windows 10 向け Live Xbox を使用した開発</a></td>
    </tr>
    <tr>
        <td>クロス プラットフォーム マッチメイキング (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Xbox-Live-Multiplayer-Introducing-services-for-cross-platform-matchmaking-and-gameplay">Xbox Live マルチプレイヤー:クロス プラットフォームのマッチメイ キングとゲームプレイのサービスの概要</a></td>
    </tr>
    <tr>
        <td>Fable Legends でのクロス デバイスのゲームプレイ (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Fable-Legends-Cross-device-Gameplay-with-Xbox-Live">Fable 凡例:クロス デバイス ゲームプレイ xbox Live します。</a></td>
    </tr>
    <tr>
        <td>Xbox Live の統計情報や達成度 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Best-Practices-for-Leveraging-Cloud-Based-User-Stats-and-Achievements-in-Xbox-Live">クラウド ベースのユーザーの統計を利用するためのベスト プラクティスし、アチーブメントで Xbox Live</a></td>
    </tr>
</table>


## <a name="additional-resources"></a>その他の資料

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <tr>
        <td>ゲーム開発ビデオ</td>
        <td><a href="https://docs.microsoft.com/windows/uwp/gaming/game-development-videos">GDC//build などの主要なカンファレンスのビデオ</a></td>
    </tr>
    <tr>
        <td>インディーズ ゲーム開発 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/New-Opportunities-for-Independent-Developers">個人開発者に新しい機会</a></td>
    </tr>
    <tr>
        <td>マルチコア モバイル デバイスに関する考慮事項 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/Sustained-gaming-performance-in-multi-core-mobile-devices">マルチコアのモバイル デバイスで持続的なゲームのパフォーマンス</a></td>
    </tr>
    <tr>
        <td>Windows 10 デスクトップ ゲームの開発 (ビデオ)</td>
        <td><a href="https://channel9.msdn.com/Events/GDC/GDC-2015/PC-Games-for-Windows-10">Windows 10 の PC ゲーム</a></td>
    </tr>
</table>



 

 

 
