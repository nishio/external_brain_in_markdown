---
title: "Devinクレジット使い切り4/28"
---

未レビューのタスクを振り返っていく
ただし諸般の事情で優先度はあるので上から順番というわけではない
それ自体をAIにさせるか

- [[Devinクレジット使い切り4/23棚卸し]]
- [[Devinクレジット使い切り4/26]]
- [[Devinクレジット使い切り4/27]]

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
- P0 ― 最優先（今日中に着手）
    - バブコメ攻撃対策まとめ（ドキュメント）
    - 目的：対策を一本の資料に集約し、関係者へ即共有できる状態にする。
...
具体的ステップ
- pubcom-filter PR をチェックアウトしテスト → マージ
- Embedding 前処理 (#361) をテストし、クラスタリング結果を 2-3 サンプル確認
- 1-2 の成果物と調査ログをまとめ、対策ドキュメント草稿を作成
- CSV コスト表示 (#79) をレビューし、攻撃コスト試算に組み込む
- 上記をもとに P0 ドキュメントを完成・配布

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>pubcom-filter PR はどこ？URLを示して

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
こちらです。すでにマージ済みになっています。
[https://github.com/nishio/pubcom-filter/pull/1](https://github.com/nishio/pubcom-filter/pull/1)

---
これはツールがDevinによって作成済み、GitHubで公開済み。
- aipubcom-dataを使って実験させよう
- [https://app.devin.ai/sessions/bba7128e4dfe4597abe9036690cf8f54](https://app.devin.ai/sessions/bba7128e4dfe4597abe9036690cf8f54)

---
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>次のステップ ― Embedding 前処理 (#361) のレビュー
やること	具体手順
1.
Issue と実装を確認
- GitHub Issue: [https://github.com/digitaldemocracy2030/kouchou-ai/issues/361](https://github.com/digitaldemocracy2030/kouchou-ai/issues/361)
- Devin 実装ログ: [https://app.devin.ai/sessions/8e7e2042e6ea4f9cb730d7e29b4623e1](https://app.devin.ai/sessions/8e7e2042e6ea4f9cb730d7e29b4623e1)

---
これはDevinが作ってたんだけどtokorotenがもっと良さそうなものを作ったのでdiscontinuedなのだ

---
僕の書き方が足りなかったと見えてo3は次のタスクを発見できない
目視振り返り

from [[Devinクレジット使い切り4/26#680d8c760000000000a39ec4]]
- [[バブコメフィルター]]
    - [https://app.devin.ai/sessions/a62b5d235be243e295c408f812077aba](https://app.devin.ai/sessions/a62b5d235be243e295c408f812077aba)
        - 作成済み、reviewする
        - linkage=minにして長さを横軸にしてプロットした方がいいかもという気がしてきている


    - ![image](https://gyazo.com/d43823a3467329404d6a62c68a3f00db/thumb/1000)


- 埋め込みベクトル作成と凝集クラスタリング
    - [https://app.devin.ai/sessions/dd26ab0e30dc43fa9ba04856cb21a8c6](https://app.devin.ai/sessions/dd26ab0e30dc43fa9ba04856cb21a8c6)

✅ released [[埋め込みベクトルと凝集クラスタリングによるパブリックコメント分析実験]]


neologdn
[https://app.devin.ai/sessions/bba7128e4dfe4597abe9036690cf8f54](https://app.devin.ai/sessions/bba7128e4dfe4597abe9036690cf8f54)
6994
6966

28
→99件

