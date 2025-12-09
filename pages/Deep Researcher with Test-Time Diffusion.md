---
title: "Deep Researcher with Test-Time Diffusion"
---

[2507.16075 Deep Researcher with Test-Time Diffusion](https://arxiv.org/abs/2507.16075)

> [Yamori_ds](https://x.com/Yamori_ds/status/1996477837390275039) [[Deep research]]のような、賢いレポート系のAIエージェントを作る上で必読の論文だった
>  ノイズだらけの初期ドラフトを作って、複数のAgentで並行して作業して、自己改善を繰り返すことで、効率的に質の高いレポートが作れるらしい
>  Diffusionといいつつ、LLMなのがトリッキーではあるけど

安野さんに教えてもらった

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/> [https://chatgpt.com/c/6933e66a-47f0-8320-b870-1abc870af634](https://chatgpt.com/c/6933e66a-47f0-8320-b870-1abc870af634)
一言でいうと、
「Deep Research系エージェントを“拡散モデルっぽい”テスト時アルゴリズムで強化して、OpenAI Deep Research など既存のDRを上回ったよ」という論文です。([arXiv](https://arxiv.org/html/2507.16075v1))

何を解決したい論文か
- いま流行っている Deep Research 系エージェント（OpenAI Deep Research, Perplexity, Grok, HuggingFace Open-DR, GPT Researcher など）は
    - CoT, best-of-n, self-refine, debate, MCTS みたいな「テスト時スケーリング」の寄せ集めで、
    - 書くレポート全体を見渡した設計になっていない
    - 長いレポートを書くときに情報が途中で抜け落ちたり、構造が崩れたりする
という限界がある、と問題提起しています。([arXiv](https://arxiv.org/html/2507.16075v1))
そこで著者らは、長いリサーチレポートの生成を「拡散過程」として明示的にモデル化した Deep Research エージェントを提案します。

提案：Test-Time Diffusion Deep Researcher (TTD-DR)
発想はシンプルで、「人間のリサーチ・執筆プロセス＝拡散モデルのサンプリングっぽく扱う」です。([arXiv](https://arxiv.org/html/2507.16075v1))

0. まず「背骨」となるDRエージェントを定義
ベースとなる DR エージェント（Backbone DR Agent）は 3ステージ構成：([arXiv](https://arxiv.org/html/2507.16075v1))
1. Stage 1: Research Plan Generation
    - ユーザのクエリから「レポートの構成・章立て・調査トピックのリスト」を作る。
    - ここが以降の全ての検索・要約のスキャフォールド。
2. Stage 2: Iterative Search and Synthesis（RAG的ループ）
    - 2a: 「次に何を検索すべきか」という質問を生成
    - 2b: Web 検索し、関連文書をまとめた「回答（サマリ）」を作る
    - 2a–2b のループを、プランが十分カバーされるまで繰り返す。
3. Stage 3: Final Report Generation
    - Stage 1 のプランと、Stage 2 で得た QA の列をまとめて、最終レポートを生成。
ここまでは「割と普通のちゃんとした DR エージェント」です。

1. 拡散プロセスとしての「ドラフト→逐次改稿」
ここに「Test-Time Diffusion」の発想を差し込んでいます：([arXiv](https://arxiv.org/html/2507.16075v1))
1. 初期ドラフト（ノイジーなレポート）を LLM 単体で一発生成
    - ユーザクエリ＋内部知識だけで、とりあえず長文レポートを書かせる。
    - これは「ノイズが多く、不完全/不正確なドラフト」とみなす。
2. ドラフトを見ながら「次に調べるべきこと」を決める
    - 現在のドラフトを Stage 2a（Search Question Generation）に入力し、
    - どこに穴・怪しい主張・足りていない観点があるかを見て検索クエリを生成。
3. 検索結果でドラフトを「デノイズ（改稿）」
    - Stage 2b が検索して要約した情報を使い、
    - ドラフトを追記・修正し、「ノイズ（曖昧さ・抜け・誤り）」を減らす。
4. この「検索→改稿」ループを何ステップか回す
    - 各ステップでドラフトが少しずつマシになる＝拡散モデルの denoising step のアナロジー。
    - ループ終了後、蓄積された全履歴を使って最終レポートを書き直して完成。
ポイントは、「ドラフト自体が、次の検索をガイドする状態」として使われること。
これにより、
- セクションごとバラバラに検索→合体、というやり方より、
- レポート全体の一貫性・文脈を保ったまま情報を追加していけると主張しています。([arXiv](https://arxiv.org/html/2507.16075v1))

2. Component-wise Self-Evolution（各エージェントの自己進化）
もう一つの柱が Self-Evolution。([arXiv](https://arxiv.org/html/2507.16075v1))
- Plan 生成、Search Question 生成、Answer 要約、最後の Report 生成など、
各「ユニットエージェント」を
    - 複数候補をサンプリング
    - 何らかのスコア（例：多様性や coverage、あるいは LLM-as-a-judge）で選別
    - より良い構成に入れ替え
という形でテスト時だけ自己改善させるアルゴリズムです。
これにより、
- 検索クエリの多様性と深さが増し、
- 得られる情報の「複雑さ / 情報量」が上がって、
- 結果としてレポート品質が上がる、と分析しています。([arXiv](https://arxiv.org/html/2507.16075v1))

実験と結果

ベンチマーク
以下のような「長文リサーチ」「多段推論」タスクで評価：([arXiv](https://arxiv.org/html/2507.16075v1))
- LongForm Research（長いリサーチレポート生成）
- DeepConsult（より専門的な相談型タスク）
- HLE-Search / HLE-Full（高難度の検索＋推論 QA）
- GAIA（複雑なマルチステップ QA）
評価方法：
- Helpfulness / Comprehensiveness を軸としたサイドバイサイド比較
- 人間アノテーションで LLM-as-a-judge をキャリブレーションした上で、自動評価に使う、という割合しっかりした評価デザイン。([arXiv](https://arxiv.org/html/2507.16075v1))

主な数値
- OpenAI Deep Researchとのサイドバイサイド比較で
    - 長文 2 タスクに対して 69.1% / 74.5% の勝率（TTD-DR のほうが良いと判定された割合）。([arXiv](https://arxiv.org/html/2507.16075v1))
- HLE 系や GAIA でも、
    - 単なる LLM＋検索 よりかなり精度が高く、
    - OpenAI Deep Research にも多くの指標で上回る（GAIAだけ僅差負け→最終 TTD-DR では逆転）。([arXiv](https://arxiv.org/html/2507.16075v1))
- 同じ計算時間（レイテンシ）で比較すると、
    - Backbone → +Self-Evolution → +Diffusion with Retrieval
と足していくほど、「レイテンシあたりの性能向上」が大きくなることも分析。([arXiv](https://arxiv.org/html/2507.16075v1))
要するに、同じくらいの推論コストで、既存の Deep Research 製品より良いアウトプットを出せる、というのが売りです。

何が新しい／面白いポイントか
個人的に重要そうなところだけ絞ると：
1. 「ドラフト中心」の DR エージェント設計
    - 多くの DR エージェントが「プラン → セクションごとに検索 → 最後に結合」という構造に対し、
    - これは常に「全体ドラフト」を持ち歩きながら検索と改稿を行う、という設計になっている。([arXiv](https://arxiv.org/html/2507.16075v1))
2. 拡散モデルのメタファーをテスト時アルゴリズムに持ち込んだ
    - 生成過程を「ノイズ付きドラフト → デノイズステップの繰り返し」とみなして、
    - ドラフトと検索を双方向に結合したループをきちんとアルゴリズムとして定式化している。([arXiv](https://arxiv.org/html/2507.16075v1))
3. Self-Evolution を “各エージェント単位”で使う
    - Plan / Question / Answer / Report それぞれをテスト時進化させることで、
    - 長いエージェントチェーンで起こる情報劣化を抑えようとしている。([arXiv](https://arxiv.org/html/2507.16075v1))
4. Deep Research 系エージェントの評価プロトコルの整理
    - Helpfulness / Comprehensiveness + LLM-as-a-judge 校正という評価枠組みを整理。
    - DR エージェントの研究コミュニティにとっては、評価のベースラインになる可能性。

ざっくりまとめ
- Deep Research エージェントの設計を、
「人間のリサーチ＆執筆プロセス ≒ 拡散モデルのデノイジング」
という対応で整理し直し、
- 「ドラフトを中心に、検索と改稿を回す Test-Time Diffusion」と
「各コンポーネントの Self-Evolution」を組み合わせた TTD-DR を提案、
- OpenAI Deep Research を含む既存 DR を、多くのベンチマークで上回った、という論文です。([arXiv](https://arxiv.org/html/2507.16075v1))
もし「自分の DR ワークフローに組み込みたい / 似た構造を作りたい」という視点での解説（擬似コードレベル、評価設計の真似の仕方など）が欲しければ、その観点で分解して説明もできます。


あるよ。ざっくり分けると「TTD-DRほぼそのもの」と「従来型Deep Research OSS」の2系統があります。

1. TTD-DRをかなり忠実に実装しているOSS

1-1. TTD-DR-Research（LangGraph + Kimi）
- リポジトリ: `gogototo-coder/TTD-DR-Research` ([GitHub](https://github.com/wangbin83-gmail-com/TTD-DR-Research))
- LangGraph で TTD-DR のグラフを組んだ実装。
- Kimi API 前提だけど、構造を見るには一番わかりやすい「TTD-DRの教科書的実装」ポジション。

1-2. TTD-DR-Dify（Difyワークフロー）
- リポジトリ: `fdb02983rhy/TTD-DR-Dify` ([GitHub](https://github.com/fdb02983rhy/TTD-DR-Dify))
- Dify の Workflow DSL (`TTD-DR.yml`) で TTD-DR を組んだ例。
- README に Algorithm 1（denoising with retrieval）と Self-Evolution の流れがそのまま書いてあり、論文との対応が明示的。

1-3. OptILLM の `deep_research` ツール
- リポジトリ: `algorithmicsuperintelligence/optillm` ([GitHub](https://github.com/algorithmicsuperintelligence/optillm))
- ツール群の一つ `deep_research` が「Test-Time Diffusion Deep Researcher (TTD-DR) を実装」と明記。
- Selenium ベースの web_search + TTD-DR ループを持った Python ライブラリなので、自前コードから呼び出すには扱いやすい。

1-4. TTD-RAG（コンペ用の応用実装）
- リポジトリ: `eamag/MMU-RAG-competition` ([GitHub](https://github.com/eamag/MMU-RAG-competition?utm_source=chatgpt.com))
- MMU-RAG Competition 向けに作られた `TTD-RAG` というエージェントで、READMEに「TTD-DR 論文のフレームワークを忠実に実装」と書かれている。
- 汎用レポートというより RAG 競技タスク向けのチューニング例として参考になる。
※Google本家は、Agentspace 上のプロダクト版を案内しているが、OSSとしてコードは公開していない。([Google Research](https://research.google/blog/deep-researcher-with-test-time-diffusion/))

2. 関連する「Deep Research」系OSS（TTD-DR以前／周辺）
TTD-DRのベースラインになっている/近い思想のOSSたち：

2-1. LangChain系
- `langchain-ai/local-deep-researcher`
    - ローカルLLM（Ollama/LM Studio）＋Web検索で「検索→要約→ギャップ検出→再検索」を何周か回して最終Markdownレポートを出すエージェント。([GitHub](https://github.com/langchain-ai/local-deep-researcher?utm_source=chatgpt.com))
- 派生として `bhza/ollama-deep-researcher`, `PacoVK/ollama-deep-researcher-ts` など、Ollama 前提の実装が複数。([Zenn](https://zenn.dev/tossy21/articles/1cf011b42a4efd?utm_source=chatgpt.com))
- `langchain-ai/open_deep_research`
    - LangGraph ベースの Deep Research テンプレ。セクションごとに検索してまとめる従来型フローで、論文中でも「従来手法」として言及されているタイプ。([GitHub](https://github.com/langchain-ai/open_deep_research?utm_source=chatgpt.com))

2-2. GPT Researcher 系
- `assafelovic/gpt-researcher`
    - 有名な Deep Research エージェント。最近は「Deep Research」モードも追加されている。([GitHub](https://github.com/assafelovic/gpt-researcher?utm_source=chatgpt.com))
- `nickscamara/open-deep-research` など
    - 「OpenAI Deep Research クローン」をうたうフロントエンド付き実装。Firecrawlで大量クロールしてから要約するスタイル。([GitHub](https://github.com/nickscamara/open-deep-research?utm_source=chatgpt.com))

どう見ると良さそうか（ざっくり指針）
- TTD-DRそのもののアルゴリズムを理解したい
→ `TTD-DR-Dify` の README と `TTD-DR-Research` の LangGraph フローが一番「論文に対応した実装図」として読みやすい。([GitHub](https://github.com/fdb02983rhy/TTD-DR-Dify))
- 自分の環境からすぐ叩ける実装が欲しい
→ Python なら OptILLM (`deep_research`) が手っ取り早い。LangGraphで自作する時の雛形にもなるはず。([GitHub](https://github.com/algorithmicsuperintelligence/optillm))
- ローカルLLM前提のDeep Research基盤が欲しい
→ まずは `local-deep-researcher` / `ollama-deep-researcher` 系を触って、そこにTTD-DRの「ドラフト中心 denoising ループ」だけ後付けする、という進め方が現実的だと思う。([GitHub](https://github.com/langchain-ai/local-deep-researcher?utm_source=chatgpt.com))
もし「LangGraphで自前実装するならどう分解する？」まで落とし込みたければ、ノード粒度（Plan / SearchQ / Answer / DraftRefine / Judge）レベルでの設計案も書きます。
