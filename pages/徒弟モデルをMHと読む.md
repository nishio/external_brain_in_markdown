---
title: "徒弟モデルをMHと読む"
---

[[Civic AIと共生的アライメントの関係]]

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/> [[Audrey Tang]] のエッセイ「Inside the Kami」（civic.ai、2026-03-05）は、6-Pack の Pack 3 にある徒弟モデルを、[[メトロポリスヘイスティングス名づけゲーム]]（MH）として読めると書いている。その解説と、しっくりこない点。

徒弟モデル（Apprentice Model）とは
- [[6-Pack of Care]] の Pack 3「能力」（Competence）にある、AI を段階的に現場に入れる手順
    1. シャドーモード：AI は本物の入力を見て行動を提案するが、実際には動かさない。提案を人や従来のシステムの判断と比べ、ずれを調べる
    2. カナリアリリース：選び方を工夫した一部の実際のケースだけに出す。ずれが決めた範囲を超えたら自動で巻き戻す
    3. 全面展開：ガードレールをつけて全体に出す
- 台中の旋盤工が主軸の音で刃のびびりを聞き分けるような[[ポランニーの暗黙知]]を、AI が徒弟として学んでから信頼される、という筋書き。[[正統的周辺参加]]（Lave & Wenger 1991）も引いている

エッセイの読み
- >  CPC offers one further analogy. An apprentice that learns through accept/reject turn-taking with its cultivator (the Apprentice Model of shadow mode, canary and general release) can be read as approximate Bayesian inference. The analogy has a limit. In the naming game both sides take turns to propose and to judge. In apprenticeship the cultivator holds the brake. So the analogy fits the learning and says nothing about who holds the authority. Apprenticeship remains a civic practice, and the maths gives no proof that shadow-mode deployment converges in the field.
- 徒弟が提案し、親方が受け入れるか断るかを繰り返す。これは MH 名づけゲームと同じ形なので、徒弟の学びは近似的なベイズ推論として読める、という主張
- エッセイ自身が限界も書いている。名づけゲームでは両方が交代で提案し判定するが、徒弟では親方がブレーキを握る。だから、このたとえは学びには合うが、誰が権限を持つかについては何も言わない。数学は、シャドーモードでの展開が現場で収束することの証明ではない
    - （2026-11-19 訂正。このページは最初、2026-09 に取得した古い版を読んで書いていて、この限界の文が無い前提だった。civic.ai の今の版にはある）

MH 名づけゲームのおさらい
- 2 人が同じ物を見ている。話し手が、自分の信念から名前を 1 つ選んで提案する
- 聞き手は、自分の今の名前と比べ、自分の信念だけに基づいて、受け入れるか断るかを確率的に決める
- 役を交代しながら繰り返すと、共有の名前は、2 人の観測をあわせたベイズ事後分布からのサンプルになる（MCMC と等価）

しっくりこない点
1. 役が交代しない
    - MH 名づけゲームでは 2 人が交代で話し手と聞き手を務め、両方が信念を更新する。だから全員の観測を合わせた事後分布に行き着く
    - 徒弟モデルでは、判定するのは親方だけで、学ぶのは徒弟だけ
    - これは[[共生的アライメント]]論文の式 (5)、「階層的アライメント」の形に近い。特権を持つ監督者 h の分布に、他のエージェントが合わせる
        - `q(w|o^k) ≈ q(w|o^h_Human)`
    - 論文が乗り越える対象に挙げているのはこちら。共生的アライメントは式 (6) で、各自が、全員の観測から出る集合的事後分布に合わせる
        - `q(w|o^k) ≈ q(w|o)`
    - 暗黙知を学ぶ段階なら、親方に合わせるのが正しいとも言える。ただ「共生」の例として出すには合わない
    - エッセイの今の版も、役が交代しないことを限界として認めている（上の引用）。違うのは切り方。エッセイは「学びには合う。権限（ブレーキ）については何も言わない」と切る。ここで言っているのは、役が固定されると学びの形そのものが式 (5) になる、つまり学びの部分も共生的ではない、ということ
2. シャドーモードには、受け入れる・断るの判定がない
    - シャドーモードは、AI の提案と人の実際の行動を後から比べるだけ。聞き手が提案を受理するかを決める MH の手順そのものではない
    - MH に近いのは、次の段階で、人が AI の提案を採用するか却下するかを決める場面
3. 人は MH の規則どおりには受け入れない
    - Okumura・谷口忠大ほか "[[Co-Creative Learning via Metropolis-Hastings Interaction between Humans and AI]]"（arXiv 2506.15468）の、人と計算機が名前を付け合う実験
        - 計算機の受け入れ方を MH の規則にすると、「常に受理」「常に却下」より良い結果。ただし「常に受理」との差は有意ではなかった
        - 人の受け入れ方は、MH の受理確率に比例しなかった。確率 0.6 未満では受理が約 2 割、0.8 以上では約 95% という段差状（論文の図からの読み取り）
    - 親方が人である以上、「近似的なベイズ推論」と言える範囲は、実験で確かめる余地がある

それでも似ているところ
- MH 名づけゲームの聞き手は、相手の理由を知らずに、自分の観測だけで受け入れるか断るかを決める。徒弟が親方に説明を求めず、採用されたか却下されたかだけから学ぶ形とは似ている
- 徒弟も親方の提案を受け入れたり断ったりし、親方も徒弟の提案から学ぶ、という双方向の[[徒弟制]]として描き直せば、MH 名づけゲームの形に近づく（Claude の考え。エッセイにはない）
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 前提として [[互いに教え合う]] / [[お互いに学び合う]] ことが必要なのだが、「徒弟制」という言葉は親方と弟子の役割が固定されているニュアンスがあるのでミスリーディングかもね
    - [[半学半教]]と関連している

出典
- Inside the Kami [https://civic.ai/inside-the-kami/](https://civic.ai/inside-the-kami/)
- Pack 3: Competence [https://civic.ai/3/](https://civic.ai/3/)
- Taniguchi et al. (2026) Symbiotic Alignment via Collective Predictive Coding, Artificial Life 32(3) [https://doi.org/10.1162/ARTL.a.475](https://doi.org/10.1162/ARTL.a.475)
- Okumura et al. Co-Creative Learning via Metropolis-Hastings Interaction between Humans and AI [https://arxiv.org/abs/2506.15468](https://arxiv.org/abs/2506.15468)