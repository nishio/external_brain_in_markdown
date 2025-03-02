---
title: "チャットログからRegroupのマップを作る機能の解説を考えたい"
---

この機能: [[✅チャットログからRegroupマップを生成]]
- 最初は「Regroupのマップを作る」というまったく伝わらない表現をしていた。
    - 話の中で出てきた表現
        - 無限に広いホワイトボードボード(Regroup)
- 「付箋」も伝わらない
    - チャットログはダラダラと長くて再利用性が良くない。それを適度な長さに刻んで、意味の浅い部分を削り、意味の濃縮された部品を作る。それが付箋
- チャットは人とホワイトボード(Regroup)の間にある、という気づき
    - ![image](https://gyazo.com/91889ac39cebf6893b8355b6d450a3bf/thumb/1000)
    - このチャットをする前に手元で書いていたのはbeforeのような図、ユーザ不在
- 最初はこの機能のことだけを考えて、どう説明を書こうかと考えていた
    - そうではなく「文章を書くのが苦手な人のための支援ツール」として使い方を解説する流れの中に今回の機能が置かれるべき
    - Regroupの解説は不足している、以前から「具体的なユースケースに沿った解説が必要」とは思ってた
    - 言葉で説明しようとするのではなく、ゲームのチュートリアルのようにまず体験させることが必要
- 実際にこの機能で作った付箋を整理
    - [[Regroup:チャットログからRegroupのマップを作る機能の解説を考えたい]]
    - 話のスタートは「文章を書くのが苦手な人いますよね。でも文章の作り方をきちんと教えてもらってないだけだったりします。まず短い文章で部品を作り、それを組み立てることで長い文章が作られます。文章を書くのが得意な人はそれを頭の中でやれるだけ。」になるのが良さそう。
    - で、その後で具体的にどう部品を作るのか、どう組み立てるのか、の話になる。
    - 今回の機能はチャットボットと話したあとワンクリックで部品ができる機能。
- 今回実装した機能はこれ
    - ![image](https://gyazo.com/04c0720b60f1fdc8615243b434819b62/thumb/1000)
- 改めて「この機能はどういう機能なのか？」
    - [[チャットボットとの会話から自動的に文章構成のための部品を作る機能]]

<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはこの会話で何が起きて欲しいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>チャットログからワンクリックでRegroupのマップを作る機能ができたのでその解説を考えたい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「チャットログ」は、どんな「チャットログ」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>このチャットでこんな感じに会話をすることで溜まるテキストデータ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「チャット」は、どんな「チャット」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>コンピュータが質問をしてそれに人間が答えることで会話のキャッチボールというかテニスでいうところの壁打ちができる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「会話」は、どんな「会話」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>解説文を何もないところから書こうとするのではなく、とりあえず雑に「こういうことを書きたい」って宣言してから流れにまかせてつらつら書く
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「ところ」は、どんな「ところ」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「何もないところ」ね。文章を作るのが苦手な人が白紙の原稿用紙を前にうんうん唸ったりするんだけど、僕からすると文章を構成するということを教師がきちんと教えられてないのだと思う。まず部品を作って、それからそれを組み替えて流れを作るのが大前提で、文章を紡ぐのが得意な人はそれが脳内でできるだけなんだ。文章を作るためにまず部品を作るの。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「ところ」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>紙を使った指導だと、ポストイットに書いてからそれを並び替えよう、というやり方をするのだけど、物理的なポストイットを使うのではなく電子的にできるようにしたのがRegroup。チャットで話すだけで付箋の準備までが電子的に行われる。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「Regroup」は、どんな「Regroup」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>付箋を使ったKJ法を今までやってきて、不便に思ったところを電子的に解決したツール。紙と違ってズームインズームアウトができるとか、重要な付箋を大きな付箋にするとかができる。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたが価値を感じているのは何ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>付箋を作ってそれを並び替えて文章を構成するってのは、今まで書籍や講演で何度も使ってきていて僕にとっては価値が実証済みの方法論。今回この聞き出しチャットシステムのログからワンクリックで付箋作成がされるようになったことで、付箋を準備するところが大幅に楽になった。知的生産のプロセスが電子化されて機械によって支援されることで知的生産にかかる無駄な時間が削減される。知的生産性が上がる。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「チャット」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>言語化が苦手な人の中に、いきなり完成形の長文を書こうとして困難を感じる人とか、他人と会話するのはできるけど一人で言語化するのが苦手とかの人がいて、そういう場合、まずはチャットで書き出しをしてからそれを整理するってプロセスは言語化の支援になる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「チャット」は、どこにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>そういう壁打ちの相手になってくれるチャットボットが、スマホの中にいて、いつでもどこでも自分の都合の良い時に会話できるわけ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「チャット」は、何のようですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>聞き役に専念してくれる話し相手だね。[[生身の人間]]だと、相手も聞いて欲しい話があったりして、自分の思考をまとめたい時に相手の話を聞くハメになると脳が溢れてしまう。話すことで頭を整理したいというシチュエーションで、自分の話を始めたりしないで聞き役に徹してくれるチャットボットがいると人間より有益なわけだ。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「チャット」に関して、何が起こるとよいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>チャット単体だと、こうやって会話している中で気づきがあると良い。だけど今回の機能は、たとえチャットで気づきが得られなくても、原稿に書いたら良さそうなことをつらつらとチャットで話して、それから付箋で再構成するので、チャットの側では単に色々話せばよい。原稿に使う部品が出揃うといいけど、それの支援機能はないし、どんな原稿を書くか明確化されてないので何が必要かも明確ではないからニワトリと卵の関係だ。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「チャット」は、どのあたりにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>今回の機能に関して言えば人間とRegroupの間にあって、対話して引き出した上でそれを付箋にしてRegroupに配置して返してくれるイメージ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  チャット単体だと、こうやって会話している中で気づきがあると良い。だけど今回の機能は、たとえチャットで気づきが得られなくても、原稿に書いたら良さそうなことをつらつらとチャットで話して、それから付箋で再構成するので、チャットの側では単に色々話せばよい。原稿に使う部品が出揃うといいけど、それの支援機能はないし、どんな原稿を書くか明確化されてないので何が必要かも明確ではないからニワトリと卵の関係だ。
- あなたはこの「チャット」をどう知るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>僕は作者だしいっぱい使ってるから知ってるのだけど、まだ使ったことのないユーザにどうやってわかってもらうかは課題だね。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  チャット単体だと、こうやって会話している中で気づきがあると良い。だけど今回の機能は、たとえチャットで気づきが得られなくても、原稿に書いたら良さそうなことをつらつらとチャットで話して、それから付箋で再構成するので、チャットの側では単に色々話せばよい。原稿に使う部品が出揃うといいけど、それの支援機能はないし、どんな原稿を書くか明確化されてないので何が必要かも明確ではないからニワトリと卵の関係だ。
- この「チャット」は、どこから来るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>このチャットのことをSNSとかでたまたま知って使ってみた人がRegroupへのエクスポートまで体験するかっていうと、しないだろうな。だからむしろ文章を書くことが苦手な人のための支援ツールです、と言って、そのガイドでまずチャットと話し、それからRegroupで整理し、と手順の解説をやるべきかな。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「Regroup」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>聞き出しチャットほど解説がきちんと作られてない。説明なしで渡されてもユーザが使えなさそう。多目的に使えるツールだから説明が曖昧になる。文章を書くことの支援を目的としてチュートリアル的に作る方がいいかも。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  今回の機能に関して言えば人間とRegroupの間にあって、対話して引き出した上でそれを付箋にしてRegroupに配置して返してくれるイメージ
- この「付箋」は、どんな「付箋」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>チャットの文章が、適度な長さに刻まれたり、キーワードが抽出されたりしている
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「文章」は、どんな「文章」ですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>チャットの文章ってしばしばダラダラと長くて、そのままだと再利用性が良くない。なのでそれを適度な長さに刻んで、意味の浅い部分を削ったりして、意味の濃縮された部品を作る。それが付箋
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「付箋」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>元の文章から部品化したことで、動かして考えることができるようになる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「文章」について、他に何かありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>チャットの文章は、最終的につくる文章よりは短いけど、まずさらに短い文より小さい単位の部品を作る必要があるのだ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「文章」は、どのあたりにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>長い文章は、部品を組み立てた後にしかない。短い文章は、元になる考えが人間の中にあって、チャットボットの質問によって引っ張り出される
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「文章」は、どこから来るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>人間の中にまだ言語化されてない湖のようなものがあって、そこに釣り針を垂らすと文章が引っかかって、釣り上げられる、みたいなイメージ
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「文章」は、どこにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>引っ張り出された後はテキストデータとして目の前にある。だからそれを見てさらに考えたりとか、電子的に自然言語処理をしたりとかができる。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  チャットの文章ってしばしばダラダラと長くて、そのままだと再利用性が良くない。なのでそれを適度な長さに刻んで、意味の浅い部分を削ったりして、意味の濃縮された部品を作る。それが付箋
- この「付箋」は、どこにありますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Regroupの無限に広いホワイトボードにある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはその「Regroup」をどう知るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これもまた僕は作者なのでよく知ってるけど、ユーザにどう知ってもらうかが課題だね
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>
- >  チャットの文章ってしばしばダラダラと長くて、そのままだと再利用性が良くない。なのでそれを適度な長さに刻んで、意味の浅い部分を削ったりして、意味の濃縮された部品を作る。それが付箋
- この「付箋」は、何のようですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>付箋を動かして構成することに慣れてる人にとっては「このデジタルデータは付箋のようなものです」で伝わるんだけど、そうでない人には何に例えると伝わるのか、だよな。うーん、似た体験をしてないなら例えてもわからないわけなので、先に「まずはこの通りに操作してみましょう」で体験してもらう方がいいのかもな。ゲームの操作を比喩で教えるかチュートリアルを実際にプレイして教えるかみたいなもの。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>あなたはその「付箋」をどう知るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>僕自身が付箋とはなんなのかをもっと良く知る必要がある？ユーザが知るためにうまく解説するためには？
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「付箋」は、どこから来るのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>従来の紙でやる方法だと、人間が作らなければならなかったから、まずその段階で「後の作業がやりやすい適切な粒度の部品にする必要がある」「しかし後の作業なんか知らない」というニワトリ卵が発生してたんだけど、今回はそこの部分を僕が実装して自動化したんで、ユーザは付箋が作られた状態からスタートできる
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「付箋」に関して、何が起こるとよいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>付箋を動かすことによって緩やかにストーリーを作り上げていくプロセスをユーザが理解できるといい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>その「付箋」は、どのあたりにありますか？

[https://keicho.netlify.app/#talk=72bK8MugmqvAnbWIDG87](https://keicho.netlify.app/#talk=72bK8MugmqvAnbWIDG87)