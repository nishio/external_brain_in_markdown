---
title: "ppoi"
---

## ppoi(っぽい)

if文の条件式を明確に記述することはできないけど、良い例と悪い例は示せるってシチュエーションで、手軽に機械学習でそれっぽい判定をするのを支援するライブラリです。
[Github](https://github.com/nishio/ppoi)

メインスクリプトが `__init__.py` なので、チェックアウトしたディレクトリがそのままPythonのモジュールとしてインポート可能です。適当なわかりやすい名前にリネームすると良いです。例えばキーワードっぽいかどうかの判定をさせたいなら `mv ppoi keyword` とかやっておくと下記のように使えます。

python

```
if keyword.ppoi(something):
    print("{} is keyword-ppoi".format(something))
```


(というのを思いついたので面白がって作ったのだけど、冷静に考えると `import keyword` はbad nameな気がするので `to_bool` をつけた。 `keyword_ppoi.to_bool(something)` の方が良い)

`__init__.py` は直接実行可能です。 `--initialize` で実行すると良いです。
実行前に未判定の入力をunknowns.txtに入れておく必要があります。
- (これよく考えたら必須ではないので将来のバージョンでは変えときます)
- (そもそも__init__.pyを実行するんじゃなくて実行用のスクリプトを別途用意したほうがいい気がした)

samplesにキーワードかどうかの判定のためのサンプルデータが入っています。このサンプルの中身は1行1アイテムでキーワードかどうか判定したいデータの例が入っています。これはこのScrapboxのデータから角かっこで囲われている範囲を抽出したもので、まあ大体はキーワードなのだけども、ソースコード中の角かっこにも誤爆しているのでキーワードっぽくないものが混ざっています。
:

```
属人性の排除
自己紹介
0
音声入力
\r\n
${currentPageTitle}
[ 0.67869952,  0.35340645, -0.37436676,  0.50602025,  0.13514392
```


`cp samples/unknown.txt .` したら `python3 __init__.py --initialize` しましょう。そうすると、最低1行の「キーワードっぽい例」と最低1行の「キーワードっぽくない例」の入力を求めてきます。(Python3とNumPyとScikit-Learnがインストール済みであることを想定しています)

:

```
Enter at least one positive examples (empty to exit)
> 
```


適当に入力します
:

```
Enter at least one positive examples (empty to exit)
> 属人性の排除
> 自己紹介
>                    
Enter at least one positive examples (empty to exit)
> ${currentPageTitle}
> [ 0.67869952,  0.35340645, -0.37436676,  0.50602025,  0.13514392
> 
```


そうすると与えた例を元に「これはキーワードっぽいぞベスト5」と「これはキーワードっぽくないぞワースト5」と「どっちだかよくわからないぞ」を表示します。
:

```
BEST 5
良いアイデアは周囲の人を刺激し、自分で成長を始める: 0.7077
自由の本性: 0.7077
自分の生産性向上に責任を持つ: 0.7077
自信のない人ほど他人の悪口を言う: 0.7077
属人性の排除には二種類ある: 0.7077

WORST 5
https://speakerdeck.com/kazuph/builderscon-tokyo-2018-day1-chan-ye-degatili-yong-sareruraspberry-pifalsehua: 0.2073
http://d.hatena.ne.jp/nishiohirokazu/20111020/1319117086: 0.2073
Elemwise{minimum,no_inplace}.0, Subtensor{:int64:}.0, Subtensor{:int64:}.0, Subtensor{:int64:}.0, Subtensor{:int64:}.0, [* IncSubtensor{Set;:int64:}.0: 0.2230
http://wedge.ismedia.jp/articles/-/12062?layout=b: 0.2230
https://www.okudahiromi.com/blog/20180310/1923: 0.2230

LESS CONFIDENT
Facebookに慣れた人のためのkintone移行Tips: 0.4967
03 1 断片的情報の構造化_前振りと実録KJ法の流れ: 0.5056
03 2 断片的情報の構造化_KJ法の実践: 0.5056
0～1の実数を{0, 1}にする: 0.5056
DB Pressの記事への補足: 0.5056
```


結果を眺めて満足できたなら、早速使うことができます。
:

```
In [1]: import ppoi

In [2]: ppoi.ppoi("Hello")
Out[2]: False

In [3]: ppoi.ppoi("キーワードの抽出")
Out[3]: True
```


満足できなかったら、学習データを追加することになります。あとで解説している「対話的能動学習」を使うと手作業でファイル編集しなくていいのだけど、今回はLESS CONFIDENTの5つを全部positive.txtに貼り付けることにします。

データを変更したら `python3 __init__.py --learn` で再学習されます。このオプションは何も表示しないで再学習するだけで、この説明では面白くないので `python3 __init__.py --describe` で再度分析結果を表示させてみましょう。

結果はこうなりました
:

```
BEST 5
" 生物的に進化したソフトウェアは時々風邪みたいに具合悪くなって、ほっとくと治ったりするだろうね。あとは、要求仕様をきちんと死に結びつけられるかどうかの問題か。: 0.9511
企業のよい点は、利益という必要条件が存在することである。つまりは倒産する機能が内在化されていることである。倒産するという機能は、自由企業体制なる制度の最も優れた点である。: 0.9231
複数組織に属する人によって接続された組織の集合体: 0.9125
" 「（結果の平等性が一見高そうな）平等なルールでも格差が生じる、驚き」という主張で、カッコの中を暗黙的に主張しているので、「結果の平等性が低いWTAなら、格差が生じるよ」というツッコミはズレてない？という話。: 0.9081
私文書は、本人又はその代理人の署名又は押印があるときは、真正に成立したものと推定する。: 0.9025

WORST 5
 0.45792096,  0.20519401,  0.77490418, -0.08403411, -0.37505412: 0.2266
 0.50602025, -0.08403411,  0.68316922, -0.34559589,  0.38823327: 0.2266
-0.20123254,  0.07652205,  0.50049221,  0.38823327,  0.74325791: 0.2266
-0.26671759,  0.89310368, -0.08178549, -0.34559589,  0.07142937: 0.2266
-0.37436676,  0.77490418,  0.04681577, -0.08178549,  0.50049221: 0.2266

LESS CONFIDENT
Feeling of Knowing in Memory and Problem Solving: 0.5010
2018-03: 0.5013
harajune: 0.4984
the structure of consumption technology: 0.4984
Scrapbox Drinkup 20180810: 0.5019

```


今回BEST5に入ってきている`" `で始まる文章はインライン引用構文 で、こいつらは「先頭が `" ` だったらキーワードではない」と明確なルールで弾けるのでppoiの外でやると良いでしょう。ロジックで書けるものはロジックで書いた方が良い。

そういう明確なルールで弾くことができず、データを追加してもうまく分離することができないケースでは、特徴量を追加する必要があります。 `_make_features` が1行テキストを受け取ってnp.arrayを返す関数なので、そこに手を加えることになるでしょう。

今は入力が改行を含まない文字列である想定になってますが、その他のケースは、僕がその他のケースを扱うときに作ります。それまではとりあえずJSONにでもしておけば良いかと。

# 対話的能動学習
`--interactive`で起動すると、対話的に学習させることがきます。これはLESS CONFIDENTな順に表示され、対話的にpositiveかnegativeか答えていくと、それがデータファイルに追記されていく仕組みです。いわゆる能動学習です。

positiveとnegativeの他にneutralがあります。ぱっと見でpositiveかnegativeかわからなかったら、なんでもneutralに入れます。

:

```
$ python3 __init__.py --interactive
Feeling of Knowing in Memory and Problem Solving: 0.5010
negative(z), neutral(x), positive(c), quit(q)>c
Peter F. Drucker: 0.5023
negative(z), neutral(x), positive(c), quit(q)>c
virtual: 0.5014
negative(z), neutral(x), positive(c), quit(q)>x
https://www.okudahiromi.com/blog/20180310/1923: 0.5016
negative(z), neutral(x), positive(c), quit(q)>z
2015: 0.4997
negative(z), neutral(x), positive(c), quit(q)>c
Lancaster1966: 0.4972
negative(z), neutral(x), positive(c), quit(q)>c
https://scrapbox.io/cybozu-make-club/: 0.4986
negative(z), neutral(x), positive(c), quit(q)>z
Regret  Analysis  of  Stochastic  and  Nonstochastic  Multi-armed  Bandit  Problems: 0.4994
negative(z), neutral(x), positive(c), quit(q)>c
2018-03: 0.4981
negative(z), neutral(x), positive(c), quit(q)>c
data.Name=="1299c1b7a9e0c2bf41af69c449464a49": 0.5034
negative(z), neutral(x), positive(c), quit(q)>z
Habitica: 0.5075
negative(z), neutral(x), positive(c), quit(q)>c
Miller1956: 0.5078
negative(z), neutral(x), positive(c), quit(q)>c
72, 101, 108, 108, 111, 44, 32, 119, 111, 114, 108, 100, 33: 0.5032
negative(z), neutral(x), positive(c), quit(q)>z
```


現在の実装では、一つ回答するたびに、データファイルを更新して、それを読み直して再学習しています。これは、一つ教えると、類似のケースも判断できて「似たようなことを何度も聞く」ことがなくなるのですが、データが増えてくるとだんだん遅くなります。

やること
- 学習済みモデルのキャッシュ(そのために--learnを作ったので)
    - 今、ライブラリを単にインポートした場合も初回判定時に学習してモデルを作っている
    - 序盤のデータを作ってるフェーズでは毎回学習し直しても良いけど、データが増えてきた時とか、単なる利用のフェーズになった時に毎回学習するのは無駄なので--learnで明示的に再学習させる方が良いのではないか
    - 逆に、序盤は再学習の必要があるかどうか人間が考えるのも負担なので勝手にやった方が良い
- 特徴量の改良の仕方についての解説を作る

- --initializeで最初に"Enter at least one positive examples (empty to exit)"と聞かれるが、unknowns.txtから選んで質問してくれるバージョンが欲しい

