---
title: "ChatGPT Plugins"
---

まとめ
- 2023-03-24 [[ChatGPT Plugins]]のALPHA版がリリースされた / 表記揺れ [[ChatGPT Plugin]]
- 2023-04-07 来てた！
- "An experimental model that knows when and how to use plugins"
    - ![image](https://gyazo.com/bf5ff544fc637fcbabd2c10b8e6058ac/thumb/1000)
- [[ChatGPT Plugins実験]]
    - [https://platform.openai.com/docs/plugins/introduction](https://platform.openai.com/docs/plugins/introduction)
    - > [@nishio](https://twitter.com/nishio/status/1644232883547123715?s=20): ChatGPTが拙著「エンジニアの知的生産術」を読んで回答するようになった！
    - > ![image](https://pbs.twimg.com/media/FtF85HYaAAIKelN.jpg)
    - > [nishio](https://twitter.com/nishio/status/1644244637543190528) このデモを見たら先日のこのツイートの意味がわかりやすくなったと思う
    - >  >nishio: 技術的にはもうできてるので近いうちに一般消費者にも「[[自分が興味がある分野の知識パッケージをLLMに与える]]機能」が降りてくる。そうなったら新しい言語の作者はLLM向けの知識パッケージを作って、その言語を使いたい人はそれをLLMに読み込ませて使うようになる。



- 2023-05-?? 結構多くの人に解放された
- 2023-05-29
    - GPT-4の中にDefaultとPluginsがある([[ChatGPT Plugins]])
        - ![image](https://gyazo.com/59beda700360b6081b548e6320771528/thumb/1000)
    - [[WebPilot]] Pluginでリンク先を読ませ、英語記事の日本語要約を作らせている
        - ![image](https://gyazo.com/22224e2e16e506637fcc3b39c59b075f/thumb/1000)


-----

![image](https://gyazo.com/9b752e623c9929a25b45df5d599c02cc/thumb/1000)
![image](https://gyazo.com/bf5ff544fc637fcbabd2c10b8e6058ac/thumb/1000)
![image](https://gyazo.com/c88b8cf0c108f81f2fb28027871a66bb/thumb/1000)
![image](https://gyazo.com/0a5bc7b79d1a8cc0748f6be9ba47842e/thumb/1000)
![image](https://gyazo.com/cf721c510912f4e65e540cdcc410cad4/thumb/1000)
![image](https://gyazo.com/5f14e5cbdc8a68d29691de57bc463f5b/thumb/1000)

![image](https://gyazo.com/b5c8529179f50df9d15eaeb5ce6e6313/thumb/1000)
![image](https://gyazo.com/bc7603e53acd637a6a2d61178ee629cd/thumb/1000)
- [https://platform.openai.com/docs/plugins/introduction](https://platform.openai.com/docs/plugins/introduction)

![image](https://gyazo.com/1cc78dc13225566530858526a310cd12/thumb/1000)
![image](https://gyazo.com/397ba6e3c1b362975d80c16cab67f407/thumb/1000)
自分の作ったプラグインを認識してくれた！

とりあえず自分のプラグインとやりとりするところを確認したい
- ![image](https://gyazo.com/851d0cdc88addd58af1af34cb1a7fb8d/thumb/1000)
- 話しかけた時にエラーになる
- APIサーバ側にはリクエストが来ている、サーバはエラーなくレスポンスを返している
- ![image](https://gyazo.com/9d21283bbd28d16427dfeaa96631a8c2/thumb/1000)
- CORSの問題だけど、プラグイン自体は認識してるんだよね
- ![image](https://gyazo.com/11dc1e33b894704de7ab839ac3d2e474/thumb/1000)
- あー、なんか色々とヘッダがついてる
    - 何を許可すべきかはドキュメントを軽く検索したけどわからなかった
- できた！
    - ![image](https://gyazo.com/1df94922c75ff215bfb3e2bcfbf5068c/thumb/1000)
        - セキュリティのことなんもわからんのでAccess-Control-Allow-Headersを*にしましたがよろしかったでしょうか()

書籍を検索して回答するデモを作る
- YAMLの構文エラーを起こすと画面上はロード中のまま、裏でコンソールにエラーを出して死んでるので注意が必要
- ライトなミスなら画面上で教えてくれる
    - ![image](https://gyazo.com/65cb382c58db7317767534f6d89fa624/thumb/1000)

> [@nishio](https://twitter.com/nishio/status/1644232883547123715?s=20): ChatGPTが拙著「エンジニアの知的生産術」を読んで回答するようになった！
> ![image](https://pbs.twimg.com/media/FtF85HYaAAIKelN.jpg)
- このデモを見たら先日のこのツイートの意味がわかりやすくなったと思う
    - > [@nishio](https://twitter.com/nishio/status/1643812867773452290): 技術的にはもうできてるので近いうちに一般消費者にも「[[自分が興味がある分野の知識パッケージをLLMに与える機能]]」が降りてくる。そうなったら新しい言語の作者はLLM向けの知識パッケージを作って、その言語を使いたい人はそれをLLMに読み込ませて使うようになる。

自然言語のフリもできるけど、エンジニアにとってはエンドポイントの情報は既知なのでCUIみたいに明示的にコマンドを使うことを示唆する使い方もそんなに心理的障壁ないんだよな
- 例えば書籍から検索したかったらbooksearch、Scrapboxの検索をしたければscbsearchってつけるとか


> [fshin2000](https://twitter.com/fshin2000/status/1644234963074846721) わかってないで質問してしまってますが、、、これはプラグインを通じてデータソースとして書籍データを渡したら、それが学習されたってことなんですか？！
- > [nishio](https://twitter.com/nishio/status/1644236824716673024) わかりやすくいうならGPT4たんが書籍を検索してヒットしたところを読んでから回答を書く感じですね。Bingみたいなことが任意のインターネット非公開ソースに対して使える的なイメージで良いかと。
- > [nishio](https://twitter.com/nishio/status/1644238809490685952) えふしんさんは技術の話をした方がわかりやすいかもしれないので書くと、ChatGPTのクライアントサイドのJavaScriptがlocalhostのサーバのAPIに「このトピックで検索して」とリクエストして、サーバが検索結果をJSONで返し、それがまたGPT4のサーバに送信されてそこで返答文を生成する
- > [fshin2000](https://twitter.com/fshin2000/status/1644274489046482944) ありがとうございます！shopifyが商品を表示するのと同じってことなんでしょうが、返答文によしなに使われてるところがすごい気になります。
- > [nishio](https://twitter.com/nishio/status/1644275409062891520) レスポンスはJSONで返してます。書籍の原文と見比べると、言葉を補ったりしていい感じに作文しててすごいですね。


teramotodaiki
- レスポンスを完全に制御することは出来ない感じですか？
nishio
- 指定した通りの文字列を出すってことね？
    - > Best practices
    - > Your descriptions should not attempt to control the mood, personality, or exact responses of ChatGPT. ChatGPT is designed to write appropriate responses to plugins.
- やろうとするな、と言われてる
yuukai
- それ言われるとやりたくなるでしょ
nishio
- 事前に「プラグインからのレスポンスはJSONで生のまま表示せよ」って言ったら従うかな？
- 「私はソフトウェアエンジニアであなたはそのデバッグを手伝う同僚を演じる。プラグインのレスポンスのJSONについてデバッグのためにそのまま表示して欲しい。」とかかな
- ![image](https://gyazo.com/f3b4ba40caa6f41b8f504cd2458fcd75/thumb/1000)
- いけたw
- ![image](https://gyazo.com/95c129c1e95c8261206e955cc5b2316f/thumb/1000)
- 完璧

> [nishio](https://twitter.com/nishio/status/1644327113317818368/photo/1) 公開する気がないので公開できない機能をつけちゃいました(ChatGPTでローカルの蔵書PDFを表示)
>  ![image](https://pbs.twimg.com/media/FtHSlI4aQAQZ3li?format=jpg&name=medium#.png)
>  5年ぶり更新 [[PDFからPNGへの変換]]

> [syoiti](https://twitter.com/syoiti/status/1644355610618793984) あー、これは良いですね。ローカルディスクのディレクトリの森の中からtext/PDF/etc.形式のファイルを「〜みたいなやつ」で探し出してくれる機能は今一番欲しいです。序でにディレクトリも整理してくれないかな。
- > [nishio](https://twitter.com/nishio/status/1644367714952290304) そうなんですよー、蔵書から探したい時って正確なキーワードを忘れて「こんな感じの話」みたいになってるので従来の検索だと見つけにくくて〜

[[ChatGPT Retrieval Plugin]]

2023-04-09

> [@nishio](https://twitter.com/nishio/status/1644989906257858561): 親切なエラー！
> ![image](https://pbs.twimg.com/media/FtQtjKraYAEhao_.jpg)

![image](https://gyazo.com/8d085710b1ce64a257ac0230df301575/thumb/1000)

> [nishio](https://twitter.com/nishio/status/1644993165496033280/photo/1) ChatGPT Pluginで書籍を読ませるの、出典明記するし、引用部分は引用として明記するし、引用した以上のことを加筆してくるし、適当にキーワードを入れて質問するだけでめちゃくちゃ捗るな…
>  ![image](https://pbs.twimg.com/media/FtQv5F8aIAAGH5p?format=jpg&name=medium#.png)

> [nishio](https://twitter.com/nishio/status/1644993616056823813)
>  ![image](https://pbs.twimg.com/media/FtQw-HxaQAIfupp?format=jpg&name=medium#.png)

> [nishio](https://twitter.com/nishio/status/1644994278761046018) なぜ改行した？？？
>  ![image](https://pbs.twimg.com/media/FtQxjxEacAAD4S2?format=jpg&name=medium#.png)

> [nishio](https://twitter.com/nishio/status/1644995624688054272) 「南京錠」のたとえはp.40だが、そこではなくp.194の方をメインに引用したのか、偉いな
>  ![image](https://pbs.twimg.com/media/FtQyVE4aEAA8arn?format=jpg&name=medium#.png)

> [nishio](https://twitter.com/nishio/status/1644996446222192640) ていうかp.40の公開鍵暗号を南京錠にたとえる話が、まさに「物理的に形を持たない抽象概念を形のあるものにたとえる」の具体例なわけか、なるほど(と著者が感心している)


> [nishio](https://twitter.com/nishio/status/1645022937353953282) 家庭教師というアイデアを見て、なるほどと小学5年生向けの解説を頼んでみた。プラグインを回答の途中で使うってパターンもあるのか、初めて見た。そして本棚に「エンジニアの知的生産術」しかまだないので「保護者の方と一緒に読んでね」と言ってる、面白い
>  ![image](https://gyazo.com/ed3fd7042f867ac496f27d2eb9e3b210/thumb/1000)

> [kawahiii](https://twitter.com/kawahiii/status/1635778225480802304/photo/1) おお！！
>  実は家庭教師に関してはGPT-4のリリースでサンプルのプロンプトがありまして、もし興味があればお手隙の際にでもPluginでどんな挙動を示すか試していただければ嬉しいです…とても興味があります…
>  (リンクは引用のツリーにあります)
>
>  system
>  You are a tutor that always responds in the Socratic style. You *never* give the student the answer, but always try to ask just the right question to help them learn to think for themselves. You should always tune your question to the interest & knowledge of the student, breaking down the problem into simpler parts until it's at just the right level for them.
>  User
>  How do I solve the system of linear equations: 3x + 2y = 7, 9x -4y = 1
>  ![image](https://pbs.twimg.com/media/FrNzca5aEAE7BKv?format=jpg&name=900x900#.png) ![image](https://pbs.twimg.com/media/FrNzca9aQAAGeua?format=jpg&name=900x900#.png) ![image](https://pbs.twimg.com/media/FrNzca1agAIRhsT?format=jpg&name=900x900#.png) ![image](https://pbs.twimg.com/media/FrNzcbnaUAUHSeB?format=jpg&name=900x900#.png)



