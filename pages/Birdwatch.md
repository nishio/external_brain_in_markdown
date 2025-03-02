
Twitterの[[Community Notes]]のアルゴリズム

Birdwatch: Crowd Wisdom and Bridging Algorithms can Inform Understanding and Reduce the Spread of Misinformation
> We present an approach for selecting objectively informative and subjectively helpful annotations to social media posts. We draw on data from on an online environment where contributors annotate misinformation and simultaneously rate the contributions of others. Our algorithm uses a matrix-factorization (MF) based approach to identify annotations that appeal broadly across heterogeneous user groups - sometimes referred to as "bridging-based ranking." We pair these data with a survey experiment in which individuals are randomly assigned to see annotations to posts. We find that annotations selected by the algorithm improve key indicators compared with overall average and crowd-generated baselines. Further, when deployed on Twitter, people who saw annotations selected through this bridging-based approach were significantly less likely to reshare social media posts than those who did not see the annotations.
- [https://arxiv.org/abs/2210.15723](https://arxiv.org/abs/2210.15723)
- (DeepL)
    - ソーシャルメディアの投稿に対して、客観的に有益な注釈と主観的に有益な注釈を選択するアプローチを提示する。
        - 日本語だと同じ「有益」に訳されてしまったが客観と主観で言葉を分けている<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
            - objectively informative
            - subjectively helpful
    - 我々は、投稿者が誤った情報に注釈を付け、同時に他の投稿を評価するオンライン環境のデータを利用する。我々のアルゴリズムは、[[行列分解]]（MF）ベースのアプローチを用いて、異質なユーザーグループに広くアピールするアノテーションを特定するもので、「[[橋渡しベースのランキング]]」(bridging-based ranking)とも呼ばれる。
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

