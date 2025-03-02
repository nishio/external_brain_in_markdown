
![image](https://gyazo.com/d184857cee408b25e6ea65eb0d7f3799/thumb/1000)


[問題文](https://atcoder.jp/contests/abc172/tasks/abc172_d)
問題文の通りに考えると、約数の個数を計算してからKを掛けて足し合わせるイメージになるが[[演算順序の変更]]を行うのが肝。[[問題文の順にやらない]]。
掛け算は足し算の繰り返しであり、足し算は順序を変えても結果が変わらない。
「条件を満たすものの数を数える」も「条件を満たすなら1、満たさないなら0」の総和を取る処理。
なので「数えた後でK倍」は順番を交換して「条件を満たすならK、の足し合わせ」にできる。
![image](https://gyazo.com/c5ad2bfbd34a616a96d2e65e5a7c4177/thumb/1000)

一旦この変換をしておいてから、[[縦横変換]]する。横に足したものがKf(K)で、それを足し合わせたものが得たい答え。先に縦に足しても足し算順序の交換なので結果に影響しない。
![image](https://gyazo.com/0d96d3c6ed540a523a4c41b8aff945c6/thumb/1000)
縦に足したものは[[等差数列の和]]なので、ループを回さなくても公式で出せる。
これが解説で紹介されてるやり方
python

```
def solve(N):
    ret = 0
    for i in range(1, N + 1):
        num = N // i
        end = num * i
        ret += (i + end) * num // 2
    print(ret)
```

AC 1565 ms [https://atcoder.jp/contests/abc172/submissions/14787794](https://atcoder.jp/contests/abc172/submissions/14787794)

この問題は、もっとオーダーの小さい方法と、大きいけどなんとか通せる方法とがあるそうなので後で探求する。

ところで、この縦に足す方法では、半分から先はどうせ1つしかないのにループを回して一つずつ足してしまう。ここを斜めに足せばループは半分で済む。しかしどうせ斜めに足すなら…
![image](https://gyazo.com/8ce00ba56e9147b6791e01a708f97b66/thumb/1000)

左上までしっかり斜めに足す。そうするとループの回数はルートNのオーダーになる。
![image](https://gyazo.com/eefa326a4a1e00751adbecea14d340fd/thumb/1000)

python

```
def solve(N):
    ret = 0
    i = 2
    while True:
        step = i // 2
        start = (i + 1) // 2 * step
        if start > N:
            break
        end = N // step * step
        ret += (start + end) * ((end - start) // step + 1) // 2
        i += 1
    print(ret)
```

AC 33 ms [https://atcoder.jp/contests/abc172/submissions/14788541](https://atcoder.jp/contests/abc172/submissions/14788541)
50倍も速くなった

[[atcoder]]
