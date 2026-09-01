---
title: "hybrid SSM/attention"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>Hybrid SSM/attention は、同じ言語モデルの中に次の二種類の記憶機構を入れた構成です。
- SSM([[State Space Models]])／Mamba系：過去を固定サイズの内部状態へ逐次圧縮する
- Attention系：過去の各トークンの表現を保持し、必要な位置へ直接アクセスする

知識表現として捉えるなら、"[[SSM]]は更新され続ける要約状態、[[Attention]]は検索可能なトークン別アーカイブ"という違いです。Hybridはこの二つを組み合わせた記憶階層だと考えると分かりやすいです。[[Jamba]]のように層単位で交互に置く方式と、[[Hymba]]や[[Falcon-H1]]のように同一層内で並列に動かす方式があります。

アテンションは長さLに対して$O(L^2)$

[2312.00752 Mamba: Linear-Time Sequence Modeling with Selective State Spaces](https://arxiv.org/abs/2312.00752)
- Mambaは$O(L)$

純粋なSSMは、任意に長い入力を固定サイズ状態へ押し込むため、無関係な細部を大量に保持しなければならないタスクでは「状態の混雑」が起きます。理論・実験の両面で、文字列コピーや文脈中の情報回収ではTransformerが固定状態モデルを上回るという結果があります。

[[Qwen3.6-27B]]はSSM hybridなのか
- 狭義には違います。ただし、設計思想はかなり近いです。→ Gated DeltaNetを使っている
- [[Gated DeltaNet]]は通常、Mamba型SSMではなく、固定サイズの行列状態を持つ再帰的な線形Attention／fast-weight memoryに分類されます。過去トークン別のKV cacheを固定サイズ状態へ置き換えるという点ではSSMと同じ役割を果たしますが、状態更新則がSSMとは異なります。
    - [2412.06464 Gated Delta Networks: Improving Mamba2 with Delta Rule](https://arxiv.org/abs/2412.06464?utm_source=chatgpt.com)

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 要するにアテンションが二乗のオーダーだとコストが高いのでそこを緩和することによって安価にロングコンテキストを実現しようと言うはなし

[[状態空間モデル]]
