---
title: "Microsoft Guidance"
---


[[トークンヒーリング]]
[https://note.com/nyosubro/n/n929da0047dc9](https://note.com/nyosubro/n/n929da0047dc9)
プロンプトの最終トークンは、トークン分割の境界を表明する効果があるため、生成される文字列の分布に多くの人が期待していないバイアスをもたらす
そこでプロンプトの最終トークンをプロンプトかは取り除いて生成し、最終トークンを制約とした棄却サンプリングにする

関連
- [[LangChain]]
