
BERT: Pre-training of Deep Bidirectional [[Transformer]]s for Language Understanding
[https://arxiv.org/abs/1810.04805](https://arxiv.org/abs/1810.04805)

解説スライド [[BERTとTransformer]]

[https://github.com/google-research/bert](https://github.com/google-research/bert)

2017年に[[RNN]]なし[[CNN]]なしで[[注意機構]]だけ構成された[[Transformer]]が翻訳タスクで良い成績を出すことが示された
> We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely.
[[BERT]]はその流れの延長線にある。

- Pre-trainingできるモデルを作った
- Pre-trainingしたモデルに出力層を付け加えるだけで、言語理解系の12種類のタスクにおいて良い成績を出すことができた
- Transformer

画像認識系タスクで、学習済みモデルを使って分野応用が容易にできるようになったのと同じような流れが、今後自然言語処理に起きる可能性が高い。(しかし日本語とかいうマイナーな言語はどうなるか…)(はっ、むしろ国プロでいい感じの学習済みモデルを作って無償で配布してくれたらいいのか？)(オリンピック前に間に合わせるつもりでぜひ)

> BERT: Bidirectional Encoder Representations from Transformers.

> proposing a new pre-training objective: the “masked language model” (MLM), inspired by the Cloze task (Taylor, 1953).
- Cloze taskはいわゆる穴埋め問題

> we also introduce a “next sentence prediction” task that jointly pre-trains text-pair representations.

Transformerの実装はオリジナルの`tensor2tensor`ライブラリを使っていて、しかも何もいじってない

[The Annotated Transformer](http://nlp.seas.harvard.edu/2018/04/03/attention.html)

単語はWordPieceで`he likes play ##ing`と分割されて、位置と文番号の情報が埋め込まれている
ランダムに15%をマスクして、マスクされたものを予想するタスク。
- 全てをMASKトークンにはしない
- 15%のうちの80%をMASK、10%をランダムな単語、10%を元どおりの単語にする
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>一見普通の単語でも、あとで質問されるかもしれないわけだ


- [[Curriculum Learning]]に相当することが起きているのではないか
    - [[MaskLM]]の学習が、他のタスクよりイージー

[https://twitter.com/_Ryobot/status/1050925881894400000](https://twitter.com/_Ryobot/status/1050925881894400000)

[汎用言語表現モデルBERTを日本語で動かす(PyTorch) - Qiita](https://qiita.com/Kosuke-Szk/items/4b74b5cce84f423b7125)
