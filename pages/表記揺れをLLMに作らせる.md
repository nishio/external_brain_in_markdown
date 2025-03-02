---
title: "表記揺れをLLMに作らせる"
---

[[表記揺れ]]を[[LLM]]に作らせる
from [/villagepump/2023/03/25](https://scrapbox.io/villagepump/2023/03/25)
<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- 「高速に動作すること」が文房具には重要だと思うので今のScrapboxが今の実装なのはいいと思うが、もしChatGPTが100倍速くなったらなら「リンクが文字列完全一致でしか張れない」というのは明らかに不便
    - その時代のScrapboxはどうなっているべきなのか
    - リンクを入力してるときに曖昧検索がされて「似た文字列」が出てくるのは良い特徴
    - それと同一の文字列にするかどうかは微妙
        - 同じ文字列にしていい場合
        - 違う文字列のままにしたいがリンクもしたい
    - [[Helpfeel]]的な仕組みが良さそう<img src='https://scrapbox.io/api/pages/villagepump/blu3mo/icon' alt='/villagepump/blu3mo.icon' height="19.5"/>
        - 例えば「元気がない時にすること」というページがある時
        - 「(元気|エネルギー|やる気)が(ない|尽きた)時に(すること|やるべきこと)」みたいなバリエーションをLLMに生成してもらって、それら全てが曖昧検索等で見つけられるような仕組み

