---
title: "Birdwatch"
---

Twitterの[[Community Notes]]のアルゴリズム

[[Birdwatch: Crowd Wisdom and Bridging Algorithms can Inform Understanding and Reduce the Spread of Misinformation]]
> We present an approach for selecting objectively informative and subjectively helpful annotations to social media posts. We draw on data from on an online environment where contributors annotate misinformation and simultaneously rate the contributions of others. Our algorithm uses a matrix-factorization (MF) based approach to identify annotations that appeal broadly across heterogeneous user groups - sometimes referred to as "bridging-based ranking." We pair these data with a survey experiment in which individuals are randomly assigned to see annotations to posts. We find that annotations selected by the algorithm improve key indicators compared with overall average and crowd-generated baselines. Further, when deployed on Twitter, people who saw annotations selected through this bridging-based approach were significantly less likely to reshare social media posts than those who did not see the annotations.
- [https://arxiv.org/abs/2210.15723](https://arxiv.org/abs/2210.15723)
- (DeepL)
    - ソーシャルメディアの投稿に対して、客観的に有益な注釈と主観的に有益な注釈を選択するアプローチを提示する。
        - 日本語だと同じ「有益」に訳されてしまったが客観と主観で言葉を分けている<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
            - objectively informative
            - subjectively helpful
    - 我々は、投稿者が誤った情報に注釈を付け、同時に他の投稿を評価するオンライン環境のデータを利用する。我々のアルゴリズムは、[[行列分解]]（MF）ベースのアプローチを用いて、異質なユーザーグループに広くアピールするアノテーションを特定するもので、「[[橋渡しベースのランキング]]」(bridging-based ranking)とも呼ばれる。 #橋渡し
    - これらのデータと、投稿への注釈を見るように無作為に割り当てられた個人を対象とした調査実験とを組み合わせている。その結果、アルゴリズムが選択したアノテーションは、全体の平均値や群衆が生成したベースラインと比較して、主要な指標を改善することがわかりました。
    - さらに、Twitterに展開したところ、このブリッジングベースのアプローチで選択された注釈を見た人は、注釈を見なかった人に比べて、ソーシャルメディアの投稿を再共有する可能性が著しく低くなりました。

(GPT3)Birdwatchプロジェクトは2つの主要な目標に取り組んでいます。第一の目標は、客観的に情報を提供する高品質なユーザー生成のノートを提示することです。この論文では、「客観的に情報提供する」とは、誤解を招く可能性のあるツイートの主要な主張を読者の理解を因果関係的に向上させるような要約ノートのことを指します。第二の目標は、広範なTwitterユーザーにとって役立つと認識されるノートを提示することです。
- この両方の目標を満たすノートを特定することは課題です。たとえば、情報源が信頼性がありながら、書き方が不十分であるために役に立たないとされる場合があります。また、バイアスや議論的であると感じられる言葉を使用している場合もあります。たとえば、ノートが攻撃的であると感じられたり、単純に読みにくいと感じたりすると、それを情報を無視する合図として受け取り、ノートに含まれる情報を考慮するのではなく、無視するかもしれません。
- 同様に、情報源が弱く、事実に基づかないノートは、当然のこととして受け入れられるアイデアや仮定を引き起こすことで人々の共感を呼ぶ場合があります。たとえば、Twitter上の大勢の人々が誤解を招いたり情報を提供しないノートに同意し、役に立つと評価するかもしれませんが、それは彼らの事前の信念と一致しているからです。
- したがって、Birdwatchにとっての核心の課題は、正確で高品質な情報を含むノートを特定するだけでなく、既に同意しやすい人々だけでなく、広範な観客に共感を呼ぶような形で書かれたノートを特定することです。
- 私たちは、ユーザー生成のノート自体と各ノートのユーザー生成評価の履歴に基づいて、情報を提供し役に立つとされるノートを特定するアルゴリズムを提案します。これらの入力を使用して、目的を達成するために2つの障害を克服しようとしています。まず、評価はノートの潜在的な特性（品質、トーン、バイアスなど）だけでなく、評価者が各評価者の事前の信念を考慮してノートにどのように反応するかによっても決まる要素です。第二に、各評価者の事前の信念、各ノートの潜在的な特性、および個々の評価を生成するプロセスでこれらの属性がどのように相互作用するかについての事前情報はありません。私たちは、Birdwatchの評価者-ノート行列からの行列因子分解（MF）メソッドを開発し、評価者がノートを「役立つ」と評価する基本的な傾向と、類似したノートの過去の評価に基づく評価者の「視点」を捉えます。

(GPT3)参加型民主主義ツールの1つである[[Polis]]は、行列因子分解の出力をクラスタリングしてユーザーを意見のクラスターに分割し、グループの共通合意（クラスター間の合意）が高いコンテンツを優先します。
- 本論文で提案するBirdwatchのブリッジングベースのランキングアルゴリズムは、（極性化された）意見空間の表現を構築するために、行列因子分解を非教示学習の方法として使用します。ただし、これまでのアプローチとは異なり、ユーザーやアイテムを異なるグループにクラスタリングすることを必要とせず、Birdwatchのアルゴリズムは連続した空間上で視点を橋渡しすることを行います。また、私たちの研究のもう一つの新しい貢献は、調査データによって示されるブリッジングベースのスコアリングの有効性です。それは、異なる政治的所属を自己申告するユーザーにとって有益と見なされるメモを、ベースラインの非ブリッジングアルゴリズムよりも選択します。

![image](https://gyazo.com/18cee5201c045e55d0459921c964ee26/thumb/1000)

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>この論文は、Twitterにおける誤情報に対処するために、Birdwatchというクラウドソーシングによるアプローチを提案しています。
主な流れは以下の通りです。
- まず、Birdwatchにおいてユーザーが誤情報を含むツイートに注釈(ノート)を付けたり、他のユーザーの注釈に評価を付けたりするシステムを構築。
- 次に、注釈の質を評価するアルゴリズムを開発。Matrix Factorizationというアプローチを用いて、政治的立場の異なるユーザー間でも広く支持される注釈を特定できるようにした。
- アルゴリズムの性能を評価するために、対象のツイートのみを見せた対照群と、ツイート+選ばれた注釈を見せた実験群に分けて調査を実施。
- 実験の結果、アルゴリズムが選んだ注釈はユーザーの理解を助け、幅広い政治的立場の人から有用だと評価された。単純な多数決ベースの選択よりも良い結果となった。
- また、注釈を見せることで、誤情報を含むツイートの拡散が25-34%抑制された。
- ただし、アルゴリズムには課題もある。悪意のあるユーザーへの耐性、大規模化した際の性能など、継続的な改善が必要。
- 最後に、こうした取り組みを進める上での倫理的な考慮事項について議論している。
全体として、クラウドの力とアルゴリズムを組み合わせて誤情報に対処する新しいアプローチを提示した論文と言えます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>[[Matrix Factorization]]をどう使うのか解説して

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>Matrix Factorization (MF) は、ユーザーと注釈の評価データから、ユーザーと注釈の潜在的な特徴を抽出する手法です。この論文では、MFを使って以下のようにBirdwatchの注釈の質を評価しています。
- ユーザー×注釈の評価行列を作成。各要素は、あるユーザーが特定の注釈を「役立つ」と評価したか否かを表す。
- MFを適用し、各ユーザーと注釈のベクトル表現を学習。これらのベクトルは、ユーザーの評価傾向や注釈の潜在的な特徴を捉えていると期待される。
- 学習されたベクトルを用いて、各注釈の「intercept term」を計算。これは、ユーザーの政治的立場などの影響を除いた上での、注釈の普遍的な質の指標と解釈できる。
- Intercept termが閾値以上の注釈を、「Currently Rated Helpful」とみなす。これらの注釈は、政治的立場が異なるユーザー間でも広く支持されていると期待される。

MFのポイントは、ユーザーと注釈の潜在的な特徴を抽出することで、単純な多数決以上に洗練された注釈の評価を可能にしている点です。特に、intercept termを使うことで、政治的に偏りのない、質の高い注釈を選べるようにしているのが特徴的です。
ただし、データが疎であることや、悪意のあるユーザーへの対策など、実際に適用する上での課題もあります。これらの点は今後の研究で改善されていくことが期待されます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Matrix Factorization、[[行列分解]]にも色々あると思いますけど、ここで使ってるのはどういう性質のもの？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この論文では、行列分解の中でも特に、[[評価予測]]のための手法を使っています。具体的には、以下のようなモデルを仮定しています。
- $\hat{r}_{un} = \mu + i_u + i_n + f_u \cdot f_n$
ここで、$\hat{r}_{un}$ はユーザー $u$ の注釈 $n$ に対する評価の予測値、$\mu$ は全体のバイアス、$i_u$ はユーザー $u$ の評価傾向を表すバイアス、$i_n$ は注釈 $n$ の一般的な質を表すバイアス（intercept term）、$f_u$ と $f_n$ はそれぞれユーザー $u$ と注釈 $n$ の潜在ベクトルです。

このモデルは、以下のような特徴を持っています。
- バイアス項（$\mu, i_u, i_n$）を導入することで、ユーザーや注釈の個性を表現できる。
- ユーザーと注釈の潜在ベクトルの内積（$f_u \cdot f_n$）を使うことで、[[協調フィルタリング]]を実現している。つまり、似たようなユーザーや注釈を自動的に発見できる。
- 注釈の intercept term ($i_n$) に着目することで、ユーザーの個人的な好みとは独立した、注釈の普遍的な質を評価できる。
このようなモデルは、Netflix Prizeなどの評価予測タスクでよく使われており、協調フィルタリングの代表的な手法の1つです。ただし、通常は $i_n$ は推薦のためのアイテムバイアスとして使われることが多く、この論文のように注釈の質の指標として使うのは珍しい使い方だと思います。

以上のように、この論文ではMFを評価予測の文脈で使いつつ、$i_n$ の解釈を工夫することで、Birdwatchという新しい問題設定に適用しているのが特徴です。





異なる意見の傾向の人から揃って支持されている情報を重視する、というスタイルは[[Plural QV]]とも関連している

主観を集めてそこから有益な情報を引き出すアプリは、Polisの[[sentiment gathering]]の側面とも関連している
- PolisのConsensus係数は、人々を意見ベクトルによってクラスタリングした上で、そのクラスタそれぞれから賛同される度合いの積を計算している
    - つまり全会一致を二値ではなく実数に拡張した形

川喜田二郎の「[[すべてのデータはうそである]]」とも関連する
- 主観的データを「客観的ではないからゴミだ」と捨てるのではなく、たくさん集めることによってそこから意味を引き出す
- かつては「[[合計]]、[[平均]]、[[多数決]]」みたいに、しょぼい特徴量しか使ってなかったので主観データをたくさん集めても有用でなかった
    - コンピュータの性能の向上と[[行列分解]]の研究の発展で、高次元の行列から意味を見出すことがやりやすくなったわけだ


Github
- [https://github.com/twitter/communitynotes](https://github.com/twitter/communitynotes)

関連
- [Twitter コミュティノートについて知って欲しいことを暑苦しく語る - フジイユウジ::ドットネット](https://fujii-yuji.net/2023/twitter/community-notes)
- [ツイートに注釈つくtwitter新機能「コミュニティノート」の評価は？ デマ防止に役立つか、不毛な議論を呼ぶか…？？ - Togetter](https://togetter.com/li/2182249)

