---
title: "Software 2.0"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
ざっくり言うと：
Software 2.0 =「手続きは書けないけど、正しさはチェックできるタスクの自動化」
という話です。

1. Software 1.0 ↔ 2.0 の対比
[[Karpathy]] の元々の枠組みは：
- Software 1.0
    - 人間が if / for などの手続き（アルゴリズム）を全部コードで書く世界
    - 「ルールを説明できるなら自動化できる」世界観
- Software 2.0
    - ニューラルネットなどの学習済みモデルそのものがプログラム
    - 人間は「目的関数（評価指標）」と「データ」「ネットワーク構造」だけ決めて、あとは学習（勾配降下やRL）が良いプログラムを自動探索する世界観 ([ウィキペディア](https://es.wikipedia.org/wiki/Software_2.0?utm_source=chatgpt.com))

ここに最近 Karpathy が
- Software 1.0 automated what we could explain.
- Software 2.0 automates what we can verify. ([Medium](https://medium.com/illumination/software-2-0-and-the-strange-shape-of-ai-progress-072e00c7dd94))
とまとめ直している。

2. 「verifiable なものの自動化」とは何か
ここでの verifiable は、だいたい次の条件を満たすタスク：
1. 結果が機械的に採点できる
    - 正解・不正解、スコア、損失関数などで数値評価できる
2. 環境をリセットして何度も試せる
    - シミュレータ・テスト環境などでトライ＆エラーが高速に回せる
3. 評価を自動で与えられる（reward / loss が自動で出る） ([Blockchain News](https://blockchain.news/flashnews/ai-software-2-0-and-verifiability-trading-implications-for-crypto-markets-btc-eth-from-karpathy-in-2025))

こういうタスクは、勾配降下や強化学習にとってエサ（フィードバック）がはっきりしているので、Software 2.0（AI）が勝手に上達しやすい＝自動化されやすい、という主張です。

3. 具体例（強い領域）
Verifiable で、Software 2.0 が得意なもの
- コーディング
    - テストを流せば通るかどうかが自動でわかる
- 数学の問題（定理証明系・計算問題）
    - 答えの正誤チェックが機械的
- 音声認識、画像認識、構造化データ抽出
    - ラベル付きデータと照合すればスコアが出る
- ゲーム（囲碁、チェス、Atari など）
    - 勝ち負け・スコアが明確で、環境もリセットし放題
こういう領域は、LLM や RL にとって
「大量に試しては採点 → パラメータを更新」を高速に回せるので、トップ人間を超えるところまで一気に行きやすい、という見立てです。([Medium](https://medium.com/illumination/software-2-0-and-the-strange-shape-of-ai-progress-072e00c7dd94))

4. 逆に、あまり verifiable でない領域
- 創作（小説・エッセイの「おもしろさ」「文学的価値」）
- 長期戦略・政策立案
- 社会的コンテクストを踏まえた判断（政治・人事・対人交渉）
- 「このデザインはイケてるか？」のような美的評価
これらは
- 正解が一つに定まらない
- 採点基準が人間の主観依存
- フィードバックが遅い or ノイズが大きい
ので、自動的にスコア計算して学習、がやりにくい。
Karpathy の言い方だと、verifiability が低いので Software 2.0 による完全自動化は進みにくい領域になります。([Medium](https://medium.com/illumination/software-2-0-and-the-strange-shape-of-ai-progress-072e00c7dd94))

5. まとめ：Karpathy が言いたいこと
- かつては
→「アルゴリズムとして書けるか？」が自動化の境界（Software 1.0）
- これからは
→「結果を自動で検証できるか？」が自動化の境界（Software 2.0）

つまり Software 2.0 = verifiable なもの（結果の良し悪しを機械的に判定できるタスク）の自動化
という読み替えで、「どんな仕事・分野が AI に飲み込まれるか」を考えるための指針だ、というイメージです。


[Software 2.0 - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/Software_2.0?utm_source=chatgpt.com)
