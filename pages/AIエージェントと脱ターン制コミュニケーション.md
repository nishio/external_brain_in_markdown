---
title: "AIエージェントと脱ターン制コミュニケーション"
---

from [[日記2025-02-10]]
[[AIエージェント]]と脱ターン制コミュニケーション
> [teramotodaiki](https://x.com/teramotodaiki/status/1888620661092089920) エージェント検索ってこんな感じかなーってエアプで作ってみた所感
>  ・全部o3-miniでいい。他のモデルは必要ない
>  ・信頼できるナレッジの構築こそが全て。他は些事
>  ・サーバーレス(ステートレス？)なアーキテクチャを前提にするとターン制コミュニケーションしか出来なくてショボい
>  ・Devinはすごい

> [teramotodaiki](https://x.com/teramotodaiki/status/1888621918045315238) ChatGPTが[[ターン制コミュニケーション]]だから「そういうもんだ」と99%の開発者は思っているのではなかろうか。
>  Devinはセッションの設計がマジで上手い。Slackスレッドに「いる」んだよな。あの体験を作るにはアーキテクチャから考え直さないといけない。

> [teramotodaiki](https://x.com/teramotodaiki/status/1888623326010163675) 広い意味ではこれもメモリーの設計なのかも知れない。どこまで記憶を引き継ぐのか。ある種の自己同一性のようなものの設計。ユーザーの期待する同一性とソフトウェアの設計を一致させるためのUI…
>  ソフトウェア開発でここまで人間の認知に深く迫れるのが楽しくてしょうがない

ここ、とても悩ましいんだけど実際ターン制コミュニケーションではない形になると思うんだよね、kintone上で人間が会話するのも交互に話してるのではないわけで。

ここでいう「ターン制コミュニケーション」とは「Aさんが話し、Bさんが話し、Aさんが話し、...」というもののこと
AIは人間のインプットに反応すればいいだけなのでアーキテクチャは楽なんだけど、それでは[[Devin的]]にはならない。
AさんはN件話せるし、BさんもM件話せるし、Aさんが話したからといってBさんのターンになったりはしない、という感じ
kintoneなどでの人間同士の会話がまさにそれで、このやりとりのしかたはChatGPTとは違うよね、ということ

[[Proactive Agent: Shifting LLM Agents from Reactive Responses to Active Assistance]]
[[Proactive Agent]]
