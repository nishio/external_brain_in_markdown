---
title: "改造LacailleのキーマップをJSONにした"
---

前回の改造でObjectiveC力が足りなくて3バイト固定になっていたキーマップを、JSONから読むことで可変長にした。ただしObjectiveC力が足りなくて最大256バイトではある
- [[NSJSONSerialization]]
- [https://github.com/nishio/Lacaille/commit/168bd9e2cadbbdd48449cfb2f05d83bfe258266e](https://github.com/nishio/Lacaille/commit/168bd9e2cadbbdd48449cfb2f05d83bfe258266e)
