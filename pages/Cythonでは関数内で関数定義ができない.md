
Numbaでは「再帰呼び出しでなければできる」Cythonでは「そもそもそこで定義できない」

AtCoderでの使用を考えると、Numbaは関数単位でコンパイルするので一つの関数にまとまっていて欲しいが、Cythonはファイル全体がCに変換されてコンパイルされるので素直にトップレベルに置いたらいい。

その場合、呼び出し元関数のローカル変数にアクセスできないので引数で渡すのか、グローバルに置く必要がある。そもそもPythonでグローバルに置くのを避けるのは生Pythonでローカル変数のアクセスがグローバル変数へのアクセスより速いからなので、Cythonで避ける理由はない。global宣言が有効なのは確認済み。
- 関連 [[Pythonでローカル変数はグローバル変数より速い]]

cython

```
def main():
  cdef foo(long x):
    if x == 0: return 0
    return foo(x - 1) + x
  return foo(1000000)

main()
```

NG: `C function definition not allowed here`

cython

```
cdef foo(long x):
  if x == 0: return 0
  return foo(x - 1) + x

def main():
  return foo(1000000)

print(main())
```

OK

[[Cython]]
