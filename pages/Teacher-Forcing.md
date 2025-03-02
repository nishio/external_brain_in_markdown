---
title: "Teacher-Forcing"
---

![image](https://gyazo.com/ae986c8c66b27fc57b06cf8991917f64/thumb/1000)

直前の自己の出力を入力に使う代わりに、正解データを使う学習方法
後半にかけて誤差が蓄積するせいで学習に時間がかかる問題を解決できるが、実際に使う時には1文字ずつ正解データが供給されたりしないという問題もある
自分の出力と正解をランダムに選んで使う[[Scheduled Sampling]]: [[Samy Bengio+ 2015]]
