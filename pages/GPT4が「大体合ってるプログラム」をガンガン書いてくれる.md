---
title: "GPT4が「大体合ってるプログラム」をガンガン書いてくれる"
---

関連
- ChatGPTにソフトウェアを実装させる
    - [/villagepump/Twitter to Scrapbox GPT](https://scrapbox.io/villagepump/Twitter to Scrapbox GPT)
- ChatGPTに違う言語への移植をさせる
    - [[GPT-4でPythonに移植]]

> [nishio](https://twitter.com/nishio/status/1638948612859400192) GPT4が本当に「大体合ってるプログラム」をガンガン書いてくれるので、エンジニアの仕事のうちの「デバッグする時間」の割合が増える。デバッグ能力を鍛える学習コンテンツが必要だ(もしくはデバッグをGPT4にさせる良いプロンプト)

> [nishio](https://twitter.com/nishio/status/1638948987620433922) もう「やりたいことはあるがどうやって書いたらいいかわからない」は言い訳にならない時代だ、最初の一歩が「ゼロからかく」ではなく「とりあえずGPT4に書かせて、それを実行してみる」に変わる

> [nishio](https://twitter.com/nishio/status/1638949497802997761) どうすればGPT4にデバッグさせられるだろう。「このコードにデバッグ出力とアサーションをたくさん入れて」ってやるのか？
- > [NaOHaq](https://twitter.com/NaOHaq/status/1638950671688044546) 「このコードのQuickCheck書いて」とか


> [nishio](https://twitter.com/nishio/status/1638949897184612352) コーディング規約「ソースコードはChatGPTに入力できるトークン数以内に収めること」とか言い出す人がいそうだな
- > [8kpx](https://twitter.com/8kpx/status/1638956571253153816) これ現実的にあり得る気がしている。小さな検証可能なモジュールに分割して組み合わせる想定。とはいえインテグレーションがエグそう

> [nishio](https://twitter.com/nishio/status/1638952982309126150) この前「デバッグしやすいように関数分割して」は試して、できてたからなー。テストケース付きの部品に分けて行くことはできるかもしれないな。

> [nishio](https://twitter.com/nishio/status/1638967933161594880) 「こういうDOMの時にうまく動かない」とGPT4に言おうとしたがDOMが大き過ぎてダメだった
- > [phono2xx](https://twitter.com/phono2xx/status/1639067859048628226) 関数レベルならテストコードも同時に書いてとお願いし、というかaiが書きやすい構成にしていくかとかですかね。サーバーとはjsonのみ、とか。セレニウムを出力させても良いかも。というか本当に仕事のやり方変わりますよね。。

> [hrjn](https://twitter.com/hrjn/status/1639025921234698240) 経験上、初学者がつまづく一番の要因は環境構築でプログラムを書くこと以外がかなり辛そうというのはある。
>  まぁ、この辺も聞いたら教えてくれそうではあるけど、聞き方が難しそう。
- > [nishio](https://twitter.com/nishio/status/1639142008571969537) 「Dockerfileを書いて」


> [tsukamoto](https://twitter.com/tsukamoto/status/1639160941182062592) [[Wikipedia]]が「大体合ってる知識」をガンガンまとめてくれてるので、調査者（学習者や宿題者を含む）の仕事のうちの「検証する時間」の割合が増えたのと、同じ構図だよね。多くの場面で人間の役割はどんどん意思決定と評価・判断にウェイトシフトしていて、その二つの間の作業は薄くなってきてる。
- なるほど
