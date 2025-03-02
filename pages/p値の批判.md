---
title: "p値の批判"
---

- 2014 Nuzzo, R.(2014). Scientific method:statistical errors. Nature, 506, 150-152
    - [https://www.nature.com/news/scientific-method-statistical-errors-1.14700](https://www.nature.com/news/scientific-method-statistical-errors-1.14700)
    - p値はFisherによって作られたが、検定の目的ではなかった
    - Neymanらが検定の仕組みを考案した
    - FisherとNeymanが互いに相手のアプローチを批判し合っている間に、他の著者らによって両者の主張がまぜこぜになり、「p値を計算した上で、それを閾値(0.05など)と比較することによって検定をする手法」が誕生した
    - 検定して0.05有意であるという結果を観測した前後で分布がどう更新されるか([[ベイズ]]的解釈)
        - 事前分布でreal effectである確率が5%だった場合、検定で有意と判定されてもその確率が11%に上がるだけ
        - 事前分布で五分五分だった場合、検定で有意と判定された後は71%に上昇する
        - よくある解釈「有意水準5%の検定をして有意だったら95%の確率で現象が実在する」は誤り

- 2015 Basic and Applied Social Psychology（BASP）
    - [論文誌内での帰無仮説有意性検定方式と p 値の提示を禁止](https://www.tandfonline.com/doi/full/10.1080/01973533.2015.1012991)
    - それに関する[Nature News](https://www.nature.com/news/psychology-journal-bans-p-values-1.17001)

- 2016 American Statistical Association（ASA）
    - [p値に関する声明](https://amstat.tandfonline.com/doi/pdf/10.1080/00031305.2016.1154108)
    - 色々あるが一部ピックアップ
        - p値は、仮説が真である確率、もしくはデータが偶然によって生成された確率の尺度ではない
        - 科学的結論と、ビジネスもしくは政策上の決定は、p値が特定の閾値を通過したかだけに依存すべきではない
        - p値もしくは統計的有意性は、効果の大きさもしくは結果の重要性の尺度ではない
        - p値はそれ単体では、モデルもしくは仮説に関して良いエビデンスとならない
    - [p値の誤用に業を煮やしたASA（米国統計学会）が声明を発表 | SciStat](http://epigraph.jugem.jp/?eid=253)

- 2016 「p 値に関する最近の議論」([日本語解説](https://www.jstage.jst.go.jp/article/jscssymo/30/0/30_153/_pdf/-char/ja))

メモ
- [http://smrmkt.hatenablog.jp/entry/2015/04/14/234856](http://smrmkt.hatenablog.jp/entry/2015/04/14/234856)
    - [[Optimizely]]
    - [[ベイズ]]
    - 時間とともにサンプル数が増えるのに、決められたサンプル数になるまでデータを見ないのは不自然
    - 繰り返し見ることは偽陽性率を高める
    - [[逐次検定]]ベース
    - [[偽陽性率]]から[[偽発見率]]へ

- [検定と区間推定](https://oku.edu.mie-u.ac.jp/~okumura/stat/tests_and_CI.html)
    - > どうするのがいいかは言い難いのですが, [[p値よりは信頼区間のほうが大切]]ですし,[[信頼区間]]を求める[[Clopper and Pearson]]の方法はもう標準になっているので,それで信頼区間を求め, p値のほうは特に報告しない(信頼区間に帰無仮説の母数が入っているかどうかで判断してもらう)というのはどうでしょうか。
