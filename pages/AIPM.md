---
title: "AIPM"
---

あいぽん

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>解説を書き直した (2026-11-09)
AIPM (AI Project Manager): AIにプロジェクトマネージャ的な役割をさせようとした試み。2025-01〜04
- コード: [https://github.com/nishio/ai_project_manager](https://github.com/nishio/ai_project_manager) (public)
- タスクデータは別の private repo (ai_project_manager_data) の backlog.json
- 問題意識: [[並列タスク管理のストレス緩和]]
    - AIで回せるプロジェクトが増えて並列になり、混乱しつつあった
- [[AIタスク管理]] (2025-01-27「~/aipm に置くことにした」) がこのプロジェクトの起点

仕組み
- タスクは backlog.json に、T0107 のようなIDつきで持つ
- 追加・更新・完了は小さなPythonスクリプトでやる (add_task.py, update_tasks.py, mark_done.py, show_tasks.py など)
    - LLMに大きなJSONを直接書き換えさせるとうまくいかなかった: [[jsonpatchではダメだった]]
- READMEに「タスク管理者」「開発者」「ユーザ」の役割を書き、READMEを読んだAIがタスク管理者として振る舞う
- [[AIPM WebUI]]: Devinに作らせたローカルのWebUI
    - タスクIDをクリックすると中身が出る、そこからdoneにできる、編集できる
- AIが出したタスクの追加・更新案を、人間がOK・リジェクト・書き換えで確かめる画面 (diffつき): [[AIタスク管理2025-03-03]]
- 使い方
    - 週の振り返りで、バックログと2週間の活動をo1 Proに渡して助言させる: [[週記2025-03-01~2025-03-08]]
    - Advanced Voiceで散歩しながら話す ([[2025振り返り]])

経緯
- 2025-02-27〜03-06 [[AIタスク管理2025-02-27]] → [[AIタスク管理2025-03-03]]: WebUI、テスト、レビュー画面
- 2025-03-11〜03-25 [[AIPM2025-03-11]]: 一般ユーザに提供する方向へ。Firestore・Firebase Auth・Vercel
    - デプロイはできたが「データがない状態だと何もできないぞw」
- 2025-04 デジタル民主主義2030の優先度が上がって放置 ([[日記2025-04-05]])
- 2025-04-21 下の「MCP化する」のメモ。MCP化はしないまま止まった
- 2025-11 [[2025振り返り]] で止めた理由を振り返った
    - > やることが明確である「いわゆるタスク管理」と研究的な何を見つけるべきか不明であり探索することが必要なプロジェクトとは適切な管理手法が異なるよな〜と感じ始めていた
- この問いは [[不定形プロジェクト]] に引き継がれている

MCP化する？→しない
[https://chatgpt.com/c/67f9b38c-a5d8-8011-920a-35c30365dcb2](https://chatgpt.com/c/67f9b38c-a5d8-8011-920a-35c30365dcb2)
