---
title: "Talk to the Cityが作られたきっかけ"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
- 「質×量」の両立が難しかったから。 既存の世論調査は“量”は取れるが“深さ（自由記述のニュアンス）”が落ちる、少人数の対話は“深さ”はあるが“規模”に弱い――このトレードオフをLLMで解消するために作られました。公式ページも「深さと規模のトレードオフを解く」ことを狙いとして明記しています。 ([Talk to the City](https://talktothe.city/about))
    - スケール×深さのトレードオフを解く
        - 引用: “…solves the trade-off between depth and scale.”（T3CのAbout） ([Talk to the City](https://talktothe.city/about))
        - 補足: 少人数の深い対話と大規模アンケートのスケールの両立という古典的ジレンマを、LLMで解決する設計思想が中核です。さらにトップページでも
        - 引用: “Focus groups capture nuance, and polls capture scale. T3C does both.”

- 民主主義への不信のスパイラルを反転させたいという問題意識。 AOI（AI Objectives Institute）は、**大規模・高速・包摂的な“広聴（broad listening）”**を可能にして、意思決定者と住民のズレを埋めることを動機に挙げています。質的データを大規模に扱える手段が乏しい、という課題認識から始まっています。 ([AI • Objectives • Institute](https://ai.objectives.institute/talk-to-the-city))
    - 民主主義の“信頼低下スパイラル”への応答
        - 引用: “…help us escape the spiral of declining trust by allowing us to consult the public in much larger numbers.”（AOIサイトの背景説明）
        - 補足: 技術の進歩でより大量・高速・包摂的に声を聴けるようにし、信頼を回復するという問題意識が動機として明記されています。

- 直接のきっかけ（初期プロトタイプ）。 2023年初頭、AIの安全・倫理をめぐる言説マッピングに使った初期版が出発点で、同年10月にオープンソース化。以後、台湾のAI AssembliesやvTaiwan系の取り組み等で展開されていきました。 ([AI • Objectives • Institute](https://ai.objectives.institute/blog/talk-to-the-city-an-open-source-ai-tool-to-scale-deliberation))
    - 初期の直接の狙い（都市レベルで“何百万人”規模の声を聴く）
        - 引用: “…designed to use a ChatGPT-like interface to survey millions of people in a city.”（WiredのAOI紹介記事） ([WIRED](https://www.wired.com/story/peter-eckersley-ai-objectives-institute))
        - 補足: AOIが立ち上がった初期から、都市規模での大規模聞き取りを想定したパイロットとして構想されていました。
    - プロダクト目的（大人数の相互理解を加速）
        - 引用: “Talk to the City helps large groups of people coordinate by understanding each other better, faster, and in more depth.”
        - 補足: 単なる要約生成ではなく、ニュアンスを保持したまま合意形成や意思決定に使える形に落とすことが目的です。

- 研究的な根拠づけ（“質×量”の両立が必要）
    - 引用: “Existing processes… must trade off scale for qualitative detail… In contrast, frontier LLMs enable rich qualitative data at scale.”（政策提言レポート）
    - 補足: 従来手法の限界（規模か深さかの二者択一）を、LLMで乗り越える必要性が背景として示されています。


要するに、**「自由記述を含む大量の声を、ニュアンスを保ったまま素早く意思決定に役立つ形にする」**という課題が“きっかけ”です。


要するに、「自由記述のニュアンスを保ったまま、都市〜国家規模で素早く“広聴”する」という課題意識と、そのためのスケールと深さの両立が、Talk to the Cityが作られた直接のきっかけです。 ([ai.objectives.institute](https://ai.objectives.institute/talk-to-the-city-landing))


出典はこの2つです。
- “Talk to the City helps large groups of people coordinate by understanding each other better, faster, and in more depth.”
→ 公式サイトのトップ見出し（Talk to the City ホーム）。 ([Talk to the City](https://talktothe.city/))
- “Existing processes… must trade off scale for qualitative detail… In contrast, frontier LLMs enable rich qualitative data at scale.”
→ AI4Democracyレポート『How can AI be used to inform policymaking?』（Turan & McKenzie, 2024）イントロダクション p.4。



要点だけサクッと 👇
- 政府レベルでの正式活用・共同作業
AOIは「台湾のデジタル発展部（moda）と協働し，2023年のAI Assemblies等で大規模な意見データの分析にT3Cを使った。modaは自前のT3Cインスタンスを運用している」と明記。 ([AI • Objectives • Institute](https://ai.objectives.institute/talk-to-the-city-landing))
- 初導入の場は“Alignment Assemblies”
2023年10月にT3Cの責任者が台北で唐鳳（Audrey Tang）大臣らと協議。最初のデプロイはmoda主催の「Alignment Assemblies」で，オンラインでPolisに集めた意見をT3Cで可視化・整理したと説明。詳細はmoda公式ページにも掲載。 ([AI • Objectives • Institute](https://ai.objectives.institute/blog/amplifying-voices-talk-to-the-city-in-taiwan))
- vTaiwan／Polisとの補完関係
vTaiwanがPolisで意見を収集→T3Cが自由記述をクラスタリング・要約という役割分担で，台湾の審議プロセスに組み込む形。 ([AI • Objectives • Institute](https://ai.objectives.institute/blog/amplifying-voices-talk-to-the-city-in-taiwan))
- 公的な言及（Audrey Tang）
2023年12月，LSE IDEASのウェビナーで唐鳳氏がT3Cを具体例として紹介。T3Cは多様性とスケールを両立する技術だと述べている。 ([govinsider.asia](https://govinsider.asia/intl-en/article/turning-conflicts-into-co-creation-taiwans-digital-ministry-moda-harnesses-digital-policy-for-democracy))
さらにT3C公式にも唐鳳氏のコメントが掲載（「コストが事実上ゼロに…“broad-listening”」）。 ([Talk to the City](https://talktothe.city/))
- 台湾での具体的ユースケース
・AI Assembly 2023：400人超から2,000件超の意見を収集し，T3Cでトピック分群・インタラクティブ閲覧を提供。 ([AI • Objectives • Institute](https://ai.objectives.institute/blog/amplifying-voices-talk-to-the-city-in-taiwan))
・同性婚（政府のJOINプラットフォームの議題）：JOINの大量コメントをT3Cで分析したケースを提示。元データは法務部の討論ページ。 ([AI • Objectives • Institute](https://ai.objectives.institute/blog/amplifying-voices-talk-to-the-city-in-taiwan))
・2024総統選後の政党別分析（KMT/DPP）：メディアReadrのデータをT3Cでレポート化。 ([AI • Objectives • Institute](https://ai.objectives.institute/blog/amplifying-voices-talk-to-the-city-in-taiwan))
- 呼称
台湾向けコミュニケーションでは**中文名「我城對談」**として紹介されることがある。 ([AI • Objectives • Institute](https://ai.objectives.institute/blog/amplifying-voices-talk-to-the-city-in-taiwan))
まとめると、T3C＝台湾のデジタル省（moda）と連携し、vTaiwan/Polisを補完する“広聴”基盤として政府・市民社会の両方で使われている——という関係です。 ([AI • Objectives • Institute](https://ai.objectives.institute/talk-to-the-city-landing))
