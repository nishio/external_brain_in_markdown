---
title: "Tampermonkey"
---

ユーザが任意のサイトに対してユーザスクリプトを書くことで拡張できるようにするChrome拡張
[https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en)

試してみた感想
- 以前に作ったコード片を呼び出すためのボタンをつけようと思った
- [[TwitterをScrapboxにまとめる]]
- DOM操作に関してコンソールで試行錯誤
- VSCodeに貼りつけて整形
- それをTampermonkeyの設定画面に貼りつけたらletやconstのついてない変数が警告されたので直した
- 画面を行ったり来たりするのは面倒だが解決は簡単ではないな

js

```javascript
const togetter_to_scrapbox = () => {
  const tweets = document.querySelectorAll(
    '.choices_box li[data-type="tweet"]'
  );
  const get_name = (tweet) =>
    tweet.querySelector(".user_link .status_name").innerText.substring(1);
  const remove_mention = (text) => text.replace(/@\w+\s+/g, "");
  const concat_line = (text) => text.replace(/\n+/g, " ");
  const quote_all_line = (text) => text.replace(/\n+/g, "\n>");
  const text = Array.from(tweets)
    .map((x) => {
      const name = get_name(x);
      const url = x.querySelector(".link[target='_blank']").href;
      let body = x.querySelector(".tweet").innerText;
      body = remove_mention(body);
      //body = concat_line(body)
      body = quote_all_line(body);
      return `>[${name} ${url}]: ${body}`;
    })
    .join("\n\n");
  document.querySelector(".title_input").value = text;
  navigator.clipboard.writeText(text);
};
const div = document.getElementById("settings");
const button = document.createElement("button");
button.onclick = togetter_to_scrapbox;
button.innerText = "Scrapbox";
div.insertBefore(button, div.children[0]);
```

