---
title: "Scrapboxのtoken/page"
---

![image](https://gyazo.com/69fca986e181b322019ad629a109187f/thumb/1000)![image](https://gyazo.com/e742c246b4f6d26315f4d35243c7c821/thumb/1000)
Scrapboxを[[cl100k_base]]でトークナイズするとどれくらいになるのか
- 元データはこのScrapbox 14178ページ
- 8192トークンに収まらないものは1%未満
    - OpenAIの[[Embedding API]]は8192トークンまで取れるので、ほとんどのページは丸ごと埋め込める
- 500トークンより短いものが過半数
    - それより長いものだけ500トークンずつに区切ることにした
:
| total | 14178 |
| -- | -- |
| < 8192 | 14092 |
| < 500 | 9344 |
