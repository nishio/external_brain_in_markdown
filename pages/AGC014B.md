---
title: "AGC014B"
---

[B - Unplanned Queries](https://atcoder.jp/contests/agc014/tasks/agc014_b)
- ![image](https://gyazo.com/6964219a87b15e25515e43510edb342e/thumb/1000)
- 考えたこと
    - 例えば
        - クエリが一つだったら木の形によらず不可能
        - クエリが二つの時、完全に重なってない限り不可能
        - クエリが3つの時ab, bc, caならOK
    - つまりサイクルになれば良さそう
        - 複数個はアリ
        - つまりクエリの端に出てくる回数を数えて偶数回ならOK
        - 証明は？
            - クエリが奇数回しか触れてない点の周辺にはからなず奇数の辺ができる
            - 木であるので2点をつなぐパスは一意
                - ab, bcがある時にabcをこの順でたどる経路のうちac上にないものは往復して2回通る
- 公式解説
    - 方針OK
    - 証明は根つき木にしてmod 2で考える

- [[問題分割]]
    - [[木の辺ラベルの更新]]
        - [[辺ラベルを更新しなくても端点だけ見れば良い]]
