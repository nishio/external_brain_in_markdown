---
title: "CypressでWebpack Compilation Error"
---

原因: インポートしたコードがtsxだった

現象
- 最初に認識したのは「あれ？補完候補に出てこないぞ？exportはされてるのにな？」だった
- 明示的にインポートしたら下記のエラーが出るようになった
:

```
./src/Canvas/Gyazo.tsx 74:12
Module parse failed: Unexpected token (74:12)
File was processed with these loaders: ...
```

- これは明示的にインポートしたtsのファイルが別のtsxのファイルをインポートしており、Cypressではtsxを読むためのローダの設定をしていなかったことによる
- ローダの設定をすべきか？
    - 今回のケースではそもそも「一つのtsxファイルの中にDOMを作る必要のないユーティリティ関数の定義まで置かれていること」が良くなかったのでそこを直した
