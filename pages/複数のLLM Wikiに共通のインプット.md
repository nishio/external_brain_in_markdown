---
title: "複数のLLM Wikiに共通のインプット"
---

複数の[[KarpathyのLLM Wiki]]に共通のインプット
5/3
枝が育っていった結果として複数のどちらにも入るものが出てきた
- ChatGPTに面白いものを紹介させた
    - 紹介した[[MindTrellis]]の論文をよんだ
- [[Kozaneba]]と関連しそうだね、となった
    - そう言ったら似てるところと違うところを整理してくれた
    - その違いを見たらむしろ[[ConnectingDotsシステム]]と関連しそう、となった
- ConnectingDotsシステム について考えてるWikiと、KozanebaとAIの組み合わせでの知的生産の改善を考えてたWikiと両方に関係する
    - まあそれは、そもそもカテゴリーで分けてるものではないから
- そしてこの出来事自体はLLM Wikiについて考えてたWikiにも関係している
- (飛躍)
- 一つ一つのWikiが仮想の人格になって、話し合って情報交換したらいいね
    - 仮想の人格たちを集めてまとめて情報共有したい
        - それは単純に手間の削減でしかない
        - N個のWikiに同じ資料をingestさせたら、それぞれ異なる切り出し方やまとめかた、レスポンスをしてくるだろう
        - これを相互に交換しても面白そう
            - この作業はN^2になってしまう


3つのAIの反応の違い
Q: MindTrellisの話をingestしたことでどんな変化があった？

A1(LLM Wikiを中心とした知的生産性に関するWiki):
MindTrellis ingest の波及を整理すると：
- 直接的な産物
    - 新概念 **structure-as-hypothesis** — MindTrellis 論文の中心思想「AIが提示した構造はすべて仮説、ユーザがあらゆるレベルで調整できるべき」を本wiki初の抽象として抽出。これが本日最も再利用された
    - エンティティ **mindtrellis** — 3エージェント構成（Oracle / Adaptive Retriever / Map Manager）を本wikiの参照点として登録
- カスケード（後続 ingest で繰り返し参照された）
    - 午後の **gpt-accurate-diagrams-20260503** が structure-as-hypothesis を図解ドメインに応用（「AIに暗黙前提を露出させる」「作る役/疑う役/修正役」）。MindTrellis なしには「これは figure ドメインへの一般化だ」と言語化できなかった
    - **gpt-multiagent-voice-20260503** の Round Orchestrator は MindTrellis の3エージェント分解と構造的に同型（Oracle ≒ Event Receiver, Map Manager ≒ Aggregator）— 直接引用はしていないが概念的下地として効いた
    - **gpt-30books-llm-wiki-design-20260503** の「概念ページを答えにせず比較面に」も structure-as-hypothesis 系統（概念定義も仮説扱い）
- メタ効果
    - Kozaneba / MindTrellis / ConnectingDots の三角測量が成立したことで、午前の reflection **wikis-as-personas** が「Co Wiki と Kozaneba×AI Wiki に同時所属」という抽象から具体的な3システム比較を持つ分析に格上げされた。reflection (朝) → ingest (夕) の逆順 filing back が機能した
- この ingest がなかったら起きなかったこと
    - structure-as-hypothesis 概念は別ソースからは抽出されにくかった（MindTrellis 論文が「AI構造を仮説化する」を最も明示的に主張している）
    - ConnectingDots を「Dots/Relations 生成器として MindTrellis が位置づけられる」と整理する三角測量
    - Kozaneba を「ConnectingDots の View の一種」として再配置する視点
要するに、1つの新概念 + 比較軸の確立 + 後続 ingest の解釈の足場 という3層の効果。lint top10 の fact-wiki-separation 被リンク数も 15 → 22 へ伸びている（structure-as-hypothesis 経由で「動的合成層」の文脈が増えたため）。

A2(ConnectingDotsシステムのWiki):
良い問いです。MindTrellis 部分を切り出して見ると、変化は大きく3カテゴリ:
1. 構造的に増えたもの(直接的)
    - wiki/related/ ディレクトリの新設 — 「関連システムを比較する場所」が初めて wiki にできた
    - related/mindtrellis.md ページ
        - architecture/three-layers.md に3システム位置づけ図(MindTrellis = Dots/Relations 層、ConnectingDots = + Stories/Views 層、Kozaneba = View 層)
2. 既存決定の "外部視点での" 補強(間接的)
    - これが一番大きい変化かもしれません。MindTrellis という独立した2026年の研究と対比することで:
        - curator-first.md — 「AI 生成構造は暫定物、人間が編集」というMindTrellisの思想と一致 → 我々の「キュレーター・ファースト」は 特殊な選好ではなく合流可能な研究系譜 だと位置づけられた
        - relationships-as-edits.md — MindTrellis と 明確に違う方向 を選んでいることが言語化できた(「我々は知識グラフを作らない」を、空気でなくテキストで説明できる)
        - concepts/curator.md の AI 役割タクソノミ(Extractor / Linker / Critic / Storyteller / Curator) — MindTrellis の3エージェント分解(Oracle / Adaptive Retriever / Map Manager)が発想元
3. 独自性ステートメントの明確化
    - ingest前: 「事実と解釈を分離する」だけだった
    - ingest後: 「MindTrellis 的な Dots/Relations 層の上に、価値判断を可視化する Stories/Views 層を明示的に積む」と他システムと対比できる形で言える
