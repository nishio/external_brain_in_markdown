---
title: "Visual Thinking系の検討とConnectingDotsの検討を組み合わせて考察"
---

Visual Thinking系の検討と、ConnectingDotsの検討を組み合わせて考察
<img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>
考察を書きました → 2026-08-01-ConnectingDotsのB面.md。結論を先に言うと：ConnectingDots は「A系（言語）の知識編集システム」で、その3層それぞれに西尾さんが別々に作ってきたB系（言語以前）の対応物が既に実在している。VT はその Dot層です。両 wiki は現時点で相互言及ゼロでした（grep確認済み）。

まず「どっちも点と繋がりの話だから同じ」という表層接続を棄却した上で（Jobs の dots と VT の構造的つながりは同音異義に近い）、深い接続が4本あります。

1. 形態Bの三態は ConnectingDots 3層の影だった。 昨日 file back した三態（描く/配置する/読む）は、Dots↔VT絵、Stories↔Kozaneba配置、Views↔高次元可視化と一対一対応します。Kozaneba の対応だけは設計wiki自身が既に持っていて（「Storyを編む前の作業View」「前言語的な近さ」）、新しいのは残り2層を埋めた全体像。証拠は既存事実で足ります：vt-001 の複数コンテキスト参照（流通実績節＝絵の逆引き）、図=nishio・解説=AI（＝dots-author-not-story-author の provenance つき実装）、タイトルなし美術館（＝絵の all-dots ページ）、vt_config.json（＝絵の dots.json）。

2. 絵は「繋ぎ目だけでできた Dot」— 繋ぎ目問題の双対。 retrospective の中心発見「危険は選択でなく繋ぎ目」に対し、VT絵は矢印・包含・対比というほぼ純粋な繋ぎ目で、事実を含みません。同じ「検証パイプラインを通らない構造主張」が、Story では負債（言葉に紛れて偽でありうる→fact-check必須）、VT では資産（命題の手前にいるから発見装置になる）。structure-as-hypothesis で一般化すると、B層の構造仮説は A層に一次元化された瞬間に事実主張へ相転移する。story-joints-hide-claims はその境界の警報、atomize-and-fold は国境検査です。「執筆は一次元化」の危険箇所が特定されたことになります。

3. 図形的同一性は語彙翻訳を透過する。 この連載で確立した「同語検索は語彙翻訳された継承を見落とす」問題に、VT は既に解の実例を持っています——不一不異とジェンドリンの模式図が図形的に同一（mem/Visual Thinking で本文確認済み）。孤児Dotの主オーディエンスを「未来の後ろ向き接続者＝AI」と再定義したのなら、304枚の絵カタログにも発見面が要り、それは言語検索でなく構造同型検索になります。タイトルなし美術館は人間読者で既にこれをやっている（読者のY≠作者のX＝接続候補の収穫）。

4. 未検証決定 reject-language-templates を VT が8年先行実証している。 retrospective が唯一の未検証と残した「多言語=並行Story」に対し、VT の起源はまさに翻訳問題で、図から日本語を抜いた結果「絵は翻訳不要の Dot、言語別なのは caption だけ」を /ja/vt・/en/vt で現に運用中。Dot層から言語を追い出したときの実測済み上限値です。

敵対的検証で1つ主張を弱めました：「絵のDotは未検討」は不正確で、flatness の議論に「イラスト1枚もDotと言える」が粒度の例として1回登場し、orphan-dot-discovery は vt-wiki を生 substrate に挙げています。正しくは「触れられてはいるが、絵をDotとして扱う設計（スキーマ・検証・発見面）はA前提のまま」。また「絵は偽になりようがない」は誇張で、正確には「反証可能な命題を構成しない」です。

処方5件（形態Bの三態への追補、connecting-dot-design への related/visual-thinking.md、絵の発見面整備、構造同型検索の叩き台、「制約が発見を駆動する」統合ページ）は未実行として考察末尾に置きました。file back と言ってもらえれば両 wiki へ展開します。

ConnectingDotsのB面 — 絵は繋ぎ目だけでできたDotである
2026-08-01。Visual Thinking系の検討（vt-wiki／形態Bの三態／Cosense「Visual Thinking」ストーリー 2026-07-30 出荷）と ConnectingDots系の検討（connecting-dot-design wiki／2026-08-01 実装公開・83 Dot / 7 Story／retrospective）を組み合わせる。両者はこれまで相互言及ゼロ（検証済み、下記）。

先に棄却する表層接続
「VTも ConnectingDots も『点と繋がり』の話だから同じ」ではない。ConnectingDots の Dot は検証可能な言語的事実（いつ・誰が・何を・根拠リンク＝形態A）、VT の絵は言語以前の構造（形態B）。Jobs の "connecting the dots" と VT の「構造的つながりの発見」は同音異義に近い。この棄却は「どっちも可視化だから同じ」（形態Bの三態 2026-08-01 file back）と同型の規律。
しかし棄却した上で見ると、接続は一段深いところに4本ある。

