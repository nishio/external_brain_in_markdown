---
title: "pSensemaker2025-10-17"
---

from [[Jigsaw Sensemakerとtttc-light-js勉強会]]
pSensemaker2025-10-17

[https://chatgpt.com/c/68eded96-ebd8-8324-a7b4-9a9f05c06b03](https://chatgpt.com/c/68eded96-ebd8-8324-a7b4-9a9f05c06b03)


[https://github.com/Jigsaw-Code/sensemaking-tools](https://github.com/Jigsaw-Code/sensemaking-tools)

最近のPol.isはレポート欄からexportができる
![image](https://gyazo.com/ef36139770250b155f89d0d18120afc1/thumb/1000)
![image](https://gyazo.com/c739caa1068845f8e2582e7cdc8d592d/thumb/1000)

npx ts-node library/runner-cli/runner.ts out/4ewtfar8u5-sensemaker.csv
cd library && pnpm add commander && pnpm add -D @types/node
pnpm add p-limit
pnpm add -D @types/p-limit

> Summary of what was fixed:
>    1. Installed missing dependencies: commander, @types/node, p-limit@3
>    2. The correct commands from the library directory are:
>      - Help: npx ts-node runner-cli/runner.ts --help
>      - Run: npx ts-node runner-cli/runner.ts -i <input-csv> -v <vertex-project>

src/models/vertex_model.ts
modelName: string = "gemini-2.5-pro-preview-06-05"

gemini-2.5-proを使おう

[https://gist.github.com/nishio/6a35dd90b96a2f70868074181c9ab973](https://gist.github.com/nishio/6a35dd90b96a2f70868074181c9ab973)
- 94 statementsから26分掛けて5つのトピックが抽出された
- 18円


20000件のデータを入れたらどうなっちゃうのかな...
- 単純計算だと100時間かかる
    - 並列実行になってくれそうな気配もある
- 費用も不安だね

----

YouTubeのいいねを賛成票として見る
表のデータなしとするバージョンも作る
比較

注意点：
- YouTubeには「いいね」しかないため、本来の投票データ（賛成/反対/保留）とは性質が異なります
- like_countを使う方法だと「人気度」の分析になりますが、「賛否の分かれ方」は分析できません
- トピック分類とテーマ抽出には影響しませんが、"Common Ground"や"Differences of Opinion"の分析は意味が薄くなります

実際のコメント数: 1105件

[https://gist.github.com/nishio/c8c02465a8da3f675e88c6010c529650](https://gist.github.com/nishio/c8c02465a8da3f675e88c6010c529650)

1時間ちょい
費用の請求、18円のままだな、おかしいな
- 時間経過で出るかな？

![image](https://gyazo.com/1ebbd1715fd8acf7ab1f52a0ea6616ec/thumb/1000)
![image](https://gyazo.com/f787909889b8f9bb9eb38a0d3b2309c3/thumb/1000)![image](https://gyazo.com/f726f05a2a98052b171dc83f352e39b1/thumb/1000)
![image](https://gyazo.com/2fe4c12c01d6e10f631fe5d638ced7b8/thumb/1000)
計算めんどくさいなw
1000円くらいは行ってるんじゃないのか

![image](https://gyazo.com/050d49fa1d16e0d3f9ba25f6ca8be934/thumb/1000)![image](https://gyazo.com/23fb8c080cc4fb0a70022520fd734c8d/thumb/1000)
[https://gist.github.com/nishio/07a0f42c78b1fb5ce634de49f674b238](https://gist.github.com/nishio/07a0f42c78b1fb5ce634de49f674b238)

