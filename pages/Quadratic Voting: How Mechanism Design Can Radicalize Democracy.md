---
title: "Quadratic Voting: How Mechanism Design Can Radicalize Democracy"
---

[[Steven Lalley]], [[E. Glen Weyl]] (2018)
> Can mechanism design save democracy? We propose a simple design that offers a chance: individuals pay for as many votes as they wish using a number of "voice credits" quadratic in the votes they buy. Only quadratic cost induces marginal costs linear in votes purchased and thus welfare optimality if individuals' valuation of votes is proportional to their value of changing the outcome. A variety of analysis and evidence suggests that this still-nascent mechanism has significant promise to robustly correct the failure of existing democracies to incorporate intensity of preference and knowledge.
>
>  The online appendix for "Quadratic Voting: How Mechanism Design Can Radicalize Democracy" may be found here: [http://ssrn.com/abstract=2790624.](http://ssrn.com/abstract=2790624.)
[https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2003531](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2003531)
American Economic Association Papers and Proceedings, Vol. 1, No. 1, 2018
なのだけどpreprintは2012に公開されてる

2024-01-30
- 下記は 2023-07-20〜 の「なんだこれは？」と思いながら読んでた時のメモ、あまり整理されてない
- 理解が進むにつれて重要な概念だなという思いが強くなった

from [[Quadratic Voting]]
Quadratic Voting: How [[Mechanism Design]] Can Radicalize Democracy
[https://www.researchgate.net/publication/325310987_Quadratic_Voting_How_Mechanism_Design_Can_Radicalize_Democracy](https://www.researchgate.net/publication/325310987_Quadratic_Voting_How_Mechanism_Design_Can_Radicalize_Democracy)
> Can mechanism design save democracy? We propose a simple design that offers a chance: individuals pay for as many votes as they wish using a number of "voice credits" in the votes they buy. Only quadratic cost induces marginal costs linear in votes purchased and thus welfare optimality if individuals' valuation of votes is proportional to their value of changing the outcome. A variety of analysis and evidence suggests that this still-nascent mechanism has significant promise to robustly correct the failure of existing democracies to incorporate intensity of preference and knowledge.
(DeepL+nishio)[[メカニズムデザイン]]は[[民主主義]]を救うことができるのか？我々は、その可能性を提供する単純なデザインを提案する。個人が購入する票の中にある「voiceクレジット」の数を用いて、望むだけの票を支払うのである。個人の投票に対する評価が、結果を変えることに対する価値に比例するのであれば、quadraticコストのみが、購入した投票数に線形な限界費用をもたらし、その結果、厚生最適となる。様々な分析と証拠から、このまだ発展途上のメカニズムが、既存の民主主義が嗜好の強さや知識を取り入れることに失敗したことを強固に修正する大きな可能性を秘めていることが示唆される。

- quadraticを「二次」って訳すのはsecondary的ニュアンスを感じるから嫌だな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - 台湾では「[[平方投票]]」らしい、こちらの方が好き [Discord](https://discord.com/channels/1087587764691808316/1093884258231267499/1114087516870561912)

- [[直接民主制]]を前提として、その実現方法を改善するものというイメージ？
    - 多くの人が投票という言葉で連想するような「市長を誰にするか複数の候補から選ぶ」的なものは議題が一つしかない？
        - > 多くの二択の集団決定（例えば、国民投票や指導者の選出）が行われます。
        - 指導者の選出も二択の集団決定にエンコードする？
    - あー、なるほど、投票権を「特定の選挙で使わなければ消滅するもの」から、継続価値を持つ[[発言権トークン]]に変えることが前提なんだ
        - > As is common in the analysis of markets for private goods (Willig, 1976), we assume there are enough issues and that each is sufficiently inconsequential that every voter has a quasi-linear “continuation value” for retaining voice credits for future votes.
        - (DeepL) 私的財市場の分析で一般的なように（Willig, 1976）、ここでは十分な数の争点があり、それぞれの争点は十分に取るに足らないものであるため、すべての有権者が将来の投票のために発言権を保持する準線形的な「継続価値」を持つと仮定する。
        - なので将来に起こりうる投票がスコープに入って「複数の議題」になる
- 「一議題につき一票」が、暗黙に「議題に対する[[アテンション]]の均等さ」を仮定してたわけだけど、実際にはそうではないよねという話


<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>私的財の市場分析で一般的なように（Willig, 1976）、問題が十分に多く、それぞれが十分に無関係であるため、すべての投票者は将来の投票のために発言権クレジットを保持する「[[継続価値]]」を持っていると仮定します。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>今の一般的な投票においては投票権は「その時に行使しなければ価値を失うトークン」なわけだが、この論文における「[[発言権クレジット]]」は将来の投票のために使うことができるので継続価値を持つ

[[Quadratic Votingはなぜ平方根を取るのか]]
![image](https://gyazo.com/790419420c09b9156f713bbfda589030/thumb/1000)
- 既存のAかBかを選ぶ二択投票において、投票者は+1か-1の投票しかできない
    - それを足し合わせたものが0より大きければAの勝ち
- その結果「Aであることがとても大事なんだ！」の人と「どっちでもいいけど、どっちかといったらBかな〜」の人の投票が同じ力を持ち相殺する
    - よくないね！
- そこで投票の重みを投票者が変えられるようにしたい
    - しかし任意に変えられるならみんな無限に強くするよね
    - そこで「発言力を強くすることにコストが掛かる」という構造を導入する
    - このコストはどのようにするのが良いか、というのを議論するためにコスト関数cが好ましい特徴を持つための条件を検討するのがこの論文
    - 結論としては二次関数にするのが良い

<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>各投票者は、いくつの票を購入するかを決定する際に、追加の票の限界コストと、その票が選挙の結果を左右する決定的な役割を果たすと認識される確率を比較します。私たちが採用する価格受け入れの仮定は、Mueller（1973）とLaine（1977）が最初に提案したもので、すべての投票者がこの問題における票の限界的な決定性pについて同意しているというものです（ただし、問題ごとに異なる場合があります）。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>`marginal pivotality of votes p`
    - 追加の投票権獲得によって結果が変わる可能性を投票権を購入する前にみんな知っていて、かつみんな同じ値だと思っている、という仮定が入っている
    - 結構強い仮定だね
    - その仮定を認めるなら、合理的な投票者は$2u_ipv_i - c(v_i)$を最大化する票数を選ぶ
- `robustly optimal`とは$\sum_i v^*_i$と $\sum_i u_i$の符号が一致すること
    - for every p > 0, N and vector u, each price-taking voter i chooses votes $v^*_i$

[/blu3mo-public/Quadratic Voting#6435f5161286260000f30f6c](https://scrapbox.io/blu3mo-public/Quadratic Voting#6435f5161286260000f30f6c)
- > n=2に設定している根拠はあるのかな..?
- これの回答
- > THEOREM 1: A vote pricing rule is robustly optimal if and only if it is quadratic.
- $2u_ipv_i - c(v_i)$が最大化されているならそれをvで微分したものは0になる
    - これを展開すればcが二次関数である時だけuとvが比例することがわかる
        - ![image](https://gyazo.com/1bf407b0356839250026e6a178224c72/thumb/1000)

- このaを変えることによる考察
    - a=1にすれば新しい一票を得るコストが一定になる
        - この場合、一番uの絶対値が大きい人の独裁になる
        - この肩の値が無限大になるから
            - ![image](https://gyazo.com/cdf578f6c0eee5eac996f037d8ed75d8/thumb/1000)
    - aを無限大にすれば、みんなが一票だけ投票する
        - 今の普通の多数決と同じ
    - a=2は[[中庸]]
- 関連
    - [/tkgshn/なぜQuadratic Votingは二乗なのか](https://scrapbox.io/tkgshn/なぜQuadratic Votingは二乗なのか)
    - <img src='https://scrapbox.io/api/pages/nishio/Quadratic Payments: A Primer/icon' alt='Quadratic Payments: A Primer.icon' height="19.5"/>


