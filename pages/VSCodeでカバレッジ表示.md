---
title: "VSCodeでカバレッジ表示"
---

![image](https://gyazo.com/35e8e3c2157682f333552cd16c84fb2a/thumb/1000)
Install: [Code Coverage Highlighter - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=brainfit.vscode-coverage-highlighter)
`$ python -m pytest <target-test-file> --cov=<source-dir> --cov-report=xml`
Cmd+Shift+P: Code Coverage: Toggle coverage display
![image](https://gyazo.com/5de6b0ef98ef282cd81d67c0b9d601ba/thumb/1000)

pytest-covは[[pytest]]をインストールしたときに一緒に入ってたみたい
- unittestでやってみた人の記事を見かけたけど、カバレッジレポートのフォーマットが同じなのでどっちでも動くのだろう

.coverageではなくcoverage.xmlを見てる
- これを削除するとハイライトが消えるので、更新したらハイライトも更新されるのではないか

`--cov=<source-dir>`で限定しないと外部ライブラリの中身も全部カバレッジを出力しようとして重たい

Gitの差分表示もハイライトしてカオスになった

[[VSCodeでpytestの設定]]
