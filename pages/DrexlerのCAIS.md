---
title: "DrexlerのCAIS"
---

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
CAIS = Comprehensive AI Services（[[包括的AIサービス]]）
- [[K. Eric Drexler]]「[[Reframing Superintelligence: Comprehensive AI Services as General Intelligence]]」
- `Future of Humanity Institute（Oxford）Technical Report #2019-1、210ページ`
    - [https://www.futureofhumanityinstitute.org/s/2019-1.pdf](https://www.futureofhumanityinstitute.org/s/2019-1.pdf)
- Drexler は1980年代に分子ナノテクノロジーを唱えた人

[[6-Pack of Care]] のマニフェスト ¶92 が系譜として挙げている
- >  The architectural case for this — that advanced AI is better reached as bounded, specialised services than as one all-managing agent — was set out within the same Oxford tradition by Eric Drexler's Comprehensive AI Services (2019); what the 6-Pack adds is the democratic legitimacy that decides who tends each garden.
- この一文は2026-06-28に追加された（audreyt/civic.ai の commit 80bcb54）

何に異議を唱えたか
- [[超知能]]の議論は、AI を「合理的に効用を最大化するエージェントの心」として思い描いてきた
    - 人間の意思決定者を理想化したモデルを、そのまま AI に当てはめている
- 実際の AI 技術は「心」とは似ていない
- 代わりに見るべきは
    - AI がどう作られるか（研究開発で）
    - 何をするか（タスクをこなしてサービスを提供する）
    - 何を可能にするか（人間の仕事の段階的な自動化）

主張の骨格
- 汎用の知能は、単一のエージェントでなく、サービスの集まりで実現できる
    - サービスが包括的（comprehensive）に揃えば、一般知能に期待された仕事はこなせる
    - 「新しいサービスを作る」こともサービスの一つ
- 再帰的な自己改良は、不透明な単一のエージェントの内部でなく、分散した研究開発の自動化として起きる
- エージェントは進歩の必然の原動力ではなく、サービスを提供する製品の一種
    - CAIS はエージェントを排除しない。エージェント型のサービスも含む
- 第12節「AGI agents offer no compelling value」
    - 包括的なサービスが手に入るなら、自己改変する AGI エージェントをわざわざ作る実用上の動機は弱い

安全の議論
- 範囲の決まったタスク（とくに時間の区切られたエピソード的なタスク）に最適化されたシステムは、[[自己保存]]・[[資源獲得]]のような[[開いた目的]]を持つ必要がない
    - [[Bostromの直交性テーゼ]]を逆に使っている：知能の高さとは無関係に、そう言える
    - サービスは「bounded results with bounded resources in bounded times」を出すよう最適化され、資源を求める動機はむしろ邪魔になる
- ただし「リスクがなくなる」とは言っていない
    - 第14節「The AI-services model brings ample risks」
    - 危険なエージェントを作る手助けになる、悪用する人に力を与える、有害だが魅力的な応用を加速する

[[Kami]] との対応
- 範囲の決まったタスク、限られた時間と資源 ↔ 有界性、資源の上限、期限（sunset）
- サービスの集まり ↔ [[singleton と plural stewardship]]
- 6-Pack が足したのは、誰がどの庭を世話するかを決める民主的な正統性
    - CAIS は「どういう形の AI が安全か」というアーキテクチャの議論
    - 6-Pack は「その範囲を誰が決めるか」という正統性の議論

よく出る批判
- 道具として作った AI も、エージェントにした方が役に立つので、エージェント化の圧力がかかる
    - CAIS 以前からある Tool AI 批判（Gwern「Why Tool AIs Want to Be Agent AIs」2016）
- 2026年はエージェント型の AI が主流になった
    - CAIS の予測は外れたとも読める
    - だからこそ範囲を仕組みで作り込む必要がある、とも読める（6-Pack の「boundedness is not intrinsic but engineered」¶87）

関連:
- [[Civic AI]]
- [[Audrey Tang]]
- [[シンギュラリティ]]
