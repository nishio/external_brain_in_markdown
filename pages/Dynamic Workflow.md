---
title: "Dynamic Workflow"
---

[[Claude Code]] の機能。2026-05-28 発表、のちに一般提供
- Claude 自身が、複数のサブエージェントを動かすスクリプト（JavaScript）を書いて、実行する
- >  Claude dynamically writes orchestration scripts that run tens to hundreds of parallel subagents in a single session
- [Introducing dynamic workflows | Claude by Anthropic](https://claude.com/ja/resources/articles/introducing-dynamic-workflows-in-claude-code)
- [A harness for every task: dynamic workflows in Claude Code](https://claude.com/blog/a-harness-for-every-task-dynamic-workflows-in-claude-code) (2026-06-02)

何が新しいか
- それまでのサブエージェントは、会話の中で Claude が1つずつ呼んでいた。Dynamic Workflow では、仕事の分け方・並べ方・検証の仕方をスクリプトとして先に書き、会話の外で走らせる
- 決まった形のワークフローはどうしても汎用的になる。用途に合わせたハーネスを、その場で Claude が書く（[[探索を加速する抽象度の設計勉強会]]）
- スクリプトの部品は、サブエージェントを1つ起こす agent()、まとめて並列に走らせる parallel()、項目ごとに段を流す pipeline() など

典型的な形
- 手分けして調べる・直す → 別のエージェントが反証を試みる → 残ったものだけを統合する
- 途中経過は保存され、中断しても続きから再開できる
- 公式の使用例：コードベース全体のバグ調査やセキュリティ監査、数百〜数千ファイルの移行、重要な作業の二重チェック

起動の仕方と注意点
- 「ワークフローを作って」と頼む。または ultracode 設定を有効にして、使うかどうかを Claude に判断させる
- 初めて起動するときは、実行内容を示して確認を求める
- トークン消費は通常のセッションよりかなり大きい。公式も、まず範囲を絞ったタスクで試すよう勧めている
- 公式発表は auto mode との併用を推奨している。サブエージェントの操作ごとに人間の承認を求めていたら、並列にした意味がなくなる → [[人間のAIに対する判断移譲]]

使用例
- [[Logosプロジェクト]]の序盤にスピーディに脆弱性スキャンを実行できたのはDynami Workflowで「領域を分けて並列に読む」「出てきた候補を批判的に読む」「結果を集約して報告する」という脆弱性スキャナをオンデマンドで作ったから
- 2026-11-03、14 個の LLM Wiki を、Wiki ごとに「現状と照合して直す → 別のエージェントが反証する → 指摘を手直しする」の3段で並列に回した
- 並列にすると、待ちになるのは人間の判断のほう → [[多面指し：人間の判断がボトルネックになる]]
- [[Codexのリセット権]] でも、並列で作業する案として挙げている