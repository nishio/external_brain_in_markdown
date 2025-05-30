---
title: "2021年のTypeScriptベストプラクティス"
---

10 bad TypeScript habits to break this year
[http://startup-cto.net/10-bad-typescript-habits-to-break-this-year/](http://startup-cto.net/10-bad-typescript-habits-to-break-this-year/)
理由もセットで書いてあって良い記事だが、一覧性が良くないので箇条書きにした

- 1: strictを使え
- 2: `||` ではなく `??` を使うか、そもそもデフォルト引数を使え
- 3: 型としてanyを使うのではなくunknownを使え
- 4: asで型キャストするのではなく、型ガードでテストして型が違えばthrowするようにせよ
- 5: テストコードで、型の要求を部分的にしか満たさないアドホックなオブジェクトをanyにキャストしてモックとして使うのではなく、ちゃんとしたモックを一箇所で定義してそれを使え
- 6: オブジェクトの種類によってあるプロパティを持っていたり持っていなかったりする時に、?でオプショナルなプロパティにするのではなく、どういう種類の時に持っているのかをインターフェースで明示せよ
- 7: ジェネリクスの型変数も変数なので一文字変数は避けよう
- 8: 真偽値でないものを条件式にしないで、明示的に比較演算子を使おう
- 9: 真偽値でないものを真偽値にするために`!!`を使うのではなく、明示的に比較演算子を使おう
- 10: nullとundefinedを同一視して`!= null`で条件分岐をするのではなく、undefinedとnullを区別して`!== null`と`!== undefined`を使い分けよ

以下、個人的感想
- 7: 意味を持たない型変数に関しては、意味を持たないことを表明するために一文字変数でいいと思う
    - まあ意味を持たない型変数を書く機会はさほど多くない
- 10: これは強いプログラマの間でも意見が分かれるところだと思う。
    - 「undefinedを使うな、nullを使え」「nullを使うな、undefinedを使え」の両方があり「両方の派閥がいるので二つを区別するな, `!= null`を使え」派もいる。see: [nullとundefined - TypeScript Deep Dive 日本語版](https://typescript-jp.gitbook.io/deep-dive/recap/null-undefined)
    - TypeScriptのstrictモードを前提にするならnullとundefinedの取り違えはコンパイラがチェックしてくれるはずであり、わざわざ緩い条件判断をする必要はない、というこの記事の主張は筋は通る。
    - 僕はTypeScriptを使い始めた時はこの辺りのことが良く分かってなかったけど、create-react-appでプロジェクトを作ったらデフォルトでこの件を警告してきたので早い段階で矯正された。see: [no-eq-null - Rules - ESLint](https://eslint.org/docs/rules/no-eq-null)
        - 今試したら警告されなかったたんだけど記憶違いなのか、警告しなくなったのか？
- 4, 6: これはやった方がベターであることに異論はないが、手間もだいぶ増えるので、トレードオフだと思う。
- 残りのところは特に異論はない
- やってみた [[2日掛けてanyを撲滅した]]
