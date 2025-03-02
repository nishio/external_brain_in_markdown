---
title: "Paper.jsをupdateすると型エラーが大量に出る"
---

from [[pRegroup2020]]
Paper.jsをupdateすると型エラーが大量に出る
- Point.xがnumberから`number | null`に変わったせい
- めちゃくちゃ使い勝手が悪い
- 本家の型がまともになるのが好ましいが、ならないようなら自前のベクトル型に最初に変換してから使う方が良い
