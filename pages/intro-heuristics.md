
[A - AtCoder Contest Scheduling](https://atcoder.jp/contests/intro-heuristics/tasks/intro_heuristics_a)
- 2時間は短く感じたが、長くなっても疲れるのでこれでいい気がする
- atcoder 605位でした。pythonでは繰り返し試行は辛い。37回しかできてなかった。numbaでコンパイルするのも間に合わなかった。
- ちなみにまずは頭からグリーディに最前の選択を繰り返して、それではどういう時にいまいちかというと「数日後に高いスコアがもらえるのに今やっちゃうと損」というパターンなので、先読みしてディスカウントする、そのディスカウント率をランダムで揺すりました。
- PyPyで出すという手があったか
    - PyPyで出し直してみたらnumpyのインポートでREだった

numbaはpref_counterが使えなくて「時間ギリギリまで計算」がやりづらい
numpyを使わず、PyPyで出すのが正解だったかも

[https://qiita.com/c-yan/items/ba0f5390c7ee8f1ba667](https://qiita.com/c-yan/items/ba0f5390c7ee8f1ba667)

[https://mdstoy.hatenablog.com/entry/2020/06/29/013915](https://mdstoy.hatenablog.com/entry/2020/06/29/013915)

[https://atcoder.jp/contests/intro-heuristics/submissions/14823819](https://atcoder.jp/contests/intro-heuristics/submissions/14823819)
[https://atcoder.jp/contests/intro-heuristics/submissions/14821744](https://atcoder.jp/contests/intro-heuristics/submissions/14821744)
[https://atcoder.jp/contests/intro-heuristics/submissions/14818177](https://atcoder.jp/contests/intro-heuristics/submissions/14818177)
[https://atcoder.jp/contests/intro-heuristics/submissions/14817099](https://atcoder.jp/contests/intro-heuristics/submissions/14817099)
[https://atcoder.jp/contests/intro-heuristics/submissions/14820088](https://atcoder.jp/contests/intro-heuristics/submissions/14820088)
