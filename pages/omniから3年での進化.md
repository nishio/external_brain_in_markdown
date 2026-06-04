---
title: "omniから3年での進化"
---

<img src='https://scrapbox.io/api/pages/nishio/KarpathyのLLM Wiki/icon' alt='KarpathyのLLM Wiki.icon' height="19.5"/>
進化の3世代
- 2023-08  [[omni]]（vector-RAG + Scrapbox常駐 + cron）　[[AIが毎日研究ノートを書く]]
- 2025-12  diary（時系列ログ + repo単位 + 対話型） 　[[Claude Codeにdiaryを書かせる]]
- 2026-04  LLM Wiki（concept network + wikilink + 対話型） [[KarpathyのLLM Wiki]]

進化した部分:
- vector embedding → wikilink（説明可能性へ）
- 自走（cron）→ 対話的（人間のリズムへ）
    - これは本当か？自走する方が適切なのでは？<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - omniの時代に対話的にやるのはレスポンスの時間の長さによって体験が悪かった、ということでは
- 時系列 → 概念ネットワーク（**diary-vs-llm-wiki**の本質的な差）

omniにあって LLM Wikiにない要素（実装可能）
- 赤リンク延伸: **X** を置くと AIが「説明のある検索」を返す
- マルチヘッド: 複数トピックの並行発展
- Pioneer Mode: スマホからエージェント起動
これらはLLM Wikiでも実装可能で、特に「赤リンク延伸」は次の改善候補に有力です。