---
title: "PAST3L"
---

[L](https://atcoder.jp/contests/past202005-open/tasks/past202005_l) 最大10万個の列に最大10万個の相異なる数値が並んでいて、数値の個数は最大30万。30万回「先頭1つの最大値を取る」か「先頭2つの最大値を取る」かのクエリーを実行する。

[[ABC170]]での[[heapq]]の勉強の結果、解ける気がした。

「先頭1つ」と「先頭2つ」のheapqを使う。
片方から取った時にもう片方に残ってしまうので読み飛ばしの手段が必要。
各列ごとにキューに入れたアイテムを指すポインタを2つ用意、取った数値はNoneに書き換えることで読み飛ばせるようにする。

AC [https://atcoder.jp/contests/past202005-open/submissions/14404930](https://atcoder.jp/contests/past202005-open/submissions/14404930)
