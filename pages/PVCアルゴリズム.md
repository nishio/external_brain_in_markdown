---
title: "PVCアルゴリズム"
---

from [[思考の結節点2025-10-10]]
PVCアルゴリズム
- [[Proportional Veto Core]]（[[比例拒否コア]]）

何か（定義）
- 有権者 (n) 人・候補 (m) 名。連合 (T)（人数 (|T|=k)）には 拒否（veto）権が与えられ、
- $v(T)=\left\lfloor \frac{m\cdot |T|}{n} \right\rfloor-1$
- 人の候補を落とせる（比例拒否原理）。([AAAI](https://cdn.aaai.org/ojs/16691/16691-13-20185-1-2-20210518.pdf))
    - 連合とは有権者の任意の部分集合である<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

- 候補 (c) について、連合 (T) が「メンバー全員が (c) より上だとみなす候補集合 (B)」を十分大きくとれれば (c) をブロックできる。どの連合にもブロックされない候補が PVC（比例拒否コア）。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - 条件は $|B| \ge m - v(T)$
        - 有権者 (n=100) 人・候補 (m=10) 名。連合 (T)（人数 (|T|=k=30)）とするとv(T) = floor(10 * 30/100) - 1 で 2になる
        - 30人が「候補者Cはダメだ」(Cより良い候補が8人以上いる)に合意した場合、残りの70人が候補者Cに投票していたとしても拒否できる、という仕組み
    - ニュアンスの要点
        - 肯定的一致は不要：連合は「この1人を推す」まで一致する必要はなく、c よりマシ”な候補が十分あることだけ一致すれば c を落とせます。
        - 反実仮想の基準：実際に連合が結成される必要はなく、「そんな連合が存在し得るなら c は不適」と判断します。これが“コア（core）”の概念です。
        - 直感の例：m=n+1 のとき、人数 k の連合はちょうど k 人分の候補を拒否できます

- 起源：Moulin（1981）が「比例拒否原理」を提示し、常にコアが空でない（少なくとも1候補は残る）ことを示した古典結果。([JSTOR](https://www.jstor.org/stable/2297154?utm_source=chatgpt.com))
- 直感：x％の連合は約 x％ の候補を落とせるので、単純多数決だけで少数派が最悪候補を押しつけられる事態を避ける仕組みです。

素朴に実装すると「任意の部分集合」が出てくるので$2^n$のオーダーになって無理なんだが、多項式時間で解ける<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

「PVCアルゴリズム」とは（計算方法の要点）
Ianovski & Kondratev（AAAI-21）が 多項式時間で PVC を計算するアルゴリズムを提示：
- 各候補 (c) について、「(c) をブロックできる ((T,B)) が存在するか」を二部グラフの最大流 / 最大完全二部分グラフ検出に帰着して判定。
- 全候補に対して実行し、ブロック不可能な候補集合＝PVCを得る。
- 計算量は ($O!\left(m\cdot\max(n^3,m^3)\right)$)。([AAAI](https://cdn.aaai.org/ojs/16691/16691-13-20185-1-2-20210518.pdf))
また、Veto by Consumption（各有権者が自分の最下位候補の「持ち点」を連続的に削っていき、最後に残る候補を選ぶ）という、匿名・中立なコア選択手続きも提案されています。([AAAI](https://cdn.aaai.org/ojs/16691/16691-13-20185-1-2-20210518.pdf))

どこで使われる？
- 少数派保護を重視する単勝者選挙の設計・分析。([AAAI](https://cdn.aaai.org/ojs/16691/16691-13-20185-1-2-20210518.pdf))
- 応用例：**連合学習（Federated Learning）**の公平性概念として PVC を拡張し、PVC-stable なモデルを学習するアルゴリズム（Rank-Core-Fed）も提案されています。([Proceedings of Machine Learning Research](https://proceedings.mlr.press/v235/ray-chaudhury24a.html?utm_source=chatgpt.com))

