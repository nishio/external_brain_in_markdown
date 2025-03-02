---
title: "o1 Proを世界に接続する"
---

[[o1 Pro]]を世界に接続するアダプターをo1 Proに書かせてたんだけど、途中で画像を貼ったらログを共有できなくなってしまった
自分用リンク: [https://chatgpt.com/c/6752f412-c08c-8011-b98e-33728de871a4](https://chatgpt.com/c/6752f412-c08c-8011-b98e-33728de871a4)

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>以下は、これまでの流れを第三者に説明するための簡潔な要約です。
要約:
- MVP構築:
    - tool_actions.jsというNode.jsスクリプトを作り、JSON形式の指示(ファイル編集、コミット、テスト実行など)を受けてプロジェクトを自動操作できる基盤を用意。
- ブラウザ内AI活用構想:
    - Playwright等でブラウザ自動化し、AIサービスにログイン・指示投入・結果取得を目指したが、Cloudflareの人間判定や要素操作が困難で別アプローチを検討。
- Tampermonkeyスクリプトへの転換:
    - 通常利用するChromeにTampermonkeyを導入し、ユーザースクリプトでAIサービスページ上にカスタムボタン(自動化ON/OFF)を追加。
    - ページ要素が動的に読み込まれる環境で、waitForElement関数やMutationObserverなどを駆使して、AI生成完了のタイミング(ストリーミング停止や特定ボタン表示)を検知。
- クリップボード操作・可視化:
    - 生成完了後にコピー用ボタンを自動クリックし、navigator.clipboard.readText()でクリップボード内容を取得して表示することで、実際の処理フローを確認可能にした。

以上のプロセスを通じて、ブラウザ上のAIサービスへの自動コマンド入力・結果取得・処理反映という作業サイクルのMVPを構築・検証する流れを試みている。

