
- [[日本語BERT]]の[[fine-tuning]]をする
- 手元でBERTの学習済みモデルをロードして文章をベクトル化して識別モデルを学習するところまではやってある
    - 72.1%だったのでこれをfine-tuningしてどこまで上がるか実験したい
- これを読む
    - [https://github.com/yoheikikuta/bert-japanese/blob/master/notebook/finetune-to-livedoor-corpus.ipynb](https://github.com/yoheikikuta/bert-japanese/blob/master/notebook/finetune-to-livedoor-corpus.ipynb)
- finetune-to-livedoor-corpus.ipynbを自分のGoogle Colab環境に複製
- GCPにおいてからgcutil cpするように書かれているが、Google Driveをマウントすることにした
    - [[Google ColabからDriveをみる]]
- run_classifierのオプション:
    - `--model_file=../model/wiki-ja.model \`
    - `--vocab_file=../model/wiki-ja.vocab \`
    - これらはSentencePieceのモデルを指定してる
        - ipynbの手順通りだとあらかじめGCPからColabのFSにコピーされている
        - 僕はやってないので、Google Driveから読むことにする
        - こうなった
            - `--model_file=/content/gdrive/My\ Drive/bert-wiki-ja/wiki-ja.model \`
            - `--vocab_file=/content/gdrive/My\ Drive/bert-wiki-ja/wiki-ja.vocab \`
            - `--init_checkpoint=/content/gdrive/My\ Drive/bert-wiki-ja/model.ckpt-1400000 \`
        - Google ColabのFSのルートは/contentなの
            - 相対パス起因の失敗をするのは嫌なので絶対パスにした
        - 注: BERTモデルの読み込みと結果の書き出し先はGCPでなければならない
            - init_checkpointはTPUが読もうとするので上記の書き方だと失敗する
            - [[TPUからGoogle ColabのローカルFSには書き込めない]]
- データの読み込みを行なっている場所
    - `train_examples = processor.get_train_examples(FLAGS.data_dir)`
        - processorは`processor = processors[task_name]()`しててコマンドライン引数で渡した`--task_name=livedoor`によって`LivedoorProcessor`が選択されている
        - `LivedoorProcessor`は`DataProcessor`を継承して親クラスのクラスメソッド`_read_tsv`を呼んでいるが、これは単にファイルを開いてTSVとして読んで各行をリストに入れて返すだけ
        - その結果を元に `LivedoorProcessor#_create_examples`の中で`InputExample`オブジェクトを作ってリストに入れている
        - `InputExample`は文章とラベルを持つ
- モデルの作成
    - `model_fn_builder(...)`で`model_fn`を作ってから、それを`tf.contrib.tpu.TPUEstimator`で包んで`estimator`と呼ぶ
        - [[学習済みモデルはどこで読むか]]
        - `model_fn_builder(...)`は`create_model`を呼ぶ
        - これはオリジナルのBERTモデルを作ってから`output_layer = model.get_pooled_output()`する
            - この`get_pooled_output`が何かは[[日本語BERTのrun_classifier読解#5db89bb6aff09e0000d4c214]]で説明した
        - `get_pooled_output`を入力とするシンプルなロジスティック回帰を実装しているように見えるが、なんで自前で実装する必要があったのかよくわからない
        - 将来的にはいろいろカスタマイズしたいが、今回は「そういうものだ」と認めて進むことにするか
        - 今回の僕のケースではラベルが0/1なのがちょっと違う点
- 実装
    - run_clussifier.pyをインポートして`LivedoorProcessor`相当のものを自作して、mainを書き換えてそれを呼ぶようにしよう
    - title(unique id)から本文への対応づけがhonbun_data.jsonに入っているのでこれを使う
    - `LivedoorProcessor`はそれぞれのメソッド呼び出しに応じて異なるファイルを読んでいるが、僕のケースでは1つ
        - クラスの外でデータを作っておいてメソッドは参照を返すだけにする
    - ネガポジのペアはnegaposi.jsonに入ってるのでこれを使う
    - > 将来的にはいろいろカスタマイズしたいが、今回は「そういうものだ」と認めて進むことにするか
        - これできないのではって気がしてきた
        - できなくはないが、2個の値のペアを受け取ってネガポジ判定するのをLRで実装するのは...
        - 組み合わせ素性がないので流石にダメでは...
        - まあ素朴な手段としてやっておくか
    - そもそも入力が2文であって、それぞれに`pooled_output`が必要か？
        - BERTのtext_aとtext_bに入れれば良いか
    - オリジナルの`_create_examples`では`tokenization.convert_to_unicode`してるけど、僕の場合0/1だからintで入れて大丈夫かな
- 少し走って死んだ
    - [[TPUからGoogle ColabのローカルFSには書き込めない]]
    - "service-***@cloud-tpu.iam.gserviceaccount.com does not have storage.objects.list access to ***.appspot.com."
        - ipynbの「TPUのチェック」と書かれたセルが、TPUに対してGCP Bucketのアクセス権を付与することまでやっている
        - うまくいかない場合はここが失敗しているので最初からやり直せば良い
:

```
***** Eval results *****
eval_accuracy = 0.9525939
eval_loss = 0.40050572
global_step = 1047
loss = 0.39979258
CPU times: user 2.1 s, sys: 313 ms, total: 2.41 s
Wall time: 7min 54s
```

classification_report

```
             precision    recall  f1-score   support

           0       0.94      0.96      0.95      1118
           1       0.95      0.94      0.95      1117

    accuracy                           0.95      2235
   macro avg       0.95      0.95      0.95      2235
weighted avg       0.95      0.95      0.95      2235
```

confusion_matrix

```
[[1068   50]
 [  68 1049]]
```

- ほんとなのかと眉に唾をつけたくなる

まとめ
- 6705件のデータを使ったBERTのfine-tuningがTPUを使うと7分程度でできる
- 72%→95%の精度
    - ![image](https://gyazo.com/e779e6a21c7867c92d9c4676110066cb/thumb/1000)
    - ただしBの処理結果をキャッシュできないという問題点がある
        - 計測してないけど処理にかかる時間が1〜2桁上がる懸念
        - 右の形を試したい
            - これは加算注意
        - 内積注意や次元削減注意を試したい
            - see [[CybozuHackathon2019]]
