
[[Cython]]で添え字を型宣言しただけでは[[PyPy]]と比べて速くない
- アクセス対象がPythonのリストやarray、Numpyのarrayでは添え字オブジェクトの作成コストがかかる
- アクセス対象がCの配列の場合は直接C的にアクセスできる、この時はPyPyより速い

実行時間まとめ
| Python | 285 ms | Original |
| -- | -- | -- |
| Cython | 316 ms | Original |
| PyPy | 82 ms | Original |
| Cython | 173 ms | 添え字を型宣言 |
| Cython | 137 ms | リストを型宣言 |
| Cython | 220 ms | リスト→array |
| Cython | CE | リスト→Numpyのnp.array |
| Cython | 25 ms | リスト→Cの配列 |
速度は全部AtCoderのコードテストで計測している

---
まず元のコード
python

```
N = 1000_000 
xs = [0] * N
for i in range(N):
  xs[i] = i
for i in range(1, N):
  xs[i] += xs[i - 1]

print(xs[N - 1])
```

Python 285 ms
Cython 316 ms
PyPy 82 ms

添え字を型宣言
:

```
cdef long i
```

Cython 173 ms
- 生Pythonより速くなったがPyPyにはかなわない

リストを型宣言
:

```
cdef long i
cdef list xs
```

Cython 137 ms
- もう少し速くなるが、やはりPyPyにかなわない

なんでかというとこの`xs[i]`はCの配列アクセスなどとは全然違って
- longの値からPyObjectを作成
- 参照カウントを1増やす
- それを引数にしてSetItemを呼ぶ
- 合間で諸々のエラー処理をする
という処理をしているから。
出力されたCのソースを読めばわかる。
`$ cython -a -3 tiny_cython.pyx`
c

```c
+07:     xs[i] = i
    __pyx_t_2 = __Pyx_PyInt_From_int(__pyx_v_11tiny_cython_i); if (unlikely(!__pyx_t_2)) __PYX_ERR(0, 7, __pyx_L1_error)
    __Pyx_GOTREF(__pyx_t_2);
    if (unlikely(__pyx_v_11tiny_cython_xs == Py_None)) {
      PyErr_SetString(PyExc_TypeError, "'NoneType' object is not subscriptable");
      __PYX_ERR(0, 7, __pyx_L1_error)
    }
    if (unlikely(__Pyx_SetItemInt(__pyx_v_11tiny_cython_xs, __pyx_v_11tiny_cython_i, __pyx_t_2, int, 1, __Pyx_PyInt_From_int, 1, 1, 1) < 0)) __PYX_ERR(0, 7, __pyx_L1_error)
    __Pyx_DECREF(__pyx_t_2); __pyx_t_2 = 0;
  }
```


listの代わりにarrayを使ったら賢く処理してくれるかと思ったが、かえって遅くなった。初期化にリストを受け取るため、実質2回領域の確保が行われる。
python

```
cdef long i
from cpython cimport array
import array as pyarray

N = 1000_000 
cdef array.array xs = pyarray.array("l", [0] * N)
for i in range(N):
  xs[i] = i
for i in range(1, N):
  xs[i] += xs[i - 1]

print(xs[N - 1])
```

220 ms
- これもCソースを観察したら添え字アクセスでPyIntを作っていた

リストではなくサイズで領域確保する方法としてnp.zerosが思いつくが…
python

```
cdef long i
import numpy as np
cimport numpy as np

N = 1000_000 
cdef np.ndarray xs = np.zeros(N, np.int32)
for i in range(N):
  xs[i] = i
for i in range(1, N):
  xs[i] += xs[i - 1]

print(xs[N - 1])
```

なんと[[AtCoderのCythonではNumpyが使えない]]
- 手元でCソースを観察したらやはりこれも添え字アクセスでPyIntを作っていた
    - Memory Viewを作る必要がある。 see [Typed Memoryviews — Cython 3.0a5 documentation](http://docs.cython.org/en/latest/src/userguide/memoryviews.html)

Cの配列を作る
cython

```
cdef long i
cdef long[1000_000] xs

N = 1000_000
for i in range(N):
  xs[i] = i
for i in range(1, N):
  xs[i] += xs[i - 1]

print(xs[N - 1])
```

25 ms
- ついにPyPyより速くなった
- Cソースを見ると単なる配列アクセスになっていることがわかる
c

```c
(__pyx_v_11tiny_cython_xs[__pyx_v_11tiny_cython_i]) = __pyx_v_11tiny_cython_i;
```

- なおサイズを変数で指定することはできない模様
cython

```
cdef long N = 1000_000 
cdef long[N] xs
```

:

```
Main.pyx:3:11: Not allowed in a constant expression
```



もう一つ、malloc/freeを自分で呼ぶ方法も残されてる
- [Memory Allocation — Cython 3.0a5 documentation](https://cython.readthedocs.io/en/latest/src/tutorial/memory_allocation.html)
