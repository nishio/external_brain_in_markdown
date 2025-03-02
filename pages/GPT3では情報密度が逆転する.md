---
title: "GPT3では情報密度が逆転する"
---

2023-02-28
![image](https://gyazo.com/14e4f77793d723af030402d9042df1bf/thumb/1000)
![image](https://gyazo.com/10c1b8c1b9b9b1817d78f1133a748f82/thumb/1000)![image](https://gyazo.com/9f52e93ff88b586b14311c82d230a8b8/thumb/1000)
![image](https://gyazo.com/f0a0af30d47e17bf5cebf9d79774f2b6/thumb/1000)![image](https://gyazo.com/b5be2d6f88a06f83777451a77264327b/thumb/1000)
[OpenAI API: Tokenizer](https://platform.openai.com/tokenizer)

[[GPT3]]の[[トークナイザー]]はしばしば漢字一文字を複数のトークンに刻む。
- これは日本人にとっては好ましくない状況

今まで漢字を使う中国人や日本人はアルファベットを使う人たちに比べてインプットする情報の密度が高かった
- 同じ内容を日本語で書くのと英語で書くのでは英語の方が約2倍面積を取っていた
- 人間の物理的視野の広さは人種によって大差ない
- なので、日本人は欧米人に比べて一度に目からインプットできる情報量が2倍大きいというアドバンテージがあった

しかし、GPT3の視点で見ると、同じ内容を日本語と英語で与えた場合には日本語の方が英語よりおよそ2〜3倍の数のトークンになる
- GPT3が一度にインプットできるトークンは4000程度
    - これが人間の物理的視野のようなもの
- つまりGPT3にとって、日本語で書かれたものは一度に見れる量が少ない
- ChatGPTに「これを参考にして返事して」と文脈情報を渡すことが広く行われているが、この場合に英語で渡す方が2〜3倍の文脈を渡せる、この差はでかい

トークン従量課金

[[Semantic Search]]の精度が日本語ではいまいちだという話がある
- 漢字が分割されてるから文字コード表で近くにある漢字は「トークンの1/2や2/3が共通のもの」とみなされてる
- そりゃあうまく動かすためのハードルが高いな

Q: トークナイザがナイーブに各バイトをトークンにしている？
- A: そういうシンプルな話ではない
- 「information」で1トークンになってるところが見所
    - ![image](https://gyazo.com/b5be2d6f88a06f83777451a77264327b/thumb/1000)
    - 元が何バイトであっても1トークンにすることには支障ない
    - よく見るとわかるんだけど漢字4文字でなぜ9トークンかというと「報」以外が2トークン、「報」が3トークンになってる
- ではなぜ「情」を構成する3バイトが2トークンに刻まれているのか
    - 入力を素朴にバイトに刻めばトークンは70種類弱ですむ
    - しかし細かく刻むと上記の「視野が狭くなる」現象が起きるので、頻出するバイト列はくっつけて複数バイトで1トークンにする
    - この「頻出のものを」というところが想定しているコーパスによって変わる
    - GPT3は日本語に特化していないので「情」の出現頻度は「information」の出現頻度よりはるかに低い
    - なので1つのトークンにする価値はないと判断されている状態
- 現状のGPT3のトークンは全部で50000種類程度
    - 増やすことは技術的には問題ないが、増やした分だけ学習コストが掛かる
    - 経済的理由により日本語とかいうマイノリティ言語に割くリソースが少ないという話

追記
> [@kitar](https://twitter.com/kitar/status/1633426489390809088): もしかしてChatGPTのトークナイザーはGPT3より改善されてるのですかね…？今tiktokenで計算してみていたのですが、
> text: 情報密度
> text-davinci-003: 9 tokens
> gpt-3.5-turbo: 4 tokens
> と出てきました。

python

```
In [10]: tiktoken.encoding_for_model("gpt-3.5-turbo")
Out[10]: <Encoding 'cl100k_base'>

In [11]: tiktoken.encoding_for_model("text-davinci-003")
Out[11]: <Encoding 'p50k_base'>
```

なるほど、確かに変わってる
いやこれChatGPT APIで新しくなったのではないな
- 2022年12月の [New and improved embedding model](https://openai.com/blog/new-and-improved-embedding-model) でも新しいトークナイザーが使われてる
- ![image](https://gyazo.com/ff6822187c0b6d035c4d7595edc1adf2/thumb/1000)
    - [https://platform.openai.com/docs/guides/embeddings/what-are-embeddings](https://platform.openai.com/docs/guides/embeddings/what-are-embeddings)
- [[cl100k_base]]なら
python

```
In [12]: tiktoken.get_encoding("cl100k_base").encode("情報密度")
Out[12]: [40474, 78943, 28741, 27479]
```

    - 4 tokensになった
- [https://platform.openai.com/tokenizer](https://platform.openai.com/tokenizer) のデモではV1のGPT-3が使われてるということ
