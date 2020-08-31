---
title: 画面への描画
description: GXDI Api と Direct3D Api を使用して、OpenGL コードを DirectX に移植し、回転するキューブを画面に描画する方法について説明します。
ms.assetid: cc681548-f694-f613-a19d-1525a184d4ab
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, DirectX, グラフィックス
ms.localizationpriority: medium
ms.openlocfilehash: 7380ede77eeb14f8b1865d4c948387df7e072453
ms.sourcegitcommit: 5d34eb13c7b840c05e5394910a22fa394097dc36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89054502"
---
# <a name="draw-to-the-screen"></a>画面への描画




**重要な API**

-   [**ID3D11Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d)
-   [**ID3D11RenderTargetView**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11rendertargetview)
-   [**IDXGISwapChain1**](https://docs.microsoft.com/windows/desktop/api/dxgi1_2/nn-dxgi1_2-idxgiswapchain1)

最後に、回転する立方体を画面に描画するコードを移植します。

OpenGL ES 2.0 では、描画コンテキストは EGLContext の型として定義されます。これには、ウィンドウとサーフェスのパラメーターのほか、ウィンドウに表示される最終的な画像の作成に使われるレンダー ターゲットへの描画に必要なリソースが含まれます。 このコンテキストを使ってグラフィックス リソースを構成し、シェーダー パイプラインの結果をディスプレイに正しく表示します。 主要なリソースの 1 つは "バック バッファー" (または "フレーム バッファー オブジェクト") と呼ばれ、ディスプレイに表示できる最終的な構成済みレンダー ターゲットが含まれます。

Direct3D を使ってディスプレイに描画するためのグラフィックス リソースを構成するプロセスは、もう少し解説が必要なプロセスであり、かなりの数の API を必要とします  (ただし、Microsoft Visual Studio Direct3D テンプレートを使うと、このプロセスを大幅に簡素化できます)。コンテキスト (Direct3D デバイス コンテキスト) を取得するには、最初に [**ID3D11Device1**](https://docs.microsoft.com/windows/desktop/api/d3d11_1/nn-d3d11_1-id3d11device1) オブジェクトを取得し、それを使って [**ID3D11DeviceContext1**](https://docs.microsoft.com/windows/desktop/api/d3d11_1/nn-d3d11_1-id3d11devicecontext1) オブジェクトを作成、構成する必要があります。 これら 2 つのオブジェクトは、ディスプレイへの描画に必要な特定のリソースを構成するために、組み合わせて使われます。

つまり、DXGI API には、グラフィックス アダプターに直接関係するリソースを管理するための API が主として含まれ、Direct3D には、CPU で実行されるメイン プログラムと GPU の橋渡しをする API が含まれます。

このサンプルでの比較のために、各 API から該当する型を紹介します。

-   [**ID3D11Device1**](https://docs.microsoft.com/windows/desktop/api/d3d11_1/nn-d3d11_1-id3d11device1): グラフィックス デバイスとそのリソースの仮想表現を提供します。
-   [**ID3D11DeviceContext1**](https://docs.microsoft.com/windows/desktop/api/d3d11_1/nn-d3d11_1-id3d11devicecontext1): バッファーを構成し、レンダリング コマンドを発行するためのインターフェイスを提供します。
-   [**IDXGISwapChain1**](https://docs.microsoft.com/windows/desktop/api/dxgi1_2/nn-dxgi1_2-idxgiswapchain1): スワップ チェーンは OpenGL ES 2.0 のバック バッファーに似ています。 これは、ディスプレイに表示する最終的なレンダリング画像を含むグラフィックス アダプターのメモリ領域です。 これは、最新のレンダリングを画面に表示するために、書き込みと "スワップ" を行うことのできるバッファーをいくつか持つため、"スワップ チェーン" と呼ばれます。
-   [**ID3D11RenderTargetView**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11rendertargetview): Direct3D デバイス コンテキストの描画先の 2D ビットマップ バッファー (スワップ チェーンによって表示される) が含まれます。 OpenGL ES 2.0 の場合と同様に、レンダー ターゲットは複数作成できます。その一部はスワップ チェーンにバインドされませんが、マルチパス シェーディング手法で利用されます。

テンプレートのレンダラー オブジェクトには次のフィールドがあります。

Direct3D 11: デバイスとデバイス コンテキストの宣言

``` syntax
Platform::Agile<Windows::UI::Core::CoreWindow>       m_window;

Microsoft::WRL::ComPtr<ID3D11Device1>                m_d3dDevice;
Microsoft::WRL::ComPtr<ID3D11DeviceContext1>          m_d3dContext;
Microsoft::WRL::ComPtr<IDXGISwapChain1>                      m_swapChainCoreWindow;
Microsoft::WRL::ComPtr<ID3D11RenderTargetView>          m_d3dRenderTargetViewWin;
```

次に、バック バッファーをレンダー ターゲットとして構成し、スワップ チェーンに提供する方法を示します。

``` syntax
ComPtr<ID3D11Texture2D> backBuffer;
m_swapChainCoreWindow->GetBuffer(0, IID_PPV_ARGS(backBuffer));
m_d3dDevice->CreateRenderTargetView(
  backBuffer.Get(),
  nullptr,
  &m_d3dRenderTargetViewWin);
```

Direct3D ランタイムは [**ID3D11Texture2D**](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11texture2d) の [**IDXGISurface1**](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgisurface1) を暗黙的に作成します。これは、スワップ チェーンで表示に使うことのできる "バック バッファー" としてのテクスチャを表します。

レンダー ターゲットのほか、Direct3D デバイスとデバイス コンテキストの初期化と構成は、Direct3D テンプレートのカスタムの **CreateDeviceResources** メソッドと **CreateWindowSizeDependentResources** メソッドで確かめることができます。

タイプと EGLContext に関連する Direct3D デバイスコンテキストの詳細については、 [ポートのコード「DXGI と Direct3D」を](moving-from-egl-to-dxgi.md)参照してください。

## <a name="instructions"></a>Instructions

### <a name="step-1-rendering-the-scene-and-displaying-it"></a>手順 1: シーンのレンダリングと表示

立方体のデータを更新した後 (この例では y 軸を中心に少し回転させる) で、Render メソッドはビューポートを描画コンテキスト (EGLContext) のサイズに設定します。 このコンテキストには、構成済みのディスプレイ (EGLDisplay) を使ってウィンドウ サーフェス (EGLSurface) に表示される色のバッファーが含まれます。 この時点で、この例では、頂点データの属性を更新する、インデックス バッファーを再バインドする、立方体を描画する、表示サーフェスへのシェーディング パイプラインによって描画される色のバッファーでスワップするという一連の処理を行います。

OpenGL ES 2.0: 表示するフレームのレンダリング

``` syntax
void Render(GraphicsContext *drawContext)
{
  Renderer *renderer = drawContext->renderer;

  int loc;
   
  // Set the viewport
  glViewport ( 0, 0, drawContext->width, drawContext->height );
   
   
  // Clear the color buffer
  glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
  glEnable(GL_DEPTH_TEST);


  // Use the program object
  glUseProgram (renderer->programObject);

  // Load the a_position attribute with the vertex position portion of a vertex buffer element
  loc = glGetAttribLocation(renderer->programObject, "a_position");
  glVertexAttribPointer(loc, 3, GL_FLOAT, GL_FALSE, 
      sizeof(Vertex), 0);
  glEnableVertexAttribArray(loc);

  // Load the a_color attribute with the color position portion of a vertex buffer element
  loc = glGetAttribLocation(renderer->programObject, "a_color");
  glVertexAttribPointer(loc, 4, GL_FLOAT, GL_FALSE, 
      sizeof(Vertex), (GLvoid*) (sizeof(float) * 3));
  glEnableVertexAttribArray(loc);

  // Bind the index buffer
  glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, renderer->indexBuffer);

  // Load the MVP matrix
  glUniformMatrix4fv(renderer->mvpLoc, 1, GL_FALSE, (GLfloat*) &renderer->mvpMatrix.m[0][0]);

  // Draw the cube
  glDrawElements(GL_TRIANGLES, renderer->numIndices, GL_UNSIGNED_INT, 0);

  eglSwapBuffers(drawContext->eglDisplay, drawContext->eglSurface);
}
```

Direct3D 11 では、プロセスはよく似ています  (Direct3D テンプレートのビューポートとレンダー ターゲットの構成を使っていることを前提とします)。

-   [**ID3D11DeviceContext1::UpdateSubresource**](https://docs.microsoft.com/windows/desktop/api/d3d11_1/nf-d3d11_1-id3d11devicecontext1-updatesubresource1) を呼び出して定数バッファー (この場合はモデル ビュー プロジェクション マトリックス) を更新します。
-   [**ID3D11DeviceContext1:: IASetVertexBuffers**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-iasetvertexbuffers)を使用して頂点バッファーを設定します。
-   [**ID3D11DeviceContext1:: IASetIndexBuffer**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-iasetindexbuffer)でインデックスバッファーを設定します。
-   [**ID3D11DeviceContext1::IASetPrimitiveTopology**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-iasetprimitivetopology) で特定の三角形のトポロジ (三角形のリスト) を設定します。
-   [**ID3D11DeviceContext1:: IASetInputLayout**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-iasetinputlayout)を使用して、頂点バッファーの入力レイアウトを設定します。
-   頂点シェーダーを [**ID3D11DeviceContext1:: VSSetShader**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-vssetshader)にバインドします。
-   フラグメントシェーダーを [**ID3D11DeviceContext1::P SSetShader**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-pssetshader)にバインドします。
-   [**ID3D11DeviceContext1::DrawIndexed**](https://docs.microsoft.com/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-drawindexed) を使って、シェーダーを通じてインデックス付き頂点を送信し、レンダー ターゲット バッファーに色の結果を出力します。
-   [**IDXGISwapChain1::Present1**](https://docs.microsoft.com/windows/desktop/api/dxgi1_2/nf-dxgi1_2-idxgiswapchain1-present1) でレンダー ターゲット バッファーを表示します。

Direct3D 11: 表示するフレームのレンダリング

``` syntax
void RenderObject::Render()
{
  // ...

  // Only update shader resources that have changed since the last frame.
  m_d3dContext->UpdateSubresource(
    m_constantBuffer.Get(),
    0,
    NULL,
    &m_constantBufferData,
    0,
    0);

  // Set up the IA stage corresponding to the current draw operation.
  UINT stride = sizeof(VertexPositionColor);
  UINT offset = 0;
  m_d3dContext->IASetVertexBuffers(
    0,
    1,
    m_vertexBuffer.GetAddressOf(),
    &stride,
    &offset);

  m_d3dContext->IASetIndexBuffer(
    m_indexBuffer.Get(),
    DXGI_FORMAT_R16_UINT,
    0);

  m_d3dContext->IASetPrimitiveTopology(D3D11_PRIMITIVE_TOPOLOGY_TRIANGLELIST);
  m_d3dContext->IASetInputLayout(m_inputLayout.Get());

  // Set up the vertex shader corresponding to the current draw operation.
  m_d3dContext->VSSetShader(
    m_vertexShader.Get(),
    nullptr,
    0);

  m_d3dContext->VSSetConstantBuffers(
    0,
    1,
    m_constantBuffer.GetAddressOf());

  // Set up the pixel shader corresponding to the current draw operation.
  m_d3dContext->PSSetShader(
    m_pixelShader.Get(),
    nullptr,
    0);

  m_d3dContext->DrawIndexed(
    m_indexCount,
    0,
    0);

    // ...

  m_swapChainCoreWindow->Present1(1, 0, &parameters);
}

```

[**IDXGISwapChain1::Present1**](https://docs.microsoft.com/windows/desktop/api/dxgi1_2/nf-dxgi1_2-idxgiswapchain1-present1) が呼び出されると、フレームが構成済みのディスプレイに出力されます。

## <a name="previous-step"></a>前の手順


[GLSL の移植](port-the-glsl.md)

## <a name="remarks"></a>注釈

この例では、デバイス リソース (特にユニバーサル Windows プラットフォーム (UWP) DirectX アプリのデバイス リソース) の構成に伴う複雑さが目立っていません。 テンプレート コード全体を調べることをお勧めします。その中でも、ウィンドウとデバイス リソースの設定と管理に関係する部分に注目してください。 UWP アプリは中断/再開イベントだけではなく回転イベントもサポートする必要がありますが、テンプレートを通じて、インターフェイスの喪失や表示パラメーターの変更を処理するうえでのベスト プラクティスを確かめることができます。

## <a name="related-topics"></a>関連トピック


* [簡単な OpenGL ES 2.0 レンダラーを Direct3D 11 に移植する方法](port-a-simple-opengl-es-2-0-renderer-to-directx-11-1.md)
* [シェーダー オブジェクトの移植](port-the-shader-config.md)
* [GLSL の移植](port-the-glsl.md)
* [画面への描画](draw-to-the-screen.md)

 

 




