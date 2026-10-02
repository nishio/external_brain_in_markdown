---
title: "THINKLET開発者コミュニティイベント"
---

2026-10-02

LT

[[THINKLETで読書支援]]
本を読んでて「〜ってなんだっけ」と聞いたら「何ページに解説があります、簡単にいうと〜〜です」みたいに回答してほしいなと思っている。
そして将来的には書籍をまたいで「これ前にも似たようなこと読んだよね」「〜〜って本にありましたね」みたいにしたい。
![image](https://scrapbox.io/files/6abf89aa03edf2395a39849d.png)


1分デモ動画
[https://youtu.be/-heTyY0l3qc](https://youtu.be/-heTyY0l3qc)
質問してから回答が再生し終わるまで1分弱

[[Andriodデバイスを声で操作する]]
![image](https://scrapbox.io/files/6abf289903edf2395a385cba.png)
- CPUは7%程度で動き続けるけど、これでも7時間くらいバッテリーが持つはずで、7時間ぶっ続けで書籍を読むわけでないなら実害はない
- ウェイクワード発生からの遅延は伸びるけど、200ms程度遅れたところでそんなに困らない肌感

今進行中の実験
- せっかくマイクアレイがついてるので5ch録音からの音源分離・話者分離をしたい
- ので今回はそのデータ取得のための録音アプリを入れてきた
- ![image](https://scrapbox.io/files/6abf53a603edf2395a38f8d8.png)
- 9時間10分録音して、電池はまだ26%残っていた。 保存容量は1時間約2.1GB、4時間で約8.3GB。空き34GBなら約16時間分。
- まだガチの「懇親会のような雑音の中で自分と相手の声をクリアに取る」という実験ができてない、今日の録音データで今後実験するつもり
    - ![image](https://scrapbox.io/files/6abf577003edf2395a390a5d.png)
    - [[ICA]]系の[[AuxIVA]]で実際に分離した結果
    - これは2人の会話の分離で、ターンは分かれている。割と音源分離できているがそもそもこういう状況なら音源分離しなくても文字起こしに支障ない
- 動作確認画面も作った(ステートフルな機械の現在のステートを確認する手段は地味に重要)
    - ![image](https://scrapbox.io/files/6abf1d9d03edf2395a383e34.png)
    - iPhoneのインターネット共有をかけることでiPhoneがWifiアクセスポイントとして機能するようになり、THINKLETがそのアクセスポイントに接続すると同一LAN内なのでiPhoneからHTTPアクセスができる、ラップトップからもそのアクセスポイントにつなげばやり取りできるのでケーブルで直結できない状況でも色々できる

その他の話題

eBadge
- [[Bad Apple on eBadge]] この解説動画の末尾に解説がある
- デバイスはこれ [[ESP32-S3-Touch-AMOLED-1.75C]]
- ソースコードはまだ公開してないけど近いうちに。Codexが全部書いたw

yujif: [首掛け型ウェアラブル THINKLET と OpenAI Realtime API で「目の前を一緒に見ながら相談できる相方」を作る](https://zenn.dev/yujif/articles/90696ac3f098e2)
- 料理支援AIおもろい
- ちゃんとシンクレットつけてる絵がどうやって生成されたのか気になる
    - before /after
        - ![image](https://scrapbox.io/files/6abfb5dc03edf2395a39cab9.png)![image](https://scrapbox.io/files/6abf89aa03edf2395a39849d.png)
        - できた！

- 音聞こえにくいのわかる


