
[[Polis]]の論文
- [https://www.e-revistes.uji.es/index.php/recerca/article/view/5516/6558](https://www.e-revistes.uji.es/index.php/recerca/article/view/5516/6558)
- > Deliberative and participatory approaches to democracy seek to directly include citizens in decision-making and agenda-setting processes. These methods date back to the very foun-dations of democracy in Athens, where regular citizens shared the burden of governance and deliberated every major issue. However, thinkers at the time rightly believed that these meth-ods could not function beyond the scale of the city-state, or polis. Representative democracy as an innovation improved on the scalability of collective decision making, but in doing so, sacrificed the extent to which regular citizens could participate in deliberation. Modern tech-nology, including advances in computational power, machine learning algorithms, and data visualization  techniques,  presents  aunique  opportunity  to  scale  out  deliberative  processes. Here we describe Polis, an open source web application capable of collecting and synthesizing feedback from people in a scalable and distributed fashion. Polis has shown itself capable of building  shared  understanding,  disincentivizing  counterproductive  behavior  (trolling),  and cultivating points of consensus. It has done this in the context of journalistic and academic research, and directly as part of decision-making bodies at local and national levels, directly affecting legislation. These  results  demonstrate  that  deliberative  processes  can be scaled up beyond the constraints of in-person gatherings and small groups.Key Words: deliberation, collective intelligence, unsupervised learning, active learning.
- (DeepL)民主主義に対する熟議と参加型のアプローチは、意思決定や議題設定のプロセスに市民を直接参加させようとするものです。これらの方法は、一般市民が統治を分担し、あらゆる重要な問題を審議したアテネの民主主義の基礎にさかのぼる。しかし、当時の思想家たちは、これらの方法が都市国家（ポリス）の規模を超えて機能することはできないと考えるのが当然であった。[[代表制民主主義]]は、[[集団的意思決定のスケーラビリティ]]を向上させたが、その反面、一般市民が審議に参加できる範囲を犠牲にしてしまった。現代のテクノロジーは、計算能力、機械学習アルゴリズム、データ可視化技術などの進歩により、[[熟議プロセスをスケールアウトする]]ユニークな機会を提供しています。ここでは、スケーラブルで分散した方法で人々からのフィードバックを収集し、合成することができるオープンソースのウェブアプリケーションであるPolisについて説明する。Polisは、共有理解を構築し、非生産的な行動（[[トローリング]]）を抑制し、合意点を育成することが可能であることを明らかにした。これは、ジャーナリズムや学術研究の文脈で、また、地方や国家レベルの意思決定機関の一部として、直接、立法に影響を与えることができました。これらの結果は、熟議プロセスは、対面式集会や小グループの制約を越えてスケールアップできることを実証している。Key Words: [[熟議]]、[[集合知]]、[[教師なし学習]]、[[アクティブラーニング]]
- ![image](https://gyazo.com/1272e02943155b514268445d784e94ee/thumb/1000)

[[集団的意思決定]] / [[意思決定]]



欠損値はコメントごとの平均で埋められる
投票の少ないユーザ(<7)は取り除かれる
PCAはパワーイテレーション法で計算する、前回の計算結果を再利用できるので効率的

欠損値を平均で埋めると、投票数の少ない人が中央付近にプロットされることになる
- そこでsqrt(C/Cp)で補正する、Cはコメント数、Cpは人pが投票した数
    - 平方根は柔らかくするため
- しかしこのスケーリングはコメントルーティング(コメントを出す順番のコントロール)で無効になった
    - 高い分散を持つコメントが先に表示されるから

意見グループ
- まず負荷低減のためにK=100でクラスタリングする
- 次にK=2〜5でクラスタリングする
- [[シルエット係数]]が最適となるKを選ぶ
- 会話の初期にばたつくのを防ぐために平滑化関数をかける

各コメントがグループをどの程度代表してるか
- グループが特定されると各コメントがグループをどの程度代表してるか計算する
- ベルヌーイ分布の平均値の推定でグループ内の人が投票する確率とグループ外の人が投票する確率を求める

p.9の上半分はスキップ

ユーザの時間を効率よく使うためにコメントは重み付きランダムで選ばれる
優先度の式は
・賛成が多いと増える項
・パスが多いと減る項
・PCA負荷の高いコメントで増える項
・投票が多くなるほど減る項
を掛けたもの
