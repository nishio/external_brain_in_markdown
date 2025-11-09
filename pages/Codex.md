---
title: "Codex"
---


<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
Codex（2025年版）概要
- 何か：OpenAIのソフトウェアエンジニアリング用エージェント群。ローカル（CLI/IDE）とクラウドの両方で動き、ChatGPTの有料プラン（Plus/Pro/Team/Edu/Enterprise）に含まれます。CLI は `npm i -g @openai/codex` で導入可。推奨モデルは GPT-5。 ([OpenAI](https://openai.com/codex/?utm_source=chatgpt.com)) ([OpenAI](https://openai.com/index/introducing-gpt-5-for-developers/?utm_source=chatgpt.com))
- できること（代表例）：機能追加、バグ修正、コードベースQ&A、テスト実行、PRの提案。各タスクはリポジトリを読み込んだクラウドのサンドボックスで並列実行できます。 ([OpenAI](https://openai.com/index/introducing-codex/?utm_source=chatgpt.com))
- 動作場所と統合：ターミナル/IDE/ウェブ/ GitHub / iOS から同一アカウントで連携。VS Code系IDE拡張、ChatGPTサインイン（APIキー不要）、ローカル↔クラウドの状態引き継ぎ、PR自動レビューや @codex メンションに対応。 ([OpenAI Help Center](https://help.openai.com/en/articles/6825453-chatgpt-release-notes?utm_source=chatgpt.com))
- モデル面：Codexはエージェント製品名で、内部のコード生成・推論は最新モデルが担います。GPT-5 は実務のコーディングで o3 を上回ると公表（SWE-bench等の実務寄り評価/事例）。 ([OpenAI](https://openai.com/index/introducing-gpt-5-for-developers/?utm_source=chatgpt.com))
- データ/プライバシ：ChatGPT Team/Enterprise/APIなどビジネス用途の入力・出力は既定で学習に使われません（組織側でオプトイン可能）。 ([OpenAI Help Center](https://help.openai.com/en/articles/10306912-sharing-feedback-evaluation-and-fine-tuning-data-and-api-inputs-and-outputs-with-openai?utm_source=chatgpt.com))

歴史と位置づけ
- 2021年：自然言語→コードの「OpenAI Codex」を発表（GPT-3をコードで追加学習した系列）。のちにAPIは終了し、現在のCodexは2025年に“エージェント”として再設計された製品ライン。 ([OpenAI](https://openai.com/news/product/?limit=18&sortBy=old&utm_source=chatgpt.com))

はじめ方（最短）
1. `npm i -g @openai/codex`
2. CLI/IDE拡張で ChatGPTにサインイン
3. リポジトリを接続してタスク（例：`codex fix tests`, `codex propose pr`）を投げる
（詳細ガイドは公式の Codex 開発者サイトとリリースノート参照） ([OpenAI](https://openai.com/codex/?utm_source=chatgpt.com), [OpenAI Help Center](https://help.openai.com/en/articles/6825453-chatgpt-release-notes?utm_source=chatgpt.com))

---
> [ringo](https://x.com/ringo/status/1961071380243574796) codex使い始めた時は、diffが見えないことが不便だと思ったけど
>  何日か使ったら要らないことがわかった。
>  コマンド実行結果がtruncateされるのも不便に思ったが、それも要らないことがわかりつつある
> [ringo](https://x.com/ringo/status/1961072095598633163) 細かいことはエージェントに任せて、僕はどう動いたのか見るのと、どういう動きが正しいのかを考えることに集中すべきなのだ。
>  codexはそのように設計されている。
>  コードは[[細かいこと]]になったのだと思う。
>  バイトコードやアセンブリのような扱いが近いか。

[[どのようなものを作りたいのか]]をイメージする力が引き続き必要
- 関連: [[作りたいものがない]]
