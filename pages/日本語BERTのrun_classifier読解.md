
[[日本語BERT]]のrun_classifier読解
[https://github.com/yoheikikuta/bert-japanese/blob/master/src/run_classifier.py](https://github.com/yoheikikuta/bert-japanese/blob/master/src/run_classifier.py) を読んでいる
- 本家のbertリポジトリをgit submoduleで取り込んでいる
    - それをsys.pathに追加してimport modelingとかで再利用している
    - BERTのモデル定義などはそちらに書かれている
    - 関連: [[VSCodeでsys.path設定より前にimportが移動される]]
- このrun_classifier.pyは本家のrun_classifier.pyを元にSentencePieceを使うなどの修正を加えたもの

- tf.app.run()がmainを呼ぶ
- main→model_fn_builder→create_model
- create_modelの中の
    - `model = modeling.BertModel(...)`
    - ここでBERTのモデルを作ってる
        - 本家BERTリポジトリからmodelingをimportしてある
        - BERTのネットワーク構造の定義はそちらでされている
            - [https://github.com/google-research/bert/blob/88a817c37f788702a363ff935fd173b6dc6ac0d6/modeling.py#L31](https://github.com/google-research/bert/blob/88a817c37f788702a363ff935fd173b6dc6ac0d6/modeling.py#L31)
    - コメント
        - >  # In the demo, we are doing a simple classification task on the entire segment.
        - >  # If you want to use the token-level output, use model.get_sequence_output() instead.
        - get_pooled_output()を使っている
        - これは何か
            - 先頭トークンに対する出力を入力としてhidden_sizeの出力を出す単なる全結合レイヤー
python

```
# The "pooler" converts the encoded sequence tensor of shape
# [batch_size, seq_length, hidden_size] to a tensor of shape
# [batch_size, hidden_size]. This is necessary for segment-level
# (or segment-pair-level) classification tasks where we need a fixed
# dimensional representation of the segment.
     with tf.variable_scope("pooler"):
       # We "pool" the model by simply taking the hidden state corresponding
       # to the first token. We assume that this has been pre-trained
       first_token_tensor = tf.squeeze(self.sequence_output[:, 0:1, :], axis=1)
       self.pooled_output = tf.layers.dense(
           first_token_tensor,
           config.hidden_size,
           activation=tf.tanh,
           kernel_initializer=create_initializer(config.initializer_range))
```

        - 「えっ、先頭トークンでいいの？文末トークンがいいのでは？」と思ったが正しくない
            - RNN的なメンタルモデルを引きずっている
            - BERTは[[自己注意]]を積み重ねた構造をしている
                - 一つ一つの自己注意は下位レイヤーに対する不定長のコンボリューションとして働く
                - なので先頭とか文末とか関係ない
        - 先頭トークンの出力はその単語自体に関する情報と文章全体の情報が詰め込まれるのか、大変だな、と思った
            - 正しくない
            - 先頭にはCLSトークンがあるので単語ではない
                - `tokens:   [CLS] the dog is hairy . [SEP]`
                - [src](https://github.com/yoheikikuta/bert-japanese/blob/df61ef5065100c8f8df4f01728020e399b4326da/src/run_classifier.py#L283)
        - 先頭トークンに対する出力を文のベクトル埋め込みだと解釈して良いのか、という議論
            - [Features extracted from layer -1 represent sentence embedding for a sentence? · Issue #71 · google-research/bert](https://github.com/google-research/bert/issues/71)
                - Why not use the hidden state of the first token as default strategy, i.e. the `[CLS]`?
                    - [Frequently Asked Questions — bert-as-service 1.6.1 documentation](https://bert-as-service.readthedocs.io/en/latest/section/faq.html#why-not-use-the-hidden-state-of-the-first-token-as-default-strategy-i-e-the-cls)
                - Why not the last hidden layer? Why second-to-last?
                    - [Frequently Asked Questions — bert-as-service 1.6.1 documentation](https://bert-as-service.readthedocs.io/en/latest/section/faq.html#why-not-the-last-hidden-layer-why-second-to-last)
            - 僕の結論はNOになった: [[BERTの文ベクトル]]
- l.728 `use_one_hot_embeddings=FLAGS.use_tpu)` これは正しいか？
    - 正しい
    - TPU上ではそれが早い、と[src](https://github.com/yoheikikuta/bert-japanese/blob/59e306faffe8e77dbf7347c8bb75c09ecfa8a1dc/src/extract_features.py#L80)に書いてあった

- tf.flagsはTensorflow 2.0にはない
    - `AttributeError: module 'tensorflow' has no attribute 'flags'`
    - argparseに置き換えるべき

- Tensorflow 2に移植するには、割と修正箇所が多いので、面倒だからvenvでTF 1の環境を作ることにした
:

```
  python3 -m venv ./venv
  source ./venv/bin/activate
  pip install --upgrade pip
  pip install tensorflow==1.15rc2
  pip install -r ../requirements.txt
```


- tokenize
    - `tokenization_sentencepiece.FullTokenizer(model_file="../model/wiki-ja.model", vocab_file="../model/wiki-ja.vocab")`
    - `In [9]: tok.tokenize("本日は晴天なりインターナルサーバーエラー")  `
    - `Out[9]: ['▁本', '日', 'は', '晴', '天', 'なり', 'インター', 'ナル', 'サーバー', 'エラー']`

- bert_config_file
    - --bert_config_file= ... にconfig.jsonを指定する必要があるがリポジトリに見つからない件
    - config.iniがある
    - run_classifier.pyの冒頭でiniからjsonを生成している
    - これをconfig.jsonって名前で保存しておくことにした

- ValueError: Couldn't find 'checkpoint' file or checkpoints in given directory ../model
    - ダウンロードした`model.ckpt-1400000.*`を../modelに置いて`--init_checkpoint=../model`したんだが...
    - `--init_checkpoint=../model/model.ckpt-1400000`が正解

- extract_feature.pyは動いた
    - コマンドはこんな感じ
        - `$ python3 extract_features.py --model_file=../model/wiki-ja.model --vocab_file=../model/wiki-ja.vocab --input_file=smallinput.txt --bert_config_file=config.json --init_checkpoint=../model/model.ckpt-1400000 --output_file=tmp/output`
        - --output_fileで指定したファイル名でJSONが吐き出される
python

```
x = json.load(open("tmp/output"))
In [8]: x["features"][2]["token"]                                                                                                                      
Out[8]: '正しい'
In [10]: x["features"][2]["layers"][0]                                                                                                                 
Out[10]: 
{'index': -1,
 'values': [-0.433769, ...]}
```

        - 各トークンごとに768次元のベクトルが入っている
            - (不用意にでかいファイルに対して使ったらものすごくでかいJSONができてしまうのでは)
        - 文に対するベクトルが欲しい僕にとってはlayer -1の最初のトークンのベクトルだけ取り出せば良いか

- read_examples
    - ` ||| `で区切られている場合には２文のペアとみなし、そうでなければ１文と判断
    - 自前のデータを流し込みたい場合、テキストから読むのではなくmainの中のread_examplesを呼んでるところを差し替えるのが良さそうって思った
        - 元データとしてScrapboxのJSONファイルを使いたいから

- extract_feature.pyをインポートしてmainを上書きした
    - 6343件のベクトル化に8245秒
    - MacBook Pro (15-inch, 2018) / 2.6 GHz Intel Core i7 / 16 GB 2400 MHz DDR4

- 実験に関するメモ: [[リンク作成支援]]

- run_classifier.py の、追加学習してfine-tuningするのはまだ試してない
    - 試したら[[日本語BERTのfine-tuning]]に書く
