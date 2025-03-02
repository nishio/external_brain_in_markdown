---
title: "外部脳GitHub作業"
---

2024-09-08
- リポジトリは作った [https://github.com/nishio/nishio-hirokazu-external-brain](https://github.com/nishio/nishio-hirokazu-external-brain)
- 次に何をするべきか考える
    - あと3分で会議なので考えるだけ
    - 翻訳システムでJSONのExportなどは自動化されている
    - それを持ってきてバックアップのシステムをまず作る
    - たぶんこれ: [https://github.com/nishio/etude-github-actions](https://github.com/nishio/etude-github-actions)
        - ![image](https://gyazo.com/021a459efdd87f7d62cca42243fdfe81/thumb/1000)
        - DeepLの課金は更新されてたが何が問題で止まってるのか
        - > This repository is over its data quota. Account responsible for LFS bandwidth should purchase more data packs to restore access.
        - あー、GitHub LFSか
    - 8/21のメール
        - > Git LFS has been disabled on your personal account nishio because you’ve exceeded your data plan by at least 150%. Please purchase additional data packs to cover your bandwidth and storage usage:
        - >    [https://github.com/account/billing/data/upgrade](https://github.com/account/billing/data/upgrade)
        - >  Current usage as of 20 Aug 2024 10:38PM UTC:
        - >    Bandwidth: 8.21 GB / 100 GB (8%)
        - >    Storage: 150.09 GB / 100 GB (150%)
        - ![image](https://gyazo.com/bff8d96967ddbe9f4ceb93d0c13e32f9/thumb/1000)
        - ![image](https://gyazo.com/733459f7f7c6c9090b12fb0aa8afa11c/thumb/1000)
        - 3 data packにしても溢れてんじゃん
        - 4にした
        - ![image](https://gyazo.com/90ed4b11eca06a9f53660a9117137cb4/thumb/1000)
        - ![image](https://gyazo.com/12bc68d243003c8244f7e33a778ea6b2/thumb/1000)
        - うーん、まあ一旦これで。
            - 150GBのJSONがある？
    - etude-github-actionsは名前の通りGitHub Actionsの練習のために作った物で、予想以上にうまくいってしまったので長らく実運用されてきた
        - そろそろ見直し
        - という検討を以前にもして忘れてる気がするな
        - [[etude-github-actions]]
        - [[pVectorSearch]]

多分だけど、いろんな機能を一つのGitHub Actionsに詰め込みすぎてると思うんだ
- 1: 最新のJSONへCosenseからのExport APIを叩かずにアクセスできる手段を作る
- 2a: (1)から、翻訳、英語Scrapboxへのimport
- 2b: (1)から、ベクトルDBにinsert
いま(1+2a)と(1+2b)が並行で走ってる
- (1)だけで完結させた方が他のいろいろなものと連携しやすい
    - 他のCosenseユーザにも「自分のCosenseのデータがアクセスしやすい形でGitHubにあってほしい」って人いるじゃろ

(1)にあんまり色々コードを書くべきでないと思うんだ

翻訳に関して
- いまDeepLで行単位で翻訳している
- GPTのコンテキスト長が長くなった2024-09-08現在としてはJSONリストで渡してJSONリストで返させるのでいいと思う

