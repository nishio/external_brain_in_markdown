---
title: "OpenAIの「Democratic inputs to AI」に応募した話"
---

for [[LLM Meetup Tokyo #3]] 2023-07-05 by 西尾泰和
- backup from [/omoikane/OpenAIの「Democratic inputs to AI」に応募した話](https://scrapbox.io/omoikane/OpenAIの「Democratic inputs to AI」に応募した話)

# OpenAIの「[[Democratic Inputs to AI]]」
- 5/25にアナウンスされた: [Democratic inputs to AI](https://openai.com/blog/democratic-inputs-to-ai)
- OpenAI「民主的プロセスを改善する実験を支援します」
- 総額$1,000,000……いちおくえん？！
- 何これ？[[民主的プロセス]]？？OpenAIはなぜこれに1億円も出すの？？？

# 「Democratic Input to AI」の目的
- AIは経済的社会的に広範囲な影響をもたらす
- 「AIがどうあるべきか」の[[意思決定]]が、営利企業の経営陣のような「[[少数の人間]]」によって行われるのは正しくない
- [[公共の利益]]を反映した「[[多様な視点]]」によって形成されるべき
- この方向性の第一歩を踏み出すために実験プロジェクトを支援する
- 「AIシステムが従うべきルールとは何か」という疑問に答えることができる[[民主的プロセス]]の[[概念実証]]を開発する[[チーム]]を募集する
- 私たち(OpenAI)はこれらの実験から学び、[[よりグローバルで、より野心的なプロセスの基礎]]としたい
- [[意思決定]]に関連する問題を探求し、将来的にはより直接的に意思決定に情報を提供できるような、[[新たな民主的ツール]]を構築することを期待している。

- すっごく面白そうじゃん？！<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='/nishio/nishio.icon' height="19.5"/>
    - OpenAIが旗を振ってる「[[AIの未来のための試み]]」に参加するのが面白い！
    - [[よりグローバルで、より野心的なプロセスの基礎]]を作ることに関与したい！！

# 応募した！！
- 7/15に結果がわかる
- 普通こういうのは採否未定の段階では話さないんだけど、プロジェクトの計画を立てるうちにプロジェクトメンバー自身がワクワクし始めて「面白いから採否関係なくやっちゃおう」ということになった
- もう活動開始して、プロジェクトへの参加を受付開始している

# 採択されたらやらなければならないこと
- 要件
    - 500人以上が参加する実験を行う
    - 実験から得られた知見に関して10/20にレポートを公開する
- 「500人以上が参加」この要件が難しそう…？

# [[Code for Japan]]
- ここでCode for Japanの話
- Code for Japanは2014年に設立された一般社団法人
    - > [[Code for Japanの目的]]: 公共サービスを市民参加型のプロセスを通じて改善し、より良い政府・自治体の実現を通じて社会に貢献する
- 2020年から参加型民主主義プラットフォーム[[Decidim]]を日本国内に展開
    - [[加古川市]]ではこれまで25の[[政策作成プロセス]]が行われ、多いものでは4,500ユーザーを獲得した
- 今回Code for Japanのプロジェクトとして応募した
    - 代表理事である[[関 治之]]さんがメンバーの一員
        - 「500人？問題ないでしょう！」
    - OpenAIとの契約などはCode for Japanが法人格としてやってくれる
    - (こういうときに活動実績のある法人格が動くと諸々とてもやりやすいのでありがたい<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='/nishio/nishio.icon' height="19.5"/>)
- という経緯で実現可能性が格段にアップ！

# プロジェクトの構造
- 詳しい説明に入るまでに少し「ピザ」のたとえ話
    - 「ピザの土台」があれば、その上に色々な「トッピング」ができる
    - プロジェクトの最低限の遂行はピザの土台部分が担保するので、トッピングでは個性的な実験ができる
    - トッピングは好き勝手に試行錯誤して、うまくいったものだけ最終的にリリースすれば良い
    - ここにいる人はみんな個性的なトッピングを作れる人たちだと思う
- ピザの土台は「[[SFプロトタイピング]]+[[Polis的システム]]」の[[反復構造]]
- そもそも[[民主的プロセス]]とは？[[OpenAI]]による定義:
    - 「民主的プロセス」とは、
        - (A)広く代表的な人々が意見を交換し、[[熟議]]を行い、
        - (B)透明な[[意思決定プロセス]]を通じて
        - (C)最終的に結果を決定するプロセスを意味します。
- ろくに議論をしないで投票をするのは民主的プロセスではない
    - 自分と異なるクラスタの人との[[熟議]]の場が必要
    - 熟議のためには共通の「[[議論の土台]]」が必要
    - それをどうやって作るか？そこでSFプロトタイピングだ
- ソフトウェア開発では、プロトタイプを作ると[[改善すべき点]]がより具体的に見えてくる
    - しかしソフトウェアでプロトタイピングするのは、ソフトウェアエンジニアしか参加できない
    - だから日本語で未来のストーリーを作るプロトタイピングが必要、これがSFプロトタイピング
    - LLMの支援でSF作家ではない一般人でも[[未来をプロトタイピングする手段]]を手に入れる
- 作られたストーリーは「[[こんな未来が起こりうる]]」という[[共有認識]]を形成する
    - いくつものストーリーによって[[未来の幅]]が見えるようになる
    - これが「どうすればより良い未来にできるか」を議論する土台になる
    - ![image](https://gyazo.com/d08523ec36905df9adc7a87f092bffe4/thumb/1000)

# Polis的システム
- [[Polis]]のことはOpenAI自身もグラント解説文の中で名指ししているし、実例としてPolisにインスパイアされたシステムを紹介している、この分野を語る上で重要な要素技術
    - 先日[[Anthropic]]とPolisのジョイントチームからプレプリントが出てたので読むといいかも
        - [/nishio/Opportunities and Risks of LLMs for Scalable Deliberation with Polis](https://scrapbox.io/nishio/Opportunities and Risks of LLMs for Scalable Deliberation with Polis)
- Polisは複数人が複数の質問にYes/Noで答えることで「[[投票行列]]」ができ、これの可視化とクラスタリングをするシステム
- ![image](https://scrapbox.io/files/64a1c2e1128d84001bd26066.png)
- 複数人が複数の質問に答えることで「人々の主観の分布」を得る
    - [[一人の主観から大勢の主観へ]]
- 我々のチームは今はPolisを単なるユーザとして使っているけど、それだと技術的に新しいことにチャレンジしにくいので、新しいシステムを作りつつある: [[コモレビカガミ]]

# SFプロトタイピングとPolis的システムを繰り返す
- ![image](https://scrapbox.io/files/6499b485af32bb001bf19a81.png)
- イテレーションを繰り返すことによって徐々に改善していく、という[[反復構造]]
- ストーリーに対する読者のフィードバックを集め、それを可視化することによって新たなアイデアが生まれ、また新しいストーリーが作られる
- それらが全部蓄積していった結果として…

# [[日本文化AI]]ができる
- 日本語話者の思考や感情をデータセットとしたAIができる
    - このAIは世界中で利用可能になり、人々がそれぞれの言語で会話できるようになる
    - このAIは言語の壁を越えて[[異文化理解]]を促進し、[[地球規模の熟議]]の前提となる
    - [[よりグローバルで、より野心的なプロセスの基礎]]
- 「日本文化」って言葉で古典的文化を連想する人も多いかもしれないが、まずイメージして欲しいのは
    - [[ドラえもん]]
        - 44年間続いている[[SF]]アニメシリーズ
        - 日本でドラえもんを知らない人はいないだろうし、世界でもかなり認知が広がっている
    - ドラえもんは「[[AIは友達]]」的な世界観を生み出している
        - ハリウッド映画的「人類を滅ぼそうとするAI」ストーリーに対するアンチテーゼ
        - 「人類を滅ぼそうとするAI」ストーリーに立脚して悪い未来を思い描いた人は、AIに対する法的拘束力のある規制を作ろうとする
- もう一つ、プロジェクトの参加者から出てきたキーワード:
    - [[付喪神]]
        - 人間が作った道具が、長く使っているうちに魂を持つようになり、最終的に[[神]]になる
        - LLMが賢くなって、人格的存在になる未来イメージ
        - それを「神」と呼ぶことに、一神教文化圏の人は反発する
        - 日本の「神」の概念が一神教の神とかなり違うもの
        - 日本はキリスト教の割合が1%しかない、一方アメリカは7割近い
    - AIは道具、人間に匹敵する能力を獲得しないように規制すべきだ論
        - 神が人間を作った
        - 神は人間より上位の存在
        - 人間がAIを作った
        - AIが人間に匹敵してしまうと？
            - 「被創造物が創造主に並びうる」は「神は人間より上位の存在」という概念への挑戦になってしまう、不遜！
            - 人間が「人間を作る」という神の御業をしたことになる
                - クローン人間同様に倫理的に好ましくない！
    - [[地球規模の熟議]]を可能にするには、こういう文化的な考え方の違いを互いに理解していく必要がある
        - ドラえもんや付喪神の概念を世界の人々が理解するためのアクションが必要

# [[日本文化AI]]の技術的実現可能性
- 夢物語のように感じられるかもしれないけど、技術的な実現可能性は高い
- まず「コミュニケーションの場」としてScrapboxを使用している
    - 生成されたストーリーや、感想、その他の雑談など、なんでもここに書かれる
- 実現済みの実装
    - ScrapboxのデータをGithub Actionsで1日1回データをエクスポートする
    - 500トークンのチャンクに分けてOpenAI Embedding APIでベクトル埋め込みし、Qdrantに格納している
    - Qdrantでベクトル検索が可能なWebサービスを公開済み: [[Omoikane Vector Search]]
    - あとは英語のUIとChatGPT APIとの繋ぎこみを作れば世界にリリースできる[[Minimum Viable Product]]になる
- 単なる自然言語コーパスと違って面白い点
    - ![image](https://scrapbox.io/files/64a1d12aa415f7001b913af4.png)
    - [[Polis的システム]]から「この問いに37%が賛成、37%が反対、25%が棄権」というデータが取れる
        - 「大勢の人の主観の分布」というデータ
        - 自然言語文と数量データのペアになってるので、ベクトル検索で前半の文章を引っ掛けて、数量データをプロンプトに積むことで、チャットボットは日本人の思考や感情の分布を知った上で話すことができる
    - 将来的にはFunction CallingでPolis的システムに質問を投げて人間の反応を集める仕組みを構築するのも面白そう
        - LangChainの[[Human as a Tool]]を[[People as a Tool]]に推し進める感じ

# オープンベータ中！
- ある参加者の感想
    - > 新作[[MMOTRPG]]の[[オープンベータ]]だと思っている<img src='https://scrapbox.io/api/pages/nishio/tsuzumik/icon' alt='tsuzumik.icon' height="19.5"/>
    - [[採否は未定]]ですが、オープンベータでプロジェクト自体のプロトタイピングをしています！
    - もちろん7/15に採択が決まった後で参加するのもウェルカムです！
- [[多様な視点]]を集めるために、いろいろなコミュニティの人を勧誘したい
    - このコミュニティはAI活用に肯定的で、みずから実装もできる人の集まりだと思う
    - みなさんが生み出したものが恐怖に怯えた[[ラッダイト]]に叩き壊されないためにも、[[共通理解]]を生み出していくことが大事！
- 参加はこちらから: [[プロジェクトに参加する]]