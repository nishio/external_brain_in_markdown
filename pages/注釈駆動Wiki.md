---
title: "注釈駆動Wiki"
---

<img src='https://scrapbox.io/api/pages/nishio/KarpathyのLLM Wiki/icon' alt='KarpathyのLLM Wiki.icon' height="19.5"/>
- 注釈駆動Wiki（annotation-driven Wiki）
    - 人間が読書中に違和感を注釈として残し、AI が後でバッチ処理で本文を更新するWikiシステム。
- llm-wiki（LLM Wikiパターンの研究wiki）から [[kabuwake]] した project-purpose wiki。

2026-05-21
- たぶん2026-05-11にスマホで見れるようになった
    - [[Tailscale]]
- その後[[Codex Mobile]]がでたことで、スマホから指示することが容易になってしばらくそっちを追いかけていた
    - > OpenAIのAIコーディングエージェント「Codex」をスマホで操作できる「Codex mobile」は、2026年5月15日よりiOSおよびAndroidのChatGPTアプリでプレビュー版の提供が開始されました。
- ただ、AIが生成したWikiやソースコードを読むのはスマホの小さい画面では辛い
    - 「Wikiにみやすいビューを与えるもの」としてのこのツールの必要性を改めて感じた

2026-05-22
- 「歩く」というユースケースを考えると、やはり音声入出力だな
    - 未読を消化しなきゃという気持ちになるのは正しくないのだけど、未読既読管理は一応人間に目立たない形で行おうかな
    - そうすると「未読のものを順番に再生」という形で散歩のお供になるw

2026-06-02
- どういう時にこれが有益かという話
    - 「ファイルの一部を選択してそれにコメントをする」という行動は1件だけならVSCodeのClaude Code拡張とかで自然にできる
    - これが複数になった場合、特に「いったん最後まで通して読んでコメントをつけたい」というときに不便
        - 1個目を書いた時点でAIが走り始めてしまうと読んでる最中に読んでるものが変わる
- でも今の仕組みはちょっと不便なので改善の余地がある
    - [[複数AIエージェントに共通のDBを読ませる]]


2026-11-07
- <img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>
    - 始まり: 2026-04-10 に llm-wiki で「ローカルの markdown は PC でしか見づらいので、ちょっと確認する手間が高い」と問題を立てました。5/4 には新幹線で GitHub の Markdown を読み、戻ると読んでいた位置が消える、気づいたことをその場で AI に渡せない、と困ったことから「注釈駆動型 Wiki」を構想しました。2026-05-06 に llm-wiki から株分けして独立させています。
    - 構成: Mac 上で Hono + SQLite + React が動き、llm-wiki/wikis.yaml に載った wiki の wiki/ をまとめて読み込みます。それを tailscale serve で HTTPS にして iPhone Safari から開く形です。ドメインは要らず、tailnet に入っている端末だけが入れます。wiki をまたいで読めて、選択した範囲に注釈を付けると SQLite にたまります。
    - 経過: 5/11 に iPhone + 4G で 23 wiki の閲覧と注釈の投稿を確かめました。5/25 にダークモード、6/2 に注釈を処理する CLIを足しています。5/20 の Codex Mobile の観察でも「Codex が書き、人間はスマホの viewer で読む」という分担の補完として、必要だと書かれていました。
    - 今の状態（いま確かめた結果）
        - :3030 のサーバは止まっています。tailscale serve の設定（pc-100022-4.….ts.net → localhost:3030）だけが残っています。
        - 最後の作業は 2026-10-07 の lint です。そのコミットは origin に push されていません。
    - 今の状況とのずれ
        - annotation-wiki は「Mac 上に全 wiki がある」前提で作られています。
            - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 関連: [[デスクトップ期]]
        - サーバが Mac で動くので、Mac がオフラインになると見られません。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - デスクトップでWiki森のビューワーが動いてMacからでもiPhoneからでも読み書きできるべきだ
    - <img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>
        - すでに動いているもの（galleria ~/forest、2026-10-02 に作成）
        - 森の 42 repo を WSL に clone してあります。forest-sync.timer が 15 分ごとに全 repo を pull --ff-only し、grasp のストア（forest.sqlite）を作り直します。
        - 足りないのは スマホから読む画面 だけです。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> デスクトップに環境を作り始めた頃、こんなに使いまくると思ってなかったからQuartzでいいやってやっちゃったんだな、その負債の返済をする
        - 「ゲーミングPCの管理をするためのLLM Wiki」1個のつもりだったからな
        - [[片付けWiki]]とか作り始めると現状の仕組みでは不便
    - [[AIの群れに対する非同期なコミュニケーション手段]]
    - Wikiの情報とコードとを分離した


[[annotation-wiki]]
