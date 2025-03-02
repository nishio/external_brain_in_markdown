
BERTを使って文章のベクトル埋め込みを得る場合に、first tokenのhidden stateを使うことが良いのか悪いのかという議論。

- create_pretraining_data.py
    - L271でおよそ0.5の確率でランダムな文を選んで2文目にする
        - [src](https://github.com/google-research/bert/blob/0fce551b55caabcfba52c61e18f34b541aef186a/create_pretraining_data.py#L271)
    - L130, L139で、ランダムな文であるかどうかはnext_sentence_labelsって名前で書き出される
        - [src](https://github.com/google-research/bert/blob/0fce551b55caabcfba52c61e18f34b541aef186a/create_pretraining_data.py#L139)
- run_pretraining.py
    - L144でmodel.get_pooled_output()とnext_sentence_labelsからlossを計算している
        - [src](https://github.com/google-research/bert/blob/e13c1f3459cc254f7abbabfc5a286a3304d573e4/run_pretraining.py#L144)
        - 具体的にはL285からのget_next_sentence_outputで計算している
            - hidden_size次元から2次元へのweight matrixと2次元のbiasがあって、入力に掛けて足してsoftmax
            - [src](https://github.com/google-research/bert/blob/e13c1f3459cc254f7abbabfc5a286a3304d573e4/run_pretraining.py#L285)
- modeling.py
    - このmodel.get_pooled_output()はfirst tokenのhidden stateにdenseを1回掛けたもの
        - [src](https://github.com/google-research/bert/blob/master/modeling.py#L225)
- pre-trainingの段階で2つの文が並びの文かランダムな文かの識別問題を解く際に、この768次元のpooled_outputだけを用いることで、このpooled_outputに「それを識別するための情報」が濃縮される
    - 2つの文が並びの文かランダムな文かを識別するためには「その文がどういう話題か」を抽出して、2つの文の話題が同一であるかどうかを判断することになる、なのでこの識別を解くことで「話題ベクトル」が抽出する
    - しかしこのネットワーク設計では、その「話題ベクトル」がpooled_outputに来る保証がない
        - 下位のネットワークで話題がつながっているかどうかの識別を済ませてしまい、pooled_outputに「Yes/No」だけが来ることも可能
        - これは下位のネットワークが両方の文を参照することができる注意機構を持っていることが原因
        - 文の埋め込みが欲しいのであれば、pre-trainingの段階でそれぞれの文は相手を見られない状態で学習し、それぞれの文のpooled_outputの内積を計算して識別に使うべきであった。
        - ![image](https://gyazo.com/3975480429dadf600bc752de564248bd/thumb/1000)
        - これなら内積で類似度を計算するのが適当であるようなベクトルがpooled_outputに出てくるはず
        - pre-trainingの段階で右の構造で学習すればよかったのだが、pre-trainingをやり直すのが高コストなので、右の構造で連続文識別問題を改めて解くことでfine-tuningするのがいいかも

-----
- そもそも文のベクトルが必要か？
    - 本当に欲しいのは複数の文からなる文章のベクトルなのでは？
    - もう1枚自己注意の層を重ねたらいい？
    - 「文のベクトルを作ろう」とか考えずに、使いたい目的に合わせてfine-tuningしたら良いのでは
