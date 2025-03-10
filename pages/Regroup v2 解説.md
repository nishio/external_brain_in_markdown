---
title: "Regroup v2 解説"
---

Q: これは何？ A: 手書き図解メモや付箋でのKJ法ができるツール
![image](https://gyazo.com/9894b46b9f2da59814a03245e24399ad/thumb/1000)
[マニュアル](http://nishio-s3.s3-website-us-west-2.amazonaws.com/#/manual) [[Regroup201907デモ動画]]

- iPad想定で作って来たのでiPhone画面だと多少乱れるけど、ブラウザ実装なので動きはする
- 明示的な保存なしに編集即クラウド保存
    - オフラインでもローカルにキャッシュされオンラインに戻ったタイミングで保存される
    - ただし、今はタブを閉じてしまうと消える(改善予定)
- 今はユーザ管理がない
    - 編集用リンクを知っている人が編集できる仕組み
- 同じリンクをPCやiPadで開けば同じものが見える
- ペイントではなくパスドロー
    - 描いたあとで選択して移動できる
- 消しゴム、線の色、太さ、点線、矢印などの機能はまだない
- 移動ツールで背景部分をドラッグすればいくらでも新しい紙が出る、紙のサイズは無限
    - 二本指ジェスチャーで拡大縮小・紙の移動ができる
- iPhoneでは「ツールバーを非表示」すれば編集スペースが広くなる

- 既知の問題
    - FIXED: [[メニューアイコンがiPhoneなどの狭い画面ではみ出す]]

    - ![image](https://gyazo.com/3caad9f4f44947f712fc34fc8ec3ca5f/thumb/1000)
        - 画面を回転させた時などにメニューバーが隠れてしまう
        - TODO: キャンバスのない白いところをタップしたら適切な位置に再配置するようにしよう
            - もしくはシェイク
    - > 画面を下にスクロールさせて新しい付箋を追加すると、その位置では見えないところ（上の方）に追加されてしまう。
        - [/rashitamemo/Regroup v2ファーストインプレッション#5de65eb79dc7d80000d0b096](https://scrapbox.io/rashitamemo/Regroup v2ファーストインプレッション#5de65eb79dc7d80000d0b096)
        - TODO: これはバグなので修正する
            - 正しく実装されていたら付箋の追加は常に現在の視野の右上隅から順番に置かれる
    - > 付箋をグループ化すると表札名の入力が求められるが、その際、前に入力した付箋のテキストが残っている
        - [/rashitamemo/Regroup v2ファーストインプレッション#5de660a49dc7d80000d0b0a4](https://scrapbox.io/rashitamemo/Regroup v2ファーストインプレッション#5de660a49dc7d80000d0b0a4)
        - TODO: これもバグ
            - プレースホルダーが良いかな
            - 表札名をつけることを強要するのは良くないのではと思い始めている
                - 特にパスをグループ化した時、表札があるのがベターだが、サムネイルでも良いかなと
    - 中見出しを開く手段がない
        - [/rashitamemo/Regroup v2ファーストインプレッション#5de6611c9dc7d80000d0b0a7](https://scrapbox.io/rashitamemo/Regroup v2ファーストインプレッション#5de6611c9dc7d80000d0b0a7)
        - TODO: うーん、これは多分割と難しいバグ
    - iPhoneで付箋入力モードにすると、iPadように設計されたテキストエリアのサイズでは大きすぎる
        - その影響でツールバーを見失ったりする

- 要望メモ
    - 削除とグループの解除
        - わかる [[pRegroup2020#5d2d4ca4aff09e00005b4e11]]

