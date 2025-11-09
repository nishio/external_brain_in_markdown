---
title: "embeddingとカーネル関数"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- [[カーネル関数]]とは[[内積]]の概念を一般化したもの
- 正規化されたembeddingベクトルにおいて内積が1に近いことを「距離が近い」と解釈している
- この「距離が近い」なら「関数の値も近い」よね、という仮定が、"カーネル関数によって入る関数の形状についての仮定"である
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
- 結論：ほぼ合ってます。が、[[ガウス過程]]の文脈では2点だけ補強するとさらに正確です。
- 1) カーネル＝「一般化内積」だけでなく“[[共分散関数]]”
    - GPでは $k(x,x')=\mathrm{cov}(f(x),f(x'))$ を直接設計するものです。
    - 内積の一般化という理解は正しい入口ですが、「どんな関数が出やすいか（滑らかさ・ふるまい）」まで決める事前（prior）の設計図になっている点を強調するとよいです。
    - [[RBF]]/[[Matérn]]のような“距離依存の（平衡・等方）カーネル”では「距離が近い ⇒ 関数値も近い」という仮定になりますが、線形・多項式・周期・スペクトル混合など距離だけではないカーネルもあります。
- 2) 「正規化embeddingで内積が1に近い＝距離が近い」
    - これは厳密に OK。単位長のベクトルなら
    - $ |x-x'|^2 = 2(1-\cos\theta)=2(1-x\cdot x')$
    - なので「内積が大＝ユークリッド距離が小」と同値です（ユーザーの確認済みの前提にも合致）。
- embedding向け：実用的なカーネル候補
    - Cosine/Linear（単位長に正規化して線形カーネル $k(x,x')=x\cdot x'$）
        - 単純・高速。相関は一次的（滑らかさの仮定が弱い）。
    - RBF（単位球での角距離版）
        - $k(x,x')=\sigma^2 \exp \Big(-\tfrac{|x-x'|^2}{2\ell^2}\Big) =\sigma^2 \exp\Big(-\tfrac{1-x \cdot x'}{\ell^2}\Big)$
        - 「近ければ強く相関・なめらか」仮定。[[GP-UCB]]([[Gaussian process upper confidence bound]])など探索方策と相性◎。
    - 他にも色々あるけど略<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - [[Matérn kernel]] これは知らなかったけどGPTが他のところでも言及してるのでリンクにしておく
- 直感をもう一歩
    - 「関数の形状」仮定
        - [[RBF]]：とても滑らか（無限回微分可）
        - Matérn (\nu) 小：より“荒い”地形も表現
        - 線形：一次的な傾きのみ
- あなたの説明に対する最終コメント
    - embedding用途の具体式として $k=\exp(-(1-x \cdot x')/\ell^2)$ を示すと、“コサイン類似度に基づくRBF” という直感に落ちます。
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- RFF（[[ランダムフーリエ特徴]], [[Random Fourier Features]]）を使っている、このことを解説して
- (GPTが出してきた説明は詳細すぎたので結論だけ引用
    - <img src='https://scrapbox.io/api/pages/nishio/gpt5/icon' alt='gpt5.icon' height="19.5"/>
        - 結論：単位長embeddingにRBFを当てるなら、ω をゼロ平均ガウスから引けばよい。
        - 単位長embeddingなら RBF＋RFF がまず鉄板。$\omega\sim \mathcal N(0,\ell^{-2}I)$ だけ覚えておけば動きます。
- スケールwを正規分布からサンプリングしたランダムなコサイン関数を作ってその足し合せで[[RBFカーネル]]を近似できる
