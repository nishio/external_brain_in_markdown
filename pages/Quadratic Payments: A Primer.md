---
title: "Quadratic Payments: A Primer"
---

[Quadratic Payments: A Primer](https://vitalik.eth.limo/general/2019/12/07/quadratic.html)(Vitalik 2019)
![image](https://gyazo.com/facc587c0186d78fe47859c9ecad72bd/thumb/1000)

一人一票でなはく一人N票にする
- ただしN番目の票を得るにはNドルの支払いを必要にする
- 票の価値を2倍高く感じている人は、2倍高い値段になるまで買う
    - 注: [[可処分所得のキャップ]]がないことが前提<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- なので、個々人が票に感じている価値と得られる票数が一致する

私的な財と公共財が対比されている
- ここでいう「[[公共財]]」は「国や地方自治体がやること」という意味ではない
    - 作る人ではなく受け取る人にフォーカスがあたっている
        - 私的で物理的な財(たとえばリンゴ)が1つ生産されたら、それを受け取る人は基本的に一人
        - 道路などのインフラや、複製コストの安いデジタルな財は、受け取る人が多数になる
            - この場合に、受け取る人が一人であることを想定した取引のメカニズムは機能しない
    - オープンソースソフトウェアは公共財
    - この解説記事も公共財
- この種の性質がある財は[[意思決定を個人単位に分解できない]]
    - > 私的財の場合は、各個人の一連の意思決定に分解できるので、問題は簡単です。各人が支払ってもいいと思った分だけ、その人のために生産されるのです。しかし、公共財の場合は「分解」できないので、別の方法で人々の選好を足し合わせる必要があるのです。
    - 受け取る人が多数であるから、個々人の意思決定に分解できないのだ

[[Quadratic Voting]]: [[Quadratic Voting: How Mechanism Design Can Radicalize Democracy]]
- 組織の文脈の中では、意思決定は公共財である。誰もが同じ決定の結果を「消費」するからだ。
    - Quadratic Voting
- Quadratic Votingは複数選択肢の投票に応用できる
    - [[耐戦略性]]がある
    - 本当？[[信任投票]]だからということ？<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - 本人の書いてる説明が戦略的操作になってるからちょっとおかしい

- 連続値の投票にも応用できる
    - 使うことはできるだろうが値の変化に対して効用が線形ではないからメリットは微妙だと思う<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - 冷房の設定を28度から27度に変えたいと思ってる人が、18度になってうれしいとは限らない
        - 18度になって欲しくないなら100クレジット使って-10の投票をするのはやりたくない

[[Quadratic Funding]]: [[Liberal Radicalism: A Flexible Design For Philanthropic Matching Funds]]
2次投票の弱点
- 投票内容を決定するメカニズムが組み込まれていない
    - 投票内容を決めることはパワーの源になる
    - 多数派が弱く承認し、少数派が強く不承認となる決定を繰り返し提案し、少数派が投票トークンを使い果たすまでそれを提案し続ける
        - （少数派は多数派よりはるかに速くトークンを使い果たす）
意思決定の選択自体をメカニズム自体の一部とする実装例が[[Quadratic Funding]]
- これは、公共財の個人的な提供という特定のユースケースに特化されている。
