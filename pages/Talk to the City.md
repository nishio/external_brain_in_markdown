---
title: "Talk to the City"
---

<img src='https://scrapbox.io/api/pages/nishio/nihia/icon' alt='nihia.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「Talk to the City」は、[[AI Objectives Institute]] (AOI)が開発したオープンソースの分析ツールです。このツールは、集団的な議論や意思決定の改善を目指しており、特に都市などのコミュニティとの対話を促進するために設計されています。
- [Talk to the City — AI • Objectives • Institute](https://ai.objectives.institute/talk-to-the-city)

## ツールの概要
「Talk to the City」は、TwitterのツイートやPolisの結果など、異なるソースからデータを収集し、それを視覚化マップとして提供します。これにより、異なる意見や議論のクラスターを可視化し、対話を促進します 。

## データのクラスタリング
このツールは、[[BERTopic]]という技術を用いてデータをクラスタリングします。BERTopicは、[[HDBSCAN]]と[[UMAP]]を使用して、異なる密度のクラスターを見つけることができます。これにより、データのクラスタリングがより安定し、パラメータの選択に対してもロバストな結果を得ることができます 。

# 実験と適用例
- AIと著作権: 文化庁が収集したAIと著作権に関するパブリックコメントを「Talk to the City」で分析し、可視化する実験が行われました 。
    - 2024年5月にやりました<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - [[AIと著作権に関するパブリックコメント]]
- [[国連IGF京都大会]]: 2023年10月 [インターネット・ガバナンス・フォーラム京都２０２３](https://www.soumu.go.jp/igfkyoto2023/)
    - Audrey TangがTalk to the Cityを紹介した
    - [/plurality-japanese/Audrey Tang Remarks in Plurality Seoul](https://scrapbox.io/plurality-japanese/Audrey Tang Remarks in Plurality Seoul)
        - この動画で軽く触れている
- 台湾の同性婚議論: 台湾の同性婚に関する議論を「Talk to the City」でレポート化する試みも行われています 。
    - [https://tttc-turbo.web.app/report/taiwan-zh](https://tttc-turbo.web.app/report/taiwan-zh)
- [[東京都知事選挙2024]]
    - [[安野たかひろ]]
- [[日テレNEWS×2024衆院選×ブロードリスニング]]


> [anderssandberg](https://x.com/anderssandberg/status/1849570772869656662) Talk to the City originally was conceived of by [[Peter Eckersley]] in a discussion we had about using AI to elicit preferences from large populations. I am happy to see what it has grown up into.
>  「Talk to the City」はもともと、ピーター・エッカーズリーが、AIを使用して大勢の人々から選好を引き出すことについての議論で考案しました。それが何に成長したのかを見るのがうれしいです。
>  >[nishio](https://x.com/nishio/status/1846185175518269742) Talk to the City was used in a special program by Nippon TV regarding an upcoming election, where live questions were asked to incumbent politicians.
>  「トーク・トゥ・ザ・シティ」は、日本テレビが控えた選挙に関する特別番組で、現職の政治家に生々しい質問を投げかける番組で使われた。
>  ![image](https://pbs.twimg.com/media/GZ726bAbAAApHYW?format=jpg&name=medium#.png)
[Anders Sandberg - Wikipedia](https://en.wikipedia.org/wiki/Anders_Sandberg)



[[ブロードリスニング]]
[[Polis 2.0]]