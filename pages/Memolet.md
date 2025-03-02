---
title: "Memolet"
---

Memolet: Reifying the Reuse of User-AI Conversational Memories
[https://www.youtube.com/watch?v=KH9yn4pg2bY](https://www.youtube.com/watch?v=KH9yn4pg2bY)

[PDF](https://www.jeffjianzhao.com/papers/memolet.pdf) from 本人サイト

### 概要（日本語要約）

「Memolet」は、ユーザとAIの対話履歴（過去のやり取り）を「Memolet」という再利用可能な単位として可視化・操作し、必要な情報を簡単に呼び出して新しい会話やタスクに活かすためのシステムです。

- 背景と課題
- 大規模言語モデルを使ったチャットシステムはやり取りが増えるほど「過去の内容」を把握しきれず、ユーザ自身も長い履歴から再利用したい情報を探し、コピー＆ペーストする作業が大変になりがちです。

- 提案手法（Memolet）
1. Long-Term Memory Repository
    - 過去のすべての対話を意味ベースで埋め込み・可視化し、ユーザが関連する会話（Memolet）を探しやすくする。
2. Memory Sandbox
    - 選んだMemoletを並べてグルーピング・整理（思考の外在化）できる領域を用意。
3. Promptへの直接参照＆生成結果の修正
    - プロンプト内で「@Memolet名」のように参照を指定し、どの過去情報を利用するかAIに明示。また生成結果に対して追加・除外・結合などの操作を直感的に行い、出力を修正する。

- 評価実験
- 1日空けて2フェーズ構成のタスクを行わせ、Memoletを使う条件と通常のチャット（Baseline）を使う条件を比較。
    - Memoletの利用者は、過去対話からの情報抽出・整理・利用が容易になり、タスクの正確性や効率、使いやすさで有意に高評価を得た。
    - 生成結果へのコントロールも強まり、不要な情報を排除したり特定のMemoletを強調して再生成したりする操作がスムーズだった。

### まとめ
「Memolet」は、ユーザが過去の会話メモを思考道具のように扱える仕組みを提案し、検索・整理・参照・再生成という一連のフローをサポートします。これにより、大規模言語モデルとの対話で散在する情報を再活用しやすくなり、無駄なプロンプトエンジニアリングやスクロール・コピペを減らせることが示されています。

private chat [https://chatgpt.com/c/679b3abe-54d8-8011-b234-429991c62396](https://chatgpt.com/c/679b3abe-54d8-8011-b234-429991c62396)
