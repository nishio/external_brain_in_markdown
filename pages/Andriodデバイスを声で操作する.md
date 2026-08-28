---
title: "Andriodデバイスを声で操作する"
---

僕「シンクレット！」 → ピポ！ → 僕「これは何」 → (写真撮影)「考え中」 → 「これは〜〜です」というシステムを作っていた。音声トリガーの部分に興味のある人がいたのでそこの解説を書こうかと思ったが、AIに音声トリガー部分だけ切り出したサンプルアプリのrepoを作ってもらうほうがいいなと思ったのでやっておいた
- [https://github.com/nishio/android-vosk-wakeword-sample](https://github.com/nishio/android-vosk-wakeword-sample)


簡単な仕組み
- Voskを使う: [Offline speech recognition on Android with VOSK](https://alphacephei.com/vosk/android)
    - デバイス内でストリーミング音声認識→「シンク レット」「シンク レッド」が出現したら以降の処理をトリガー
    - VoskはAndroid等で[[ストリーミング認識]]できる汎用ASR（音声文字起こし）
        - 新しいモデルを学習するのではなくVoskの学習済み日本語モデルをそのまま使い、認識候補をウェイクワード周辺だけに絞って使っている
- [[ウェイクワード]]専用エンジンPicovoice Porcupineを使わなかったのは、これが7日間の無償試用以降は営業に問い合わせろとか書いてあってめんどくさかったから
    - ストリーミング認識はウェイクワード専用エンジンに比べるとCPU消費や遅延の点で不利ではある
        - CPU利用率は6.9%だった
        - Picovoice Porcupineは音声処理単位が32msでVoskは200msなのでまあ遅延はある
            - [https://scrapbox.io/files/6a8f8fcc714feb3f19557554.mp3](https://scrapbox.io/files/6a8f8fcc714feb3f19557554.mp3)
            - これくらいのスピードで反応する
        - 僕の目的には問題ないかな〜という気持ち

Androidデバイスとしては[[THINKLET]]を使った。
- 首掛け型で3264x2448の高解像度の写真が撮れる。
- ボタンもあるのでそれでトリガーするのが確実だが僕は[[THINKLETで読書支援]]の「書籍を両手で持って読んでる時に使いたい」というニーズのために音声で操作したかった
