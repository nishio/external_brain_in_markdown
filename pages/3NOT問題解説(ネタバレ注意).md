
[[3NOT問題]]
![image](https://gyazo.com/10e6d74d0b066e4206ddb5c12faaaabc/thumb/1000)
自然言語での解説は下の方にあります(が、コードの意図を自然言語で解説するものです)
python

```
values = {}
values["X"] = [1 if i & 1 else 0 for i in range(8)]
values["Y"] = [1 if i & 2 else 0 for i in range(8)]
values["Z"] = [1 if i & 4 else 0 for i in range(8)]
print(values)
```

output

```
{'X': [0, 1, 0, 1, 0, 1, 0, 1], 'Y': [0, 0, 1, 1, 0, 0, 1, 1], 'Z': [0, 0, 0, 0, 1, 1, 1, 1]}
```


python

```
def do_and(a, b):
    return [values[a][i] & values[b][i] for i in range(8)]


def do_or(a, b):
    return [values[a][i] | values[b][i] for i in range(8)]


print(do_and("X", "Y"))
```

output

```
[0, 0, 0, 1, 0, 0, 0, 1]
```


python

```
def to_str(bits):
    return "".join(str(i) for i in bits)


for v in values:
    print(v, to_str(values[v]))
```

output

```
X 01010101
Y 00110011
Z 00001111
```


python

```
exists = {to_str(v) for v in values}
new_values = values
next_values = {}
for a in new_values:
    for b in values:
        if a != b:
            v = do_and(a, b)
            s = to_str(v)
            if s not in exists:
                exists.add(s)
                next_values[join("&", a, b)] = v
            v = do_or(a, b)
            s = to_str(v)
            if s not in exists:
                exists.add(s)
                next_values[join("|", a, b)] = v
print(next_values)
```

output

```
{'X&Y': [0, 0, 0, 1, 0, 0, 0, 1], 'X|Y': [0, 1, 1, 1, 0, 1, 1, 1], 'X&Z': [0, 0, 0, 0, 0, 1, 0, 1], 'X|Z': [0, 1, 0, 1, 1, 1, 1, 1], 'Y&Z': [0, 0, 0, 0, 0, 0, 1, 1], 'Y|Z': [0, 0, 1, 1, 1, 1, 1, 1]}
```


python

```
exists = {to_str(v) for v in values}
new_values = values
while True:
    next_values = {}
    for a in new_values:
        va = new_values[a]
        for b in values:
            vb = values[b]
            if a != b:
                v = do_and(va, vb)
                s = to_str(v)
                if s not in exists:
                    exists.add(s)
                    next_values[join("&", a, b)] = v
                v = do_or(va, vb)
                s = to_str(v)
                if s not in exists:
                    exists.add(s)
                    next_values[join("|", a, b)] = v
    values.update(new_values)
    new_values = next_values
    if not new_values:
        break
```

output

```
X       01010101
Y       00110011
Z       00001111
X&Y     00010001
X|Y     01110111
X&Z     00000101
X|Z     01011111
Y&Z     00000011
Y|Z     00111111
(X&Y)|X 01010101
(X&Y)|Y 00110011
(X&Y)&Z 00000001
(X&Y)|Z 00011111
(X|Y)&Z 00000111
(X|Y)|Z 01111111
(X&Z)|Y 00110111
(X&Z)|Z 00001111
(X|Z)&Y 00010011
(Y&Z)|X 01010111
(Y|Z)&X 00010101
((X&Y)|Z)&(X|Y) 00010111
```


python

```
ONE_NOT = {"P": do_not(values["((X&Y)|Z)&(X|Y)"])}

update_values(ONE_NOT)
print_values(values)
# (P|((X&Y)&Z))&((X|Y)|Z) 01101001

TWO_NOT = {"Q": do_not(values["(P|((X&Y)&Z))&((X|Y)|Z)"])}
update_values(TWO_NOT)
print_values(values)
# OK

reverse_map = {to_str(v): k for k, v in values.items()}
for name in "XYZ":
    v = values[name]
    s = to_str(do_not(v))
    print(f"~{name} = {reverse_map[s]}")
```

:

```
~X = (Q&(P|(Y&Z)))|(P&(Y|Z))
~Y = (Q&(P|(X&Z)))|(P&(X|Z))
~Z = (Q&(P|(X&Y)))|(P&(X|Y))
```


[full code](https://gist.github.com/nishio/3a76e573c53289049fa985777ef2cc24)

自然言語での解説
- 論理回路の出力は0/1のいずれかである
- それに影響を与える入力は3ビット8種類である
- よって「論理回路」とは
    - 3ビット8通りの入力を受け取って1ビットを出力する関数である
    - これは「8通りの入力に対して0/1のどちらを返すか」の8つの1ビットの集まり
    - だから8ビットの値として表現できる
- 同じビット表現のものは区別しなくて良い
    - 同じ振る舞いをする異なる論理回路を区別する必要はない
    - 最もシンプルなもので代表させればいい
    - つまり高々256個の8ビット整数について考えれば良い
- X,Y,Zの3つの関数が与えられる
    - これを加工して~X, ~Y, ~Zを作る
- not演算を2回しか使えない
    - S0「NOT0回で作れる関数全体の集合」
    - S1「S0の中の一つの関数のNOTを付け加え、それで作れる関数全体の集合」
    - S2「S1の中の一つの関数のNOTを付け加え、それで作れる関数全体の集合」
    - S2が~X, ~Y, ~Zを含むように「うまいことNOTする関数を選べ」というパズル
- S0を全列挙したら`((X&Y)|Z)&(X|Y) 00010111`という明らかに怪しいやつがいる
    - これのNOTをPとする
- S1には対称性の高い`(P|((X&Y)&Z))&((X|Y)|Z) 01101001`がいる
    - これのNOTをQとする
- S2をざっと眺めると~X, ~Y, ~Zが無事生成できてそう
    - それを綺麗に出力した
:

```
~X = (Q&(P|(Y&Z)))|(P&(Y|Z))
~Y = (Q&(P|(X&Z)))|(P&(X|Z))
~Z = (Q&(P|(X&Y)))|(P&(X|Y))
```


事後考察
- ![image](https://gyazo.com/2743b94757a8faacfddec898a3144287/thumb/1000)
- PとQは立っているビットの数をnとした場合に
    - $P(n) = [n \le 2]$
    - $Q(n) = [n {\,\text{is even}}]$
    - となる関数
    - 反転前を考えるとnの各ビット、こっちの方がわかりやすいか
- コードでandの計算を先にしてるから「最終的にandで括られる式」になってるけど、人間にとってはorで括った方がわかりやすい
    - `~P = ((X&Y)|Z)&(X|Y) = X&Y | Z&X | Z&Y`
        - X, Y, Zどれか二つのandが1のとき「nは2以上」
    - `~Q = (P|((X&Y)&Z))&((X|Y)|Z) = X&Y&Z | (P & (X|Y|Z))`
        - X, Y, Z3つ全て1である(X&Y&Z)か、「nが2未満(P)で、X, Y, Zどれか1つが1(X|Y|Z)」のとき、nは奇数
    - `~X = (Q&(P|(Y&Z)))|(P&(Y|Z)) = Q&P | P&Y | P&Z | Q&Y&Z`
        - 「nが偶数(Q)で2未満(P)」つまりnが0でX, Y, Zすべて0
        - 「nが2未満(P)でYかZ」
        - 「nが偶数(Q)でYかつZ」
        - のときにXは0である
