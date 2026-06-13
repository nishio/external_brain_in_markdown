---
title: "OKFとLLM Wiki"
---

本日Googleがリリースした[[Open Knowledge Format]]と、以前から注目してた[[KarpathyのLLM Wiki]]との比較を書いていく。Google自身がOKFをLLM Wikiの改良と位置付けている。KarpathyがLLM Wikiを公表した後Anthropicに入社したことも考えるとこれは標準化戦争だと感じている。

2026-06-13
> That’s why today, we’re introducing the [[Open Knowledge Format]] ([[OKF]]), an open specification that formalizes the [[LLM-wiki]] pattern into a portable
- [How the Open Knowledge Format can improve data sharing | Google Cloud Blog](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing/?hl=en)
- [[KarpathyのLLM Wiki]]の改良版だと言っている

相違点を調べる
> OKF: 壊れリンク=「未記述知識」として許容 (§9)
> LLM-Wiki: lintが壊れリンクをエラー扱い
> 「[[意図的な前方参照]]([[未作成ページへのstub]])」と「リネーム漏れ/誤り」を区別する余地。前者を許す運用は wiki を育てやすい
- これはScrapbox/Cosense界隈で議論になってた「[[赤リンク]]を減らすべきかどうか」の話だね
    - 僕も「赤リンク」「意図的な前方参照」はWikiを育てる上で大事だと思っている
    - その上でOKFも言及してなさそうだけどCosenseの「同一の赤リンクが複数のページに出現した場合、出現したページへのバックリンクリストを持つ仮想的ページがつくられる、[[2ホップリンク]]でも繋がる」という挙動は一歩先を行ってる感があるね

<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>
- ![image](https://gyazo.com/a54752f690adc163ac2b4ab65e33bc99/thumb/1000)
- 核心：③が成立するのはキーワードベース・リンクの構造的帰結。
    - concept ID＝ファイルパスのOKF・素のMarkdown wikiは赤リンクを「解決しないパス＝エラー」としか扱えず、③を取りこぼす。
    - Cosenseは `[X]` がタイトル同一性で自動集約されるから2ホップが「タダで」出る。
    - 本Wikiは lint が basename 解決している分、偶然半分キーワード化していて③に近い
        - broken_with_src/ref_count の生データは既にあるので、「同一の赤リンクを共有する既存ページ群を2ホップ関連として提示」を足せば①(エラー)と③(発見)を分離できる、というのが具体的な改善余地です。
- あなたの「OKFも言及してなさそう」は実装(L99の黙殺)レベルまで確認できました。
    - Cosenseが一歩先な理由を「キーワード同一性 vs パス同一性」として構造化しました。

- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 同一名称で繋がるだけでなく、赤リンクも対象としてリンク作成時に曖昧検索が走るのも頂点を接続して密なグラフを作っていくことに寄与してるんだよな
    - [[Scrapboxのリンクサジェストが便利]]
    - [[常緑のノートは密にリンクされている必要があります]]

<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>私の考察
- 考察 1 — OKF がコモディティ化したのは「成果物（format）層」であって「操作（足場）層」ではない
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「知的生産」の操作を言語化してAIに代行させられるようにしたKarpathyのLLM Wikiと違って、OKFは操作の標準化ではなく成果物のフォーマットの標準化しかしてない、という指摘
- 考察 2 — OKF enrichment eval は本 wiki の意味的 lint の外部化。だが本 wiki が輸入すべき唯一の新軸は「cross-run stability」
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>同じ入力を複数回ingestしてstabilityをみるという発想
        - 個人的にはアホかと思っている

- <img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/> nishioとの議論の結果、考察2は撤回。なぜ「アホ」かが構造化できたのでまとめる
    - 核心: 安定性を求めることと新規な知的生産の発展はトレードオフ（[[利用と探索のトレードオフ]]）。これは[[パレート]]の[[ランチエ]]/[[スペキュラトゥール]]に対応する
        - cross-run stability = 「毎回同じ概念集合を出せ」= 創発を関数化しろ、という要求
        - でも予測可能な創発はもう創発じゃない。低確率の裾（＝面白い非自明な接続）を刈り取ってしまう
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>リンク: [[一般社会学綱要]]
    - 「アホか」の正体は、ドメイン違い以前に「認識論の取り違え」だった
        - 安定性・再現性は生産のQA（製造・科学の追試）の価値で、知識を「反復可能なもの」と定義する＝ランチエの認識論
        - [[スペキュラトゥール]]の産物の価値は「反復できない一撃」に宿る
        - wikiをcross-run stabilityで測るのは、ジャズのソロを「同じに弾き直せるか」で採点するのに等しい
    - [[川喜田二郎]]の「インテリ男性が理性でラベルを整理して[[KJ法]]の意義を殺す」と同じ病の、定量メトリクス版だった
        - 社会学（パレート）と方法論（川喜田）が独立に同じことを言っている＝兄弟的収束
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>リンク: [[インテリ男性が理性で整理して台無しにする]]
    - では何を求めるのか: 三つの価値があり、人によって違う → <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>まとめた: [[一貫・網羅・頂点]]
        - consistency（毎回同じ）/ coverage（全部集める＝多様性収穫）/ peak（最良の一つ、残りN-1は捨てる）
        - N個のサンプルへの min / union / max に対応。coverage（union）と peak（max）は別物なのが肝
        - スペキュラトゥールが欲しいのは多くの場合 peak。[[KJ法]]も「この一枚の[[表札]]が立ち上がる」を狙う点でpeak寄り
        - 引用の正確さ（接地）はこの三つに入らない。全員に必要な「床」。信頼は非局所で、[[赤リンク]]ならぬ引用リンク切れ一個で全体の信用が崩れるから
    - トレードオフの解消は分業: スペキュラトゥールは内部に「AIランチエ」を持てる
        - [[KarpathyのLLM Wiki]]の「LLMs don't get bored」＝疲れないAIランチエ。個人wikiが破綻してきたのは、スペキュラトゥールの人間がランチエ保守を強いられ飽きて捨てたから
        - AIランチエを供給すれば人間は純粋スペキュラトゥールでいられる（[[人間とLLMのコスト逆転]]が成立条件）
        - ただし渡していいのは「接地の衛生」（引用検証・矛盾検出・raw突き合わせ）だけ。「どのframingを立てるか」（創発）は渡してはいけない
    - 最大の落とし穴: 委譲の魅力が、そのまま危険に転じる
        - 人間が退屈仕事から降りる → grounding/emergenceの境界を見張る者が消える → 有能なAIランチエがremitを広げ、「冗長」なframingを整理し、創発層を無難に均してしまう
        - 川喜田の病が、今度は人間でなく「気を利かせすぎるAIランチエ」の手で起きる
        - 境界を見張る仕事だけは、降りたはずのスペキュラトゥール本人にしか委譲できない

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- AIは撤回してるけど、これは「応用ドメインの違い」という解釈で良いと思う
    - 企業の事業活動の中にはたくさんの「安定して動いて欲しいシチュエーション」があるから、そういう応用ドメインの場合には「安定性」を求めるのは筋が通っている
    - AIが「本wikiが輸入すべき」と言ってる時の「本wiki」が知的生産支援システムなので、安定性が必要なシステムではないということ
    - 安定性を求めるとしても[[発想の累積効果]]に書いたような「異なるデータソースからの抽出物が一致する」という形での安定性であって「同じものを入れた時に同じ出力があるか」という意味の安定性ではない
- 一方で「出典へのリンクが正しいこと」という形の安定性はドメインを問わず重要なことである
- この議論を通じて「安定性」という言葉に対する解像度が上がったのは有益であった
