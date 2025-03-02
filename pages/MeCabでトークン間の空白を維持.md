
トークンに刻んだものを再度結合したら元に戻って欲しい
python

```
>>> concat_tokens(tokenize("This is a pen"))
'This is a pen'
```

でもMeCabのnode.surfaceは空白を含まないので、よくやる方法では'Thisisapen'になってしまう。
この問題を解決した。

[MeCab: 出力フォーマット](https://taku910.github.io/mecab/format.html)に`%M 形態素の表層文字列, ただし空白文字も含めて出力`があるので、解析後のノードがこれを表示するのに必要な情報を持っているはずと考えた
- [code](https://github.com/taku910/mecab/blob/3a07c4eefaffb4e7a0690a7f4e5e0263d3ddb8a3/mecab/src/writer.cpp#L280)
cpp

```cpp
case 'S': os->write(reinterpret_cast<const char*>
                    (node->surface -
                     node->rlength + node->length),
                    node->rlength - node->length);
```

- というわけで手前の空白自体を持っているのではなく、node.rlengthが空白も含んだ長さを持っている
- 元の文字列をみないと実際にトークンの直前にあって無視された文字がどんなものかはわからない

python

```
word = node.surface
# keep whitespace before token
wslength = node.rlength - node.length
ws = s[start:start+wslength]
word = ws + word
```

