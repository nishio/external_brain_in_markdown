
作業メモ
- [[ppoi]]をclone
- `meanless_newline_ppoi`にリネーム
- > 実行前に未判定の入力をunknowns.txtに入れておく必要があります
    - いきなり階段の段差が大きいな
    - 今回「PDFをテキスト化した時に行ごとに分かれている、これを結合したいが、結合してよいものと悪いものがある」というシチュエーション
    - 「意味のない改行っぽいものを削除」したい
lines

```
['第一編\u3000 序論', '', '元来ギリシャでも   filosofiva 〔フィロソフィア〕という一つの言葉があったのではない。  ', 'filosofoV  =  Weisheitsfreund という言葉はヘラクレイトス〔 Herakleitos, ca. 540-ca. 480B.C.〕に現れ', 'たのが最初であり、ピタゴラスからとも云われるがそれは誤である。ところで今日の  Philosophie ', 'の源をなす言葉は歴史学の父と呼ばれるヘロドトス〔 Herodotos, 484-ca. 425B.C.〕が   filosofei:n と', 'いう言葉を使ったのに由来し、それは上述したように「知慧を愛求する」という動詞の形であり、', '', '6', '', 'それから   filosofiva 〈愛知〉という名詞の形に変ったのである。フィロソフィアという言葉は最', '初はこのように「知慧を愛すること」とか「知的教養を求めること」とかいうように広い意味で', '', '用いられていたが、それがソフィスト達やソクラテス〔 Sokrates, 470/69-399B.C.〕を通じて「学問', '', 'をすること」という意味に段々と限定されてきた。尤もソフィスト達やソクラテスでは、ソフィ', '', 'アという言葉は古くからの技術的知能という意味をなお含んでいた。それが純粋に精神的な意味', '', 'での知慧になるのはプラトンからである。', '', 'プラトンは知識を二種類に区別した。一つは  ejpisthvmh = Erkenntnis, knowledge 〔知識〕であり、', '一つは   dovxa  =  Meinung,  opinion 〔臆見〕である。前者即ちエピステーメーは真の知識であり、真', '実在の知識であり、プラトンの所謂イデヤを知ることである。イデヤとは永遠不変の真実在であ', '', '']
```

py

```
import json
data = open("哲学概論.txt").read()
data = data.split("\x0c")
# print(len(data))
unknowns = []
for page in data:
    lines = ["SOP"] + page.split("\n") + ["EOP"]
    for i in range(len(lines) - 3):
        unknowns.append(json.dumps({
            "i": i,
            "neg_i": len(lines) - i - 4,
            "lines": lines[i:i+4],
        }, ensure_ascii=False))

with open("unknowns.txt", "w") as f:
    f.write("\n".join(unknowns))
```

- `%run meanless_newline_ppoi/cli.py`
    - `ImportError: cannot import name 'clock' from 'time' (unknown location)`
- `%run meanless_newline_ppoi/cli.py --initialize`
    - `Enter at least one positive examples (empty to exit)`
    - `{"i": 10, "neg_i": 15, "lines": ["", "哲学とは何か。この問いに簡単な答えを与えることは困難である。哲学は古くからあり、個々", "", "の特殊科学に先んじて起った。また哲学は歴史上色々と変遷しており、将来もなお発展して行"]}`
- テキスト形式で入力させるの、やりにくいな
    - これって修正しなかったっけ…
- `FileNotFoundError: [Errno 2] No such file or directory: '/Users/nishio/scaffold_network/kitaro/meanless_newline_ppoi/ppoi/unknown.txt'`
    - これ最初に確認して警告すべきだよな
    - 置き場所、unknownsのsの有無
:

```
%run meanless_newline_ppoi/cli.py --interactive
{"i": 0, "neg_i": 28, "lines": ["SOP", "者は習慣となれば快感を減ずる、等々。マーシャル  Henry R. Marshall 〔 1852-1927〕の美学  Pain, ", "Pleasure and Aesthetics, 1894 〔『苦痛・快感・美学』〕などはこうした立場のものであろう。心理学", "的にはこのように説明する外はあるまい。しかし美や善の与える快感は、単に肉体的な快感と単"]}: 0.5001
negative(z), neutral(x), positive(c), quit(q)>
```

- 動くようになった
    - 表示を改善
    - あれ、表示方法をユーザがカスタマイズできるようにした気がするが…
- [[ppoi改善案]]
    - [[ppoi改善2021-02-05]]
    - > 「どこのコードが最新だ？」とか言いそうなのでとりあえず今のコードをpushしておいた
    - どこにだよ
    - 今見てるリポジトリの前の更新は2018年だな
    - あー、keichobotのリポジトリの中にある
    - [[動きの抽出作業メモ#6018e017aff09e0000f60b4e]]
        - > そのまま使うというより編集して使おう
        - あー、そう言うことか

整理
- if文の条件式を現時点で人間が明確に言語化することはできないが、事例を見るとtrueかfalseが判定できる、というケースにおいて能動学習が都合が良い
- 能動学習のコードはゼロから2〜3回書いて「毎回ゼロから作るのは非効率だからまとめたい」と考えてppoiを作った
    - しかしツールの構造として現状のppoiは適当でない
    - なのでkeichobotで使うときに柔軟性が足りず「コピーして書き換え」を行い、それを大元のリポジトリに反映していなかった

2022-04-05

正しい構造が何かはわからないので今回もコピーして書き換える
対話的学習が回るようになった
- ダウンサンプリングを5秒から1秒に変更した
`$ python3 -m ppoi.main --cross-val  `
Accuracy: 0.80 (+/- 0.18)

2022-04-06

今回は特徴量を作る上で各行ではなくページ全体が必要
- こういうところがケースバイケースで変わるから一般的設計が難しいのだよなー
