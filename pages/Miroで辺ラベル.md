---
title: "Miroで辺ラベル"
---

[[線ラベル]] / [[辺ラベル]]
[https://chatgpt.com/c/68f0b1d1-ce84-8321-b69e-56c48b0ef732](https://chatgpt.com/c/68f0b1d1-ce84-8321-b69e-56c48b0ef732)
- [[Miro]]のREST API v2／Web SDKの「[[コネクタ]]（connector）」は“キャプション（＝[[矢印線上のラベル]]）”をサポートしています。テキスト内容、線上の相対位置（0.0〜1.0）、上下方向の配置、色やフォントサイズなどを指定できます。複数ラベルも可です。
    - [Connector](https://developers.miro.com/docs/connector_intro)
- 付箋や線ラベルに関して、クリックすると詳細が表示される的なことは可能？
    - [[Miro Web SDK]]でクリック（選択）を検知してパネル／モーダルで詳細を表示
        - [Board UI](https://developers.miro.com/docs/websdk-reference-ui)

[[Kozaneba]]でやろうと思ってたけど、まず詳細情報抜きのは[[Miro REST API]]でやるのがよさそう
- 次に詳細情報パネルをつけるのは[[Miro Web SDK]]でやる
- Kozanebaでやると自由度が高すぎてなんでもできるが、まずは　Miroでやってみて不満点がなければMiroの方がいい