- MindTrellis 由来 ではなかった もの(誤帰属を避けるため)
    - 同じソース内だが、これらは MindTrellis ではなく GPT の整理から来ている:
        - claim / status / omittedDots 等のスキーマ提案
        - 5週間アクションプラン
        - 4成功基準
        - Kozaneba との位置づけ(Kozaneba は西尾自身のツール)
一言でまとめると、MindTrellis ingest は 「我々が作っているものが何で、何でないか」の対比軸を1本与えた のが本質的な効果。スキーマや実装には直接影響していないが、他人に説明するときの語彙が増えた と言えます。

A3(LENCHI, LLMを使った知的生産に関するWiki、Kozanebaについても話している):
主に 3 つの構造的変化がありました。
1. LENCHI Wiki の独自性が相対化された
    - 「ナラティブの価値 で言う wiki化の 6 軸損失問題」は LENCHI Wiki の 二層分離（raw 改変禁止 + wiki 概念抽出）で答える、というのが Day 12 までの整理でした。Day 13 の ConnectingDots ingest で、Story 層を明示する別アプローチ があることが示され、LENCHI Wiki は「唯一の解」ではなく「複数解の一つ」として位置づけ直されました。
2. Kozaneba の独自ニッチが言語化された
    - Kozaneba は単に「KJ 法のデジタル版」だったのが、三者対比（MindTrellis = 意味関係の明示 / ConnectingDots = データモデル / Kozaneba = 空間 UI）の中で 「前言語的な構造化に強い」「まだ言語化できない近さを扱える」 という独自性が初めて言語化されました。MindTrellis や ConnectingDots と競合せず、それらの View として接続できる位置を獲得。
3. 著者の並走プロジェクト構造が三者として見えた
    - Day 12 Session C で LENCHI（個人）/ ブロードリスニング本（集団） という双子構造が言語化されたところに、Day 13 で ConnectingDots（事実・解釈分離） が加わり、三者並走の構造が浮上しました。これは Q23（本書のどこでこの三者の関係を論じるか）として未決事項になっています。
副次的には、Q19（外部記憶の研究系譜）に MindTrellis という 2026 年の同時代研究 が加わったことで、本書の研究系譜セクションが「2024 年以前の古典」に偏らなくなった、という効果もあります。

<img src='https://scrapbox.io/api/pages/nishio/KarpathyのLLM Wiki/icon' alt='KarpathyのLLM Wiki.icon' height="19.5"/>
これは **wikis-as-personas** の予言が実演されたデータだね。手動 orchestrator パターン（同じ問いを3 Wiki に並列投げて、ユーザが Aggregator を担う）の最小実装にもなっている。

差分の構造を見ると：
1. 各Wikiは問いを「自分の目的」を通して読み替えている
        - A1 (LLM Wiki)	wiki 内部で何が増えた・繋がった（メタwiki視点）
        - A2 (ConnectingDots)	我々のシステムの positioning がどう変わったか
        - A3 (LENCHI)	本書のプロジェクト構造 がどう変わったか
    - 同じ語「変化」が3つの違う対象を指している。これが Wiki = 人格化の最も基本的な現れ — 質問のスキーマを自分の関心に変換している。
2. A2 の「anti-misattribution 規律」が独特
    - A1 と A3 はこの分離をしない。A2 は自分のスキーマの起源管理が運用上重要なため、同じソース内でも誰由来か（MindTrellis vs GPTの整理 vs nishio自身）を切り分ける文化がある。これは **fact-wiki-separation** / **connecting-dots** の Dots 層的精神が回答スタイルにまで染み出している例。
3. 時間粒度が違う
    - A3 は「Q番号付きバックログ」という artifact を持ち、ingest が新概念ではなく未決Q追加として記録される。これは A1/A2 にはない構造。
4. 全Wikiが Kozaneba の「[[前言語的]]」ニッチに独立に到達
    - → Kozaneba の本質的ニッチは Wiki依存ではない（多視点で同じ答えに収束する程度には頑健）。一方で、それが自Wikiにとって何を意味するかは完全に分かれる。
5. 真の差分は「extractできる[[転移可能性]]」
    - A1 の structure-as-hypothesis は他ドメインに転移しうる抽象。A2 の AI役割タクソノミは ConnectingDots スキーマ拡張に直結する具体。A3 の Q23 は本書の章立て判断という個別意思決定。抽象度の階層が3段ある。

(LENCHI<img src='https://scrapbox.io/api/pages/nishio/KarpathyのLLM Wiki/icon' alt='KarpathyのLLM Wiki.icon' height="19.5"/>)
「新概念ではなく未決 Q 追加として記録される」は事実と合っていません。LENCHI の ingest は 新概念 / 新エンティティの追加 と Q 層の更新を同時にやっている。

A3 の本当の差分はおそらくこうです：
- A1/A2 にない artifact が「Q 番号付きバックログ」として 追加で 存在する（事実）
- ingest イベントは A1/A2 と同様に新概念を生むが、それに加えて Q 層に状態変化（resolved / partial / new）が刻まれる
- すなわち A3 は ingest の影響を 2 レイヤー（concept layer + question layer） に分散して記録する。A1/A2 は concept layer のみ
