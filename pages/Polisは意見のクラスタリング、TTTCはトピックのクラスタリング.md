---
title: "Polisは意見のクラスタリング、TTTCはトピックのクラスタリング"
---

from [[Talk to the City試す]]
[[Polis]]は[[意見のクラスタリング]]、[[Talk to the City]]は[[トピックのクラスタリング]]

TTTCは「[[意見のクラスタリング]]」ではなく「[[トピックのクラスタリング]]」
- [[Talk to the Cityのクラスタリング]]をみた時点でそうなのではと思っていたが、具体的な事実で捕捉された
    - [[BERTopic]]、TF-IDFだし、実際の実装でも[[CountVectorizer]]を使ってる
- つまりどういうことかというと「Xを禁止しろ」と「Xを妨げるな」は同じクラスタに入るということ。
- ![image](https://gyazo.com/1dce5751a19f8b8a3aa63f7b610c478f/thumb/1000)
- ![image](https://gyazo.com/a89d24e0979cb84b551be5de6ec47b80/thumb/1000)
- [[著作権法30条の4]]は[[著作物に表現された思想又は感情の享受を目的としない利用]]に関して著作権を制限する規定
    - 前者はこの規定がクリエイターの福祉を損なう(からbadだ)と言ってる
    - 後者はこの規定のただし書ただし、当該著作物の種類及び用途並びに当該利用の態様に照らし著作権者の利益を不当に害することとなる場合は、この限りでないをメディアなどの権利者が拡大解釈して強く使うと、「AI 開発のための大規模な言語データ収集」を妨げる(からbadだ)と言ってる
        - つまり「AI 開発のための大規模な言語データ収集」はGoodだと言ってる
    - この二つは近い位置にplotされている
    - この種のgood/badの感情([[センチメント]])を分析する仕組みは入ってない

