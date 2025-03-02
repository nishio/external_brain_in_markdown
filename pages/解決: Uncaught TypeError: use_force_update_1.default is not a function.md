---
title: "解決: Uncaught TypeError: use_force_update_1.default is not a function"
---


2023-01-13 Kozanebaが、エラーなくビルドが通ってデプロイされた関わらず、ブラウザ上では下記の実行時エラーを出すようになった
- `Uncaught TypeError: use_force_update_1.default is not a function`

原因
- [[Kozanebaの開発環境を作る]]で半年ぶりに環境を作り直した
- 最新の[[react-scripts]]と[[ReactN]]が内部で使う[[use-force-update]]が衝突する
- 後者がesmとcjsの両方を提供していて、前者がその状況を正しく理解できないバグだ、と後者の著者は主張している
    - > Downgrade react-scripts to ^4 until they resolve it in ^5.
    - > Downgrade use-force-update to 1.0.8.
    - [Dependency Use force update 1.0.10 causes a Type Error · Issue #227 · CharlesStover/reactn · GitHub](https://github.com/CharlesStover/reactn/issues/227)

解決(for [[Yarn]]1)
- use-force-updateをダウングレードした
package.json

```json
{
  "resolutions": {
    "use-force-update": "1.0.8"
  }
}
```

- 他の解決策もGithubに書いてある

[[ReactN]] [[use-force-update]]