---
title: "Chrome拡張からLLMへタブ情報を連携"
---

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
Chrome拡張から開いているタブの情報をファイルシステムに書き出し、LLMに渡すまでの大まかな流れは以下です。

1. ### 権限設定
    - `tabs` パーミッションを使用し、開いているタブ情報を取得。
        - Manifest V3の場合は `permissions` に `"tabs"` を加える。

2. ### タブ情報の取得
    - `chrome.tabs.query({})` などでURLやタイトルなどを取得。

3. ### ファイル書き込み
    - Chrome拡張は直接ローカルファイルへの書き込みが難しいため、以下いずれかの方法を取る。
        - バックエンド経由: XMLHttpRequest/fetchでサーバへPOSTし、サーバ側でファイルに書き込む。
            - File System Access API: ユーザ操作を伴うが、ブラウザ上からファイルにアクセスできる（対応状況には注意）。
        - storage API: `chrome.storage.local` などに一時的に保存し、別の仕組みで取り出してファイル化。

4. ### LLMへの入力
    - ファイルへ保存したタブ情報（URLやタイトル、テキストなど）をLLMの入力として読み込む。
        - ローカルでLLMを動かすなら、ファイルを直接処理。Web API経由ならテキストデータをリクエストとして送る。

ポイントとしては、Chrome拡張ではセキュリティ上、直接ローカルファイルに書き込むのが制限されているため、たいていはサーバやstorage APIを使う形になります。こうして取得したタブ情報をまとめて出力し、LLMに入力することで状況を把握しやすくできます。