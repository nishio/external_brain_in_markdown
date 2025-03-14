---
title: "abc106_d"
---

[https://atcoder.jp/contests/abc106/tasks/abc106_d](https://atcoder.jp/contests/abc106/tasks/abc106_d)
- 考えたこと
    - 区間が20万個与えられて、10万回与えられた区間に完全に包含されるものの個数を答える
    - なんらかの前処理をして定数か対数のオーダーで答えたい
    - 一般論として考えて難しいので制約を確認
        - Nが500なので二乗のオーダーのテーブルを確保しても良い
        - 二次元の長方形の区間をインクリメントできるデータ構造があればいいのだけど…
            - 双対セグメント木が二次元になったようなやつ
- 公式解説
    - 各クエリごとにO(N)でもNが小さいから間に合う
        - Nが小さいことには気づいたのに空間計算量の方ばかり考えてた、「定数か対数のオーダーで」も緩まるのか
    - データ構造の方でも範囲インクリメント点取得の双対セグメント木をイメージしてたが、点インクリメント範囲和で考える方が自然だった
    - そこまで考えが及んでいれば範囲和のO(N^2)を[[累積和]]でO(N)にするだけ
    - [[二次元累積話]]を使えばもっと速いがそこまでは求められてない
