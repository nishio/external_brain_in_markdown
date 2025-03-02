---
title: "OOPLとサブタイピング"
---

> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382325195994660867): kmizuさんの言う通り、現在の主要なOOPLを見ると「サブタイピングの存在」しか非OOPLとの本質的な差異がなくて、かつ主流の言語ではサブタイピングと実装継承が密接に絡みついてて、実装継承は容易にカプセル化を破壊するので使うべきじゃない的な事が一般的に言われるまでになっており、じゃあ非OOPLの方がよくね？みたいな話になってしまうのだけど、OOPL擁護論でこの辺を上手く論じてる記事があるならぜひ読んでみたい

「データ構造と手続きが一緒に定義できるのは便利だよね」はOOPLの特徴ではない
- > [megascus](https://twitter.com/megascus/status/1382325803451523085): データ構造と手続きが一緒に定義できるのは便利だよね！ぐらいで良いんじゃないですかね？
- > [gakuzzzz](https://twitter.com/gakuzzzz/status/1382326369061801985): 別にそれ非OOPLでもできますし……
- > [kmizu](https://twitter.com/kmizu/status/1382698355902533643): 構造体＋手続きでひとまとめは、抽象データ型って名前が既についてるんですよね（なので、非OOPの世界でも出てくる概念です）。
- > [kmizu](https://twitter.com/kmizu/status/1382698986205765635): 抽象データ型の概念は、OOPって用語よりもだいぶ前ですし、実際、SMLにはabstypeってそのものを定義する構文があります。故に、非OOPLでもできちゃう、んですよね（違うとしたら、主流のOOPLだとチェインが書きやすい？）。
- > [gakuzzzz](https://twitter.com/gakuzzzz/status/1382740941195206663): あーなるほど。SMLのabstypeってデータコンストラクタの可視範囲をモジュール機構とか使わずに限定できるんですね。この機能知りませんでした、ありがとうございます
- > [kmizu](https://twitter.com/kmizu/status/1382896708644794368): 抽象データ型という概念は、OOP（という用語）より歴史が古く（詳しくないのですが）、英語版WikipediaによればLiskovが1974に提案したとあります。 [Abstract data type - Wikipedia](https://en.wikipedia.org/wiki/Abstract_data_type)

抽象データ型との差は継承・サブタイピング
- > [nagise](https://twitter.com/nagise/status/1382828660068024321): 「構造体＋手続きでひとまとめは、抽象データ型って名前が既についてるんですよね（なので、非OOPの世界でも出てくる概念です）」という部分が個人的にかなり気になって、そこが抽象データ型なら、OOPで「増えた部分」って何？ってなったので再考中
- > [kmizu](https://twitter.com/kmizu/status/1382898009655050243): 歴史の話としては、抽象データ型＝OOPなら、新語要らなかったでしょうし、実際、抽象データ型には継承もサブタイピングも無い

Stroustrupも抽象データ型と違って一般的な属性と特殊な属性の区別ができるところ(サブタイピング)や、その定義を書き換えることなく新しい用途に使うこと(継承してメソッドを追加することなど)がOOPの特徴だと言っている
- > [zehnpaard](https://twitter.com/zehnpaard/status/1383177329254531072): ちなみにStroustrupのThe C++ Programming Language(1986)ではAbstract Data Typeに直接言及してObject Oriented Programmingと対比させているようです
- > [zehnpaard](https://twitter.com/zehnpaard/status/1383177654166228994): Stroustrupの"History of C++: 1979-1991"からの孫引きですが
- > "An abstract data type defines a sort of black box. Once it has been defined, it does not really interact with the rest of the program. There is no way of adapting it to new uses except by modifying its definition. ...
- > [zehnpaard](https://twitter.com/zehnpaard/status/1383177730448056321): "The problem is that there is no distinction between the general properties of any shape (a shape has a color, it can be drawn, and so forth) and the properties of a specific shape (a circle is a shape that has a radius, is drawn by a circle-drawing function, and so forth). ...
- > [zehnpaard](https://twitter.com/zehnpaard/status/1383177807317065729): "Expressing this distinction and taking advantage of it defines object-orientedprogramming. A language with constructs that allows this distinction to be expressed and used supports object-oriented programming. Other languages don't."


未整理---

> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382321740685078530): 初学者にインスタンス化の概念は確かにわかりづらいよなー。自分もクラス定義が解釈されるタイミングとメインの処理が実行されるタイミングの区別がつけられなくて混乱してた記憶ある。これ非OOP言語でデータコンストラクタとかだったらわかりやすかったりするのかな？同様の混乱生むのだろうか？
> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382322533039415299): Javaの場合はコンパイルタイムとランタイムという分類で（正確じゃないけど）ある程度思考の整理がつけやすいけど、Rubyだとクラス定義の解釈も実行時に行って更にメタプロでわちゃわちゃできるので余計に混乱しやすかったり……
> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382322945075257347): やっぱ現代ではOOPは足を撃ち抜きやすいパラダイムなのではないだろうか……？


> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382328498329505792): OOPLだと非OOPLと比較してopen recursionの実現が容易というメリットはあるけど、現実にそんなopen recursionを沢山活用してるコード書いてるかというとそうでもないよね？
> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382333367484514304): 本質的にOOPというパラダイムにメリットが薄いなら初学者にわざわざ理解しにくい概念を教える必要無いのでは？みたいな気持ちが浮かんでしまう……
> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382333944658497538): クラス-インスタンスの概念とADTの概念のどっちが初学者にとって理解しやすいのかは誰か統計とってくれないかな……？


> [zehnpaard](https://twitter.com/zehnpaard/status/1382330112008392705): OCamlのdiscussにあったこの発言がよくまとまってる
> 「Basically, when you use the inheritance relation you’re invoking two orthogonal things at once, the inheritance of implementation (aka subclassing) and the refinement of type/interface (aka subtyping).」
> [What is the "right" way to add constraints on a type, to handle recursive structures with variants and to combine fragments of types? - Learning - OCaml](https://discuss.ocaml.org/t/what-is-the-right-way-to-add-constraints-on-a-type-to-handle-recursive-structures-with-variants-and-to-combine-fragments-of-types/2810/29)


> [todesking](https://twitter.com/todesking/status/1382329768016629761): Rustをやった結果、型クラスとADTあればsubtypingなくても困らない説というのが出てきてしまった。
>  まあ動的にディスパッチしたいという局面は少数ながらあるのでdynないと困るのだが、用法はかなり限定されるよね……
> [todesking](https://twitter.com/todesking/status/1382342306804600836): Rustのimpl T{}は単に名前空間を分離しているだけなんだけど、OOPで感じるうれしさの大半はこれなのではという気がしています。データに対して処理を関連付けることができて補完がきくとユーザたいけんが良い……
> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382344103782879236): この辺のIDEでの親和性みたいなメリットはわかりますね。
> とはいえIDEがパイプオペレータで型から補完候補探すとかしてくれると実質的に似たような体験を得られそう？
> [todesking](https://twitter.com/todesking/status/1382345302326222849): この「名詞から書き始めるほうが直感的」というのはわたしがOOP脳なだけで、FPに習熟してると感覚は違うのかもしれない。いやでも最初に操作の対象の方を思い浮かべませんか??
> [gakuzzzz](https://twitter.com/gakuzzzz/status/1382346402487934985): 名詞から書き始めたいし処理の順序も左から右の順で書きたいから、パイプオペレータを全言語に入れましょう


> [kmizu](https://twitter.com/kmizu/status/1382991587068682240): ところで、実は初めて、 "Programming with abstract data types"をまともに読んだ（？）のですが、年代的には先行するSIMULA'67への言及もあるのですね。ただ、SIMULAはデータ隠蔽の機能がなくて、そこが違うのだと。
- ![image](https://gyazo.com/2974a5e9dd44dc4c6018b7974c92fd99/thumb/1000)
- [Programming with abstract data types | ACM SIGPLAN Notices](https://dl.acm.org/doi/10.1145/942572.807045) Barbara Liskov, Stephen Zilles, 1974

> [TakashiSasaki](https://twitter.com/TakashiSasaki/status/1382902897290059777): 多相性の観点から整理できないかな。OOPLはサブタイピング多相を必須とする多相性を持つ。OOPLによってパラメトリック多相やアドホック多相とどう折り合いをつけるかはまちまち。

> [cedretaber](https://twitter.com/cedretaber/status/1382331764241178624): 非 OOPL だと、ちゃんと設計論を持っていないとデータ構造とその手続とをバラバラにしちゃうけど、 OOPL だと言語の標準的な書き方に従うだけでそこをまとめておける、というのは利点だと思うんだよなぁ……。
> [cedretaber](https://twitter.com/cedretaber/status/1382332115421863943): あまりに抽象データ型の考え方に馴染んでしまった人は、言われなくてもそれをやるから「 OOPL なんて不要では」と考えるのだと類推するけど（私もそう感じている節はある）、世の中にはそうじゃない人も多いと思っている。




