---
title: 設定
description: グラフィックスを表示するレンダリング パイプラインをアセンブルする方法について説明します。 ゲームのレンダリング、データのセットアップと準備。
ms.assetid: 7720ac98-9662-4cf3-89c5-7ff81896364a
ms.date: 10/24/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, レンダリング
ms.localizationpriority: medium
ms.openlocfilehash: a87382aeffb0e0b7a8eaca1c4baec8561049e91e
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89168246"
---
# <a name="rendering-framework-ii-game-rendering"></a>レンダリング フレームワーク II: ゲームのレンダリング

> [!NOTE]
> このトピックは、「DirectX チュートリアルシリーズ [を含む simple ユニバーサル Windows プラットフォーム (UWP) ゲームの作成](tutorial--create-your-first-uwp-directx-game.md) 」に含まれています。 このリンクのトピックでは、系列のコンテキストを設定します。

「[レンダリング フレームワーク I](tutorial--assembling-the-rendering-pipeline.md)」では、シーン情報を取得し、ディスプレイの画面に表示する方法を説明しました。 ここでは、一歩戻って、レンダリングのためのデータを準備する方法について説明します。

>[!Note]
>このサンプルの最新のゲームコードをダウンロードしていない場合は、「 [Direct3D サンプルゲーム](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/Simple3DGameDX)」にアクセスしてください。 このサンプルは、UWP 機能のサンプルの大規模なコレクションの一部です。 サンプルをダウンロードする手順については、「[GitHub から UWP のサンプルを取得する](../get-started/get-app-samples.md)」をご覧ください。

## <a name="objective"></a>目的

目標について簡単に要約します。 基本的なレンダリング フレームワークを設定して、UWP DirectX ゲームのグラフィックス出力を表示する方法を理解することです。 これらはおおまかに 3 つの手順にグループ分けすることができます。

 1. グラフィックス インターフェイスへの接続を確立する
 2. 準備: グラフィックスを描画するために必要なリソースを作成する
 3. グラフィックの表示: フレームをレンダリングする

「[レンダリング フレームワーク I: レンダリングの概要](tutorial--assembling-the-rendering-pipeline.md)」では、手順 1 と 3 を含む、グラフィックスをレンダリングする方法について説明しました。 

この記事では、このフレームワークの他の部分を設定し、レンダリングの前に必要なデータを準備する方法 (プロセスの手順 2 に相当) について説明します。

## <a name="design-the-renderer"></a>レンダラーの設計

レンダラーは、ゲームの視覚効果を生成するために使用する、すべての D3D11 オブジェクトと D2D オブジェクトの作成と保守を担当します。 __GameRenderer__ クラスは、このサンプル ゲームのレンダラーであり、し、ゲームのレンダリングのニーズに合わせて設計されています。

