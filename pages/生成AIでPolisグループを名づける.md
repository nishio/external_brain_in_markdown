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

