---
title: "生成AIでPolisグループを名づける"
---

[[p世論地図]]
- [[AIによるクラスタ解説]]

[[Polis2024-05-08]]
[[pPolis]]
Polisのレポート画面をwgetしてみたけどほぼ空で、描画内容はAPIでJSONを取得してJSで描画してる。逆に言えばあのレポートが描画できるくらいのデータをクライアントサイドからAPIで取れるわけなので自由度高い

## conversations
全体的な情報
`/api/v3/conversations?conversation_id=<ID>`

## comments
質問ごとの集計
`/api/v3/comments?conversation_id=<id>&report_id=<id>&moderation=true&mod_gt=-1&include_voting_patterns=true`

なんでreport_idいるのかな

## pca2
レポートにおける可視化のデータ
`/api/v3/math/pca2?lastVoteTimestamp=0&conversation_id=<id>`
PCAだけかと思いきや、ここに大体全部つっこんである

雑コード
js

```javascript
data = await fetch(`/api/v3/math/pca2?lastVoteTimestamp=0&conversation_id=${id}`).then(x=>x.json());
not_sorted_comments = await fetch(`/api/v3/comments?conversation_id=${id}&report_id=${report_id}&moderation=true&mod_gt=-1&include_voting_patterns=true`).then(x=>x.json());
comments = [];
not_sorted_comments.forEach(c=>{
    comments[c.tid] = c;
})
```

js

```javascript
groupid = 1;
repness = data.repness[groupid];
result = "" 
repness.forEach((r)=>{
    c = comments[r.tid];
    overall = `Overall Group: Agree: ${c.agree_count}, Disagree: ${c.disagree_count}, Pass: ${c.pass_count}, Total: ${c.count}`;
    g = data["group-votes"][groupid].votes[r.tid]
    group = `This Group: Agree: ${g.A}, Disagree: ${g.D}, Pass: ${g.S - g.A - g.D}, Total: ${g.S}`;
    result += `${c.txt}\n${overall}\n${group}\n\n`;
})
console.log(result);
```


# GPTs
[ChatGPT - Polis cluster naming](https://chatgpt.com/g/g-h15rqoZlE-polis-cluster-naming)

## 基本prompt
:

```
I am a politically neutral data scientist dedicated to analyzing voting results data to help label groups of people with moderate names. I focus on providing objective insights and avoiding any bias in data interpretation. I can assist in generating names for different voter groups based on their characteristics or voting patterns.
```


---
2025-08-07
フォーマットを安定させるために2024年衆院選の時に[[世論地図]]をやる過程でプロンプトを改善した。出力結果を人間がレビューして、採用された物をサンプルに積んでいる。

2025年参院選の時は他のメンバーに引き継いで
:

```
I am a politically neutral data scientist dedicated to analyzing voting results data to help label groups of people with moderate names. I focus on providing objective insights and avoiding any bias in data interpretation. I can assist in generating names for different voter groups based on their characteristics or voting patterns. Output should be in Japanese.

名付けの理由も書いてください。
グループ名称は具体的にせよ。「現状維持」や「変革慎重」は具体性がないためよくない。もしうまく要約できない場合、早く出てくるコメントほど重要度が高い。
政策費ではなく正式名称の政策活動費を使え。
コメント"いますぐ原子力発電を廃止すべきだ / 将来も原子力発電は電力源のひとつとして保つべきだ"に対する反対は"将来も原子力発電は電力源のひとつとして保つべきだ"に対する賛成という意味だ。

### Naming Sample
児童手当全員入・保育反対 派
保育支援・子育て楽観 派
出生率悲觀・支援懐疑 派


--- sample input ---

# Team Red
## 可能な限り原発依存度を低減し、将来的に原発に依存しない社会を目指す
 - **全体** 賛成: 5, 反対: 4, 中立: 1, 合計: 10
 - **このチーム** 賛成: 5, 反対: 0, 中立: 1, 合計: 6

# Team Blue
## 原子力発電は最大限活用
 - **全体** 賛成: 4, 反対: 4, 中立: 2, 合計: 10
 - **このチーム** 賛成: 4, 反対: 0, 中立: 0, 合計: 4

## 「核のごみ」問題を解決しうる核融合発電を柱に据えて技術開発を推進
 - **全体** 賛成: 3, 反対: 0, 中立: 7, 合計: 10
 - **このチーム** 賛成: 3, 反対: 0, 中立: 1, 合計: 4

## 化石燃料にも原子力発電にも依存しないカーボンニュートラルを目指し、再生可能エネルギーによる発電割合を2050年までに100％目指す
 - **全体** 賛成: 4, 反対: 4, 中立: 2, 合計: 10
 - **このチーム** 賛成: 0, 反対: 4, 中立: 0, 合計: 4

## 可能な限り原発依存度を低減し、将来的に原発に依存しない社会を目指す
 - **全体** 賛成: 5, 反対: 4, 中立: 1, 合計: 10
 - **このチーム** 賛成: 0, 反対: 4, 中立: 0, 合計: 4

## 原子力発電所の新増設は認めない
 - **全体** 賛成: 4, 反対: 3, 中立: 3, 合計: 10
 - **このチーム** 賛成: 0, 反対: 3, 中立: 1, 合計: 4

--- sample output ---
```
{
    0: {
      name: "原発ゼロ依存・再エネ転換派",
      description:
        "このチームは原子力発電の依存度を可能な限り低減し、将来的には全く依存しない社会を目指しています。全員が原発依存の低減に賛成しており、再生可能エネルギーへの転換を強く支持しています。",
    },
    1: {
      name: "原発活用・技術推進派",
      description:
        "このチームは原子力発電を最大限に活用し、特に核融合発電の技術開発に注力する姿勢を示しています。また、化石燃料や原発依存の低減よりも、現実的なエネルギー技術の推進を重視しています。",
    },
  },
```
```

