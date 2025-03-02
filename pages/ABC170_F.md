
[[atcoder]] [F - Pond Skater](https://atcoder.jp/contests/abc170/tasks/abc170_f)  [[ABC170]]
- 解説の通り位置と向きを頂点として[[ダイクストラ法]] #長方形グラフ探索
- 1コストでKマス進めるのに1歩ずつ進むのを疑問に思って解説を無視してみたが、ダメだった
    - 探索の1ステップでKマス進むとTLEになるため、1マスずつ探索する必要がある
- 1マスずつ進む場合、直前に進んだ向きと同じ向きかどうかでコストが変わるので頂点が向きを持つ必要がある
- グラフを作ってからダイクストラするのではたぶん遅いので、作りながらやる
- コストは1/K単位になる。浮動小数点数だと誤差が心配なので整数部と分子の2つの整数で持つ
- 上記の実装をした段階で8TLE
    - まめな高速化が面倒なので[[numba]]に初挑戦、事前にコンパイルするスタイル
        - inputは型不明で使えないので読んでからコンパイルした関数に渡す
        - 地図データは番兵付きで通行可能boolの配列にする
            - 衝突チェックと範囲内チェックが一本化できる　see[[番兵付きの一次元配列]]
        - numbaでdefaultdictは使えない
            - dictにしたがgetがらみで型エラーが起きる
            - そもそもタプルをキーにすると型エラーなので整数にパックする必要がある
            - じゃあ素直に配列使おう
- 通常は90度ターンだけで良いが、初手だけは真後ろに進む可能性があることを見落としていて2WA
    - 初回だけ5番目の向きにしたが、始状態を90度回転した2つにすればよかっただけかも
その他
- TLEの時の消費時間は実行完了前に打ち切られているので参考にならない

-----
解説によれば[[ダイクストラ法]]とのこと。
- 明示的に頂点と辺を構築するとコスト高そうなので、必要に応じてその場で構築することにした。

一度コストの和ではなくパスを構成する辺の数を返してしまいWA
- 直してTLE [https://atcoder.jp/contests/abc170/submissions/14474187](https://atcoder.jp/contests/abc170/submissions/14474187)
- PyPy3で3314 ms、タイムリミットを1割ほど超過している(誤解A)
- とりあえず全部mainで包んで[[line_profiler]]したが、のっぺりと遅いのでどうしたものやら。他の人のコードを読んでみよう。

python

```
if sys.argv[-1] == 'ONLINE_JUDGE':
    from numba.pycc import CC
    cc = CC('my_module')
    cc.export('main', '(b1[:],i8,i8,i8,i8,i8)')(main)
    cc.compile()
    exit()
from my_module import main
```

[https://atcoder.jp/contests/abc170/submissions/14405996](https://atcoder.jp/contests/abc170/submissions/14405996)
なんと。 [[numba]]で事前にコンパイルしてる。

今、直進していけるところまでは進んでる
- それだと面積100万以下の制約がついてるのに、1歩進むコードがその何百倍もの回数呼ばれてしまう。
- `    49  20156497   22145363.0      1.1     11.3                  nx += dx`
- 解説に「位置と向きを頂点」にすると書いてあったが理由が分からなくて無視してた

こんな状態で1割程度遅いだけとは思えないな？
- > PyPy3で3314 ms、タイムリミットを1割ほど超過している。(誤解A)
- →これはTLEしてちょっとのところで打ち切られてる
    - 実際にはどれくらい縮める必要があるのかはここからは読み取れない
- サーバで2174 msのものを手元で走らせてみたら14.450sだった。
    - 7倍遅いので、手元で21秒で終わるようにしないといけないのか。

向き変更時の距離の更新が間違ってたバグを直してサブミット、WA
- killer01が手元で18秒、killer02が36秒なのでどっちみちTLE

WAの原因は距離が2つの数のタプルになったのに到達不能の判定が1つの数との比較のままだったから。
- killer04が24秒
- うーん、やっぱり[TLE](https://atcoder.jp/contests/abc170/submissions/14488691)
- killer_03.txt
:

```
7.3          (d, frac), (frm, direction) = heappop(queue) 

8.5          for dir in range(4):
6.0              if dir == direction:

5.3              if nx < 1 or H < nx or ny < 1 or W < ny:

7.7              dp(nx, ny, mapdata[nx - 1][ny - 1])

5.4              if mapdata[nx - 1][ny - 1] == leaf:

5.7              if distances[to] > newdist:
```

デバッグプリントの消し忘れはコメントアウトする
- デバッグモード以外ではデバッグ出力しない設計にしてたんだけど、引数の評価は行われちゃう
- [[デバッグプリントのコメントアウト]]

4方向から今向いてる方向を取り除いたものを実行してるけど、このループは砕いた方がいいかも。
- x,yの片方は更新しなくてよくなる
- 画面内外チェックのコストも半分になる。
    - (追記: ループアンローリングしたので1/4になった)

トータル実行時間が80秒から27秒になった。サブミットしてみよう。
- あっ、またWAになってしまった
- ループアンローリングした時にcontinueを対処し忘れて後半が実行されないバグ
- 直してサブミット、8件TLE
    - タプルを整数に置き換えるかな…と思ってるけど、計測なしに憶測で高速化してはいけない
:

```
11.1          (d, frac), (frm, direction) = heappop(queue)
```

    - うーん、まあ、そうですよね…
    - この辺を直していくの、あんまりやる気が起きないなぁ

[[numba]]を試そう！

inputは型が不明と言われるのでmainの外で読み込んでから渡す
- `Untyped global name 'input': cannot determine Numba type of <class 'builtin_function_or_method'>`

マップはどうやって渡してるかな？ああ、なるほど、番兵付きの一次元配列にするのか。
- [[番兵付きの一次元配列]]
- `b1[:]`

Untyped global name 'defaultdict': cannot determine Numba type of <class 'numba.core.ir.UndefinedType'>
- グローバルでインポートした値が使えない？
- 関数内でインポートする？

`Use of unsupported opcode (IMPORT_NAME) found`
- うーむ、関数内でのインポートはできないのか、defaultdictはさておきheapqを自前で実装するのはやりたくないなぁ
    - あれ？使ってはいるな？
    - heapqはできる
    - defaultdictだけがダメなのか？
- [Supported NumPy features — Numba 0.50.0.dev0+236.g64fbf2b-py3.7-linux-x86_64.egg documentation](https://numba.pydata.org/numba-doc/dev/reference/numpysupported.html)

結局タプルをキーにするのはダメ
っぽい
- `No implementation of function Function(<built-in function setitem>) found for signature:`
- `>>> setitem(DictType[Tuple(UniTuple(int64 x 2), int64),UniTuple(int64 x 2)], Tuple(UniTuple(int64 x 2), Literal[int](0)), none)`
- intとstrだけってみた気がする
- それを直して、minの引数をリストにした。

defaultdictをやめたことによるキーエラーはコンパイルした状況ではどこで起きたか分からないので、Pythonモードで実行

`'NoneType' object has no attribute 'args'`という謎のエラー
- 本体のバグでした
    - [https://github.com/numba/numba/issues/5896](https://github.com/numba/numba/issues/5896)

辞書からのgetで型がおかしくなるっぽいので、辞書からのgetをしないようにリストで実装し直した
- TLEなし2WAまで来た
    - killer_04.txt
    - rand_1000_03.txt
- この2件に関して正しい答えより1多く答えている

高速化の過程で90度のターンしかしなくなったことにより、初手が真後ろの盤面において1つ多く答えていた
- AC 881ms [https://atcoder.jp/contests/abc170/submissions/14505545](https://atcoder.jp/contests/abc170/submissions/14505545)

初回だけ5番目の向きにしたが、始状態を90度回転した2つにすればよかっただけかも
- AC 844 ms [https://atcoder.jp/contests/abc170/submissions/14516254](https://atcoder.jp/contests/abc170/submissions/14516254)