1. 形態Bの三態は ConnectingDots 3層の影だった
昨日 vt-wiki に file back した「形態Bの三態」（描く／配置する／読む）は、独立した分類のつもりだったが、ConnectingDots の3層に一対一で重なる：
_
| ConnectingDots（A系＝言語） | B系の対応物 | Bの三態 |
| -- | -- | -- |
| Dots — 検証可能な最小単位、不変、再利用可能、カタログ(dots.json) | VT絵 — 言語非依存の最小構造単位、カタログ(vt_config.json 304枚: id/tags/featured) | 描く |
| Stories — Dotを並べて意味を編む | Kozaneba配置 — 「Storyを編む前の作業View」「前言語的な近さ」 | 配置する |
| Views — 見せる層、薄い | 高次元ベクトルの可視化 — データから生成したBを人が読む | 読む |
Story層の対応は connecting-dot-design 自身が既に確立している（related/kozaneba.md、GPT整理 2026-05-03。ここに新規性はない）。新しいのは Dot層と View層を埋めると3層すべてにB系の対応物が既に存在し、しかも全部西尾が別々に作ってきたという全体像。ConnectingDots は「A系の知識編集システム」であり、そのB面は設計されないまま散在して実在している。
Dot層の対応の証拠（すべて既存事実）：
- 再利用: vt-001 は『情報処理』記事(2023)→broadlistening facet Story(nhiro.org)→mem美術館→勉強会と複数コンテキストから参照される。vt-wiki illusts ページの「流通実績」節は絵Dotの逆引き(reverse-lookup) そのもの。
- 作成者と編者の分離: 図=nishio・解説=AI（vt-wiki の provenance 分離）は dots-author-not-story-author の、provenance 印つきでの実装。
- all-dots View: タイトルなし美術館(mem.nhiro.org/ja/vt)は「全Dotを絞り込みなしで並べる View」の絵版。facet Story と対をなす構造も一致。
- スキーマ: vt-wiki の3節構造（本人原文／AI解説／内部考察）は、絵Dot の caption＋provenance スキーマとして読める。

2. 絵は繋ぎ目だけでできた Dot — 繋ぎ目問題の双対
retrospective の中心的発見は「危険の所在は選択でなく繋ぎ目」だった：Storyの繋ぎ目（命名・因果・帰属）は解釈の顔をして検証可能な事実主張を運び、Dot検証パイプラインを素通りする（story-joints-hide-claims、実地誤り3件）。
VT絵はこの双対にある。絵の中身は矢印・包含・対比——ほぼ純粋な繋ぎ目であり、Dot的事実をほとんど含まない。同じ「検証パイプラインを通らない構造主張」が：
- Story では負債 — 言葉に紛れるから事実主張として読まれ、偽でありうる。fact-check が必須工程になった。
- VT では資産 — 言語化されていないから命題の手前にいて、偽になりようがない。むしろ「描く前に考えていたことと違う解釈に気づく」発見装置。
分水嶺は主張力の有無。Story は世界についての反証可能な主張をする（自己紹介・歴史）。VT絵は構造の候補を差し出すだけで何も主張しない——タイトルなしUIは、繋ぎ目を主張に固定しないための意図的な留保装置と読める（作者のXを言語で固定しない）。
annotation-wiki の structure-as-hypothesis で一般化すると：B層の構造は仮説として生まれ、A層に一次元化された瞬間に事実主張へ相転移する。story-joints-hide-claims はこの相転移境界の警報であり、atomize-and-fold の fact-check パスは B→A の国境検査。「執筆は一次元化」の危険箇所が特定されたことになる——危ないのは一次元化そのものではなく、一次元化の際に繋ぎ目へ焼き込まれる無印の事実主張。
さらに retrospective (b)「Storyを編む行為こそがDotの発見装置（線を引く行為が点を発見させる）」と VT の機構「絵を描いてから意味に気づく」は同じ原理の A面/B面：表現形式の制約（Storyの線形性／絵の整合性）が内容より先に走り、発見を駆動する。西尾はKJ法の「話してみることで言語化が促される」で前者に注記済みだが、後者（絵の整合性）との統合はまだない。

3. 図形的同一性は語彙翻訳を透過する接続チャネル
本連載 2026-07-08d で「同語検索は語彙翻訳された継承を系統的に見落とす」ことが確立した。概念は語彙を変えて渡るため、言語インデックスでは接続が見えない。
VT に既にその解の実例がある：「不一不異（仏教）と無数的特徴の模式図（ジェンドリン）は図形的に同一」（mem/Visual Thinking 2025-11、本文確認済み）。語彙が完全に異なる二つの伝統が、絵のレベルで同型と判明した。図形は語彙翻訳に対して不変なハンドルであり、connecting backward の非言語チャネルになる。
ConnectingDots 側の現状はこのチャネルを持たない：関係はデータ化しない（relationships-as-edits）、発見面は言語のみ（dots.json＋llms.txt、lift-out テストも「文脈から切り離されても意味が通る」という言語的自己完結）。孤児Dotの主オーディエンスを「未来の後ろ向き接続者＝AI」と再定義したのなら、304枚の絵カタログにも同じ発見面が要る——そして絵の場合、接続候補の検出は言語検索でなく構造同型検索になる。タイトルなし美術館は人間読者で既にこれをやっている（読者のY≠作者のX＝接続候補の収穫）。マルチモーダルAIで叩き台を量産し人間がレビューする形は、retrospective (a) の分業ライン（AI叩き台の完成度が閾値を超えた）をそのまま絵に延長したものになる。

