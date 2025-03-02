---
title: "dwango2015_prelims_2"
---

[B - ニコニコ文字列](https://atcoder.jp/contests/dwango2015-prelims/tasks/dwango2015_prelims_2)
- 与えられた文字列から「25」の繰り返しの文字列を切り出す方法がいくつあるか[[数え上げ]]る
- 25がN個続いた部分文字列がある時、[[三角数]]tri(N)がその部分から切り出せる個数
- 続いてる部分を調べるのに自分でループ回すより[[正規表現]]で切り出す方が速かろう
- 簡単だと思ってテストドリブンにしなかったせいで「正規表現の中でカッコが使われた場合findallはその範囲だけを返す」という仕様を忘れててWAした
    - `(?:  )`はキャプチャしないグループ化
python

```
import re 

def tri(x):
    return x * (x + 1) // 2

S = input()
ret = 0
print(sum(tri(len(s) // 2) for s in re.findall("(?:25)+", S)))
```

[提出 #15126969 - dwangoプログラミングコンテスト](https://atcoder.jp/contests/dwango2015-prelims/submissions/15126969)
