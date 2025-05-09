---
title: "COMET: Commonsense Transformers for Automatic Knowledge Graph Construction"
---

![image](https://gyazo.com/fb0e9ead12ab12f78ec1c4b720576632/thumb/1000)
[https://arxiv.org/abs/1906.05317](https://arxiv.org/abs/1906.05317)

<img src='https://scrapbox.io/api/pages/nishio/o3-mini-high/icon' alt='o3-mini-high.icon' height="19.5"/>
- 目的と背景
- COMETは、[[ATOMIC]]や[[ConceptNet]]といった常識知識グラフの「欠落部分」を自動生成する手法です。従来の知識抽出が明示的な記述に依存していたのに対し、暗黙の常識知識を言語生成モデルで明示化する点が特徴です。

- 手法
    - 事前に大規模言語モデル（GPT）の重みで初期化し、既存の知識タプル（主語、関係、目的語）を用いてファインチューニングします。
    - 入力として主語と関係を与え、目的語を生成することで新たな知識タプルを構築します。
    - Transformerアーキテクチャのマルチヘッド・アテンションとフィードフォワード層を利用し、文脈情報を効果的に捉えます。

- 実験結果
    - 人手評価では、ATOMICで77.5%、ConceptNetで91.7%の正確性が確認され、人間に近いパフォーマンスを発揮。
    - また、生成された知識の多くが既存の訓練データには含まれない新規な内容であることが示されました。
    - 事前学習済みモデルの利用により、ランダム初期化と比べ大幅な性能向上が得られています。

- 意義
- 自動生成による常識知識ベースの拡充が、従来の抽出型手法に代わる有力なアプローチとなり、将来的には幅広い知識ベース構築への応用が期待されます。

以上が、COMETの概要と主な貢献点です。