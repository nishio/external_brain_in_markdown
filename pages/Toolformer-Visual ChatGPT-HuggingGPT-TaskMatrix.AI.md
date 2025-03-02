
> [mi141](https://twitter.com/mi141/status/1643909035664773120/photo/1) GPT/ChatGPTをベースに、複数の外部API（他の基盤モデルなども）をうまく使いこなして様々なタスクを解く手法に興味があったので
>  ・[[Toolformer]]
>  ・[[Visual ChatGPT]]
>  ・[[HuggingGPT]]
>  ・[[TaskMatrix.AI]]（下図はこれ）
>  あたりを読みました。主に知りたかったのは、APIの使い方をどのように学ぶかです
>  ![image](https://pbs.twimg.com/media/FtBUryWakAM3txd?format=jpg&name=medium#.png)

> [mi141](https://twitter.com/mi141/status/1643909038042906624) ToolformerはAPIの使い方をfine-tuningで学習しています。API用の特殊なトークンを用意し、それを含むデータセットをうまく自動的に作成して学習。APIを利用して数値計算や知識が必要なタスクが解けるようになっています。
>  ただ、fine-tuneが必要なので、APIの新規追加や削除のコストが高いです。
>  ![image](https://pbs.twimg.com/media/FtBOwuKaMAAzX_d?format=png&name=900x900#.png)

> [mi141](https://twitter.com/mi141/status/1643909040379162625) [[Visual ChatGPT]]は、APIの種類や使い方などをプロンプトに書いておくというまさにプロンプトエンジニアリング的なアプローチ。当然、追加や削除も容易で、画像生成や編集も含む様々なAPIをうまく使ってユーザの指示に従った処理が可能。
>  ただし今度は、使えるAPIの数がプロンプトの長さで制限されます。
>  ![image](https://pbs.twimg.com/media/FtBP85ZaYAADHku?format=png&name=small#.png) ![image](https://pbs.twimg.com/media/FtBR-eEakAAvKm_?format=jpg&name=small#.png)
- [[ChatGPT Plugins]]も同じような仕組みかな
- 自分が作ったばっかりのプラグインが早速使われるわけなのでプロンプトに積むしかないように思う


> [mi141](https://twitter.com/mi141/status/1643909043449384962) [[HuggingGPT]]も似たアプローチです。ただ、こちらは[[HuggingFace]]にあるモデルを使いこなすというコンセプト上、とてもたくさんのAPIを扱える必要があります。そこで、（図のModel Selectionの部分で）事前に候補となるAPIをフィルタリングしておき、その結果だけをプロンプトに入れているようです。
>  ![image](https://pbs.twimg.com/media/FtBSOGuaIAAzaRJ?format=jpg&name=large#.png) ![image](https://pbs.twimg.com/media/FtBSZRGaAAEiM8c?format=jpg&name=small#.png)

> [mi141](https://twitter.com/mi141/status/1643909046506864640) 最後がTaskMatrix.AIで、こちらはAPIを登録したデータベースから必要に応じて検索を行うことで、適切なAPIを利用しているようです（詳細な記述がない…）
>  プロンプトに書き込む方法ではないので、とてもたくさんのAPIを扱うことが可能です（タイトルにはMillions of APIsとある）
>  ![image](https://pbs.twimg.com/media/FtBTKpiaMAAWGvP?format=jpg&name=medium#.png)

> [mi141](https://twitter.com/mi141/status/1643909049447247872) まあ結果的に3/4はMicrosoftの研究（しかも全部2023/03公開）だったんですけど、変遷が動機と共に辿れて面白かったです。複数の基盤モデルのハブとしてのChatGPTというのは魅力的ですね。
>  [https://arxiv.org/abs/2302.04761](https://arxiv.org/abs/2302.04761)
>  [https://arxiv.org/abs/2303.04671](https://arxiv.org/abs/2303.04671)
>  [https://arxiv.org/abs/2303.17580](https://arxiv.org/abs/2303.17580)
>  [https://arxiv.org/abs/2303.16434](https://arxiv.org/abs/2303.16434)
