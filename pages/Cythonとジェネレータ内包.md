
Cythonでジェネレータ内包表記を使ったら謎のエラー
`ret = max(get_longest(v, edges, longest) for v in edges[start]) + 1`
:

```
Fatal Python error: Acquisition count is 0 (line 17220)
Python runtime state: initialized

Current thread 0x00007f4b63c4a740 (most recent call first):
<no Python frame>
```


手軽な再現方法
- リンク1のコードと標準入力をリンク2のコードテストに入れる
    - [https://gist.github.com/nishio/c464319471c7382391424d60041da217](https://gist.github.com/nishio/c464319471c7382391424d60041da217)
    - [https://atcoder.jp/contests/dp/custom_test](https://atcoder.jp/contests/dp/custom_test)

ジェネレータ内包がダメわけではない
- 下記のコードでは引数longestがグローバルスコープに移った以外はほぼ同じなのにこのエラーが再現しない
    - [https://atcoder.jp/contests/dp/submissions/14913553](https://atcoder.jp/contests/dp/submissions/14913553)
    - たぶんジェネレータ内包をCに変換する際に、何か特定の条件で参照カウントの上げ下げを間違えてるのではないだろうか
    - ちなみに上記コードがTLEになってることから「動くけど遅い」ということがわかる
