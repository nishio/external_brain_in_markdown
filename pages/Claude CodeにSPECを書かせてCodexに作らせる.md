---
title: "Claude CodeにSPECを書かせてCodexに作らせる"
---

2026-06-23
([[KarpathyのLLM Wiki]]に関して)「ただのMarkdownの束」より先に行く必要性が増えてきたので
Codexにゴリっと新しいWiki基盤を作らせようとしている
基本はCosenseだが、ローカルで動き、いくつかの設計上の問題を直したデータモデルになっているもの


Claude CodeにSPECを書かせてCodexに作らせる
MVPとして「ちょっとバグがあるが大体機能する、ただし速度(非機能要件)がダメ」というものができた


まあ機能確認のために速度度外視でJSONを毎回読むのは悪くない判断
次はJSONをSQLiteに置き換える


リリースした
nishio/[[grasp]]
[https://github.com/nishio/grasp](https://github.com/nishio/grasp)

これをLLM Wikiの下のレイヤーに入れられるか今後試していく