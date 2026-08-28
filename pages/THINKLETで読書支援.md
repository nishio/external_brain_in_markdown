---
title: "THINKLETで読書支援"
---

本を読んでて「〜ってなんだっけ」と聞いたら「何ページに解説があります、簡単にいうと〜〜です」みたいに回答したいなと思っている。
そして将来的には「これ前にも似たようなこと読んだよね」「〜〜って本にありましたね」みたいにしたい。

[https://youtu.be/-heTyY0l3qc](https://youtu.be/-heTyY0l3qc)
- とりあえず単一見開きをAIが読んで内容を理解するってところまではできた
- 2~30秒かかる

AIによる読書支援の段階わけ
- 1: 本を読んで深く知りたいキーワードをChatGPTなどでしらべる
- 2: 本の内容の画像から要約などを作る
- 3: 深く知りたいキーワードを音声などで入力して、誌面の情報から聞きたいキーワードの正しい表記や文脈を把握して回答生成する
- 4: 現在の誌面だけではなく、過去の誌面もコンテキストに入れる
    - これをやるためには画像を全部載せるのは現実的ではないので質問が発生する前にOCRや要約などを走らせておく必要がある
- 5: 現在の書籍だけではなく、過去の書籍もコンテキストに入れる


<img src='https://scrapbox.io/api/pages/nishio/Codex/icon' alt='Codex.icon' height="19.5"/>参考にした公開repo
- このPoCをそのまま実現する既存repoがあったわけではありません。THINKLET向けの公開実装を調べ、撮影、保存、Vision APIとの接続、結果のreviewといった要素ごとに設計や実装を参考にしました。
    - [thinklet-realtime-companion](https://github.com/yujif/thinklet-realtime-companion)は、カメラ画像と音声をOpenAIへ渡し、sessionを保存してHTMLで振り返るend-to-end実装です。本PoCに最も近く、特に入力とAIの判断を後から対応づけて確認する設計の参考にしました。
    - [thinklet.fivechannel.video.recorder](https://github.com/FairyDevicesRD/thinklet.fivechannel.video.recorder)は、THINKLETで動画と5ch音声を収録し、ADBでPCへ回収するFairy Devices公式実装です。最初の実機データ取得方法を考える土台になりました。
    - [thinklet.app.lifelog](https://github.com/FairyDevicesRD/thinklet.app.lifelog)は、長時間の定期撮影と録音を行う公式アプリです。質問していないページも後から探せるようにする「読書の記憶」の、連続稼働と保存設計を考える際に参照しました。
    - [thinklet-meter-reader](https://github.com/tokoroten/thinklet-meter-reader)は、一人称画像をOpenAI Visionへ送り、決められたJSON形式で結果を得る実装です。Visionの出力を構造化し、失敗も曖昧にせず記録する考え方を参考にしました。
- このほか、公式の[開発者向けsample](https://github.com/FairyDevicesRD/thinklet.app.developer)、[SDK](https://github.com/FairyDevicesRD/thinklet.app.sdk)、[Photo Viewer](https://github.com/FairyDevicesRD/thinklet.app.photoviewer)を、端末設定、カメラや音声の扱い、別端末からの構図確認の参考にしています。


