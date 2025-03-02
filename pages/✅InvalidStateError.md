---
title: "✅InvalidStateError"
---

`Failed to execute 'transaction' on 'IDBDatabase': The database connection is closing.`

- > The reason could be ... or if there is a newer version of the db loaded in another tab or window, so the db has to close down to resume an upgrade.
    - [Error InvalidStateError: Failed to execute 'transaction' on 'IDBDatabase': The database connection is closing. · Issue #2710 · firebase/firebase-js-sdk](https://github.com/firebase/firebase-js-sdk/issues/2710)
- これが原因ならスキーマを変えた今、タブを開きっぱなしだった人にだけ発生したことになる
    - 今のところスキーマの変更は予定してない
    - 当面起こらないかも
- これは過去の会話リストという必須でない機能のところなので、再発するかどうかウォッチしつつ、エラーになったとしてもユーザの操作は続行させたい
    - →エラーダイアログを出さずに裏でSentryに報告する
