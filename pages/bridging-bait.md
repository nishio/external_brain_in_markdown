---
title: "bridging-bait"
---

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
[[Bridging Systems]] の論文（Ovadya & Thorburn 2023、arXiv 2301.09976 v3）が未解決問題として出した語
- OQ 3.6
    - > How could bridging signals be gamed or abused? What would "bridging-bait" content look like?
- clickbait の bridging 版: 「対立する両側から支持された」という信号を狙って作られた内容
- 論文は問いを出しただけで、具体例や対策は書いていない

同じ論文の近い指摘
- OQ 3.7: diverse approval（ふだん意見の違う人からの支持）のような信号は
    - > incentivize shallow content (e.g., cat memes)
- 5.2.1: 子犬の動画を上げれば多様な支持は増えるが、政治の議論の質は何も変わらない
- 結論: 「浅い bridging のヒューリスティック」から「深い bridging」へ進む必要がある、とするが方法は無い
- 6.2: 逆に、左右が共有する少数派への偏見のように、害のあるところに橋が架かることもある
    - > bridging is too neutral a goal
- OQ 4.3: [[グッドハートの法則]]

2つを分けると（Claude の読み）
- 浅い内容: 両側が賛成するが、対立とは関係がない（猫、子犬、一般論）
- bait: 両側の支持を取ること自体を目的に作られた内容。浅いとは限らず、信号の測り方の穴を突く
- どちらも「両側から支持された」という指標の上では、本物の橋渡しと区別がつかない

生成AIで作らせる場合（Claude の読み）
- 論文の中心は既存の投稿の順位づけで、生成には結論で「広げられる」と触れるだけ
- LLM に[[橋渡し文]]を作らせると、両側の賛成を最大化する文はいくらでも作れる
    - 順位づけなら浅い内容がたまたま上がるだけだが、生成では最適化の圧力が文の中身に直接かかる
    - bridging-bait を自動で量産しうる
- すでに出ている観察
    - [[ハーバーマス・マシン]]の後続研究（arXiv 2601.05904）は、支持を最適化すると短く当たり障りのない文になる危険をはっきり挙げる
    - Collective Dialogues（Konya ほか 2025、arXiv 2503.01769）の著者も、賛成の信号だけだと無難な文に偏ると認めている
- 避ける方向
    - [[Generative Social Choice]] は評価の問いを「賛成か」ではなく「この文はあなたの見方をどれだけよく表すか」にして、一般論に流れるのを避けている
    - [[意外な橋渡し文]]: 意外さを条件に入れる。誰も相手が一般論に反対するとは思っていないので、一般論は意外ではない（[[偽の分極]]）
        - ただし意外さを狙って最適化すれば、それもまた bait の的になる