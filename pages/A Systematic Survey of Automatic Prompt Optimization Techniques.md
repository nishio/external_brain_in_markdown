---
title: "A Systematic Survey of Automatic Prompt Optimization Techniques"
---

2025 [https://arxiv.org/pdf/2502.16923](https://arxiv.org/pdf/2502.16923)

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
1枚サマリ
- テーマ: “[[Automatic Prompt Optimization]] ([[APO]])”＝モデルの重みには触れず、プロンプト（指示文）だけを自動で改良して性能を上げる黒箱最適化のサーベイ。
- 中核: 「①シード作成 → ②評価とフィードバック → ③候補生成 → ④選抜・探索 → ⑤反復」の5部フレームワークで、既存研究を網羅的に分類。
- 効き所: ルール編集・進化計算・RL・LLM評価・メタプロンプト・MoE・プログラム合成（DSPY系）などを部品化し、タスク特性とコストに応じて組む。
- 注意点: dev過学習、評価者（LLM-as-a-judge）バイアス、ギブリッシュ分割子・“evil twin”現象、自己反省の失敗、コストの爆発。

5部フレームワークの要点
1. Seed Prompts（初期プロンプト）
    - 手書き（ProteGi, SPRIG など）
    - LLMによる誘導＝Instruction Induction（APE, DAPO, MOP）。READMEや構造化テンプレを埋める派（SCULPT, UniPrompt）も。
2. Inference Evaluation & Feedback（評価とFB）
    - 数値評価: タスク正解率/実行精度、BLEU/ROUGE/BERTScore、報酬モデル、（要ログ確率）NLL/エントロピー。
    - LLMフィードバック: 1候補を磨く（SCULPT, PACE, CRISPO）/ 複数候補を一斉に改善（ProTeGi, PromptAgent, PREFER, SOS）。
    - 人のフィードバック: GATE, PROMST, APOHF など。
3. Candidate Generation（候補生成）
    - ヒューリスティック編集:
        - モンテカルロ/MCTS（ProTeGi, PromptAgent）
        - 遺伝的アルゴ（SPRIG, PromptBreeder, EvoPrompt, StraGo）
        - 語/句レベル置換・語彙剪定（COPLE, CLAPS, BDPL, PIN）
    - 補助NNで編集: RL（RLPrompt, OIRL, PRewrite）, 小型LLM微調整（BPO, FIPO）, GAN的枠組み。
    - メタプロンプト設計（[[OPRO]], PE2, DAPO）
    - カバレッジ志向:
        - 単一プロンプトを枝分かれ拡張（AMPO）
        - Mixture-of-Experts（MOP：クラスタ別プロンプト）
        - アンサンブル（PromptBoosting, PREFER, GPO）
    - プログラム合成: DSP/[[DSPY]], MIPRO, SAMMO… モジュール別に指示と例示を最適化。
4. Search & Select（探索・選抜）
    - Top-K貪欲、UCB/UCT（バンディット）（ProTeGi, PromptAgent, SPRIG, AELP）、
    - 領域別同時探索（RBJS: MOP）、メタヒューリスティクス混成（PLUM）。
5. Iteration Depth（反復）
    - 固定回数 or 早期打ち切り（負利得が続く/閾値到達）。

代表手法の「位置づけ一言メモ」
- OPRO: “メタプロンプト”で「より良い指示文」を言語的に最適化。汎用・実装が楽。
- ProTeGi / PromptAgent: LLMフィードバック＋MCTS/UCBで離散探索を手堅く回す。
- APE: Instruction Inductionの古典。初期プロンプト作りの強い土台。
- SPRIG: システムプロンプト最適化も射程。大規模だが効く。
- CRISPO: 多観点（精度/様式/整合性…）で批評→改稿。生成系に有効。
- MOP: MoE的にクラスタ別プロンプトを用意し、入力ごとに最適な専門家を選ぶ。
- DSPY/MIPRO/SAMMO: LLMパイプラインを部品化して各段を同時に鍛える「設計学」。
- AMPO: 失敗パターンを分岐で吸収、if-then枝でカバレッジ確保。
- COPLE: 影響語の同義置換だけで大きく効くことを示す。後処理最適化にも良い。

使い分けガイド（実務の勘所）
- 分類・MCQ中心/少量データ: Top-K＋UCBでProTeGi系。COPLEの語置換を最後に当てるとラク。
- 要約/翻訳/創作など生成系: LLM批評→改稿（CRISPO/PE2）＋少量の人間FBでハイリターン。
- ドメイン広い/入力多様: MOP（MoE）やアンサンブルで頑健化。
- 長大な手順指示が必要: SCULPT（階層化して磨く）、AMPO（分岐で抜け漏れ封じ）。
- 複数段のRAG/ツール連携: DSPY/MIPROで段ごとに指示・例示を最適化。
- セキュリティ/安全性も同時最適: SOS（性能×安全の多目的最適）。
- とにかく低コストの初期ライン: ランダム区切り文字・単純改稿が意外と強い（強ベースライン）。

実験設計のミニ青写真
- D_val: 50–200例（多様性重視）。k=8〜16候補、N=5〜15反復。
- 評価: 主要目標（正解率/実行精度）＋副目標（安全/体裁/長さ）を多目的でログ。
- 探索: Top-K→UCB（or UCT）。改善<εをp回連続で早期停止。
- 再現性: 乱数seed・LLMバージョン・候補全文・サンプル分割を全保存。
- コスト制御: 1反復あたり「候補数×評価バッチ×API呼数」を見積り、上限を固定。

ありがちな落とし穴（論文が指摘）
- dev過学習: 固定D_valだけで選抜→本番落ち。→サブサンプル/折返し検証。
- LLM評価の偏り: “LLM-as-a-judge”の先入観/スタイル嗜好。→複数審査員×アグリゲーション。
- “evil twins”/ギブリッシュ分割子: 解釈不能なのに効く文字列（再現性×安全性のリスク）。
- 自己反省の誤誘導: 誤ったエラー特定→悪化。→負例の質と誘導プロンプトを吟味。
- ログ確率要求（NLL/エントロピー）は黒箱APIでは不可な場合あり。
- コスト爆発: 候補増殖×評価多段。→早期停止・候補去勢・圧縮FB。

研究の余白（次の一手）
- タスク非依存APO（実運用ではタスク境界が曖昧）
- システム/エージェント全体の同時最適（SPRIGは入口、まだ重い）
- マルチモーダルAPO（テキスト＋画像/音声の同時最適化）
- 理論限界（AlignProは上界を示すが、下界・一般条件は未整理）

すぐ試せる最小ループ（疑似コード）
_

```
P ← SeedPrompts(hand | APE)
for t in 1..N:
  C ← RewriteCandidates(P, LLM_feedback or GA or OPRO)
  score(C) ← Eval(accuracy or reward or LLM-judge) on sampled D_val
  P ← SelectTopK_or_UCB(C, score)
  if no_gain ε for p rounds: break
return argmax_P Eval(P on full D_val)
```


現場Tips（短冊）
- まずは“単純だが強い”基準線（手書き+少量few-shot+整形指示）。
- LLM審査は2名以上（モデル違い/温度違い）＋規準文を固定。
- **テキスト最適→最後に語置換（COPLE）**で微増を拾う。
- **用途が広いならMoE（MOP）か分岐（AMPO）**を検討。
- パイプラインならDSPY/MIPROで段別に最適化。
- 安全/スタイルは多目的で一緒に回す（SOS/CRISPO流）。

必要なら、あなたの実データ（例：分類・要約・Q&A）に合わせて**具体的な実験設計（D_val設計・K/N・予算）**と、OPRO/[[ProTeGi]]/DSPYの叩き台プロンプトを作ります。

