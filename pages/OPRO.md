---
title: "OPRO"
---

[[Large Language Models as Optimizers]]
[https://arxiv.org/abs/2309.03409](https://arxiv.org/abs/2309.03409)

リンクの論文は「Large Language Models as Optimizers（OPRO）」です。要はLLMそのものを“最適化器”として使う手法の紹介です。([arXiv](https://arxiv.org/abs/2309.03409?utm_source=chatgpt.com))

要点
- 発想：最適化したいタスクを自然言語で説明し、過去の「解→スコア」の履歴（解の候補とその評価値）をまとめたメタプロンプトをLLMに投げる。LLMはそれを見て次の候補解をいくつも提案→外部で評価→履歴に追記…を繰り返す。勾配不要のブラックボックス最適化として動く。([ar5iv](https://ar5iv.org/pdf/2309.03409))
- 適用例：
    1. 小規模の線形回帰・巡回セールスマン問題（TSP）の玩具例で、履歴だけから改善方向を学習して良解に近づく挙動を確認。
    2. 本命はプロンプト最適化。例えばGSM8K/BBHで、OPROが自動生成した“指示文”が、人手の有名プロンプトより良い精度を出すことがある。([ar5iv](https://ar5iv.org/pdf/2309.03409))
- 代表的な成果：GSM8Kでは、人手の「Let’s think step by step.（71.8%）」より、OPROが見つけた「Take a deep breath and work on this problem step-by-step.（80.2%）」などが高精度。BBHでも大幅改善の例を示す（論文中“最大でGSM8K+8pt、BBHで+50pt”の記述）。([ar5iv](https://ar5iv.org/pdf/2309.03409))

仕組み（設計のキモ）
- [[メタプロンプト]]に入れるもの：
    - (a) タスク説明（目的関数・制約、プロンプト最適化なら少数の入出力例）
    - (b) これまでの解とスコアの一覧（スコア順）
        - → LLMは履歴のパターンを見て“良解”の特徴を抽出し、新候補を生成。([ar5iv](https://ar5iv.org/pdf/2309.03409))
- 探索と活用の両立：各ステップで複数案を生成して分散探索し、温度で探索（高温）/活用（低温）を調整。安定化のための実装指針も記述。([ar5iv](https://ar5iv.org/pdf/2309.03409))
- スコアラーと最適化器の分離：しばしばスコア評価用LLM（例：PaLM2-L, text-bison）と、最適化するLLM（例：PaLM2-IT, GPT-3.5/4）を分けて使う。([ar5iv](https://ar5iv.org/pdf/2309.03409))

最小の再現手順（公式実装あり）
- 公式実装：`google-deepmind/opro`（GSM8K/BBH、線形回帰、TSPのスクリプトあり）。例：`optimize_instructions.py` で optimizer（生成側） と scorer（採点側） を指定して回す。([GitHub](https://github.com/google-deepmind/opro))

実務での使いどころ・注意
- 使いどころ：評価関数が用意できるが勾配が取れない問題（UI文言最適化、プロンプト設計、ヒューリスティク探索）に相性良。
- 注意：
    - 評価器への過適合（評価LLMにだけ効く“ハック”語彙）に注意→別モデル/別分割で検証。
    - コスト管理（各ステップ複数案生成でAPI費用が増える）と早期打ち切り基準。
    - 履歴が長くなるとコンテキスト制約にかかるので、上位kのみ保持などの工夫が必要。([ar5iv](https://ar5iv.org/pdf/2309.03409))

まとめ
OPRO＝「履歴付きの生成→評価→追記」のループで、LLMを勾配不要の最適化器として使う枠組み。 プロンプト最適化で実用的なゲインが確認され、コードも公開されている。([ar5iv](https://ar5iv.org/pdf/2309.03409))
必要なら、GSM8K/BBH以外のあなたのデータセットに合わせたメタプロンプト雛形やコスト最適化の設計もその場で作ります。
