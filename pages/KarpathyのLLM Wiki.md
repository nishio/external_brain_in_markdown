---
title: "KarpathyのLLM Wiki"
---

Andrej Karpathy が2026-04に提唱したパーソナルLLMナレッジベース手法。
- LLMが読み書きできる Markdown wiki に知識を蓄積し、Ingest/Query/Lint の3操作で育てるパーソナルLLMナレッジベース手法。

由来
- 2026-04-03 Andrej Karpathy の X 投稿「LLM Knowledge Bases」が大バズり
- 2026-04-05 フォローアップでブートストラップ用Gist（"LLM Wiki"というタイトル）が共有 → これが名称の由来
- Karpathy は OpenAI 創立メンバー、Tesla Autopilot 元責任者、CS231n、nanoGPT、Eureka Labs などの教育者・研究者
- 「vibe coding」という語を広めた人物でもある

3つの中核操作
- Ingest
    - 新しいソースを `raw/` に投入し、LLMが既存wikiと照合して関連ページを更新/作成、indexとlogを更新。1ソースで10〜15ページに影響することがあり、これは単発要約ではなく既存ネットワークへの「編み込み」
- Query
    - wikiに対する質問。LLMが関連ページを検索・統合し、出典付きで回答。良い回答はwikiに新ページとしてfiling backする — チャット履歴に埋もれないよう
- Lint
    - 定期的な健全性チェック。機械的（孤立ページ、壊れたリンク、未登録）+ 意味的（矛盾、stale claim、概念ページ不足、新質問の提案）。「成長方向の提案」までやる

西尾の実践（20+ Wiki から得た知見 [[KarpathyのLLM Wiki勉強会]]）
- 個人系Wikiが最も価値を出す（家計Wiki、猫Wiki など）— 一般知識との接続点が多数生まれる
- 「研究目的のWiki」と「プロジェクト目的のWiki」の区別が大事
    - 前者: 抽象化して整合性のあるネットワークが目的
    - 後者: 具体のレイヤーに接続する必要、作業から得た具体的知識をfiling back
- 「育ってから分ける」（株分け/kabuwake）が事前計画より良い
- 同時にactiveなのは6件程度 — wiki森は自然に注意配分を圧縮する
- Lintは想像より自動的に整えられていることが多い


2026-04-17
- KarpathyのTweet 1: [https://x.com/karpathy/status/2039805659525644595](https://x.com/karpathy/status/2039805659525644595) 2026-04-03
- KarpathyのTweet 2: [https://x.com/karpathy/status/2040470801506541998](https://x.com/karpathy/status/2040470801506541998) 2026-04-05
    - Gist: [https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)

いい名前が無さすぎて困っている<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- しかたがないので"KaparthyのLLM Wiki"と呼んでる
- [[LLM Wiki]] / [[LLM-Wiki]] は広すぎる

[/villagepump/AIを使った知識マネジメント](https://scrapbox.io/villagepump/AIを使った知識マネジメント)

2026-04-20~26
- [[家計LLM-wiki]]
- [[ブロードリスニング本Wiki]]
- [[サステナブル・ブランド国際会議 2026]]
    - 音声データからingest
- ChatGPT Proのサーベイ結果をingestしてから、各論文をingest
- 書籍の各章とCosense Export for AIをingest
- 他人との干渉が発生した方が面白いかと思ってこっちに書いてる: [/villagepump/AIを使った知識マネジメント](https://scrapbox.io/villagepump/AIを使った知識マネジメント)

2026-05-01
- Cosense上での議論を1-hopで周辺ページごとエクスポート
    - [/villagepump/赤リンクの数の議論のLLM Wiki](https://scrapbox.io/villagepump/赤リンクの数の議論のLLM Wiki)
- [[LLM Wikiは要約の改良版ではない]]
- 4/27~ [[猫LLM Wiki]]

![image](https://gyazo.com/0b92fc86b91b0d1a3f2faed8e91b80cb/thumb/1000)
- ChatGPTが作った適当なアイコン

2026-05-16
- [[Karwi]]
