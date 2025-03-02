---
title: "Whisperの活用振り返り"
---

2024-03-22
[[Whisper]]での文字起こしに関して、過去にやったことがあるのに何をやったのか忘れて、新しい応用をやることの開始コストが高くなっていた
これはよくないので振り返りをまず作る

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 2022年12月
    - KJ法勉強会振り返り勉強会の質疑応答部分をWhisperを使って文字起こしした。 --- [[週記2022-12-18]]
        - 直前2022-12-19にGitからのWhisperのインストールとffmpegでの分割をしてる --- [[Whisper]]
        - 問題なく日本語が文字起こしできた
        - CPUでFP16がサポートされていない警告が表示された。
            - --device mpsオプションを使用。
        - 文字起こしに長時間かかった (11時間以上)。
- 2023年3月1日
    - OpenAIがChatGPT APIとWhisper APIをリリース。
        - 2022年9月にオープンソース化されたWhisperモデルがAPIとして提供開始。
        - large-v2モデルを使用し、価格は1分あたり0.006ドル。
        - 最適化されたサービングスタックにより、他のサービスよりも高速。
        - transcriptionsエンドポイント(音声を文字起こし)とtranslationsエンドポイント(英語に翻訳)を提供。
- 2023年4月
    - [SYSTRAN/faster-whisper: Faster Whisper transcription with CTranslate2](https://github.com/SYSTRAN/faster-whisper)
- 2023年4月30日
    - 英会話スクールの録音をWhisperで文字起こし、GPT-4で要約。 --- [[日記2023-04-30]] / [[英会話→Whisper→GPT4]]
    - 40分の英会話を丸ごとGPT-4に与えると長すぎるため、適切な長さに分割して与える必要がある。
    - 英会話の内容を思い出すのに十分な品質の要約が得られた。
- 2023年5月3日  --- [[日記2023-05-03]]
    - Whisperを使って英会話の録音ファイルを文字起こし。
    - 文字起こしに3時間以上かかった。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Whisperを用いて日本語を文字起こしする2024年時点で最高精度の方法をまとめて
<img src='https://scrapbox.io/api/pages/nishio/pplx/icon' alt='pplx.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
2024年時点でWhisperを用いて日本語音声を最高精度で文字起こしするベストな方法をまとめると以下のようになります。
1. API版のwhisper-1モデルを利用する
    - Whisperには無料のGitHub版と有料のAPI版(whisper-1)がある
    - API版はGitHub版のlargeモデルをベースにしつつ、より高速かつ高精度
    - 音声1分あたり約0.86円の従量課金制
2. 高品質の音声データを用意する
    - ノイズの少ないクリアな音声を録音する
    - 録音時は目安として55dB未満の静かな環境を確保する
    - 音声フォーマットはmp3, mp4, mpeg, mpga, m4a, wav, webmに対応
3. 25MB以下の音声ファイルに分割する
    - 現在のWhisperは25MBまでの音声ファイルしか処理できない
    - 長時間の音声は25MB以下のファイルに分割する必要がある
    - 分割ファイルは時系列順に番号を振るのが良い
4. verbose=Trueオプションで処理過程を可視化する
    - 処理過程を表示できるverbose=Trueをtranscribeのオプションに追加
    - 言語の検出状況や時間ごとの文字起こし結果を確認できる
5. 固有名詞や専門用語の誤りは手動で修正する
    - Whisperでも同音異義語などの判別は難しい
    - 文脈的に明らかな誤りは、文字起こし後に人手で修正するのが確実

以上が、Whisperで日本語音声を高精度に文字起こしするポイントです。
実際にAPI版のwhisper-1モデルで文字起こしを試したところ、ほぼ完璧な精度が得られました。
ただし、固有名詞の誤りなどは発生するため、最終的に人間のチェックが必要不可欠と言えます。
コストと手間のバランスを見て、用途に応じた最適な方法を選ぶのが良いでしょう。

