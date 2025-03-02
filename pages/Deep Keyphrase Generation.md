---
title: "Deep Keyphrase Generation"
---

- [https://arxiv.org/abs/1704.06879](https://arxiv.org/abs/1704.06879)
- Mui Meng+
- [[文中に出現しないキーフレーズ]]を生成することができる


- 入力単語列の入力を受けてキーフレーズを出力するEncoder-Decoderを作成
- 隠れ層 $\mathbf{h}_t = f(x_t, \mathbf{h}_{t-1})$
- context vector $\mathbb{c} = q(h_1, ..., h_T)$

- Gated recurrent unit(GRU)を使う
- $\mathbf{c}_i = \sum_{j=1}^T \alpha_{ij}h_j$
- $\alpha_{ij} = { \exp(a(s_{i-1}, h_j)) \over \sum_{k=1}^T \exp(a(s_{i-1}, h_j)) }$

- Copying Mechanism
    - 語彙の数を減らすために、例えば頻出30000単語だけを使って、残りは未知語として無視する、などが行われる。
    - しかし、単語自体が未知であっても、周辺の文脈からそれがキーワードだと分かるケースがある。
    - Copying Mechanismはソーステキストに含まれる未知語を選択することができるようにするメカニズム



実装
- [https://github.com/memray/seq2seq-keyphrase](https://github.com/memray/seq2seq-keyphrase)
- とりあえず作者らのデータで動かしてみよう
- 追加で必要なライブラリ
    - nltk
    - hickle
    - fuel
    - Resource punkt not found.
        - Please use the NLTK Downloader to obtain the resource:
        - nltk.downloadする
    - from theano.compile.nanguardmode import NanGuardMode
        - ImportError: No module named nanguardmode
        - 0.7.0以上にアップグレード
    - deepdish
- 'seq2seq-keyphrase/dataset/keyphrase/punctuation-20000validation-20000testing/all_600k_dataset.pkl'がないといけない
    - 'seq2seq-keyphrase/keyphrase/dataset/keyphrase'に置いてしまった
    - unzipしたところからmoveしてしまってたので今から分離するの何なのでシンボリックリンクで解決

:

```
Use Coverage Trick!
01/01/2018 21:46:12 [INFO] covc_encdec: adjust decoder ok.
args=()
kwargs={'clipnorm': 0.1}
{'beta_1': 0.9, 'beta_2': 0.999, 'epsilon': 1e-08, 'self': <emolga.basic.optimizers.Adam object at 0x7f08ad9b0150>, 'args': (), 'rng': <theano.sandbox.rng_mrg.MRG_RandomStreams object at 0x7f08cadadb10>, 'lr': 0.0001, 'kwargs': {'clipnorm': 0.1}, 'save': False}
01/01/2018 21:46:12 [INFO] covc_encdec: build ok.
01/01/2018 21:46:14 [INFO] covc_encdec: total number of the parameters of the model: 78835750
Traceback (most recent call last):
  File "keyphrase_copynet.py", line 264, in <module>
    agent.compile_('all')
  File "/home/nishio/find_keyphrases/seq2seq-keyphrase/emolga/models/covc_encdec.py", line 1849, in compile_
    self.compile_train()
  File "/home/nishio/find_keyphrases/seq2seq-keyphrase/emolga/models/covc_encdec.py", line 1880, in compile_train
    logPxz, logPPL     = self.decoder.build_decoder(target, cc_matrix, code, c_mask)
  File "/home/nishio/find_keyphrases/seq2seq-keyphrase/emolga/models/covc_encdec.py", line 996, in build_decoder
    non_sequences=[context, c_mask, context_A]
  File "/usr/local/lib/python2.7/dist-packages/theano/scan_module/scan.py", line 1076, in scan
    scan_outs = local_op(*scan_inputs)
  File "/usr/local/lib/python2.7/dist-packages/theano/gof/op.py", line 615, in __call__
    node = self.make_node(*inputs, **kwargs)
  File "/usr/local/lib/python2.7/dist-packages/theano/scan_module/scan_op.py", line 546, in make_node
    inner_sitsot_out.type.dtype))
ValueError: When compiling the inner function of scan the following error has been encountered: The initial state (`outputs_info` in scan nomenclature) of variable IncSubtensor{Set;:int64:}.0 (argument number 5) has dtype float32, while the result of the inner function (`fn`) has dtype float64. This can happen if the inner function of scan results in an upcast or downcast.
python keyphrase_copynet.py  177.96s user 9.00s system 93% cpu 3:19.28 total
```


:

```
(Pdb) print inner_sitsot_out
Elemwise{mul,no_inplace}.0
(Pdb) print outer_sitsot
IncSubtensor{Set;:int64:}.0
```


:

```
(Pdb) print scan_inputs
[Elemwise{minimum,no_inplace}.0, Subtensor{:int64:}.0, Subtensor{:int64:}.0, Subtensor{:int64:}.0, Subtensor{:int64:}.0, [* IncSubtensor{Set;:int64:}.0], IncSubtensor{Set;:int64:}.0, IncSubtensor{Set;:int64:}.0, Elemwise{minimum,no_inplace}.0, Elemwise{minimum,no_inplace}.0, dec_cell_Wz, dec_cell_bz, source_attention_Wa, source_attention_Ua, source_attention_Ca, source_attention_va, dec_cell_Cz, dec_cell_Uz, dec_cell_Wh, dec_cell_bh, dec_cell_Ch, dec_cell_Wr, dec_cell_br, dec_cell_Cr, dec_cell_Ur, dec_cell_Uh, dec_hidden_readout_W, dec_hidden_readout_b, dec_context_readout_W, dec_context_readout_b, dec_prev_word_readout_W, dec_prev_word_readout_b, out-trans_W, out-trans_b, Join.0, Elemwise{Cast{float32}}.0, Elemwise{tanh,no_inplace}.0]
```


:

```
> /home/nishio/find_keyphrases/seq2seq-keyphrase/emolga/models/covc_encdec.py(996)build_decoder()
-> non_sequences=[context, c_mask, context_A]
```


:

```
992             outputs, _ = theano.scan(
993                 _recurrence,
994                 sequences=[X, X_mask, LL, XL_mask],
995                 outputs_info=[Init_h, Init_a, coverage, None, None],
996  ->             non_sequences=[context, c_mask, context_A]
997             )

```


:

```
(Pdb) print X
InplaceDimShuffle{1,0,2}.0
(Pdb) print X_mask
InplaceDimShuffle{1,0}.0
(Pdb) print LL
InplaceDimShuffle{1,0,2}.0
(Pdb) print XL_mask
InplaceDimShuffle{1,0}.0
(Pdb) print Init_h
Elemwise{tanh,no_inplace}.0
(Pdb) print Init_a
Alloc.0
(Pdb) print coverage
Alloc.0
(Pdb) print context
Join.0
(Pdb) print c_mask
Elemwise{Cast{float32}}.0
(Pdb) print context_A
Elemwise{tanh,no_inplace}.0
(Pdb) print c_mask.type
TensorType(float32, matrix)
```


> This can happen if the inner function of scan results in an upcast or downcast.

cmaskが怪しいかな

:

```
(Pdb) w
  /usr/lib/python2.7/pdb.py(1314)main()
-> pdb._runscript(mainpyfile)
  /usr/lib/python2.7/pdb.py(1233)_runscript()
-> self.run(statement)
  /usr/lib/python2.7/bdb.py(400)run()
-> exec cmd in globals, locals
  <string>(1)<module>()
  /home/nishio/find_keyphrases/seq2seq-keyphrase/keyphrase/keyphrase_copynet.py(1)<module>()
-> import logging
  /home/nishio/find_keyphrases/seq2seq-keyphrase/emolga/models/covc_encdec.py(1849)compile_()
-> self.compile_train()
  /home/nishio/find_keyphrases/seq2seq-keyphrase/emolga/models/covc_encdec.py(1880)compile_train()
-> logPxz, logPPL     = self.decoder.build_decoder(target, cc_matrix, code, c_mask)
  /home/nishio/find_keyphrases/seq2seq-keyphrase/emolga/models/covc_encdec.py(996)build_decoder()
-> non_sequences=[context, c_mask, context_A]
  /usr/local/lib/python2.7/dist-packages/theano/scan_module/scan.py(1076)scan()
-> scan_outs = local_op(*scan_inputs)
  /usr/local/lib/python2.7/dist-packages/theano/gof/op.py(615)__call__()
-> node = self.make_node(*inputs, **kwargs)
> /usr/local/lib/python2.7/dist-packages/theano/scan_module/scan_op.py(546)make_node()
-> inner_sitsot_out.type.dtype))
```


:

```
scan(fn, sequences=None, outputs_info=None, non_sequences=None, n_steps=None, truncate_gradient=-1, go_backwards=False, mode=None, name=None, profile=False, allow_gc=None, strict=False, return_list=False)
    This function constructs and applies a Scan op to the provided

```


:

```
992             outputs, _ = theano.scan(
993                 _recurrence,
994                 sequences=[X, X_mask, LL, XL_mask],
995                 outputs_info=[Init_h, Init_a, coverage, None, None],
996  ->             non_sequences=[context, c_mask, context_A]
997             ) 
```


outputs_infoが問題だと言われているのだが…

:

```
(Pdb) print Init_a.type
TensorType(float32, matrix)
(Pdb) print Init_h.type
TensorType(float64, matrix) 
```


はー、確かに不穏な感じ。Init_aの側がおかしいのかな。

:

```
   Init_h   = self.Initializer(context[:, 0, :])  # initialize hidden vector by converting the last state
   Init_a   = T.zeros((context.shape[0], context.shape[1]), dtype='float32') # (batch_size, src_len)
   coverage = T.zeros((context.shape[0], context.shape[1]), dtype='float32') # (batch_size, src_len)
```


そこを64にしても
:

```
ValueError: When compiling the inner function of scan the following error has been encountered: The initial state (`outputs_info` in scan nomenclature) of variable IncSubtensor{Set;:int64:}.0 (argument number 5) has dtype float32, while the result of the inner function (`fn`) has dtype float64. This can happen if the inner function of scan results in an upcast or downcast.
```

エラーに変化はないなぁ。

ほかにも何カ所かfloat32が指定されているところがある。おそらく宣言していない時に作者らの環境ではfloat32になるが、筆者の環境ではfloat64になるとかだろう。デフォルトの型を指定できるかな？

[http://deeplearning.net/software/theano/library/config.html#config.floatX](http://deeplearning.net/software/theano/library/config.html#config.floatX)
> config.floatX
> String value: 'float64', 'float32', or 'float16' (with limited support)
> Default: 'float64'
これを指定してみよう

エラーの種類が変わった
:

```
  File "/usr/local/lib/python2.7/dist-packages/numpy/core/_methods.py", line 26, in _amax
    return umr_maximum(a, axis, None, out, keepdims)
ValueError: zero-size array to reduction operation maximum which has no identity
```


