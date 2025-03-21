---
title: "Keichobot:高度な使い方"
---

### フィードバックボタン
- ![image](https://gyazo.com/1a5e171ddaa9b12f6a154b3493ab57c9/thumb/1000)

- Keiは適切なキーワードに対して適切な質問をしようと努力しますが、間違えることもあります。そんな時に人間がKeiに「その質問はイマイチだよ」と教える機能があります。
    - NGKWボタンは「このキーワードを掘り下げるな」と教えます。
        - かなり強い命令です。そのキーワードはほとんど選ばれなくなります。
        - 想定ユースケースは「マジかw」の「w」がキーワードに選ばれてしまった場合に候補から削除するような場合
        - 会話の序盤でこれをたくさん使うと話が膨らまなくなります。
    - UPKWボタンは「そんなキーワードより、こっちを掘り下げてよ」と教えます。
    - NGボタンは不満げな表情をプログラムに伝えます。
        - これは「イマイチな質問だなぁ」という感情表現です。
        - 「うーん…」みたいな発言でも機械学習を使って同様に判定します。
        - これはテキスト欄に絵文字を挿入するだけで送信はしません。追加でメッセージを書くこともできます。
        - 「不満げな顔をしながら答える」みたいなイメージです
    - 隣のニコニコマークは特に機能はありません。
        - 不満な顔ができてニコニコできないのはアンバランスなのでつけました

### 相槌モード
- 話したいことが沢山あって、まずは質問せずに聞いて欲しい場合「まず聞いて」と入力するとプログラムは相槌モードに入ります
- 相槌モードでは質問をせずに相槌を打ちます。
- 話し終わったら「おしまい」と入力すると、そこまでの入力を覚えた状態で対話開始します。
- ![image](https://gyazo.com/310940b6b4f5e2f7d7b0159a86a050f8/thumb/1000)


### 心の声
- プログラムに入力したいわけではないがログに残しておきたいことがある場合、開きカッコで始めると「心の声」になります
- ![image](https://gyazo.com/90c8661dfd37ffbe8ba9a671802d16fe/thumb/1000)

さらに高度な話
- [[Keichobotのさらに高度なテクニック]]

---
from [[聞き出しチャットシステム]]
old title: Keicho:高度な使い方

