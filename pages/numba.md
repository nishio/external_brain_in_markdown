---
title: "numba"
---

- [[RBST]]

![image](https://gyazo.com/72214310c3dffd3c4f2f73f55aa9c5a7/thumb/1000)

[Compiling code ahead of time — Numba 0.50.0.dev0+236.g64fbf2b-py3.7-linux-x86_64.egg documentation](https://numba.pydata.org/numba-doc/dev/user/pycc.html)

- The use of yield in a closure is unsupported.
    - NG: ` dist = min(distances[(goal, dir)] for dir in range(4))`

- `Untyped global name 'input': cannot determine Numba type of ...`
    - inputは型不明で使えないので読んでからコンパイルした関数に渡す

- numbaでdefaultdictは使えない
    - dictにしたがgetがらみで型エラーが起きる
    - そもそもタプルをキーにすると型エラーなので整数にパックする必要がある
    - →じゃあ素直に配列使おう
- [Supported Python features — Numba 0.50.0 documentation](https://numba.pydata.org/numba-doc/latest/reference/pysupported.html)
- [Supported NumPy features — Numba 0.50.0 documentation](https://numba.pydata.org/numba-doc/latest/reference/numpysupported.html)

Invalid use of type(CPUDispatcher(<function merge at 0x12be8de60>)) with parameters (array(int64, 1d, A), array(int64, 1d, A), array(int64, 1d, A), array(int64, 1d, A), array(int64, 1d, A), int64, int64, array(int64, 1d, A))

During: resolving callee type: type(CPUDispatcher(<function merge at 0x12be8de60>))
During: typing of call at rbst.py (96)