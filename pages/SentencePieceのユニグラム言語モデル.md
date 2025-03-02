
[[SentencePiece]]のユニグラム言語モデルについて
- ![image](https://gyazo.com/60c096fa001c7a81578e8c1e99c021e7/thumb/1000)
[[サブワード正則化]]: 複数のサブワード分割候補を用いたニューラル機械翻訳 [[工藤 拓]] 2008
- [http://www.anlp.jp/proceedings/annual_meeting/2018/pdf_dir/B1-5.pdf](http://www.anlp.jp/proceedings/annual_meeting/2018/pdf_dir/B1-5.pdf)
- 例えば、文字列ABCがあって、語彙集合に各文字とABとが入っている場合に$p(AB) > p(A)p(B)$が成り立つなら"AB/C"の分割の方が"A/B/C"の分割よりもP(x)が大きくなる
- で、この手法だとVを事前に与える必要があるため、十分に大きな語彙からスタートして刈り込んで行く
    - ![image](https://gyazo.com/3de118fd9537e450c1e530d352ddf00d/thumb/1000)

Subword regularization: Improving neural network translation models with multiple subword candidates. In Proc. of ACL.
[https://aclweb.org/anthology/P18-1007](https://aclweb.org/anthology/P18-1007)

SentencePiece: A simple and language independent subword tokenizer and detokenizer for Neural Text Processing
Taku Kudo, John Richardson (Submitted on 19 Aug 2018)
[https://arxiv.org/abs/1808.06226](https://arxiv.org/abs/1808.06226)
