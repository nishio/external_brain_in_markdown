---
title: "Satya Nadella on the Future of SaaS"
---

Satya Nadella on the Future of SaaS, How 2025 is the year of Agents, Advice for Indian Engineers
[https://www.youtube.com/watch?v=GuqAUv4UKXo](https://www.youtube.com/watch?v=GuqAUv4UKXo)
「Is SaaS Dead?」という言葉で話題になった動画(2025/01/13)
- 実際はSaaSが死ぬとは言っていない(が今のままで存続するとも言ってない)

<img src='https://scrapbox.io/api/pages/nishio/GPT/icon' alt='GPT.icon' height="19.5"/>
Satya Nadella's statement:
- > "This time around the thing about agents is they are not going to be bound to essentially anyone’s SaaS application and its data, right? So I’ll have an agentic sort of view where the task, the intent, and I will go operate and orchestrate all the logic across multiple SaaS applications, right? I’ll go call a bunch of APIs through tools use, so I’ll call a bunch of APIs. I will in fact most likely fine-tune my model to know about multiple SaaS applications in the agent tier and so that’s what’s going to happen."
- エージェントは、基本的に誰のSaaSアプリケーションやデータにも縛られることはありません。だから、私はエージェント的な見方でタスクや意図を把握し、複数のSaaSアプリケーションにまたがってすべてのロジックを操作し、オーケストレーションします。ツールを使ってAPIをたくさん呼び出します。実際には、エージェント層で複数のSaaSアプリケーションについて知るためにモデルを微調整することになるでしょう。
- > "So I think what’ll happen is these CRUD… I mean SaaS applications are a CRUD database with a lot of business logic. So the CRUD database will then get orchestrated outside of the business logic tier of just the SaaS application is what I mean is going to happen."
- つまり、SaaSアプリケーションは、多くのビジネス・ロジックを含むCRUDデータベースなのです。つまり、CRUDデータベースは、SaaSアプリケーションのビジネス・ロジック層の外側でオーケストレーションされることになります。
出典: Interview with Satya Nadella, Timestamp ~1:09-2:01

この発言から、ナデラ氏はAIエージェントがSaaSアプリケーションを横断して業務を遂行し、データベースのCRUD操作をSaaSのビジネスロジック層の外部でオーケストレーションする未来像を描いていることが分かる。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
簡単に言うと、ソフトウェアは「渾然一体の一塊のもの」から「ロジック部分と、データを永続化する部分」という形に分離してきた。それが[[(1.4.4) Model / View / Controller]]だったりとかデータベース(RDBMS)の発明と分離だったりするわけ。で、その構図がシフトして、エージェントの[[オーケストレーション層]]がかつてのロジック層相当になり、SaaSはかつてのデータベース層になる、というわけ。
個人的にはエージェントのオーケストレーション層には時間とコストと不確実性のオーバーヘッドがあるので、エージェントを通さずに操作したいニーズは残り続けると思う。ただ、オーバーヘッドの縮まる速度が思った以上に速い。

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>+<img src='https://scrapbox.io/api/pages/nishio/o3-mini-high/icon' alt='o3-mini-high.icon' height="19.5"/>
サティア・ナデラのインタビュー内容を簡潔にまとめると以下のポイントになります:

- アーキテクチャの進化
    - 昔はアプリ内に組み込まれたISAMデータベースから、リレーショナルデータベースによりデータとロジックを分離。
    - SaaSはCRUD操作とビジネスロジックを持つ形態で普及してきたが、今後はこれを超える新たな形態が登場する。
- エージェントの登場
    - 新しいパラダイムは、個々のSaaSアプリケーションに縛られず、複数のシステム間を統合・調整する「エージェント」が主役となる。
    - エージェントは複数のAPIを呼び出してデータを取得・統合し、効率的なワークフローを実現する。
    - 例として、CRMやOffice365などから情報を引き出し、統一されたデータを使った業務プロセスが挙げられる。
- SaaSは“死んだ”のではなく変革期にある
    - 従来のSaaSは「データベース＋ビジネスロジック」という構造だが、今後はエージェント（AIアシスタント）が各種SaaSやツールのAPIを統合的に呼び出し、ユーザの意図に応じて処理を行うようになる。
        - その結果、ユーザがわざわざ個別のSaaSにログインして操作する必要が減り、SaaSの価値は「エージェントが参照可能なデータや機能を提供する」部分に移っていく。
- エージェント化による大きな変化
    - 人を雇う際も「エージェントの活用力」や「どんなエージェントを使えるか」が重要になる。
        - 個人レベルでも「自分専用のエージェントを複数持ち、それらを組み合わせて業務効率を高める」使い方が一般化していく。
- インドを含む各地域にとっての機会
    - 大規模言語モデルは多様化し、さまざまな業種・領域・科学研究向けの最適化モデルが必要になる。
        - インドなどの開発コミュニティが新しいSaaSモデルやAIサービスを迅速に取り入れれば、大手に対する新たな攻撃（市場攻略）のチャンスになる。
- 若手エンジニアへのアドバイス
    - 若手エンジニアは、常に最新の技術（AIや新モデル）を試しながら、既存システムの最適化も同時に進める「[[ダブルギア]]」戦略が重要。
    - 急速な技術進化（数ヶ月ごとに性能向上するモデル）に対応するため、継続的な実験と学習が求められる。
- 今後特に注目される領域
    - 科学技術（化学、材料、バイオなど）への応用で大きな飛躍が見込まれる。
        - 大規模モデルと組み合わせた研究が新素材開発や創薬などを加速させる可能性がある。
- レガシー企業への提言
    - 過去のモデルでの失敗を基に導入を諦めるのは損失が大きい。
        - 使えそうな部分から着手して試行を続け、自社に合った形に最適化していく必要がある。

要するに「SaaSの時代が終わるのではなく、“エージェント主導”の新しいSaaS活用の形に変わっていく」というのがサティア・ナデラの主張です。

同じ動画に対する記事
- [「SaaSは死んだのか？」サティア・ナデラが語るAI時代のクラウドビジネス｜daka | AI](https://note.com/daka1/n/n6ba507aa0b1b?utm_source=chatgpt.com)
