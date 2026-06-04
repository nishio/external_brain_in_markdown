---
title: "LLM Wikiで賑わう一人の場所ができた"
---

<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>
- [[Scrapboxのprivate→public転送について]] (2021-05-04) で nishio が Keichobot 相手に 言語化 した状況:
    - private は「死んだメモの束」「枯れてる」「沈んでる」
    - 同じ nishio が書いているのに、private だけ干からびる
- なぜ private が枯れたか
    - 一人で private でやってたら沈み込み忘れ去られる
    - public は言及されることで改善のきっかけが生まれる、社会的トリガーが入ってくる
- → 賑わいの源は 「自分以外の知性との相互作用」。public Scrapbox は他人 (検索流入 / SNS 言及) が trigger を投げ込むので生き続ける。private は自分しかいないので、書き捨てて忘れる。

- 2021 nishio の解決案 (まだ実装できなかった)
    - ボットが中継する。ここは単なるコピーではなくもっと賢い仕組みにする余地はある
    - ボットは人間ではないので、他人に見せられないような情報を見せることができる
    - public を人間が即時更新 → ボットがそれを private に転載 → private と public の間で相互作用
- → AI / ボットを「もう一つの知性」として private に住まわせることで賑わいを生む案。ただし 2021 時点で利用可能な「ボット」は弱く (= GPT-3.5 以前)、operational に動かない vision にとどまった。

- 5 年後の本wiki (llm-wiki) を見ると:
    - repo は local file system 上の private, nishio 一人しか書いていない
    - にもかかわらず 激しく賑わっている (今日だけで 4 ingest、243 page、相互リンク多数)
- なぜ枯れないか:
    - → Claude Code (AI) が「もう一つの知性」として private に住んでいるから。
        - 毎 ingest: AI が raw を読む、既存 page と照合、リンクを張る、page を更新
        - 毎 session: AI が違和感を articulate し、handle crystallize を提案
        - 毎 file back: AI が ephemeral session を distilled page に変換
- これは 2021 nishio が「ボットが中継する」と posit した vision の operational 実装。設計の意図は同じ:
    - AI = private を読める (他人と違い「他人に見せられないような情報を見せることができる」)
    - AI = page 間相互作用を生む (一人では起きない link 生成 / 矛盾検出 / 統合)
    - AI = 社会的 trigger の代替 (他人による言及の代わりに、AI が問いを投げる)