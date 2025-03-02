---
title: "RAKE実験1"
---

[[RAKE]]
:

```
input:
Wikipediaのダンプデータを眺めてたのだけど、リンク記法はSentencePieceでもいい感じに1トークンになってたのでこれを使うことができそう。前処理を色々やらないといけないけど。
```


SentencePiece / 100 document stoplist
:

```
output:
リンク記法はsentencepiece:      81.00
wikipedia:      25.00
ダンプデータを眺め:     16.00
1トークンになって:      16.00
色々:   4.00
前処理: 4.00
もいい感じ:     4.00
ことができそう: 4.00
```


- "リンク 記 法は S ent ence P ie ce"
- "W i ki pe dia"
- 5トークンに分かれてる「Wikipedia」を正しく束ねている
- 「法は」が1トークンのせいでストップリストから漏れている
    - ストップリストがWikipedia100ページ分程度しか使ってないから、もっと増やせばストップリストに入る可能性はある
    - そもそも「リンク記法」がキーワード入って欲しいのでSentencePieceの刻み方が不適切かも
        - BERT日本語モデルの時に使ったvocab_size: 32000のやつなのでトークンが大きすぎるのかも

Mecab / 1000 document stoplist
:

```
いけないけど:   7.50
やらない:       4.50
前処理: 4.00
リンク記法:     4.00
のでこれ:       4.00
できそう:       4.00
1トークン:      4.00
なって: 3.50
けど:   2.00
て:     1.50
ダンプデータ:   1.00
こと:   1.00
いい:   1.00
wikipedia:      1.00
sentencepiece:  1.00
```


- 「いけないけど」「やらない」「のでこれ」「できそう」
    - これは確かにWikipediaにはあまり出てこなさそう
- 他に残念なところ
    - WikipediaやSentencePieceがスコア低くなってしまう
    - MeCabだと[[一単語なのでスコア低くなる]]

Mecab / 1000 document stoplist / use average phrase-character-length instead of average pharase-token-length
:

```
いけないけど:   15.00
sentencepiece:  13.00
リンク記法:     10.00
1トークン:      10.00
やらない:       9.00
wikipedia:      9.00
のでこれ:       8.00
できそう:       8.00
前処理: 6.00
ダンプデータ:   6.00
なって: 5.00
けど:   4.00
て:     2.00
こと:   2.00
いい:   2.00
```

