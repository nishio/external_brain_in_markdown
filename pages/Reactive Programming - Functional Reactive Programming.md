---
title: "Reactive Programming / Functional Reactive Programming"
---

Rx* is not FRP

[The introduction to Reactive Programming you've been missing · GitHub](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)
- > [@ReactiveX](https://twitter.com/ReactiveX/status/483625917491970048?s=20&t=qLr-sa2ZRTF-JQsfLa9biA): A nice introduction to Reactive Programming using RxJS from @andrestaltz [https://t.co/breKB68ndK](https://t.co/breKB68ndK) although Rx* is not FRP
- > [@ReactiveX](https://twitter.com/ReactiveX/status/483644526368931842): @andrestaltz @phadej @conal the big difference is the separation between Behaviors and Events. We do have that eg BehaviorSubject/Observable
- [【翻訳】あなたが求めていたリアクティブプログラミング入門 - ninjinkun's diary](https://ninjinkun.hatenablog.com/entry/introrxja)
    - [リアクティブプログラミングとは何だったのか - Qiita](https://qiita.com/hiruberuto/items/39e4126f470d8b84b291)

[terminology - What is (functional) reactive programming? - Stack Overflow](https://stackoverflow.com/questions/1028250/what-is-functional-reactive-programming?answertab=votes)
- [Q. （関数型）リアクティブプログラミングとは何ですか？ | POSTD](https://postd.cc/what-is-functional-reactive-programming/)
- これの英語版を見たけど、なるほどこれは混乱する人が出るのもわかる
    - "datatypes that represent a value 'over time' " = Behavior
    - 要するにこれじゃん
    - 世界をどういう部品の組み合わせで記述するか、という認知の部分を変える
    - 電子回路の設計の経験がある人は理解しやすいかもね
        - wireは電圧の変化する存在
            - これをファーストクラスの存在とみなす
        - 部品を置くことはその存在の間の関係の記述
            - 宣言的と言っても良い
    - こういう「今のコンピュータのアーキテクチャと異なった」認知で世界を記述した上で、それを今のコンピュータで実行可能な形に落とし込む必要がある
    - the big difference is the separation between Behaviors and Events
        - ここを混同したらダメだ
        - 根本的に何をファーストクラスにしたくてやってるのかわかってない

[The Essence of FRP](https://begriffs.com/posts/2015-07-22-essence-of-frp.html)

[リアクティブプログラミングとは何だったのか - Qiita](https://qiita.com/hiruberuto/items/39e4126f470d8b84b291)


説明を書こうとして理解してないことに気づいた
- 説明できるほど詳しくないことに気づいたので今回はざっと眺めるだけにする
- 一つのオブジェクトを時間軸に沿って破壊的に書き換えていくのではなく、
- 変更不能な(イミュータブルな)オブジェクトを受け取って、新しいオブジェクトを作って返す
- ストリームにメッセージが流れている的メンタルモデル

