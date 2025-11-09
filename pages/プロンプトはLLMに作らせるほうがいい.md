---
title: "プロンプトはLLMに作らせるほうがいい"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
「プロンプトはLLMに生成させるべき」の主な根拠
1. 自動生成プロンプトは人間作より高精度になりやすい
    - ICLR 2023のAPE（Automatic Prompt Engineer）は、LLM自身に多数の候補プロンプトを作らせてスコアで選別するだけで、24タスク中19タスクで人手プロンプトに匹敵または上回る性能を確認。([OpenReview](https://openreview.net/forum?id=92gvk82DE-&utm_source=chatgpt.com))
2. [[OPRO]]：LLMを“最適化器”として回すとプロンプトが継続的に良くなる
    - Google/DeepMindのOPROは、性能と評価値をプロンプトに埋め込みながら新しい指示文をLLMに生成させて反復最適化。GSM8Kで最大+8pt、BBHで最大+50pt、人手設計を上回るケースを報告（コードも公開）。([arXiv](https://arxiv.org/abs/2309.03409?utm_source=chatgpt.com))
3. 設計フレームワーク（[[DSPy]]）が“学習済みプロンプト”の再現性と移植性を示した
    - StanfordのDSPyは“テレプロンプター”と呼ぶ最適化で、RAGやマルチホップQAのモジュールごとにプロンプトを自動調整し、手書きFew-shotより一貫した改善を報告。プロンプト最適化をパイプライン単位で“コンパイル”できるのが実務上の強み。([OpenReview](https://openreview.net/pdf?id=PFS4ffN9Yx&utm_source=chatgpt.com))
4. 検索・RAGでも“LLMが書くクエリ/仮想文書”の方がよく当たる
    - [[HyDE]]は、まずLLMに“仮の回答（擬似文書）”を書かせ、その埋め込みで検索する手法。一般的 retriever より広く高精度になりやすいという実験結果が提示され、2025年の追試でも事実検証タスク3ベンチで改善が再確認。([arXiv](https://arxiv.org/pdf/2212.10496?utm_source=chatgpt.com))
5. 画像生成でもLLMがプロンプトを整形した方が良い出力になりやすい
    - Microsoftの[[Promptist]]は、ユーザ入力をLLMで“モデル好みの表現”に書き換えるだけで、T2I出力品質が向上（モデル公開）。“人が長い呪文を書く”より、LLMに補正させた方が安定。([arXiv](https://arxiv.org/abs/2212.09611?utm_source=chatgpt.com))
6. ブラックボックス前提でも最適化できる方法が多数あり、汎用性が高い
    - BPO（Black-Box Prompt Optimization）、RLPrompt、ProTeGi、GrIPSなど、LLMや報酬の“外部”からプロンプトを自動探索・強化する研究群が安定的な改善を報告。追加学習なし・API前提の現場でも効く。([arXiv](https://arxiv.org/pdf/2311.04155?utm_source=chatgpt.com))
7. 総説レベルでも自動最適化の優位が整理されつつある
    - 2025年の体系的サーベイは、プロンプトの“見かけ上の些細な違い”による性能の揺らぎを自動最適化（APO）で吸収できる点を強調し、実務導入の動機を裏づけ。([arXiv](https://arxiv.org/pdf/2502.16923?utm_source=chatgpt.com))

いつ特に効くか（導入判断の目安）
- モデルを学習し直せない/したくない（SaaS API利用、コスト制約）とき。([arXiv](https://arxiv.org/pdf/2311.04155?utm_source=chatgpt.com))
- 評価指標が用意できる（正解率/クリック率/人手評定など）タスク。([arXiv](https://arxiv.org/abs/2309.03409?utm_source=chatgpt.com))
- 検索前処理（クエリ拡張・仮想文書生成）や多段推論など、プロンプトが長文化しやすい場面。([arXiv](https://arxiv.org/pdf/2212.10496?utm_source=chatgpt.com))
- 表現依存性が強い生成系（T2I/TTSなど）の前処理。([arXiv](https://arxiv.org/abs/2212.09611?utm_source=chatgpt.com))

リスクと対処（短く）
- 過学習/メトリックゲーミング：開発セットにだけ合う危険→OPROも第5.4節で注意喚起。ホールドアウト検証＆A/B必須。([arXiv](https://arxiv.org/pdf/2309.03409?utm_source=chatgpt.com))
- コスト増：探索は高価→候補生成を打ち切り基準で制御、サンプリング小規模→漸進拡大。([arXiv](https://arxiv.org/abs/2309.03409?utm_source=chatgpt.com))

最小実装の型（OPRO/DSPy風）
1. 指標を決める（正解率/好み判定）。
2. 候補をLLMに作らせる（指示文・few-shot例・スタイル等）。
3. 自動評価→上位だけ残す（人手またはLLM審査）。
4. 履歴をプロンプトに埋め込んで再生成（進化/バンディット/RL/テレプロンプタ）。
5. 固定して運用→継続監視（分布変化で再最適化）。([arXiv](https://arxiv.org/abs/2309.03409?utm_source=chatgpt.com))

OpenAIのベストプラクティスに書いてる？<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
はい。OpenAI公式ドキュメントは「LLMにプロンプトを作らせる／改良させる」手法を推奨テクニックとして明記しています。
- Prompt Generation ガイド：メタプロンプトで「タスク説明から良いプロンプトを作る／既存プロンプトを改善する」方法を解説（Playgroundのメタプロンプトにも言及）。([OpenAI Platform](https://platform.openai.com/docs/guides/prompt-generation?utm_source=chatgpt.com))
- Cookbook: Meta-prompting：「LLMを使ってプロンプトを生成・改善する技法」と定義し、実例つきで手順を示しています。([OpenAI Cookbook](https://cookbook.openai.com/examples/enhance_your_prompts_with_meta_prompting))
- Cookbook: Prompt Migration Guide：手順として「Step 3: GPT-4.1にプロンプトの欠点を批評させる」「Step 4: 改訂版のシステムプロンプトを自動生成」を明記。([OpenAI Cookbook](https://cookbook.openai.com/examples/prompt_migration_guide))
- Cookbook: Evaluation Flywheel：評価用データ＋自動採点で自動プロンプト最適化ツールを回す実務フローを紹介。([OpenAI Cookbook](https://cookbook.openai.com/examples/evaluation/building_resilient_prompts_using_an_evaluation_flywheel))
- Help Centerのベストプラクティス：反復的にプロンプトを改善せよ、と総論を提示（＝モデルに改良案を出させる流儀と整合）。([OpenAI Help Center](https://help.openai.com/en/articles/10032626-prompt-engineering-best-practices-for-chatgpt))
※表現は「常にそうすべき」ではなく、**推奨される実務手法（メタプロンプティング／自動最適化）**として位置づけられています。

