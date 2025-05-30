---
title: "付箋の選択・圧縮 UI設計"
---

- [[付箋・パスの投げ縄選択]] done
- [[選択されたもののグループ化]] done
- [[表札の表示]] done
- グループの開閉 done
    - 閉じてる状態のグループをワンクリックで開く
        - これを実現するためにデフォルトで選ばれているMoveツールを見てみたが
            - クリックされたものがGroupかPathか、みたいな分岐をしているので、
            - 先ほど定義した型情報を使って綺麗にしてから機能追加する必要がある
        - Enumにした
- グループの移動 done
    - グループを掴んでドラッグした場合、ドラッグ中は動いているけど話すと元の位置に戻る
        - これはグループの座標更新が実装されていないから
        - グループのpositionを変更するのではなく、子要素のpositionを変更することにした
            - [[グループの子要素の位置を再帰的に更新]]
        - なぜなら親に遡らなくてもオブジェクト単体を見てそのオブジェクトの位置がわかる方があとあと[[コネクタ]]などで良さそうだから

- [[グループの中の付箋をドラッグで出し入れ・配置変更]] これはまだ
- [[表札の編集]] done


-----
開いている状態のグループに対して投げ縄で要素の付箋ごと囲んだら変なグループができないかなと思ったが、それは問題なかった
これは、投げ縄の当たり判定を行う対象がレイヤーのトップレベルのオブジェクトに限定されているから。
これはこの仕様のままで良いと思う。
- グループが選択されない、少なくとも閉じている時には選択されるべき


- [[バルーンメニュー]]は保留

- 今の「描画するものを描画する順にArrayに入れてある」だと微妙？
    - Firestoreでの保存時に...
    - それは後で考える。save/load時に変換するのでも良いはず

グループ化して表札編集モードに入った時、そのまま付箋にペン入力できてほしいなぁ
- まずはテキスト入力で最後まで完成させるべき
- 「iPadでキーボードを使うのイマイチだな」という気持ちだったんだけど、音声入力という選択肢も


-----議論
- グループは開閉が容易でなければならない
    - [[グループ化#5bd6d729aff09e000076a600]]
    - 中身を確認することに手間が掛かってはいけない
        - A: 表札付箋のワンタップで開閉
        - B: 表札付箋の周りにリングメニュー

- グループは明示的に作らなくてよいのではないか
    - 明示的なグループの所属関係があると、入れる、出す、が必要になる
    - まとめて移動する時、畳む際に初めて、どれが畳む対象か指定すればよい
    - まとめて移動する対象が必ずしもグループとは限らない
- ⇔グループは明示的に作るべきである
    - 表札をつけるプロセスが大事 +1

- [[ReGroup2018#5b72e0e2aff09e000000883c]]
    - グループ化
        - 「束ねるモード開始ボタン→対象付箋をタップ(トグル)→完了ボタン/キャンセルボタン」でよい。
        - 投げ縄ツールを作ったところで「投げ縄モード」「選択」「グループ化」と手数が同じだから。
        - 手順
            - 束ねるモード開始
            - 対象付箋をタップ
            - 完了ボタン
            - 表札を選択or新規作成
- ⇔投げ縄ツールは必要だろう
    - グループ化と無関係に、単なる移動の時にも必要
    - 選択してから圧縮ボタン
        - そこで表札付箋が作成され編集モードへ
    - [[付箋の圧縮展開]]
        - 選択する
            - 選択+/選択-を考えているが、必要だろうか、投げ縄があればいらないのでは
        - 表札のドラッグで全体移動
            - 必要か？
        - 開いた

[[圧縮付箋の展開時どうなるべきか]]
- 案1: 物理演算で反発
- 案2: ユークリッド空間である必要はないのでは
- 案3: 収まらないものはズームアウト
- ⇔ダメ
    - 密集している表札付箋をタップした時に、小さくて読めない付箋が表示されるとズームで一手間かかる
    - 表札付箋をタップするのは「中身を確認したい」という意図なのは明らかなのだから、追加操作なく最も中身を確認しやすい形で表示される必要がある
    - オーバーレイだろう
        - ![image](https://gyazo.com/bb85089b7974fce7436609ca922f976f/thumb/1000)
        - [[付箋の圧縮展開]]
            - 開いたグループに対してドラッグドロップでグループに追加削除
                - [[既存グループの付箋追加削除UI]]

[[pRegroup-done-2019]]
