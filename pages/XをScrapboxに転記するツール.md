---
title: "XをScrapboxに転記するツール"
---

from [[日記2025-11-04]]
XをScrapboxに転記するツール
XをScrapboxに転記するChrome拡張が動かなくなってる、たぶんXの側のUI変更
- こういうのをメンテすることをAIにさせたい
- そもそもソースコードはどこか
結論
- "Chrome拡張"という記憶が人間のハルシネーション
    - 正解はTampermonkey
- Tampermonkeyが正常に動いてないだけだった
    - ブラウザを再起動したら治った
    - [[Tampermonkey]](2021-09)のページから[[TwitterをScrapboxにまとめる]](2021-04)を発見したが最新版はどこか
    - Tampermonkeyならx.comに対するarrow指示が含まれているはず、とGitHubを検索
        - [https://github.com/nishio/twitter_to_scrapbox_gpt/tree/main](https://github.com/nishio/twitter_to_scrapbox_gpt/tree/main) (2023-03)
            - [/villagepump/Twitter to Scrapbox GPT](https://scrapbox.io/villagepump/Twitter to Scrapbox GPT)
                - > 2023-03-21にGPT4にプログラムを書かせる実験として作った

1ポモドーロ調査して、README改善をDevin.aiに投げた
