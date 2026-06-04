---
title: "Stacked diffs"
---

[https://graphite.com/guides/stacked-diffs](https://graphite.com/guides/stacked-diffs)

[3000 ドルかけて Devin と React 18 移行して得た学び](https://zenn.dev/teramotodaiki/articles/react18-migration-with-devin)
- の中で出てきた
- [[寺本 大輝]] / [[Devin]]

無自覚にこの形になった上で「通常のPR形式に変換しなきゃ」と思ってやらせてしまった
- 結局通常のPR形式にしたPR1, PR2, ...はPR1をmergeした段階でPR2がoutdatedになって二度手間だった
- 分割したPRをバンバン送ったらCodeRabbitがover capacityになってレビューされなくなってしまったから良くなかった
