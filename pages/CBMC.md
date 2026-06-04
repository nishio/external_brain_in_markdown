---
title: "CBMC"
---

> CBMC is a Bounded Model Checker for C and C++ programs. It sup­ports C89, C99, most of C11/C17 and most compi­ler exten­sions pro­vided by gcc, clang, and Visual Studio.
[https://www.cprover.org/cbmc/](https://www.cprover.org/cbmc/)

まず「x + 1.0はxではないよね」とassertして
c

```c
#include <assert.h>

int main() {
  double x;
  __CPROVER_assume(x == x);
  __CPROVER_assume(x < __builtin_inf());
  __CPROVER_assume(x > -__builtin_inf());

  assert(x != x + 1.0);
}
```


cbmc tmp.c --traceする

:

```
** Results:
tmp.c function main
[main.assertion.1] line 9 assertion x != x + 1.0: FAILURE

Trace for main.assertion.1:

State 11 file tmp.c function main line 4 thread 0
----------------------------------------------------
 x=-1.701412e+38 (11000111 11100000 00000000 00000000 00000000 00000000 00000000 00000000)
```


ちゃんとx != x + 1.0が成り立たない例を発見した！面白い！

昔教えてもらったやつ「割り算は安全だよね」
:

```
int main() {
  int x;
  int y;

  // 0除算は別のエラーなので除外
  __CPROVER_assume(y != 0);

  // 「割り算しても安全なはず」と主張する
  int z = x / y;

  // z を使わないと最適化・解析上わかりにくいので一応使う
  assert(z == x / y);

  return 0;
}
```


実行すると-1での除算でオーバーフローが起きるケースが見つかる

:

```
** Results:
tmp.c function main
[main.division-by-zero.1] line 13 division by zero in x / y: SUCCESS
[main.overflow.1] line 13 arithmetic overflow on signed division in x / y: FAILURE
[main.assertion.1] line 16 assertion z == x / y: SUCCESS

Trace for main.overflow.1:

State 11 file tmp.c function main line 6 thread 0
----------------------------------------------------
  x=-2147483648 (10000000 00000000 00000000 00000000)

State 12 file tmp.c function main line 7 thread 0
----------------------------------------------------
  y=-1 (11111111 11111111 11111111 11111111)

Assumption:
  file tmp.c line 10 function main
  y != 0

Violated property:
  file tmp.c function main line 13 thread 0
  arithmetic overflow on signed division in x / y
```


面白い
SATは使っているが、全部boolで扱ってたら項が多すぎてこんな速度で答えでないと思うから色々頑張ってそう

論理パズル
c

```c
#include <assert.h>

int main() {
  int A, B, C, D, E;

  __CPROVER_assume(1 <= A && A <= 5);
  __CPROVER_assume(1 <= B && B <= 5);
  __CPROVER_assume(1 <= C && C <= 5);
  __CPROVER_assume(1 <= D && D <= 5);
  __CPROVER_assume(1 <= E && E <= 5);

  __CPROVER_assume(A != B && A != C && A != D && A != E);
  __CPROVER_assume(B != C && B != D && B != E);
  __CPROVER_assume(C != D && C != E);
  __CPROVER_assume(D != E);

  // 証言：
  // A「私はBより先にゴールした」
  // B「私は4位ではなかった」
  // C「私はBより先にゴールしたが、1位ではない」
  // D「私はEの1つ前だった」
  // E「Aは2位ではなかった」
  //
  // 全員の証言が真だとする。
  __CPROVER_assume(A < B);
  __CPROVER_assume(B != 4);
  __CPROVER_assume(C < B && C != 1);
  __CPROVER_assume(D + 1 == E);
  __CPROVER_assume(A != 2);

  assert(0);
}
```


ちゃんと解けた
- GPTには「そういうことがしたかったらAlloyの方がいいのでは」と言われたw
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>`all disj p, q: Person | Result.place[p] != Result.place[q]`のように「全員順位が異なる」と書けます。
