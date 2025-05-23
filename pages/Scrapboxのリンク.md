---
title: "Scrapboxのリンク"
---

サムネイル
![image](https://gyazo.com/d9e8cfd05228f6b1ddca7e8f9ffc588b/thumb/1000)

Scrapboxのリンクの概念は独特で、多くの人が「リンク」という言葉でイメージする概念よりだいぶ広い
- その広がりの部分が知的生産に有益だが、伝わりにくいので説明を試みる
- ![image](https://gyazo.com/a24b19790f393891a467c000245cf82e/thumb/1000)
- 多くの人が「リンク」という言葉で連想するのはこういうプロセスだろう
    - 1: 文書Aがある
    - 2: 文書Bがある
    - 3: AとBの間にリンクを作る
- Scrapboxに慣れた人から見ると、これはごく狭い考え方
    - リンクの一部にすぎない
    - 「これ人間が事前にAとBのことを知ってる前提だよね？」
        - そういう時にしか成立できないリンク

Scrapboxに慣れた人がリンクと言ってるプロセスは下記のものを含む
- ![image](https://gyazo.com/d9e8cfd05228f6b1ddca7e8f9ffc588b/thumb/1000)
    - 1: 文書Aがある
    - 2: Aからたくさんの「リンク先に既存のページが存在することを仮定しないリンク」が伸びる
    - 3: 各リンクが曖昧検索によって類似のリンクを探す
    - 4: 類似のリンクが見つかった！
    - 5: それをたどることで文書Bがみつかる
- リンクとリンクがつながることによって結果的に根本の文書の間につながりが見出される仕組みに関して「[[2-hopリンク]]」とも呼ばれる
    - このスタイルのリンクが発生する確率は、既にあるリンクの量が増えることで上昇する
    - ![image](https://gyazo.com/89f0b5d587518206e9ba159873941070/thumb/1000)

これを「人間が見て操作するインターフェース」としてではなく「LLMが操作できるAPI」として実現できないかなぁということを考えている
