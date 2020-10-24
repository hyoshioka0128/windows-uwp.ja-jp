---
Description: オーディオ入力の品質が原因で発生する音声認識の精度の問題を管理する方法について説明します。
title: 音声入力の問題の管理
ms.assetid: 3E36C683-C96A-4FEE-AD52-FDB87E0CC299
label: Manage audio input issues
template: detail.hbs
keywords: スピーチ, 音声, 音声認識, 自然言語, ディクテーション, 入力, ユーザーの操作
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: bbbe9a887afa4637aaf8e6576e14979a92aa6b8f
ms.sourcegitcommit: 7b2febddb3e8a17c9ab158abcdd2a59ce126661c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89173396"
---
# <a name="manage-issues-with-audio-input"></a>音声入力の問題の管理


オーディオ入力の品質が原因で発生する音声認識の精度の問題を管理する方法について説明します。

> **重要な API**: [**SpeechRecognizer**](/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognizer)、[**RecognitionQualityDegrading**](/uwp/api/windows.media.speechrecognition.speechrecognizer.recognitionqualitydegrading)、[**SpeechRecognitionAudioProblem**](/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionAudioProblem)


## <a name="assess-audio-input-quality"></a>オーディオ入力の品質を評価する


音声認識がアクティブな場合は、音声認識エンジンの [**RecognitionQualityDegrading**](/uwp/api/windows.media.speechrecognition.speechrecognizer.recognitionqualitydegrading) イベントを使用して、1 つ以上のオーディオの問題によって音声入力が妨げられている可能性があるかどうかを判断します。 イベント引数 ([**SpeechRecognitionQualityDegradingEventArgs**](/uwp/api/Windows.Media.SpeechRecognition.SpeechRecognitionQualityDegradingEventArgs)) には、[**Problem**](/uwp/api/windows.media.speechrecognition.speechrecognitionqualitydegradingeventargs.problem) プロパティがあり、オーディオ入力で検出された問題の説明が含まれています。

認識は、多すぎる背景の雑音、ミュートされたマイク、およびスピーカーのボリュームや速度の影響を受ける場合があります。

ここでは、音声認識エンジンを構成し、[**RecognitionQualityDegrading**](/uwp/api/windows.media.speechrecognition.speechrecognizer.recognitionqualitydegrading) イベントのリッスンを開始します。

```CSharp
private async void WeatherSearch_Click(object sender, RoutedEventArgs e)
{
    // Create an instance of SpeechRecognizer.
    var speechRecognizer = new Windows.Media.SpeechRecognition.SpeechRecognizer();

    // Listen for audio input issues.
    speechRecognizer.RecognitionQualityDegrading += speechRecognizer_RecognitionQualityDegrading;

    // Add a web search grammar to the recognizer.
    var webSearchGrammar = new Windows.Media.SpeechRecognition.SpeechRecognitionTopicConstraint(Windows.Media.SpeechRecognition.SpeechRecognitionScenario.WebSearch, "webSearch");


    speechRecognizer.UIOptions.AudiblePrompt = "Say what you want to search for...";
    speechRecognizer.UIOptions.ExampleText = "Ex. 'weather for London'";
    speechRecognizer.Constraints.Add(webSearchGrammar);

    // Compile the constraint.
    await speechRecognizer.CompileConstraintsAsync();

    // Start recognition.
    Windows.Media.SpeechRecognition.SpeechRecognitionResult speechRecognitionResult = await speechRecognizer.RecognizeWithUIAsync();
    //await speechRecognizer.RecognizeWithUIAsync();

    // Do something with the recognition result.
    var messageDialog = new Windows.UI.Popups.MessageDialog(speechRecognitionResult.Text, "Text spoken");
    await messageDialog.ShowAsync();
}
```

## <a name="manage-the-speech-recognition-experience"></a>音声認識エクスペリエンスを管理する


[**Problem**](/uwp/api/windows.media.speechrecognition.speechrecognitionqualitydegradingeventargs.problem) プロパティにある説明を使用して、ユーザーが認識の状態を改善できるようにします。

ここでは、低い音量レベルをチェックする [**RecognitionQualityDegrading**](/uwp/api/windows.media.speechrecognition.speechrecognizer.recognitionqualitydegrading) イベント用のハンドラーを作成します。 次に、[**SpeechSynthesizer**](/uwp/api/Windows.Media.SpeechSynthesis.SpeechSynthesizer) オブジェクトを使って、より大きな声で話すことをユーザーに提示します。

```CSharp
private async void speechRecognizer_RecognitionQualityDegrading(
    Windows.Media.SpeechRecognition.SpeechRecognizer sender,
    Windows.Media.SpeechRecognition.SpeechRecognitionQualityDegradingEventArgs args)
{
    // Create an instance of a speech synthesis engine (voice).
    var speechSynthesizer =
        new Windows.Media.SpeechSynthesis.SpeechSynthesizer();

    // If input speech is too quiet, prompt the user to speak louder.
    if (args.Problem == Windows.Media.SpeechRecognition.SpeechRecognitionAudioProblem.TooQuiet)
    {
        // Generate the audio stream from plain text.
        Windows.Media.SpeechSynthesis.SpeechSynthesisStream stream;
        try
        {
            stream = await speechSynthesizer.SynthesizeTextToStreamAsync("Try speaking louder");
            stream.Seek(0);
        }
        catch (Exception)
        {
            stream = null;
        }

        // Send the stream to the MediaElement declared in XAML.
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.High, () =>
        {
            this.media.SetSource(stream, stream.ContentType);
        });
    }
}
```

## <a name="related-articles"></a>関連記事


* [音声操作](speech-interactions.md)

**サンプル**
* [音声認識と音声合成のサンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpeechRecognitionAndSynthesis)
 

 