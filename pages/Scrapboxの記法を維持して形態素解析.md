---
title: "Scrapboxの記法を維持して形態素解析"
---

2022-04-07
![image](https://gyazo.com/05d8ee0d4c4a5f47ace96e804e2cb77a/thumb/1000)
[[mecabで入力の一部を分割しない]]を使う
- ただしScrapboxの場合は保護したい記法が複数あるので前処理を正規表現での置換で済ませるのは困難
- 今回は前処理部分だけ[[Deno]]で[[scrapbox-parser]]を使って行うことにした
ts

```typescript
data.pages.forEach((page: ScrapboxPage) => {
  const text = page.lines.map((line: ScrapboxLine) => line.text).join("\n");
  const blocks = parse(text);
  const mecab = [] as string[];
  blocks.forEach((block) => {
    if (block.type === "line") {
      const indent = " ".repeat(block.indent);
      mecab.push(`[${indent}]\tSCRAPBOX_INDENT`);

      let trailing_space = "";
      block.nodes.forEach((node) => {
        if (node.type === "plain") {
          const m = node.text.match(/(.*?)(\s*)$/);
          mecab.push(m![1]);
          trailing_space = m![2];
        } else if (node.type === "link" || node.type === "icon") {
          const tag = node.type === "link" ? "SCRAPBOX_LINK" : "SCRAPBOX_ICON";
          mecab.push(`${trailing_space}${node.raw}\t${tag}`);
          trailing_space = "";
        }
      });
      mecab.push("[NEWLINE]\tNEWLINE");
    }
  });
  page.mecab = mecab.join("\n");
});
```



---
old version
ts

```typescript
const blocks = parse(text);

const mecab = [] as string[];
blocks.forEach((block) => {
  if (block.type === "line") {
    const indent = " ".repeat(block.indent);
    mecab.push(`[${indent}]\tSCRAPBOX_INDENT`);
    block.nodes.forEach((node) => {
      console.log(node);
      if (node.type === "plain") {
        mecab.push(node.text);
      } else if (node.type === "link") {
        mecab.push(`${node.raw}\tSCRAPBOX_LINK`);
      } else if (node.type === "icon") {
        mecab.push(`${node.raw}\tSCRAPBOX_ICON`);
      }
    });
    mecab.push("[NEWLINE]\tNEWLINE");
  }
});
```


- error `tokenizer.cpp(368) [new_node->feature]`
- 下流のMeCabの仕様によりリンク記法やアイコン記法の直前のテキストが空白文字で終わってはいけない
    - [mecabの制約付き解析（部分解析）のエラー - エイエイレトリック](https://eieito.hatenablog.com/entry/2021/09/24/090000)
        - > 制約ありテキスト列の 直前 に 半角スペース があるときだけ起こるエラーです。
    - 単に削ると復元できなくなるので、今回はその空白文字を記法の側に追加することにする