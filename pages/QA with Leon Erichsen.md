---
title: "QA with Leon Erichsen"
---

[[Leon Erichsen]]
1. What do you see as the most urgent or overlooked issues in Japanese society today?
1. 今日の日本社会で最も緊急性の高い、または見過ごされている問題は何だと思いますか?

AIの発展が「全員に影響を及ぼす環境の変化」ではなく「一部の人が使うツールの変化」にすぎないと考える人が多い。Annoらのマニフェストを見ても「手段の話であってイデオロギーがない」などの批判をする人がいる。Pluralityの「21世紀の3つのイデオロギー」は技術との付き合い方に関する議論だが、まだその議論の枠組みが理解されていないように思う。これが見過ごされている問題。

緊急性の高い課題は、少子高齢化によって年金制度が破綻しつつあることだと思う。若い現役世代は高齢者を支えるための社会保障料の負担に苦しみ、高齢者世代へのヘイトを溜めていく。民主主義は「若者よりも人数の多い高齢者」が力を持ち、政治家も高齢者を重視して活動する。この世代間対立が高まると、民主主義ではなく暴力によって高齢者から力を奪い返そうとする勢力が強くなってしまう。

2. How would you describe your role in the Mirai movement -- what you do, and how you feel within it?
2. MIRAI運動におけるご自身の役割、つまり、あなたが何をしているのか、そしてその中でどのように感じているのか、どのように説明しますか?

Annoが都知事選に出た時、Talk to the Cityをもちいて民意を可視化するプロジェクトをやっていた。その後、Annoが東京都と一緒にブロードリスニングをもちいて長期戦略を策定した際に、Talk to the Cityとオリジナルのアルゴリズムによって協力していた。Annoが3月にリリースしたブロードリスニングのためのOSSツール「広聴AI(kouchou-ai)」において設計段階から関わっておりコードオーナーの一人である(メインの開発者は今回の選挙において候補者の一人として出馬するSumino Nasukaである)

今回の選挙戦に関しては、エンジニアの遊撃手として色々な情報を見て必要なところの活動をしているので、わかりやすい目立った活動はしていない気がする。今回はチームみらいのボランティアに対して希望者はAIエージェントのDevinを使い放題にしていて、そのための仕組みを作った。チームが受け取った寄付金額の可視化のバックエンドを実装した。ボランティアの郵便番号に基づく地理的な位置の可視化を実装した。GitHubで公開した政策案に対する2000件を超える修正提案をAIによって処理できる仕組みを作った。要約するなら、情報流通を促進していると言えるかも。

3. If Mirai were to succeed, what kind of Japan do you imagine? What would feel different in daily life?
3. もしMIRAIが成功するとしたら、どんな日本を想像しますか?日常生活では何が違うと感じるでしょうか?

成功の定義による。かなり高い確率で政党は成立すると考えている。その場合、AIを使って生産性を向上することについてしっかり体験に基づいて理解している党首による技術親和的政党が誕生することになる。これを私は堤防に穴を開けるようなものだと考えている。穴が開けばそこを水が流れて穴がだんだん大きくなる。

この話は安野と議論して合意したわけではないが、回答1とも関連すると思っている。世代間対立のエネルギーが物理的な暴力による実力行使ではなく、技術によってシステムをより良くしていくことに使われると良いと思う。そのための最初の道筋をつくることによって、暴力的な状態にならずに高齢化社会の問題を緩和していくことが長期的な意味での成功だと思う。

-----

- [[高齢者に対する暴力革命が起きる確率を下げることが課題]]
- [[義賊が若者の間で人気になる可能性がある]]
- [[「詐欺は社会正義」ナラティブ]]
-----

I was curious whether you’ve seen moments where this generational conflict has already tipped into more emotionally or physically violent territory. You described the risk so clearly -- and I can see how that underlying tension could easily intensify.
この世代間の対立が、すでに感情的または肉体的に暴力的な領域に突入している瞬間を見たことがあるのかどうか、興味がありました。あなたはリスクを非常に明確に説明しましたが、その根底にある緊張がいかに簡単に強まるかがわかります。

警察は高齢者を対象とした詐欺事件の増加に困っている。
2024は21,043件	718.8 億円、前年比+10.5 %（件数）／+58.8 %（金額）
[https://www.npa.go.jp/bureau/criminal/souni/tokusyusagi/hurikomesagi_toukei2024.pdf](https://www.npa.go.jp/bureau/criminal/souni/tokusyusagi/hurikomesagi_toukei2024.pdf)

この詐欺の実行犯は「高齢者が金銭を溜め込んでいるのは死に金であり、奪って貧困層に分配するのは正義である」や「高額な社会保障料を払わせられ、自分が高齢者になる頃には破綻して自分が受け取ることができない我々の世代は被害者である」といったナラティブで研修を行なっていることが知られている。

暴力的行動としては
2022年に起こった広域強盗事件が有名
[https://ja.wikipedia.org/wiki/ルフィ広域強盗事件](https://ja.wikipedia.org/wiki/ルフィ広域強盗事件)
この6月にも就寝中の高齢者宅を狙う窃盗が140件発生し、25歳被疑者ら3名が逮捕した。
前者ではTelegramが使われていたことがわかっており、首謀者の安全が高まること、実行で得られたノウハウが匿名性を保ったまま流通してしまうことが大きな問題だと思う。

Kouchou-AIはTalk to the Cityをもとに、安野らによる日本での実践から感じられた必要性をもとに機能追加をしたものです。
[https://note.com/nishiohirokazu/n/nb37adf96fe50](https://note.com/nishiohirokazu/n/nb37adf96fe50)
Digital Democracy 2030で活発に開発が進んでいます。
[https://github.com/digitaldemocracy2030/kouchou-ai](https://github.com/digitaldemocracy2030/kouchou-ai)

Devinは我々が作ったものではなく、Scott WuがCEOであるCognition社が提供しているサービスです。
[https://devin.ai/](https://devin.ai/)
私や青山さん、annoさんは日本におけるかなり早い時点からのユーザであり、先日Scott Wu氏から対談の申し込みがあったためYouTube動画を作った
このRefferalによって安野氏は潤沢なクレジットを獲得した。これを使ってサポーター(ポランティア)を含めたチームメンバーに対して、予算を気にせずAIエージェントを使える環境を提供している

[https://github.com/orgs/team-mirai/repositories](https://github.com/orgs/team-mirai/repositories)
[https://github.com/orgs/team-mirai-volunteer/repositories](https://github.com/orgs/team-mirai-volunteer/repositories)
後者がポランティアによる開発である、この後者の統計はここで見ることができる(これも私が作った)
[https://lookerstudio.google.com/u/0/reporting/e4efc74f-051c-4815-87f1-e4b5e93a3a8c/page/p_lcx31g9ktd](https://lookerstudio.google.com/u/0/reporting/e4efc74f-051c-4815-87f1-e4b5e93a3a8c/page/p_lcx31g9ktd)

PRの優先順位付けに市民を関与させる仕組みは長期的には重要な要素だと思う。GlenらのPlural Management論文を読んで、Plurality BookのProjectで使われているのも見た。彼らも同様の問題意識を持っているという理解だ。
一方で民主主義と意思決定速度のトレードオフがあると思う。選挙まで数週間というタイミングでは使いづらいだろうね。
こういう民主的なシステムは選挙のタイミングだけではなく日常的に動かすべきものと思う。その状況を作っていくために、今は選挙に集まる注目を生かしてそういう未来があり得るんだとより多くの人に認識させるフェーズだと思う。


