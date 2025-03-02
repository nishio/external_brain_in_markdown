
AtCoder環境でPythonプログラムが2回実行されることを使って、初回でC++で書かれた拡張モジュールをコンパイルし、2回目でインポートするアプローチ
[https://atcoder.jp/contests/cpsco2019-s1/submissions/14705333](https://atcoder.jp/contests/cpsco2019-s1/submissions/14705333)
[[Pythonでmultiset]]

「おおっ、究極兵器か？」と思ったけど、これボクシングのコストがどの程度影響するか心配だな
- 単純に100万件追加する速度ではC++版が529msなのに対してPyPy向けに実装されたAVL木が495msなので負けている
    - [https://github.com/nishio/atcoder/blob/master/multiset/cpp.py](https://github.com/nishio/atcoder/blob/master/multiset/cpp.py)
    - [https://github.com/nishio/atcoder/blob/master/multiset/pypyavl.py](https://github.com/nishio/atcoder/blob/master/multiset/pypyavl.py)
→雑に比較しただけなのでもう少しちゃんと比較したい

[[PythonからC++のsetを使う]]

[[PythonからC++を呼ぶ]]