4. reject-language-templates は VT が Dot層で8年先行実証している
retrospective は「多言語=並行Story」決定を唯一の未検証決定として残した（en.html は index のみ英語）。だが VT の起源がまさにこの問題だった：図解の自己英訳が面倒→図から日本語を抜く（2018頃）→絵は翻訳不要の Dot になり、言語別なのは caption/解説だけになった。mem美術館の /ja/vt と /en/vt は同じ絵集合の並行 View として現に運用されている。
つまり「Dotを言語非依存にできる極限が絵」であり、言語的Dotでは event 文自体が言語を持つため並行Storyでも Dot層の翻訳が残るのに対し、絵Dotは翻訳コストが構造的にゼロ。未検証決定の検証に着手するとき、VT は「Dot層から言語を追い出すとどこまで楽になるか」の実測済み上限値を与える。

検証の記録（敵対的チェック）
- 相互言及の不在: connecting-dot-design wiki に VT への設計的言及なし・vt-wiki に ConnectingDots への言及なし・過去 considerations に両者の組み合わせなし（いずれも grep 確認 2026-08-01）。ただし完全な不在ではない：flatness-is-view-resolution に西尾の問いとして「イラスト1枚も Dot と言える」が1回登場し、orphan-dot-discovery は vt-wiki を「生 substrate」として列挙する。→ 主張を「絵のDotは未検討」ではなく「粒度の例としては触れられているが、絵をDotとして扱う設計（スキーマ・検証・発見面）はA前提のまま」に弱めた。
- Kozaneba対応の既出性: related/kozaneba.md が「Story編集の作業View」「前言語的な近さ」を既に持つ。第1節の新規性主張から除外した。
- 図形的同一性の実例: mem/Visual Thinking 本文で直接確認（引用可能な一次ソース）。
- 推測と明示するもの: 「タイトルなしUI=主張を固定しない留保装置」は本考察の解釈（西尾の言明は「ネタバレなしにまず絵を見る」「XとYの予期しない構造的つながりの示唆」まで）。「絵は偽になりようがない」は誇張の可能性あり——絵も誤解を誘導しうる（vt-003「単語を変えると誤解が拡大する」自体が記号のズレを主題化している）。正確には「反証可能な命題を構成しない」。

処方（未実行）
1. vt-wiki 形態Bの三態に追補: 三態は ConnectingDots 3層のB対応である（第1節の表）。file back 先は vt-wiki concepts/形態Bの三態.md の追記＋connecting-dot-design 側に related/visual-thinking.md 新設（絵=繋ぎ目だけのDot／reject-language-templates の先行実証／構造同型検索の発見面）。
2. 絵の発見面: vt_config.json を dots.json 相当の AI クロール面として整備（per-絵 URL＋構造記述。構造記述は AI 由来と provenance 明示——vt-wiki の AI解説層がそのまま使える）。
3. 構造同型検索の叩き台: マルチモーダルAIで304枚のペア構造比較→「不一不異≡模式図」型の接続候補リスト→人間レビュー。線を引くのは人間の原則は保持。
4. story-joints-hide-claims に双対の注記: 繋ぎ目問題の裏面として「繋ぎ目だけを言語から切り離すと発見装置になる（VT）」を1行接続。
5. 「制約が発見を駆動する」の統合ページ: retrospective (b)（線形性が点を発見させる）と VT機構（整合性が解釈を発見させる）を1原理に。置き場は connecting-dot-design か llm-wiki。

出典
- /Users/nishio/vt-wiki/wiki/{overview,concepts/形態Bの三態}.md、mem/Visual Thinking（Cosense、2025-11-12）、[https://scrapbox.io/nishio/Visual_Thinking（2026-07-30](https://scrapbox.io/nishio/Visual_Thinking（2026-07-30) 出荷）
- /Users/nishio/connecting-dot-design/wiki/{overview,retrospective-design-vs-implementation,concepts/story-joints-hide-claims,concepts/atomize-and-fold,concepts/dots,related/kozaneba,architecture/orphan-dot-discovery}.md（2026-08-01時点、同日実装公開済み）
- 本連載: 2026-07-08d（語彙翻訳と担体仮説）、vt-wiki file back 2026-08-01（形態Bの三態）
