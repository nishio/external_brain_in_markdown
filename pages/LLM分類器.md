---
title: "LLM分類器"
---

[[Jev]]が出てきてSNSが大盛り上がりになった
- 「これはすごい！」という派閥と「こんなの昔からあったじゃん」という派閥がいて争っていた
- しばらく経って検証がいろいろ出てきている

![image](https://scrapbox.io/files/6aed28349bec2c4c54ce492f.png)
- [Frontier quality at 1% of the cost: a production benchmark of LLM classifiers | Airbnb Engineering & Data Science](https://airbnb.tech/ai-ml/frontier-quality-at-1-of-the-cost-a-production-benchmark-of-llm-classifiers/)
- 精度としてはGPT-6.1 Solを使ったら高いんだが、200ms以内に収めたいと言う要件があり、Jevはその領域
- Gemma4-31Bのほうが精度が高い、NVIDIA RTX Pro 6000 を 1 枚挿したマシンで200msの条件を満たせる
- Gemma4-E2B を数十万件の例で fine-tune した分類器が F1 0.902、中央値 36ms
    - フロンティア API と同じくらいの質で、費用は約 1/100
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> この fine-tune はどれくらいのコストかかりそう？
    - <img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/> GPU の費用は数十ドル、試行錯誤を含めても数百ドルくらいです。お金がかかるのは数十万件のラベル付きデータのほうです。
        - 1 件 300 トークン × 30 万件 × 3 周 ≈ 2.7 億トークンを、実効 2B のモデルで学習するとします。RTX Pro 6000 を 1 枚、実効 100 TFLOPS 程度で回すと約 9 時間です。貸出価格を 1 時間 1〜2 ドル（記憶からの仮定で、確認していません）とすると 10〜50 ドルです。

