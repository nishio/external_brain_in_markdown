---
title: "Quadratic Votingがシナジーの発見に有用"
---

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
[[Meetup with Audrey & Glen]]でAudrey Tang が「二次投票（Quadratic Voting, QV）」を使って supermodular（スーパーモジュラ）なシナジーの高いプロジェクトを見いだす事例を説明している箇所の引用です（英語原文のまま抜粋）。続いてポイントを簡潔に解説します。

> (Audrey Tang)
>  "So in Taiwan since 2018 the Presidential Hackathon every year we have like 200 teams, many many teams. A classic question is how to make sure that we discover which teams have synergy, which teams they work together. ... In Taiwan we use quadratic voting for this. So once you get to the Presidential Hackathon website, you’re asked to log in, and once you log in, you have 99 points, 99 credits.
>  Nobody spends 99 points on 99 projects so far—I’ve not seen anyone do this. They prefer to go to their favorite project and start voting on it, but they very quickly find they cannot vote 99 votes because 1 vote costs 1 point, 2 votes cost 4 points, 3 votes cost 9 points, and so on—quadratic. ... With 99 points you can’t cast 10 votes (which would require 100), you only have 9 votes (81 points). Once you vote that 9th vote, you still have 18 points left. Nobody wants to waste those 18 points, so people start looking for other projects to see which ones have synergy. ... When people started using quadratic voting, we have much, much better synergy information just based on who voted for which combination of projects—how these would work together.
>  ... And the top 20 (projects) tends to be the ones that work best with many projects, which means they’re more supermodular. So this is how we concretely use quadratic voting to discover that something is more supermodular than the other."

解説
- 問題意識
    - 多数のプロジェクト（例: 大統領ハッカソンの 200 チーム）から「どれが[[シナジー]]（[[相乗効果]]）を持ち、組み合わせると全体成果が最大化されるか」を見つけるのは難しい。
- QV（Quadratic Voting）のしくみ
    - 1票目→1ポイント、2票目→さらに合計4ポイント、3票目→合計9ポイント… のように“二乗”コストが増える。
    - 一人あたり99ポイントが配分されても、「好きなプロジェクトに極端に偏らせる」とポイントがすぐ足りなくなるため、投票者は「他のプロジェクトにも分散して投票する方が得かもしれない」と考える。
    - その過程で、似た分野・相乗効果の高い複数プロジェクトに目を向けるインセンティブが働き、自然に「最適な組み合わせ」を探ろうとする。
- [[supermodularity]]（[[スーパーモジュラリティ]]）との関係
    - 「組み合わせることで、単体の合計を上回る価値が出る」＝スーパーモジュラ性が高い（相乗効果が大きい）プロジェクトを、投票行動を通じて浮かび上がらせやすくなる。
    - QVの結果「多くの人が併せて投票したプロジェクト」= [[シナジー]]のある組み合わせが把握でき、さらに予算配分や連携の優先度を決めやすい。
    - すなわち、QVは「複数プロジェクト間の相乗効果（supermodularity）」を市場原理や通常の多数決では捉えにくい領域でも、参加者が自発的に“組み合わせ”を探りながら意思表示する仕組みとなり、シナジーの高いプロジェクトを発見するのに有効だと示されています。