ゲームのレンダラーを設計する際に役立ついくつかの概念を以下に示します。
* Direct3D 11 API は [COM](/windows/desktop/com/the-component-object-model) API として定義されるため、これらの API で定義されたオブジェクトへの [ComPtr](/cpp/windows/comptr-class) 参照を指定する必要があります。 これらのオブジェクトは、アプリ終了時に最後の参照がスコープ外になったときに自動的に解放されます。 詳細については、「[ComPtr](https://github.com/Microsoft/DirectXTK/wiki/ComPtr)」を参照してください。 このようなオブジェクトの例として、定数バッファー、シェーダー オブジェクト ([頂点シェーダー](tutorial--assembling-the-rendering-pipeline.md#vertex-shaders-and-pixel-shaders)、[ピクセル シェーダー](tutorial--assembling-the-rendering-pipeline.md#vertex-shaders-and-pixel-shaders))、シェーダー リソース オブジェクトがあります。
* 定数バッファーは、レンダリングに必要なさまざまなデータを保持するために、このクラスで定義されます。
    * GPU に送信するデータの 1 フレームあたりの量を減らすために、更新頻度の異なる複数の定数バッファーを使用します。 このサンプルでは、更新する必要のある頻度に基づいて定数を異なるバッファーに分けています。 Direct3D プログラミングでは、このような処理をお勧めします。 
    * このサンプルゲームでは、4つの定数バッファーが定義されています。
        1. __m \_ constantBufferNeverChanges__ には、光源のパラメーターが含まれています。 これは、__FinalizeCreateGameDeviceResources__ メソッドで一度設定されると、再び変更されることはありません。
        2. __m \_ constantBufferChangeOnResize__ は、射影行列を含みます。 プロジェクション マトリックスは、ウィンドウのサイズと縦横比に依存します。 これは、[__CreateWindowSizeDependentResources__](#createwindowsizedependentresource-method) で設定され、[__FinalizeCreateGameDeviceResources__](#finalizecreategamedeviceresources-method) メソッドでリソースが読み込まれた後で更新されます。 3D でレンダリングする場合は、フレームごとに 2 回変更されます。
        3. __m \_ constantBufferChangesEveryFrame__ には、ビュー行列が含まれています。 このマトリックスは、カメラ位置とルック方向 (標準はプロジェクション方向) に依存し、__Render__ メソッドで 1 フレームあたり 1 回変更されます。 これについては、「__レンダリング フレームワーク I: レンダリングの概要__」の「[__GameRenderer::Render__ メソッド](tutorial--assembling-the-rendering-pipeline.md#gamerendererrender-method)」で既に説明しました。
        4. __m \_ constantBufferChangesEveryPrim__ には、各プリミティブのモデルマトリックスと素材のプロパティが含まれています。 モデル マトリックスは、頂点をローカル座標からワールド座標に変換します。 これらの定数は各プリミティブに固有で、描画呼び出しのたびに更新されます。 これについては、「__レンダリング フレームワーク I: レンダリングの概要__」の「[プリミティブのレンダリング](tutorial--assembling-the-rendering-pipeline.md#primitive-rendering)」で既に説明しました。
* プリミティブのテクスチャを保持するシェーダー リソース オブジェクトも、このクラスで定義されます。
    * 一部のテクスチャは事前に定義されています ([DDS](/windows/desktop/direct3ddds/dx-graphics-dds-pguide) は、圧縮および非圧縮テクスチャを格納するために使用されるファイル形式です。 DDS テクスチャは、ワールドの壁や床、弾薬の球体に使用されます)。
    * このサンプルゲームでは、シェーダーリソースオブジェクトは __m \_ sphereTexture__、 __m \_ cylinderTexture__、 __m \_ ceilingTexture__、 __m \_ floorTexture__、 __m \_ wallsTexture__です。
* シェーダー オブジェクトは、プリミティブやテクスチャを計算するために、このクラスで定義されます。 
    * このサンプルゲームでは、シェーダーオブジェクトは __m \_ vertexshader__、 __m \_ vertexShaderFlat__、 __m \_ pixelShader__、 __m \_ pixelShaderFlat__です。
    * 頂点シェーダーはプリミティブと基本的な照明を処理し、ピクセル シェーダー (フラグメント シェーダーとも呼ばれます) はテクスチャとピクセルごとの効果を処理します。
    * これらのシェーダーには、異なるプリミティブをレンダリングするための 2 つのバージョン (標準とフラット) があります。 異なるバージョンを用意しているでは、フラット バージョンは、標準と比べるときわめて単純であり、鏡面ハイライトやピクセル単位の照明効果が一切実行されないためです。 壁に使われ、低電力デバイスでレンダリングを高速化します。

## <a name="gamerendererh"></a>GameRenderer.h

次に、サンプルゲームのレンダラークラスオブジェクトのコードを見てみましょう。

```cppwinrt
// Class handling the rendering of the game
class GameRenderer : public std::enable_shared_from_this<GameRenderer>
{
public:
    GameRenderer(std::shared_ptr<DX::DeviceResources> const& deviceResources);

    void CreateDeviceDependentResources();
    void CreateWindowSizeDependentResources();
    void ReleaseDeviceDependentResources();
    void Render();
    // --- end of async related methods section

    winrt::Windows::Foundation::IAsyncAction CreateGameDeviceResourcesAsync(_In_ std::shared_ptr<Simple3DGame> game);
    void FinalizeCreateGameDeviceResources();
    winrt::Windows::Foundation::IAsyncAction LoadLevelResourcesAsync();
    void FinalizeLoadLevelResources();

    Simple3DGameDX::IGameUIControl* GameUIControl() { return &m_gameInfoOverlay; };

    DirectX::XMFLOAT2 GameInfoOverlayUpperLeft()
    {
        return DirectX::XMFLOAT2(m_gameInfoOverlayRect.left, m_gameInfoOverlayRect.top);
    };
    DirectX::XMFLOAT2 GameInfoOverlayLowerRight()
    {
        return DirectX::XMFLOAT2(m_gameInfoOverlayRect.right, m_gameInfoOverlayRect.bottom);
    };
    bool GameInfoOverlayVisible() { return m_gameInfoOverlay.Visible(); }
    // --- end of rendering overlay section
...
private:
    // Cached pointer to device resources.
    std::shared_ptr<DX::DeviceResources>        m_deviceResources;

    ...

    // Shader resource objects
    winrt::com_ptr<ID3D11ShaderResourceView>    m_sphereTexture;
    winrt::com_ptr<ID3D11ShaderResourceView>    m_cylinderTexture;
    winrt::com_ptr<ID3D11ShaderResourceView>    m_ceilingTexture;
    winrt::com_ptr<ID3D11ShaderResourceView>    m_floorTexture;
    winrt::com_ptr<ID3D11ShaderResourceView>    m_wallsTexture;

    // Constant buffers
    winrt::com_ptr<ID3D11Buffer>                m_constantBufferNeverChanges;
    winrt::com_ptr<ID3D11Buffer>                m_constantBufferChangeOnResize;
    winrt::com_ptr<ID3D11Buffer>                m_constantBufferChangesEveryFrame;
    winrt::com_ptr<ID3D11Buffer>                m_constantBufferChangesEveryPrim;

    // Texture sampler
    winrt::com_ptr<ID3D11SamplerState>          m_samplerLinear;

    // Shader objects: Vertex shaders and pixel shaders
    winrt::com_ptr<ID3D11VertexShader>          m_vertexShader;
    winrt::com_ptr<ID3D11VertexShader>          m_vertexShaderFlat;
    winrt::com_ptr<ID3D11PixelShader>           m_pixelShader;
    winrt::com_ptr<ID3D11PixelShader>           m_pixelShaderFlat;
    winrt::com_ptr<ID3D11InputLayout>           m_vertexLayout;
};
```

## <a name="constructor"></a>コンストラクター

次に、サンプルゲームの __GameRenderer__ コンストラクターを調べて、DirectX 11 アプリケーションテンプレートで提供されている __Sample3DSceneRenderer__ コンストラクターと比較してみましょう。

```cppwinrt
// Constructor method of the main rendering class object
GameRenderer::GameRenderer(std::shared_ptr<DX::DeviceResources> const& deviceResources) : ...
    m_gameInfoOverlay(deviceResources),
    m_gameHud(deviceResources, L"Windows platform samples", L"DirectX first-person game sample")
{
    // m_gameInfoOverlay is a GameHud object to render text in the top left corner of the screen.
    // m_gameHud is Game info rendered as an overlay on the top-right corner of the screen,
    // for example hits, shots, and time.

    CreateDeviceDependentResources();
    CreateWindowSizeDependentResources();
}
```

## <a name="create-and-load-directx-graphic-resources"></a>DirectX グラフィックス リソースの作成と読み込み

サンプルゲーム (および Visual Studio の __DirectX 11 アプリ (ユニバーサル Windows)__ テンプレート) では、 __GameRenderer__ コンストラクターから呼び出される次の2つのメソッドを使用して、ゲームリソースの作成と読み込みが実装されます。

* [__CreateDeviceDependentResources__](#createdevicedependentresources-method)
* [__CreateWindowSizeDependentResources__](#createwindowsizedependentresource-method)

## <a name="createdevicedependentresources-method"></a>CreateDeviceDependentResources メソッド

DirectX 11 アプリ テンプレートでは、このメソッドを使用して、頂点シェーダーとピクセル シェーダーの非道敵的な読み込み、シェーダーと定数バッファーの作成、位置と色の情報を含む頂点を持つメッシュの作成が行われます。 

サンプル ゲームでは、シーン オブジェクトのこれらの操作は、[__CreateGameDeviceResourcesAsync__](#creategamedeviceresourcesasync-method) メソッドと [__FinalizeCreateGameDeviceResources__](#finalizecreategamedeviceresources-method) メソッドに分割されています。 

このサンプルゲームでは、この方法について説明します。

* レンダリングに進む前にリソースが読み込まれているかどうかを示す、インスタンス化された変数 (__m \_ gameResourcesLoaded__ = false および __m \_ levelresourcesloaded__ = false)。これは、それらを非同期に読み込むためです。 
* HUD とオーバーレイのレンダリングは別のクラスのオブジェクトで行われるため、ここでは __GameHud::CreateDeviceDependentResources__ メソッドと __GameInfoOverlay::CreateDeviceDependentResources__ メソッドを呼び出します。

__GameRenderer::CreateDeviceDependentResources__ のコードは次のとおりです。

```cppwinrt
// This method is called in GameRenderer constructor when it's created in GameMain constructor.
void GameRenderer::CreateDeviceDependentResources()
{
    // instantiate variables that indicate whether resources were loaded.
    m_gameResourcesLoaded = false;
    m_levelResourcesLoaded = false;

    // game HUD and overlay are design as separate class objects.
    m_gameHud.CreateDeviceDependentResources();
    m_gameInfoOverlay.CreateDeviceDependentResources();
}
```

リソースの作成と読み込みに使用されるメソッドの一覧を次に示します。

- CreateDeviceDependentResources
  - CreateGameDeviceResourcesAsync (追加)
  - FinalizeCreateGameDeviceResources (追加)
- CreateWindowSizeDependentResources

リソースの作成と読み込みに使用される他のメソッドについて解説する前に、まずレンダラーを作成し、ゲーム ループに適していることを確認してみましょう。

## <a name="create-the-renderer"></a>レンダラーの作成

__GameRenderer__ は __GameMain__ のコンストラクターで作成されます。 また、リソースの作成と読み込みのために追加された、他の 2 つメソッド [__CreateGameDeviceResourcesAsync__](#creategamedeviceresourcesasync-method) と [__FinalizeCreateGameDeviceResources__](#finalizecreategamedeviceresources-method) も呼び出します。

```cppwinrt
GameMain::GameMain(std::shared_ptr<DX::DeviceResources> const& deviceResources) : ...
{
    m_deviceResources->RegisterDeviceNotify(this);

    // Creation of GameRenderer
    m_renderer = std::make_shared<GameRenderer>(m_deviceResources);

    ...

    ConstructInBackground();
}

winrt::fire_and_forget GameMain::ConstructInBackground()
{
    ...

    // Asynchronously initialize the game class and load the renderer device resources.
    // By doing all this asynchronously, the game gets to its main loop more quickly
    // and in parallel all the necessary resources are loaded on other threads.
    m_game->Initialize(m_controller, m_renderer);

    co_await m_renderer->CreateGameDeviceResourcesAsync(m_game);

    // The finalize code needs to run in the same thread context
    // as the m_renderer object was created because the D3D device context
    // can ONLY be accessed on a single thread.
    // co_await of an IAsyncAction resumes in the same thread context.
    m_renderer->FinalizeCreateGameDeviceResources();

    InitializeGameState();

    ...
}
```

## <a name="creategamedeviceresourcesasync-method"></a>CreateGameDeviceResourcesAsync メソッド

__CreateGameDeviceResourcesAsync__は、ゲームリソースを非同期的に読み込むため、 __create \_ task__ループの__GameMain__ constructor メソッドから呼び出されます。
        
__CreateDeviceResourcesAsync__ は、ゲームのリソースを読み込むための一連の非同期タスクとして別個に実行されるメソッドです。 個別のスレッドで実行されると想定されるので、Direct3D 11 デバイス メソッド (__ID3D11Device__ で定義されているメソッド) にのみアクセスでき、デバイス コンテキスト メソッド (__ID3D11DeviceContext__ で定義されているメソッド) にはアクセスできないため、レンダリングは実行されません。

__FinalizeCreateGameDeviceResources__ メソッドはメイン スレッドで実行され、Direct3D 11 デバイス コンテキスト メソッドにアクセスできます。

原則は次のとおりです。
* __CreateGameDeviceResourcesAsync__ では __ID3D11Device__ のメソッドのみを使用します。これは、フリー スレッド化されている (任意のスレッドで実行できることを意味する) ためです。 また、__GameRenderer__ が作成されたスレッドと同じスレッドでは実行されないことも想定されています。 
* 1 つのスレッドで実行する必要があり、かつ __GameRenderer__ と同じスレッドで実行する必要があるため、ここでは __ID3D11DeviceContext__ のスレッドを使用しないでください。
* 定数バッファーを作成するには、このメソッドを使用します。
* テクスチャ (.dds ファイルなど) やシェーダー情報 (.cso ファイルなど) を、[シェーダー](tutorial--assembling-the-rendering-pipeline.md#shaders)に読み込むには、このメソッドを使用します。

このメソッドを使用して、次の処理を行います。
* 4つの[定数バッファー](tutorial--assembling-the-rendering-pipeline.md#buffer)( __m \_ constantBufferNeverChanges__、 __m \_ constantBufferChangeOnResize__、 __m \_ constantBufferChangesEveryFrame__、 __m \_ constantBufferChangesEveryPrim__ ) を作成します。
* テクスチャーのサンプリング情報をカプセル化する[サンプラー ステート](tutorial--assembling-the-rendering-pipeline.md#sampler-state) オブジェクトを作成します。
* メソッドで作成されたすべての非同期タスクを含むタスク グループを作成します。 メソッドは、これらすべての非同期タスクが完了するまで待機してから __FinalizeCreateGameDeviceResources__ を呼び出します。
* [Basic Loader](tutorial--assembling-the-rendering-pipeline.md#the-basicloader-class) を使用してローダーを作成します。 前の手順で作成したタスク グループに、ローダーの非同期読み込み操作をタスクとして追加します。
* __BasicLoader::LoadShaderAsync__ や __BasicLoader::LoadTextureAsync__ などのメソッドは、以下を読み込むために使用されます。
    * コンパイル済みのシェーダー オブジェクト (VertextShader.cso、VertexShaderFlat.cso、PixelShader.cso、PixelShaderFlat.cso)。 詳細については、「[さまざまなシェーダー ファイル形式](tutorial--assembling-the-rendering-pipeline.md#various-shader-file-formats)」を参照してください。
    * ゲーム固有のテクスチャ (asset seafloor、metal_texture. dds、cellceiling、、cellceiling、および、 \\ )。

```cppwinrt
IAsyncAction GameRenderer::CreateGameDeviceResourcesAsync(_In_ std::shared_ptr<Simple3DGame> game)
{
    auto lifetime = shared_from_this();

    // Create the device dependent game resources.
    // Only the d3dDevice is used in this method. It is expected
    // to not run on the same thread as the GameRenderer was created.
    // Create methods on the d3dDevice are free-threaded and are safe while any methods
    // in the d3dContext should only be used on a single thread and handled
    // in the FinalizeCreateGameDeviceResources method.
    m_game = game;

    auto d3dDevice = m_deviceResources->GetD3DDevice();

    // Define D3D11_BUFFER_DESC. See
    // https://docs.microsoft.com/windows/win32/api/d3d11/ns-d3d11-d3d11_buffer_desc
    D3D11_BUFFER_DESC bd;
    ZeroMemory(&bd, sizeof(bd));

    // Create the constant buffers.
    bd.Usage = D3D11_USAGE_DEFAULT;
    ...

    // Create the constant buffers: m_constantBufferNeverChanges, m_constantBufferChangeOnResize,
    // m_constantBufferChangesEveryFrame, m_constantBufferChangesEveryPrim
    // CreateBuffer is used to create one of these buffers: vertex buffer, index buffer, or 
    // shader-constant buffer. For CreateBuffer API ref info, see
    // https://docs.microsoft.com/windows/win32/api/d3d11/nf-d3d11-id3d11device-createbuffer.
    winrt::check_hresult(
        d3dDevice->CreateBuffer(&bd, nullptr, m_constantBufferNeverChanges.put())
        );

    ...

    // Define D3D11_SAMPLER_DESC. For API ref, see
    // https://docs.microsoft.com/windows/win32/api/d3d11/ns-d3d11-d3d11_sampler_desc.
    D3D11_SAMPLER_DESC sampDesc;

    // ZeroMemory fills a block of memory with zeros. For API ref, see
    // https://docs.microsoft.com/previous-versions/windows/desktop/legacy/aa366920(v=vs.85).
    ZeroMemory(&sampDesc, sizeof(sampDesc));

    sampDesc.Filter = D3D11_FILTER_MIN_MAG_MIP_LINEAR;
    sampDesc.AddressU = D3D11_TEXTURE_ADDRESS_WRAP;
    sampDesc.AddressV = D3D11_TEXTURE_ADDRESS_WRAP;
    ...

    // Create a sampler-state object that encapsulates sampling information for a texture.
    // The sampler-state interface holds a description for sampler state that you can bind to any 
    // shader stage of the pipeline for reference by texture sample operations.
    winrt::check_hresult(
        d3dDevice->CreateSamplerState(&sampDesc, m_samplerLinear.put())
        );

    // Start the async tasks to load the shaders and textures.

    // Load compiled shader objects (VertextShader.cso, VertexShaderFlat.cso, PixelShader.cso, and PixelShaderFlat.cso).
    // The BasicLoader class is used to convert and load common graphics resources, such as meshes, textures, 
    // and various shader objects into the constant buffers. For more info, see
    // https://docs.microsoft.com/windows/uwp/gaming/complete-code-for-basicloader.
    BasicLoader loader{ d3dDevice };

    std::vector<IAsyncAction> tasks;

    uint32_t numElements = ARRAYSIZE(PNTVertexLayout);

    // Load shaders asynchronously with the shader and pixel data using the
    // BasicLoader::LoadShaderAsync method. Push these method calls into a list of tasks.
    tasks.push_back(loader.LoadShaderAsync(L"VertexShader.cso", PNTVertexLayout, numElements, m_vertexShader.put(), m_vertexLayout.put()));
    tasks.push_back(loader.LoadShaderAsync(L"VertexShaderFlat.cso", nullptr, numElements, m_vertexShaderFlat.put(), nullptr));
    tasks.push_back(loader.LoadShaderAsync(L"PixelShader.cso", m_pixelShader.put()));
    tasks.push_back(loader.LoadShaderAsync(L"PixelShaderFlat.cso", m_pixelShaderFlat.put()));

    // Make sure the previous versions if any of the textures are released.
    m_sphereTexture = nullptr;
    ...

    // Load Game specific textures (Assets\\seafloor.dds, metal_texture.dds, cellceiling.dds,
    // cellfloor.dds, cellwall.dds).
    // Push these method calls also into a list of tasks.
    tasks.push_back(loader.LoadTextureAsync(L"Assets\\seafloor.dds", nullptr, m_sphereTexture.put()));
    ...

    // Simulate loading additional resources by introducing a delay.
    tasks.push_back([]() -> IAsyncAction { co_await winrt::resume_after(GameConstants::InitialLoadingDelay); }());

    // Returns when all the async tasks for loading the shader and texture assets have completed.
    for (auto&& task : tasks)
    {
        co_await task;
    }
}
```

## <a name="finalizecreategamedeviceresources-method"></a>FinalizeCreateGameDeviceResources メソッド

__FinalizeCreateGameDeviceResources__メソッドは、__CreateGameDeviceResourcesAsync__メソッド内のすべてのリソース読み込みタスクが完了した後で呼び出されます。 

* ライトの位置と色を使用して constantBufferNeverChanges を初期化します。 デバイス コンテキスト メソッド __ID3D11DeviceContext::UpdateSubresource__ の呼び出しによって、最初のデータを定数バッファーに読み込みます。
* 非同期的に読み込まれるリソースの読み込みが完了したら、適切なゲーム オブジェクトに関連付けます。
* ゲーム オブジェクトごとに、読み込まれたテクスチャを使用して、メッシュとマテリアルを作成します。 次に、メッシュとマテリアルをゲーム オブジェクトに関連付けます。
* ターゲットのゲーム オブジェクトの場合、同心円の色付きのリングとその上の数値で構成されるテクスチャは、テクスチャー ファイルからは読み込まれません。 代わりに、__TargetTexture.cpp__ 内のコードを使用して手続き的に生成されます。 __TargetTexture__ クラスは、初期化時にオフスクリーン リソースにテクスチャを描画するために必要なリソースを作成します。 生成されたテクスチャは、適切なターゲット ゲーム オブジェクトに関連付けられます。

__FinalizeCreateGameDeviceResources__ と [__CreateWindowSizeDependentResources__](#createwindowsizedependentresource-method) は、以下について、コードの同様の部分を共有します。
* __SetProjParams__ を使用して、カメラのプロジェクション マトリックスが適切になるように設定します。 詳しくは、「[カメラと座標空間](tutorial--assembling-the-rendering-pipeline.md#camera-and-coordinate-space)」をご覧ください。
* カメラのプロジェクション マトリックスに 3D 回転マトリックスを乗算することにより、画面の向きを処理します。 結果として得られるプロジェクション マトリックスを使って、__ConstantBufferChangeOnResize__ 定数バッファーを更新します。
* __M \_ gameResourcesLoaded__ __Boolean__グローバル変数を設定して、リソースがバッファーに読み込まれ、次の手順の準備ができたことを示します。 最初に __GameRenderer__ のコンストラクター メソッドで、__GameRenderer::CreateDeviceDependentResources__ メソッドを使用して、この変数を __FALSE__ として初期化したことを思い出してください。 
* この __m \_ GameResourcesLoaded__ が __TRUE__の場合、シーンオブジェクトのレンダリングを実行できます。 これについては、「__レンダリング フレームワーク I: レンダリングの概要__」の「[__GameRenderer::Render メソッド__](tutorial--assembling-the-rendering-pipeline.md#gamerendererrender-method)」で説明しました。

```cppwinrt
// This method is called from the GameMain constructor.
// Make sure that 2D rendering is occurring on the same thread as the main rendering.
void GameRenderer::FinalizeCreateGameDeviceResources()
{
    // All asynchronously loaded resources have completed loading.
    // Now associate all the resources with the appropriate game objects.
    // This method is expected to run in the same thread as the GameRenderer
    // was created. All work will happen behind the "Loading ..." screen after the
    // main loop has been entered.

    // Initialize the Constant buffer with the light positions
    // These are handled here to ensure that the d3dContext is only
    // used in one thread.

    auto d3dDevice = m_deviceResources->GetD3DDevice();

    ConstantBufferNeverChanges constantBufferNeverChanges;
    constantBufferNeverChanges.lightPosition[0] = XMFLOAT4(3.5f, 2.5f, 5.5f, 1.0f);
    ...
    constantBufferNeverChanges.lightColor = XMFLOAT4(0.25f, 0.25f, 0.25f, 1.0f);

    // CPU copies data from memory (constantBufferNeverChanges) to a subresource 
    // created in non-mappable memory (m_constantBufferNeverChanges) which was created in the earlier 
    // CreateGameDeviceResourcesAsync method. For UpdateSubresource API ref info, 
    // go to: https://msdn.microsoft.com/library/windows/desktop/ff476486.aspx
    // To learn more about what a subresource is, go to:
    // https://msdn.microsoft.com/library/windows/desktop/ff476901.aspx

    m_deviceResources->GetD3DDeviceContext()->UpdateSubresource(
        m_constantBufferNeverChanges.get(),
        0,
        nullptr,
        &constantBufferNeverChanges,
        0,
        0
        );

    // For the objects that function as targets, they have two unique generated textures.
    // One version is used to show that they have never been hit and the other is 
    // used to show that they have been hit.
    // TargetTexture is a helper class to procedurally generate textures for game
    // targets. The class creates the necessary resources to draw the texture into 
    // an off screen resource at initialization time.

    TargetTexture textureGenerator(
        d3dDevice,
        m_deviceResources->GetD2DFactory(),
        m_deviceResources->GetDWriteFactory(),
        m_deviceResources->GetD2DDeviceContext()
        );

    // CylinderMesh is a class derived from MeshObject and creates a ID3D11Buffer of
    // vertices and indices to represent a canonical cylinder (capped at
    // both ends) that is positioned at the origin with a radius of 1.0,
    // a height of 1.0 and with its axis in the +Z direction.
    // In the game sample, there are various types of mesh types:
    // CylinderMesh (vertical rods), SphereMesh (balls that the player shoots), 
    // FaceMesh (target objects), and WorldMesh (Floors and ceilings that define the enclosed area)

    auto cylinderMesh = std::make_shared<CylinderMesh>(d3dDevice, (uint16_t)26);
    ...

    // The Material class maintains the properties that represent how an object will
    // look when it is rendered.  This includes the color of the object, the
    // texture used to render the object, and the vertex and pixel shader that
    // should be used for rendering.

    auto cylinderMaterial = std::make_shared<Material>(
        XMFLOAT4(0.8f, 0.8f, 0.8f, .5f),
        XMFLOAT4(0.8f, 0.8f, 0.8f, .5f),
        XMFLOAT4(1.0f, 1.0f, 1.0f, 1.0f),
        15.0f,
        m_cylinderTexture.get(),
        m_vertexShader.get(),
        m_pixelShader.get()
        );

    ...

    // Attach the textures to the appropriate game objects.
    // We'll loop through all the objects that need to be rendered.
    for (auto&& object : m_game->RenderObjects())
    {
        if (object->TargetId() == GameConstants::WorldFloorId)
        {
            // Assign a normal material for the floor object.
            // This normal material uses the floor texture (cellfloor.dds) that was loaded asynchronously from
            // the Assets folder using BasicLoader::LoadTextureAsync method in the earlier 
            // CreateGameDeviceResourcesAsync loop

            object->NormalMaterial(
                std::make_shared<Material>(
                    XMFLOAT4(0.5f, 0.5f, 0.5f, 1.0f),
                    XMFLOAT4(0.8f, 0.8f, 0.8f, 1.0f),
                    XMFLOAT4(0.3f, 0.3f, 0.3f, 1.0f),
                    150.0f,
                    m_floorTexture.get(),
                    m_vertexShaderFlat.get(),
                    m_pixelShaderFlat.get()
                    )
                );
            // Creates a mesh object called WorldFloorMesh and assign it to the floor object.
            object->Mesh(std::make_shared<WorldFloorMesh>(d3dDevice));
        }
        ...
        else if (auto cylinder = dynamic_cast<Cylinder*>(object.get()))
        {
            cylinder->Mesh(cylinderMesh);
            cylinder->NormalMaterial(cylinderMaterial);
        }
        else if (auto target = dynamic_cast<Face*>(object.get()))
        {
            const int bufferLength = 16;
            wchar_t str[bufferLength];
            int len = swprintf_s(str, bufferLength, L"%d", target->TargetId());
            auto string{ winrt::hstring(str, len) };

            winrt::com_ptr<ID3D11ShaderResourceView> texture;
            textureGenerator.CreateTextureResourceView(string, texture.put());
            target->NormalMaterial(
                std::make_shared<Material>(
                    XMFLOAT4(0.8f, 0.8f, 0.8f, 0.5f),
                    XMFLOAT4(0.8f, 0.8f, 0.8f, 0.5f),
                    XMFLOAT4(0.3f, 0.3f, 0.3f, 1.0f),
                    5.0f,
                    texture.get(),
                    m_vertexShader.get(),
                    m_pixelShader.get()
                    )
                );

            texture = nullptr;
            textureGenerator.CreateHitTextureResourceView(string, texture.put());
            target->HitMaterial(
                std::make_shared<Material>(
                    XMFLOAT4(0.8f, 0.8f, 0.8f, 0.5f),
                    XMFLOAT4(0.8f, 0.8f, 0.8f, 0.5f),
                    XMFLOAT4(0.3f, 0.3f, 0.3f, 1.0f),
                    5.0f,
                    texture.get(),
                    m_vertexShader.get(),
                    m_pixelShader.get()
                    )
                );

            target->Mesh(targetMesh);
        }
        ...
    }

    // The SetProjParams method calculates the projection matrix based on input params and
    // ensures that the camera has been initialized with the right projection
    // matrix.  
    // The camera is not created at the time the first window resize event occurs.

    auto renderTargetSize = m_deviceResources->GetRenderTargetSize();
    m_game->GameCamera().SetProjParams(
        XM_PI / 2,
        renderTargetSize.Width / renderTargetSize.Height,
        0.01f,
        100.0f
        );

    // Make sure that the correct projection matrix is set in the ConstantBufferChangeOnResize buffer.

    // Get the 3D rotation transform matrix. We are handling screen rotations directly to eliminate an unaligned 
    // fullscreen copy. So it is necessary to post multiply the 3D rotation matrix to the camera's projection matrix
    // to get the projection matrix that we need.

    auto orientation = m_deviceResources->GetOrientationTransform3D();

    ConstantBufferChangeOnResize changesOnResize;

    // The matrices are transposed due to the shader code expecting the matrices in the opposite
    // row/column order from the DirectX math library.

    // XMStoreFloat4x4 takes a matrix and writes the components out to sixteen single-precision floating-point values at the given address. 
    // The most significant component of the first row vector is written to the first four bytes of the address, 
    // followed by the second most significant component of the first row, and so on. The second row is then written out in a 
    // like manner to memory beginning at byte 16, followed by the third row to memory beginning at byte 32, and finally 
    // the fourth row to memory beginning at byte 48. For more API ref info, go to: 
    // https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.storing.xmstorefloat4x4.aspx

    XMStoreFloat4x4(
        &changesOnResize.projection,
        XMMatrixMultiply(
            XMMatrixTranspose(m_game->GameCamera().Projection()),
            XMMatrixTranspose(XMLoadFloat4x4(&orientation))
            )
        );

    // UpdateSubresource method instructs CPU to copy data from memory (changesOnResize) to a subresource 
    // created in non-mappable memory (m_constantBufferChangeOnResize ) which was created in the earlier 
    // CreateGameDeviceResourcesAsync method.

    m_deviceResources->GetD3DDeviceContext()->UpdateSubresource(
        m_constantBufferChangeOnResize.get(),
        0,
        nullptr,
        &changesOnResize,
        0,
        0
        );

    // Finally we set the m_gameResourcesLoaded as TRUE, so we can start rendering.
    m_gameResourcesLoaded = true;
}
```

## <a name="createwindowsizedependentresource-method"></a>CreateWindowSizeDependentResource メソッド

CreateWindowSizeDependentResources メソッドは、ウィンドウのサイズ、向き、ステレオに対応したレンダリング、解像度を変更するたびに呼び出されます。 サンプルゲームでは、 __ConstantBufferChangeOnResize__の射影行列を更新します。

ウィンドウ サイズのリソースは、次の方法で更新されます。 
* アプリ フレームワークが、ウィンドウの状態の変更を表すいくつかの考えられるイベントのいずれかを取得します。 
* メイン ゲーム ループにイベントが通知され、メイン クラス (__GameMain__) インスタンスで __CreateWindowSizeDependentResources__ を呼び出します。これは、次に、ゲーム レンダラー (__GameRenderer__) クラスでの __CreateWindowSizeDependentResources__ の実装を呼び出します。
* このメソッドの主な役割は、ウィンドウのプロパティが変化したために視覚効果が混乱したり、誤ったものにならないようにすることです。

このサンプルゲームでは、多くのメソッド呼び出しは [__FinalizeCreateGameDeviceResources__](#finalizecreategamedeviceresources-method) メソッドと同じです。 コード チュートリアルについては、前のセクションを参照してください。

ゲームの HUD とオーバーレイ ウィンドウ サイズのレンダリングの調整については、「[ユーザー インターフェイスの追加](tutorial--adding-a-user-interface.md)」を参照してください。

```cppwinrt
// Initializes view parameters when the window size changes.
void GameRenderer::CreateWindowSizeDependentResources()
{
    // Game HUD and overlay window size rendering adjustments are done here
    // but they'll be covered in the UI section instead.

    m_gameHud.CreateWindowSizeDependentResources();

    ...

    auto d3dContext = m_deviceResources->GetD3DDeviceContext();
    // In Sample3DSceneRenderer::CreateWindowSizeDependentResources, we had:
    // Size outputSize = m_deviceResources->GetOutputSize();

    auto renderTargetSize = m_deviceResources->GetRenderTargetSize();

    ...

    m_gameInfoOverlay.CreateWindowSizeDependentResources(m_gameInfoOverlaySize);

    if (m_game != nullptr)
    {
        // Similar operations as the last section of FinalizeCreateGameDeviceResources method
        m_game->GameCamera().SetProjParams(
            XM_PI / 2, renderTargetSize.Width / renderTargetSize.Height,
            0.01f,
            100.0f
            );

        XMFLOAT4X4 orientation = m_deviceResources->GetOrientationTransform3D();

        ConstantBufferChangeOnResize changesOnResize;
        XMStoreFloat4x4(
            &changesOnResize.projection,
            XMMatrixMultiply(
                XMMatrixTranspose(m_game->GameCamera().Projection()),
                XMMatrixTranspose(XMLoadFloat4x4(&orientation))
                )
            );

        d3dContext->UpdateSubresource(
            m_constantBufferChangeOnResize.get(),
            0,
            nullptr,
            &changesOnResize,
            0,
            0
            );
    }
}
```

## <a name="next-steps"></a>次の手順

これは、ゲームのグラフィックス レンダリング フレームワークを実装する基本的なプロセスです。 ゲームの規模が大きくなるほど、オブジェクトの種類とアニメーションの動作の階層を処理するために必要な抽象化も増加します。 メッシュやテクスチャなどのアセットを読み込んで管理するために、より複雑なメソッドの実装が必要になります。 次に、[ユーザー インターフェイスを追加する](tutorial--adding-a-user-interface.md)方法について説明します。