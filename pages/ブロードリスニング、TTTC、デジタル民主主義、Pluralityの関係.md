---
title: "ブロードリスニング、TTTC、デジタル民主主義、Pluralityの関係"
---

先日1時間の勉強会講義のために[[Talk to the City勉強会]]をつくった。これは長いので、LTをするために10分のバージョンを作った

# [[ブロードリスニング]]とは
> [nishio](https://x.com/nishio/status/1801205477990359465) ブロードキャスティングとブロードリスニングの違い
>  ![image](https://gyazo.com/1a5328d749ad7a4ad4525e7cbed2a01e/thumb/1000)
矢印の向きが逆



# [[Talk to the City]](TTTC)とは
![image](https://gyazo.com/e05735418ecaf67a8a95d29cd9806442/thumb/1000)
トピックがクラスタになって要約表示されるOSS(AGPL)のツール
- [https://github.com/AIObjectives/talk-to-the-city-reports/tree/main/scatter](https://github.com/AIObjectives/talk-to-the-city-reports/tree/main/scatter)
具体例
- [東京都議会で議論されている論点と質問](https://takahiroanno2024.github.io/tokyo-metropolitan-assembly-analysis-20240615/)
    - 6/15 [安野さんが公開](https://x.com/takahiroanno/status/1801856440145219827)
- [安野たかひろ都知事選出馬に関しての人々の反応と論点](https://takahiroanno2024.github.io/yahoo-comment-analysis-20240610/)
    - 6/12 [安野さんが公開](https://x.com/takahiroanno/status/1800734598344925656)
- [AIと著作権に関するパブリックコメント](https://nishio.github.io/tttc_aipubcom_japan/)
    - 5/31 僕がやった [[TTTC: AIと著作権に関するパブリックコメント]]



# Talk to the Cityの仕組み
- ![image](https://gyazo.com/0630e4176f72582ae4cb259e84268e0a/thumb/1000)
    - 入力は"comment-id"と"comment-body"の2カラムだけのシンプルなCSV
    - LLMで適度なサイズの意見を抽出
    - BERTopicでクラスタリングと可視化
    - Reactでそれを表示するWeb UIが作られていて、静的HTMLにレンダリング
    - それを今はGitHub Pagesでホストしている
- 1つPythonスクリプトを実行するだけで全部やってくれる！簡単！
- 入力データは政治と無関係でもよい
    - 例: 書籍一冊入れてみた: [[Talk to the CityでPlurality本の内容を可視化]]



# なぜ今までブロードキャスティングばかりで、ブロードリスニングが少なかったのか
![image](https://gyazo.com/8aed1a6ee239c672d1e504cdb48d0e9e/thumb/1000)
    - [[ブロードリスニング]]
- 情報を「複製」して伝える技術の方が早く発展し「多くの人に声を伝える」ことが可能になった(例: 1930年代のラジオ)
- しかし逆向きは無理だった、情報洪水が発生してしまった
- 2020年代になってLLM技術の発展によって情報を「要約」して伝えることが可能になった



# [[デジタル民主主義]]とは
- デジタル民主主義と投票・多数決は無関係
    - 「大勢でのコミュニケーションを改善して、集団の意思決定を助ける仕組み」と思った方がよい
- 「要約」技術が貧弱だった時代に「投票」が「人々の意見の要約」をする手段として発明された
    - 「箱に名前を書いた紙を入れて多数決で人を選ぶ」「選ばれた人が選んだ人の代表として語る」という仕組み
    - LLMの進歩で、よりよい「人々の意見の要約」の実現が可能になりつつある
    - とはいえ「紙と箱の投票」をベースにして組み立てられている今の「社会システム」を消して作り直すのは大変なので、少しずつやりやすいところから改善していくのが現実的
- デジタル民主主義と[[デジタル投票]]を混同する人が多い
    - 「[[民主主義]]=[[投票]]で[[政治家]]を選ぶこと」という思い込みが強い
    - この考え方だと「デジタル投票で政治家を選ぶためには[[公職選挙法]]の改正が必要だ〜」となるんだが、それは「やりやすいところから改善」じゃない
    - 例えば: [[参加型予算編成]], [[参加型予算編成:東京の事例]]
        - 杉並区の参加型予算編成では既にインターネット投票によって予算の一部の用途を決定している
        - 集団が意思決定をする方法は政治家を選ぶことだけではない



# [[Plurality]]とは
- 元台湾デジタル大臣[[Audrey Tang]]らが推し進めている社会運動
- Audrey TangとGlen Weylによる書籍が5/20に出た
    - ⿻數位 Plurality: The Future of Collaborative Technology and Democracy
    - 日本語: ⿻數位 Plurality: 協働技術と民主主義の未来
        - 未来の民主主義(=[[デジタル民主主義]])についての本
    - ![image](https://gyazo.com/1778594b1d609d53004799b20872cf33/thumb/1000)
    - 実はContributorです
- 日本語版は山形浩生さんが翻訳中、6章まで翻訳が終わった
    - CC0なので全部オンラインで読めるし、質問もできる
        - 詳しい話はこちら: [/plurality-japanese](https://scrapbox.io/plurality-japanese)
    - 年内にはサイボウズ式ブックスから出版予定
- AudreyはPluralityを世界に広めるために世界ツアーをする予定
    - 7月にAudreyたちが東京に来るのでイベントをする予定 [[Funding the Commons Tokyo 2024]]


# 参考資料
- [[Talk to the City勉強会]]
    - 多分現時点でTalk to the City周辺の概念に関するたぶん日本で一番詳しいまとめ
    - なぜそう思うというと、この記事を書くために台湾デジタル省の友人に色々聞いてたら日本における第一人者として開発元に紹介されたからw
    - 公開されてない情報も含めて色々知ってから書いてます
- Audrey Tangによる2023-12のPlurality Seoulでの講演(日本語字幕つけました)
    - [https://youtu.be/4J9v-j995LU](https://youtu.be/4J9v-j995LU)
    - Talk to the Cityについて語っている
- [[Audrey Tang]]のドキュメンタリー映画[[Good Enough Ancestor]]のトレイラー
    - [https://www.youtube.com/watch?v=Sqyxvyh69cU&t=8s](https://www.youtube.com/watch?v=Sqyxvyh69cU&t=8s)
    - 5/20にリリースされた、民主主義のアップデートについても語っている