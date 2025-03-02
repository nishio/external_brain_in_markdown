
関数の中である名前への代入がある場合、その名前はその関数のローカル変数だと判定される
代入がある場合とない場合で、その変数の読み書きは異なるバイトコードへとコンパイルされる

python

```
In [1]: def foo():
   ...:     print(x)
   ...:     x = 10
   ...:     

In [2]: import dis

In [3]: dis.dis(foo)
  2           0 LOAD_GLOBAL              0 (print)
              2 LOAD_FAST                0 (x)
              4 CALL_FUNCTION            1
              6 POP_TOP

  3           8 LOAD_CONST               1 (10)
             10 STORE_FAST               0 (x)
             12 LOAD_CONST               0 (None)
             14 RETURN_VALUE

In [4]: def bar():
   ...:     print(x)
   ...:     

In [5]: dis.dis(bar)
  2           0 LOAD_GLOBAL              0 (print)
              2 LOAD_GLOBAL              1 (x)
              4 CALL_FUNCTION            1
              6 POP_TOP
              8 LOAD_CONST               0 (None)
             10 RETURN_VALUE
```


global宣言は関数内での代入の有無によらずLOAD_GLOBAL/STORE_GLOBALを強制する効果がある。

python

```
In [6]: def foo():
   ...:     global x
   ...:     print(x)
   ...:     x = 10
   ...:     

In [7]: dis.dis(foo)
  3           0 LOAD_GLOBAL              0 (print)
              2 LOAD_GLOBAL              1 (x)
              4 CALL_FUNCTION            1
              6 POP_TOP

  4           8 LOAD_CONST               1 (10)
             10 STORE_GLOBAL             1 (x)
             12 LOAD_CONST               0 (None)
             14 RETURN_VALUE
```


