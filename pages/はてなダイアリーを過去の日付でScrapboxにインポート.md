---
title: "はてなダイアリーを過去の日付でScrapboxにインポート"
---

from [[機械がScrapboxに書く]]

目的
- Scrapboxを検索した時に過去のブログ記事がヒットしない、ヒットした方が良いと思う
- はてなブログに自動コンバートされてるけど、課金してないので広告が出る
    - リンクする時に嫌な気持ちになる
- 過去の記事もブラケティングしたい

2021-05-04 [[はてなダイアリー]]を過去の日付でScrapboxにインポートした [script](https://github.com/nishio/scbot/blob/main/from_hatena.py)
2021-12-20
- Q: 半年経つけどどう？
- A: すごく良い
    - [[過去のブログ記事をScrapboxにインポートして半年、とても良い]]

過去(2018)に「エクスポートしたXMLからScrapbox形式のJSONにするスクリプト」までは作ってあった
- [[はてなダイアリーをScrapboxにインポートする]]
- なぜこのプロジェクトにインポートしてないのか？
- フォーマットの対応が完全ではない
- 機械的記事でトップが埋まるのが嫌だった
    - →更新日時を過去のものにすればトップが埋まることはないと気づいた

フォーマット
- bs4で読んだときに実体参照`&gt;`が消し飛んでるみたい
    - そんなはずあるかいと思うんだけど失われたものが出てきて解決方法がよくわからない
    - 大したことではないので自前でパースした
- はてな記法→Scrapbox記法の変換はしない
    - まとめてScrapboxのコード記法にした
    - 検索にヒットして読めたらそれで良い
    - `html.unescape`する
    - ブログのタイトルをページタイトルにするつもりだったが、必要ない気がしたのでやめた
        - タイトルがすべて機械生成のものになる
            - インポートした後でダメだと思ったときに機械的な除去が簡単
                - Q: インポート前にバックアップ取っておくのでもいいのでは？
                    - A: インポートした後しばらく運用して色々なページを編集した後でインポートを取り消したくなったらバックアップからの復元をするわけに行かない
            - 安心して上書きできる運用
                - スクリプトを更新して変換し直したときに、上書きして人間が書いた文章が失われると悲しい
                - この不安が「更新していくこと」を妨げる
                - 機械生成ページは変更せず、変更したい時には複製して良いタイトルのページを作れば良い
- ![image](https://gyazo.com/64bf2d44ad71f4b8515f6e6016d98f67/thumb/1000)
    - 作成日時がちゃんと3年前にになってる
    - けどまあ、正確に作成日時をあわせなくても「トップページに出ない」というだけで十分だったかもね
python

```
def timestamp(*args):
    return datetime.datetime(*map(int, args)).timestamp()
```

    - 2021-06-29 追記: 検索結果が時系列に並ぶのが心地よいので、やはり現状の「実際にその記事を書いた日時」がいい

検索
- ![image](https://gyazo.com/e3626a3f075a86a8838aa67c3723f9d4/thumb/1000)

見出しページ作ったけど絶対使わないと思ったので削除した
- ![image](https://gyazo.com/8f7f138a86ffc2610f8e703406b0ec5e/thumb/1000)![image](https://gyazo.com/a8cacff7f08c9b94a2ca9755746640fe/thumb/1000)
- [[無味乾燥なリスト]]は良くない


規模
- 12万行のXML
- 22万行のJSON
- 1500ページ

上書き
- 予定: 変更日時が変わってなければ上書き可能
- 予定: インポート時にコンフリクトが起こるかチェック
- 実際: 常に上書き可能

空のプロジェクトで試す
- adminにならないといけない

ボットがプロジェクトに参加することもスクリプトでできるようにする？
:

```
Request URL: "https://scrapbox.io/api/projects/{project}/invitations/{key}"
POST
```

