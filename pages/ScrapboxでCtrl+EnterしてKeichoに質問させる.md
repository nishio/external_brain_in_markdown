
![image](https://gyazo.com/1858e84d0c918645c4c089ec8e92f3ee/thumb/1000)
ScrapboxでCtrl+EnterしてKeichoに質問させる
[https://keicho.netlify.app/#talk=lSI8KHGqEfzXAACvih5f](https://keicho.netlify.app/#talk=lSI8KHGqEfzXAACvih5f)
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「Scrapbox」は、どんな「Scrapbox」ですか？
チャットではなくWiki
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「Wiki」は、どんな「Wiki」ですか？
...(keicho)

derived from [/takker/選択範囲をKeichoに尋ねるPopupMenu](https://scrapbox.io/takker/選択範囲をKeichoに尋ねるPopupMenu)
- [[選択範囲をKeichoに尋ねるPopupMenu]]

script.js

```javascript
import { insertText } from "/api/code/takker/scrapbox-insert-text-2/script.js";
document.body.onkeypress = (e) => {
  if (e.key === "Enter" && e.ctrlKey) {
    ask_keicho();
  }
};

const REGEXP_URL = /https:\/\/keicho\.netlify\.app\/#talk=(\w+)/;
const getTalkId = () => {
  let talkId = null;
  scrapbox.Page.lines.forEach((line) => {
    const matches = line.text.match(REGEXP_URL);
    if (matches !== null) {
      matches.forEach((m) => {
        talkId = m;
      });
    }
  });
  return talkId;
};

const ask_keicho = async (text = null) => {
  // idを取得する
  const id = await getTalkId();
  if (text === null) {
    const XPATH = "//span[@class='text' and contains(.,'(keicho)')]";
    const current_line = document.evaluate(XPATH, document).iterateNext();
    text = current_line.innerText.replace("(keicho)", "");
  }
  console.log(text);
  let { id: _id, text: answer } = await askKeicho(text, { id });
  // idが更新されたらURLを作る
  const code = id !== _id ? `https://keicho.netlify.app/#talk=${_id}\n` : "";
  answer = answer.replace(/\n+/g, "\n").replaceAll(">\n", "\n");
  const ICON = "[/nishio/nisbot.icon]";
  await insertText(`\n${code}${ICON}${answer}\n`);
};

scrapbox.PopupMenu.addButton({
  title: "🤖",
  onClick: (text) => {
    ask_keicho(text);

    // botの記入欄を作っておく
    return `${text}\n`;
  },
});
```



---
ver.1
![image](https://gyazo.com/dd0fb433a12ee640218814c6b2307b2c/thumb/1000)
コンソールに入力文が流れてるタイミングでCtrl+Enterしてる

最後に画面にない引用文が出てるのは、今のシステムがScrapboxのページを見て引用するのではなく、過去に入力されたものから引用するから、ここまでにテスト入力したものがScrapboxの方で消してもKeichoは覚えてることが原因
