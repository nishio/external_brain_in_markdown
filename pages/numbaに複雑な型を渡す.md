
素直にnp.arrayにできるならそれが楽でいいのだけど、実用上は「キーが整数である辞書で、値は可変長のリスト。リストの要素は2整数のタプル」みたいな複雑な型のことがあり(実話)これをnp.arrayに詰め込もうとしてエンバグするのは不毛。

この型は、生のPythonの辞書やリストのままではnumbaでうまく扱えないのだが、typed.Dictとtyped.Listを使えば実現できる。問題はこれを関数に渡す時に関数の型シグニチャがどうなるか。

numba.typeofで調べると
- `DictType[int64,ListType[UniTuple(int64 x 2)]]`
と表示されるが、これをそのまま型シグニチャに書くと動かない。修正点は
- `UniTuple(int64 x 2)` → `UniTuple(int64, 2)`
- `XXXType[xxx]` → `XXXType(xxx)`
(たぶんこれ、パーサを作らないでevalで解決してる。だからPython的文法にする必要がある)

文字列にせず、typeofで推定させる手もある
python

```
@nb.jit(nb.typeof((1.0,1.0))(nb.double),nopython=True)
def f(a):
  return a,a
```


これで当初の目的である複雑な型の値をnumbaコンパイル済みの関数に渡すことができた。

追加: atcoderのnumbaは0.48と古いのでtyped.Listが引数を取れないようだ

python

```
import sys
import numba


def foo(x):
    for k in x:
        print("k:", k)
        for a, b in x[k]:
            print(a, b)


if sys.argv[-1] == "-c":
    # numba compile
    print("compiling")
    from numba.pycc import CC
    cc = CC('my_module')
    cc.export(
        'foo', 'void(DictType(int64,ListType(UniTuple(int64,2))))')(foo)
    cc.compile()
    exit()
else:
    x = numba.typed.Dict()
    x[1] = numba.typed.List([(1, 2), (3, 4)])
    x[100] = numba.typed.List([(100, 200)])

    if sys.argv[-1] == "-p":
        print(numba.typeof(x))
        # => DictType[int64,ListType[UniTuple(int64 x 2)]]
    else:
        from my_module import foo
        foo(x)
```


[[numba]]
