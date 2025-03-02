---
title: "np.dot, np.tensordot, np.matmulの違い"
---

[[np.einsum]]という表現力の高いメソッドを知ったので、np.dot, np.tensordot, np.matmulをそれぞれnp.einsumで表現することで違いを確認してみる。


python

```
import numpy as np

def same_matrix(A, B):
    return (A.shape == B.shape) and all(A.flatten() == B.flatten())


# 3-dim
T1 = np.arange(27).reshape(3, 3, 3)
T2 = np.arange(27).reshape(3, 3, 3) + 1

assert same_matrix(
    np.einsum('ijk,jkl->il', T1, T2),
    np.tensordot(T1, T2))

assert same_matrix(
    np.einsum('ijk,lkm->ijlm', T1, T2),
    np.dot(T1, T2))

assert same_matrix(
    np.einsum('ijk,ikm->ijm', T1, T2),
    np.matmul(T1, T2))
```


ついでに4次元と2次元の時もやってみた。
python

```
# 4-dim
T1 = np.arange(81).reshape(3, 3, 3, 3)
T2 = np.arange(81).reshape(3, 3, 3, 3) + 1

assert same_matrix(
    np.einsum('ijkl,klmn->ijmn', T1, T2),
    np.tensordot(T1, T2))

assert same_matrix(
    np.einsum('ijkl,mnlo->ijkmno', T1, T2),
    np.dot(T1, T2))

assert same_matrix(
    np.einsum('ijkl,ijlm->ijkm', T1, T2),
    np.matmul(T1, T2))


# 2-dim
T1 = np.arange(9).reshape(3, 3)
T2 = np.arange(9).reshape(3, 3) + 1

assert same_matrix(
    np.einsum('ij,ij->', T1, T2),
    np.tensordot(T1, T2))

assert same_matrix(
    np.einsum('ij,jk->ik', T1, T2),
    np.dot(T1, T2))

assert same_matrix(
    np.einsum('ij,jk->ik', T1, T2),
    np.matmul(T1, T2))
```



# 解説編

python

```
 assert same_matrix(
     np.einsum('ijk,jkl->il', T1, T2),
     np.tensordot(T1, T2))
```


tensordorはT1の後ろ2つとT2の前2つを潰す。なのでijkのjkとjklのjkが潰されてilが残る。いくつ潰すかはオプションで指定できる。

python

```
 assert same_matrix(
     np.einsum('ijk,lkm->ijlm', T1, T2),
     np.dot(T1, T2))
```


dotはT1の最後の1つと、T2の最後から2番目を潰す。なのでijkのkとlkmのkが潰されてijlmが残る。

python

```
 assert same_matrix(
     np.einsum('ijk,ikm->ijm', T1, T2),
     np.matmul(T1, T2))
```


matmulは2次のテンソルの掛算を想定している。なのでこれはまず「jkとkmを掛けてjmを作る(jk,km->jm)」が基礎にあって、その上で「行列の1つのマスにi個の値が積まれている」という扱いがされて、結果的にijk,ikm->ijmになっている。なおiの部分ではよしなにブロードキャストもするので`np.matmul(np.ones((2, 1, 3, 4)), np.ones((1, 5, 4, 6)))`はvalidである。
#NumPy