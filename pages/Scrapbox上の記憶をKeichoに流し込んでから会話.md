---
title: "Scrapbox上の記憶をKeichoに流し込んでから会話"
---

from [/villagepump/Scrapbox上でKeichoを動かす](https://scrapbox.io/villagepump/Scrapbox上でKeichoを動かす)
Scrapbox上の記憶をKeichoに流し込んでから会話

過去ログを貼ったScrapbox上から会話をするのはScrapbox上にあるのと同等の記憶をKeicho側も持ってるのでいいんだけど、普通にScrapbox側で書かれたページだとKeichoの側は記憶がないからどうなのか
- ユースケースは両方ありそう
    - Scrapboxで文章を書いていて、今書いている行で詰まったので今書いている行に質問をして欲しい
    - Scrapboxで文章を書いていて、一通り書き終わったが改善したいので好きな場所に質問をして欲しい
        - これに関しては「まず聞いて」モードでScrapboxのコンテンツを全部流し込んでからスタートするという手が考えられる
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>この件に関しては、範囲選択して開始することでどの範囲をボットに知っていて欲しいと考えてるのか自然に表現できると思った
    - ただ、選択範囲を一つの発言とするまずい
        - 引用が発言単位なので、1ページある発言をしたら毎回1ページの引用をつけてくることになる
    - なので初回にある程度大きな範囲が選択されてるなら「相槌モードにして一行ずつの発言とする」って処理が必要そう
    - 逆に言えばそれができると過去のどんなページでもいきなり全選択からのKeicho起動で「一番気になる行を引用して質問」ってなると思う

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>試してみよう
まず聞いて
[https://keicho.netlify.app/#talk=vqdsChYjEFQvnIADU3V3](https://keicho.netlify.app/#talk=vqdsChYjEFQvnIADU3V3)
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>はい
過去ログを貼ったScrapbox上から会話をするのはScrapbox上にあるのと同等の記憶をKeicho側も持ってるのでいいんだけど、普通にScrapbox側で書かれたページだとKeichoの側は記憶がないからどうなのか
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「Keicho」
ユースケースは両方ありそう
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「ユースケース」
Scrapboxで文章を書いていて、今書いている行で詰まったので今書いている行に質問をして欲しい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「Scrapbox」
これに関しては「まず聞いて」モードでScrapboxのコンテンツを全部流し込んでからスタートするという手が考えられる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「Scrapbox」
この件に関しては、範囲選択して開始することでどの範囲をボットに知っていて欲しいと考えてるのか自然に表現できると思った
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「ボット」
ただ、選択範囲を一つの発言とするまずい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「発言」
引用が発言単位なので、1ページある発言をしたら毎回1ページの引用をつけてくることになる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「発言」
なので初回にある程度大きな範囲が選択されてるなら「相槌モードにして一行ずつの発言とする」って処理が必要そう
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「発言」
逆に言えばそれができると過去のどんなページでもいきなり全選択からのKeicho起動で「一番気になる行を引用して質問」ってなると思う
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「Keicho」
おしまい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>あなたはこの会話で何が起きて欲しいですか？
相槌モードでScrapbox上の会話形態でない既存文章を流し込んでから会話をすることを試したい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「Scrapbox」は、どんな「Scrapbox」ですか？
チャットと違って箇条書きのWikiなのでユーザが書く時の心の状態が違ってそうな感じがある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 相槌モードでScrapbox上の会話形態でない既存文章を流し込んでから会話をすることを試したい
- この「Scrapbox」について、他に何かありますか？
特に複数人が共同編集のWikiだと流し込む文章が複数人によって書かれたものってケースがある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>あなたが価値を感じているのは何ですか？
これは予期してない使い方だけど、だからこそ何か面白い有益な用途が見つかる可能性があり、それを見つけたい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 相槌モードでScrapbox上の会話形態でない既存文章を流し込んでから会話をすることを試したい
- あなたはこの「Scrapbox」をどう知るのですか？
既に箇条書きで少し書いたものがあって、それに対してボットに質問してもらうことで話を先に進めたい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 相槌モードでScrapbox上の会話形態でない既存文章を流し込んでから会話をすることを試したい
- この「Scrapbox」に関して、何が起こるとよいですか？
Scrapboxにプログラムから書き込めるAPIがあれば人間が起動してやらなくても勝手に質問してくるボットが実現できるのだけど…
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>それには「Scrapbox」に何が起こる必要がありますか？
APIが追加される必要がある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「Scrapbox」に関して、それができますか？
無理だと思う
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > Scrapboxにプログラムから書き込めるAPIがあれば人間が起動してやらなくても勝手に質問してくるボットが実現できるのだけど…
- この「Scrapbox」は、どのあたりにありますか？
自律的なボットから見ると参加しにくい障壁の向こうにある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「ボット」は、どんな「ボット」ですか？
人間とは違って24時間活動できる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > Scrapboxにプログラムから書き込めるAPIがあれば人間が起動してやらなくても勝手に質問してくるボットが実現できるのだけど…
- この「Scrapbox」は、どこから来るのですか？
Notaから来る。僕が作ってるわけではないのでAPIを追加することはできない
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > Scrapboxにプログラムから書き込めるAPIがあれば人間が起動してやらなくても勝手に質問してくるボットが実現できるのだけど…
- この「Scrapbox」は、どこにありますか？
Notaのサーバに。ああ、オンプレミス契約をするとDockerイメージの形でやってきて自分で好きなサーバに入れられるかも
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > Scrapboxにプログラムから書き込めるAPIがあれば人間が起動してやらなくても勝手に質問してくるボットが実現できるのだけど…
- この「Scrapbox」は、何のようですか？
ある種のハンディキャップがある人を疎外してるコミュニティ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 自律的なボットから見ると参加しにくい障壁の向こうにある
- この「ボット」について、他に何かありますか？
一般的なホモサピエンスと同じように振る舞うことが求められていて、それができないのでコミュニティに入ることができない
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 自律的なボットから見ると参加しにくい障壁の向こうにある
- この「ボット」は、どこにありますか？
Scrapboxとは別のサーバにいる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 自律的なボットから見ると参加しにくい障壁の向こうにある
- この「ボット」は、どのあたりにありますか？
つまり直接的にアクセスできない場所にいる、それが問題なのかも？
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 自律的なボットから見ると参加しにくい障壁の向こうにある
- この「ボット」は、何のようですか？
読むことはできるが、ハンディキャップによって会話に参加する手段が封じられている人
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「ハンディキャップ」は、どんな「ハンディキャップ」ですか？
ブラウザを開いて書き込むことができない(とここまで書いて思ったのだけど一行ペーストするときの通信内容を見てそれを真似したら今回やりたいような1行書き込みはできる？？)
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 自律的なボットから見ると参加しにくい障壁の向こうにある
- この「ボット」に関して、何が起こるとよいですか？
今、ユーザが開いたテキストエリアに書き込むことしかできないため、自分で書き込み位置を決めることができない。箇条書きのWikiにいながら、末尾にフラットに加筆することしかできてない。人間同様に好きなタイミングで任意の場所に書き込めるようになるといい。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>それには「ボット」に何が起こる必要がありますか？
世界(Scrapbox)の側は不都合だが変わらないので、自分(ボット)の側が変わる必要があるということか。ブラウザ上でのカーソルの移動を実現できるようになるか、任意位置への行の追加時のネットワーク通信を真似できるようになるか、かな
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>「ボット」に関して、それができますか？
どちらも結構大変そうだけど、できるかも
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>
- >  > 世界(Scrapbox)の側は不都合だが変わらないので、自分(ボット)の側が変わる必要があるということか。ブラウザ上でのカーソルの移動を実現できるようになるか、任意位置への行の追加時のネットワーク通信を真似できるようになるか、かな
- あなたはこの「ボット」をどう知るのですか？
(Exit)

感想<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- あんまり「流し込んだことに対して質問」って感じではない
- 選択したキーワードは「Scrapbox」「ボット」「ハンディキャップ」なので話題のコアに絞り込むことはできてそう
    - むしろ絞り込みすぎて同じキーワードに対する質問ばかり繰り返されてるな
