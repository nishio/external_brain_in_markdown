---
title: "LCP array"
---

- [LCP array - Wikipedia](https://en.wikipedia.org/wiki/LCP_array)
- [LCP(Longest Common Prefix)を用いたSuffix Arrayの検索 - EchizenBlog-Zwei](https://echizen-tm.hatenadiary.org/entry/20110728/1311871765)
- [[接尾辞配列]]を作った後、隣接してる文字列のLCP(longest common prefix)の長さを記録しておく
    - Kasai法でO(N)
        - 『部分語計数問題の接尾辞配列を用いた高速アルゴリズム』[PDF](http://www-ikn.ist.hokudai.ac.jp/mthesis/H11_tohru_kasai_mastersthesis99_feb1999.pdf)
    - [https://naoyat.hatenablog.jp/entry/construct-suffix-array-and-lcp-in-linear-time](https://naoyat.hatenablog.jp/entry/construct-suffix-array-and-lcp-in-linear-time)
        - [http://www.nct9.ne.jp/m_hiroi/light/pyalgo60.html](http://www.nct9.ne.jp/m_hiroi/light/pyalgo60.html)
- 任意の2つの項目のLCP長は、その2つの間のLCP長の最小値に一致する
    - [[RMQ]]
- この情報を使うと二分探索が高速化できる
    - クエリ長Mの時、素朴なO(MlogN)がO(M+logN)になる
